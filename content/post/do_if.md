+++
date = 2019-05-14
lastmod = 2019-05-14
draft = false
tags = ["functions", "rstats"]
title = "do_if"
math = true
summary = """
A helper function to create a pipable if statement.
"""

[header]
image = "headers/do_if.png"
caption = "Pipable if statement"

+++



So recently I was writing functions with many if statements and pipes. Given that
I am a huge fan of the `%>%` pipe workflow, I was thinking about
creating a pipable if environment. Here is my attempt to implement
exactly that. With a lot help from my good friend [Ben](https://twitter.com/Ben_Guinaudeau). If you are reading this, thank you! You made this possible.

Import gist from here:

``` r
library(dplyr)
source("https://gist.githubusercontent.com/favstats/3e1d8b65a019b24344b7b3dea6002a0b/raw/6919b22f01db6d672d64ebcac5798b8495c89ad2/do_if.R")
```

So let’s say you want to create a function that has multiple if
specifications but you also want to always create two columns regardless
of the input. You might create something like this:

``` r
mock_function <- function(.data, argument = "") {
  
  if (argument == "do_this1") {
    .data <-.data %>%
          dplyr::filter(am == 1) %>%
          dplyr::filter(cyl == 6) %>%
          dplyr::mutate(x = disp >= 100)
  } else if (argument == "do_this2") {
    .data <-.data %>%
          dplyr::filter(am == 0) %>%
          dplyr::filter(cyl == 4) %>%
          dplyr::mutate(x = disp < 100)
  }
  
  final <- .data %>% 
    mutate(new_column = "Say What") %>% 
    mutate(other_column = "Say That")
  
  return(final)
  
}
```

So if you leave the argument blank you will receive the entire dataset
with two new columns:

``` r
mtcars %>% 
  mock_function() %>% 
  select(vs:other_column) %>% 
  as_tibble()
```

    ## # A tibble: 32 x 6
    ##       vs    am  gear  carb new_column other_column
    ##    <dbl> <dbl> <dbl> <dbl> <chr>      <chr>       
    ##  1     0     1     4     4 Say What   Say That    
    ##  2     0     1     4     4 Say What   Say That    
    ##  3     1     1     4     1 Say What   Say That    
    ##  4     1     0     3     1 Say What   Say That    
    ##  5     0     0     3     2 Say What   Say That    
    ##  6     1     0     3     1 Say What   Say That    
    ##  7     0     0     3     4 Say What   Say That    
    ##  8     1     0     4     2 Say What   Say That    
    ##  9     1     0     4     2 Say What   Say That    
    ## 10     1     0     4     4 Say What   Say That    
    ## # ... with 22 more rows

If you add `"do_this1` to the argument you will receive a filtered
dataset:

``` r
mtcars %>% 
  mock_function("do_this1") %>% 
  select(vs:other_column) %>% 
  as_tibble()
```

    ## # A tibble: 3 x 7
    ##      vs    am  gear  carb x     new_column other_column
    ##   <dbl> <dbl> <dbl> <dbl> <lgl> <chr>      <chr>       
    ## 1     0     1     4     4 TRUE  Say What   Say That    
    ## 2     0     1     4     4 TRUE  Say What   Say That    
    ## 3     0     1     5     6 TRUE  Say What   Say That

And if you specify `"do_this2` it will create a different subset.. but
always with the `new_column` and `other_column` intact.

``` r
mtcars %>% 
  mock_function("do_this2") %>% 
  select(vs:other_column) %>% 
  as_tibble()
```

    ## # A tibble: 3 x 7
    ##      vs    am  gear  carb x     new_column other_column
    ##   <dbl> <dbl> <dbl> <dbl> <lgl> <chr>      <chr>       
    ## 1     1     0     4     2 FALSE Say What   Say That    
    ## 2     1     0     4     2 FALSE Say What   Say That    
    ## 3     1     0     3     1 FALSE Say What   Say That

Now this would work just fine. But what if you have multiple if
statements along your pipe chain and you don’t want to split into so
many different if statements? Well this is where `do_if` comes in\!

``` r
#' A pipable if statement
#'
#' This function allows to create an if statement that can be used within a pipable workflow
#'
#' @importFrom magrittr %>%
#' @importFrom rlang parse_expr
#' @param .data tibble
#' @param condition logical test
#' @param call a formula descibing a pipe to be evaluated if condition is \code{code}
#' @examples
#' any_condition <- T
#'
#' mtcars %>%
#' do_if(any_condition, ~{
#' .x %>%
#'  dplyr::filter(cyl == 6) %>%
#'  dplyr::mutate(x = disp > 170)
#' })
#' @export
do_if <- function(.data, condition, call){

  if(condition){
    .x <- .data

    call_str <- call %>%
      as.character %>%
      .[2]

    out <- eval(rlang::parse_expr(call_str))

    return(out)
  } else {
    return(.data)
  }
}
```

With `do_if` you can specify an if statement *within* a pipable
workflow\!

Example:

``` r
any_condition <- T

mtcars %>%
  do_if(any_condition, ~{
    .x %>%
      dplyr::filter(cyl == 6) %>%
      dplyr::mutate(x = disp > 170)
    }) %>% 
  as_tibble()
```

    ## # A tibble: 7 x 12
    ##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb x    
    ##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <lgl>
    ## 1  21       6  160    110  3.9   2.62  16.5     0     1     4     4 FALSE
    ## 2  21       6  160    110  3.9   2.88  17.0     0     1     4     4 FALSE
    ## 3  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1 TRUE 
    ## 4  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1 TRUE 
    ## 5  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4 FALSE
    ## 6  17.8     6  168.   123  3.92  3.44  18.9     1     0     4     4 FALSE
    ## 7  19.7     6  145    175  3.62  2.77  15.5     0     1     5     6 FALSE

This can come in really handy if you are not a big fan of seperating
your pipe workflow all too often. Let’s recreate the mock\_function with
the help of `do_if`

``` r
mock_function <- function(.data, argument = "") {
  .data %>% 
    do_if(
      argument == "do_this1",
      ~{.x %>%
          dplyr::filter(am == 1) %>%
          dplyr::filter(cyl == 6) %>%
          dplyr::mutate(x = disp >= 100)
        }
    ) %>% 
    do_if(
      argument == "do_this2",
      ~{.x %>%
          dplyr::filter(am == 0) %>%
          dplyr::filter(cyl == 4) %>%
          dplyr::mutate(x = disp < 100)
        }
    ) %>% 
    mutate(other_column = "Say That") %>% 
    mutate(new_column = "Say What") 
}
```

And again we can get the same results, only with a slighly less
troublesome workflow within a function\!

``` r
mtcars %>% 
  mock_function() %>% 
  as_tibble()
```

    ## # A tibble: 32 x 13
    ##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
    ##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
    ##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
    ##  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
    ##  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
    ##  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
    ##  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
    ##  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
    ##  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
    ##  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
    ## 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
    ## # ... with 22 more rows, and 2 more variables: other_column <chr>,
    ## #   new_column <chr>

``` r
mtcars %>% 
  mock_function(argument = "do_this1") %>% 
  as_tibble()
```

    ## # A tibble: 3 x 14
    ##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb x    
    ##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <lgl>
    ## 1  21       6   160   110  3.9   2.62  16.5     0     1     4     4 TRUE 
    ## 2  21       6   160   110  3.9   2.88  17.0     0     1     4     4 TRUE 
    ## 3  19.7     6   145   175  3.62  2.77  15.5     0     1     5     6 TRUE 
    ## # ... with 2 more variables: other_column <chr>, new_column <chr>

``` r
mtcars %>% 
  mock_function(argument = "do_this2") %>% 
  as_tibble()
```

    ## # A tibble: 3 x 14
    ##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb x    
    ##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <lgl>
    ## 1  24.4     4  147.    62  3.69  3.19  20       1     0     4     2 FALSE
    ## 2  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2 FALSE
    ## 3  21.5     4  120.    97  3.7   2.46  20.0     1     0     3     1 FALSE
    ## # ... with 2 more variables: other_column <chr>, new_column <chr>


UPDATE:


 
[Mike Kearney](https://twitter.com/kearneymw) created a much smoother version with the ability to create an else statement as well.

Check it out [here](https://gist.github.com/mkearney/bb2ce47eb635c14d5f99151636e26b21):



``` r

#' Conditionally apply expressions on a data object
#' 
#' @param .data Input data
#' @param condition A logical value to determine whether to use .if or .else
#' @param .if Formula or function to apply to intput data when condition is TRUE
#' @param .else Formula or function to apply to intput data when condition is FALSE
#' @return Output of appropriate .if/.else call
#' @export
#' @importFrom rlang as_closure
do_if_else <- function(.data, condition, .if, .else = identity) {
  if (condition) {
    call <- rlang::as_closure(.if)
  } else {
    call <- rlang::as_closure(.else)
  }
  do.call(call, list(.data))
}
```




Usage Example:

![](https://pbs.twimg.com/media/D6i5BJ2X4AAcnVx.jpg)
