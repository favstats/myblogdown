+++
date = 2018-01-03
lastmod = 2018-01-03
draft = false
tags = ["maps", "ggplot", "highcharter", "dataviz"]
title = "Mapping Terror Attacks with Highcharter"
math = true
summary = """
A short blogpost about creating an interactive map with Highcharter
"""

[header]
image = "headers/terror_title.png"
caption = "The finished map"

+++


A few days ago someone asked me whether I could visualize the terror attacks of recent years in Europe. Here is an attempt to do exactly this.

The code for this blogpost can be found in this [GitHub Repository](https://github.com/favstats/terror_map).

**Getting Started**

First I need data about terror attacks. For this I downloaded the [Global Terrorism Database](https://www.start.umd.edu/gtd/).

Now in Rstudio, I load in the needed packages:

```{r}
pacman::p_load(tidyverse, magrittr, readxl, highcharter)
```

After I put the downloaded `.xlsx` file into my working directory, I use `readxl` to read in the data.

```{r}
terror <- read_xlsx("data/globalterrorism.xlsx", sheet = "Data")
```

Now comes the **data wrangling part**. 


```{r}
terror_map <- terror %>% 
  filter(iyear >= 2000) %>% 
  filter(region %in% c(8, 9)) %>% 
  filter(nkill > 0) %>% 
  filter(longitude <= 38) %>% 
  # filter(longitude >= 24) %>% 
  # filter(latitude >= 13) %>% 
  arrange(desc(nkill)) %>% 
  mutate(lon = longitude) %>% 
  mutate(lat = latitude) %>% 
  mutate(date = paste(iyear, imonth, iday, sep = "-")) %>% 
  mutate(name = paste0("<br> <b>Country:</b> ", country_txt,
                       "<br> <b>City:</b> ", city, 
                       "<br> <b>Date:</b> ", date,
                       "<br> <b>Group:</b> ", gname,
                       "<br> <b>Attack Type:</b> ", attacktype1_txt,
                       "<br> <b>Target:</b> ", target1,
                       "<br> <b>Death Count</b>")) %>% 
  select(name, lon = longitude, lat,  z = nkill)
```

And finally, I apply the `highcharter` functions to create a beautiful interactive map. 

```{r}
hcmap("custom/europe", showInLegend = FALSE) %>%
  hc_add_series(data = na.omit(terror_map), type = "mapbubble",
                minSize = 0, maxSize = 30,
                name = "Terror Attack", fillOpacity = 0.01) %>%
  highcharter::hc_title(text = "Terror Attacks with Casualties > 1 (2000 - 2016)", 
                        style = list(fontWeight = "bold")) %>%
  hc_subtitle(text = "Source: <a href='https://www.start.umd.edu/gtd/'>Global Terrorism Database (GTD)</a>")
```

The result:

![](https://github.com/favstats/terror_map/blob/master/images/terror_map.png?raw=true)

**Click [here](https://favstats.github.io/terror_map/) for interactive version.**

