+++
date = 2017-12-26
lastmod = 2017-12-27
draft = false
tags = ["Daesh", "ISIS", "Arab Barometer", "Survey Data"]
title = "What do Arab Muslims think about ISIS (Daesh)?"
math = true
summary = """
Here I want to dive a little bit into how Arab Muslims see Daesh (*a term for ISIS often used by Arabic speakers*). The data I will be using is from the [Arab Barometer Wave 4](http://www.arabbarometer.org/), released just a few weeks ago.
"""

[header]
image = "headers/isis.jpg"
caption = "Photograph by Nour Fourat/Reuters"

+++

Welcome to my *very first blogpost*. Here I want to dive a little bit into how Arab Muslims see Daesh (*a term for ISIS often used by Arab speakers*). The data I will be using is from the [Arab Barometer Wave 4](http://www.arabbarometer.org/), released just a few weeks ago. I will also be using the Arab Barometer in the future because it has a lot of interesting questions asked, including a small sample size of *Syrian refugees*. So stay tuned. 

Survey data from the Middle East is especially interesting to me because it is a region that is often talked about without considering local voices. 

*Note: Whenever I speak of Arab Muslims in this blogpost, I am referring to the sample at hand.*

Without further ado, here are some insights into the perception of Daesh in the Arab world.

{{% toc %}}

## Data Preparation

First of all, the data has to be prepared. For all of the following charts I use the provided weights that are meant to make the survey more representative.[^1] 

Furthermore, the data is filtered by religious affiliation, only including Muslim respondents `q1012 == 1`. Unfortunately, questions about Daesh were not asked in Egypt (which is included in the original survey project). This leaves us with *7149 respondents* across 6 different countries including a sample of Syrian refugees.[^2] 

All questions that are of interest here, can be found in *Section VIII: Current Affairs* of the [Arab Barometer Wave 4 Codebook](http://www.arabbarometer.org/sites/default/files/code_book/AB4%20English%20Codebook%20Final%20English_0.pdf)

If you are interested in the code that produced the following charts, feel free to visit this [GitHub Repository](https://github.com/favstats/GodlyGovernance/).


## The Threat of Daesh

The first charts we are going to look at are visualizations of two questions:

> Does Daesh pose a threat to our country? (`q826`)

> Does Daesh pose a threat to the Arab region? (`q827`)

Respondents could answer on a three-point scale:

1. Very grave threat

2. Somewhat of a threat

3. No threat at all

There were also two options for *missing values* (not included in visualization):

98. I don’t know (Do not read)

99. Declined to answer (Do not read)

*Here come the charts:*

### Threat to Country

![](https://github.com/favstats/GodlyGovernance/blob/master/images/threat_cntry.png?raw=true)

Overall, one can see that pretty much all populations seem to be quite concerned about the threat that Daesh poses to their country. *Lebanon* is on top of the chart with over **98%** of people saying that Daesh poses somewhat of a threat or even a grave threat to their country. Not surprising, since the Lebanese army and the Hezbollah militia are [directly involved](https://www.reuters.com/article/us-mideast-crisis-lebanon-syria/lebanese-army-hezbollah-announce-offensives-against-islamic-state-on-syrian-border-idUSKCN1AZ03G) in the Syrian civil war and the threat of terror attacks is always present.

Next on the list is *Tunisia*, where about **95%** consider Daesh to be a threat to their country. This might have something to do with the unusual number of Tunisians who have gone to fight with Daesh and are expected to [return soon to Tunisia](https://www.nytimes.com/2017/02/25/world/europe/isis-tunisia.html).

The countries least concerned seem to be *Morocco* and *Palestine*, where only **half the population** considers Daesh to be a grave threat, although it adds up to **75%** who think they are at least somewhat of a threat. 

### Threat to Region

![](https://github.com/favstats/GodlyGovernance/blob/master/images/threat_reg.png?raw=true)

Considering the entire Arab region, a clearer picture emerges. The fraction of people who don't consider Daesh a threat at all is consistently **below 10%**. This clearly shows that Arab Muslims are very concerned and well aware about the threat that Daesh poses to the entire region. Again, Lebanon and Tunisia appear on top of the chart, however, there don't seem to be very significant differences between the countries.

## Does Daesh represent Islam?

Next, we will take a look at a very interesting question. It is often alleged that Daesh represents what can be called *true Islam*. As Graeme Wood put it in his widely cited *The Atlantic* article [What ISIS really wants](https://www.theatlantic.com/magazine/archive/2015/03/what-isis-really-wants/384980/9): "The reality is that the Islamic State is Islamic. *Very Islamic.*" And he isn't alone with this perception. In fact, the organization itself claims to represent the only authentic form of Islam. But how do Arab Muslims themselves see this organization that claims to represent their faith? We are about to find out.

We are looking at the following question:

> To what extent do you believe Daesh’s tactics are compatible with the teachings of Islam? (`q828`)

Respondents were able to answer in the following way:

1. Certainly represents true Islam

2. Represents true Islam

3. Does not represent true Islam

4. Certainly does not represent true Islam

The categories for *missing values* (don't know and decline to answer) have been summarized into a single category.

*Note: The chart includes differently worded answer categories, but only because they fit better on the graphic.*

Here is the chart:

![](https://github.com/favstats/GodlyGovernance/blob/master/images/compatible.png?raw=true)

Right from the get go, we can see that the left side of the chart is quite empty. The overwhelming majority of Arab Muslims does not believe that the tactics of Daesh are in any way compatible with Islam. However, it's also worth investigating the fraction of people who do agree with this notion. Populations that most perceive the actions of Daesh as Islamic are found in Palestine (9.0%), Algeria (9.4%), Lebanon (5.6%) and Tunisia (5.3%). 


## Daesh's violence and goals

The next chart we will be looking at goes in the same direction as the previous one. The questions asked are the following:

> To what extent do you agree with the goals of Daesh? (`q829`)

> To what extent to do you support Daesh’s use of violence? (`q830`)

Here is the chart:

![](https://github.com/favstats/GodlyGovernance/blob/master/images/combined.png?raw=true)

Again, one can see that a very similar pattern emerges. The overwhelming majority of Arab Muslims does not agree with Daesh's goals nor their use of violence. The highest approval ratings of both goals and use of violence can be found in the same countries that have the highest proportion of people that think Daesh's tactics represent *true Islam*: Palestine (6.4%; 5.4%), Algeria (4.9%; 5.1%), Lebanon (2.0%; 0%) and Tunisia (1.8%; 1.5%). Of course, one has to keep in mind that a sensitive question like this (asking flat out if someone supports use of violence) could be subject to *social desirability bias*. However, the overall low number of declined answers indicates that the possible bias isn't as severe as one might expect (although this can never be guaranteed).


## Who is responsible for Daesh?

The last question I will be looking at is also very interesting. It asks about the origins of Daesh and who or what is responsible for its creation. Here is the phrasing:

> Who or what do you think is responsible for creating Daesh? (`q830` and `q831`)

The variable (`q831`) includes the *"Other"* category. I opened it up and coded a few more categories.

Here is the resulting chart:

![](https://github.com/favstats/GodlyGovernance/blob/master/images/daesh_Arab Barometer.png?raw=true)

A quarter of people (25.36%) seem to blame the United States for the creation of Daesh. It is however not clear whether they mean that Western countries are literally responsible for Daesh's creation (a quite popular conspiracy theory which strangely enough was also repeated by the [current President of the United States during his bid for office](http://www.businessinsider.de/trump-obama-clinton-isis-2016-8?r=US&IR=T)) or whether they mean that the United States created the conditions that ultimately led to the creation of Daesh. 

However, this ambiguous interpretation is not readily available when it comes to blaming Israel for the creation of Daesh (14.02%) hinting at [anti-Israeli and antisemitic conspiracy theories](https://www.adl.org/blog/anti-israel-conspiracy-theories-appear-in-arabic-language-media-in-wake-of-sinai-massacre). 

Another interesting number shows up when considering Iran (4.48%) which might be rooted in anti-Shia sentiments.

Individual charts for each country can be found [here](https://imgur.com/a/fR4Li).

**Addendum:**

After I was asked to include this: [here](https://imgur.com/a/wQV3H) are the same visualizations that only include *Sunni Muslims*. Unfortunately, this question was only asked in Lebanon, Morocco, Algeria and Tunisia. However, the results are very similar to what is shown here.

## What is next?

I am looking forward to further analyze the data. 

Here are some ideas: 

Extract the people who are sympathetic to Daesh (respondents who see them as representing Islam, agree with their violence and their goals) and find out how they compare to people who aren't. For example, I could see how religious, educated, well-off or poor ISIS sympathizers are compared to their peers.

Let me know if you have any other ideas, I am always open to suggestions!

Here are some other projects I am currently working on and will appear in my blog in the near future:

+ The Evolution of the Atheist/Skeptic Community on YouTube

+ Alt Right discourse on Mainstream media

+ Who supports populist parties in Europe (European Social Survey 8 Data)

+ Visualization of Terror Incidents in 2017



[^1]: Download the [Arab Barometer IV Methodology Statement](http://www.arabbarometer.org/sites/default/files/code_book/Arab%20Barometer%20Fourth%20Wave%20Methodology.pdf) for more details. 

[^2]: Note that in a first version of this blog post the sample size was wrongly stated as 8259.