# HMK 08 template

``` r
library(nycflights13)
library(tidyverse)
```

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.1.2     ✔ readr     2.1.4
    ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ✔ purrr     1.0.2     
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(dplyr)
```

# Joins

1.  Imagine you’ve found the top 10 most popular destinations using this
    code:

``` r
top_dest <- flights |>
  count(dest, sort = TRUE) |>
  head(10)
```

How can you find all flights to those destinations? - Worked wtih Eva in
class Friday

``` r
#Use top_dest as primary key, adding all of secondary key columns to it
all_flights_sloppy<- top_dest|>
  left_join(flights)|>
  select(dest, flight)

#Use top_dest as primary key, add only selected column from secondary key to it
all_flights_pretty <- top_dest |>
  cross_join(as.data.frame(flights$flight))
#I don't know if this actually worked
```

# Functions

2.  Write a function to ‘rescale’ a numeric vector by subtracting the
    mean of the vector from each element and then dividing each element
    by the standard deviation.

``` r
vector<- c(5,6,7,8,9,10,11,12,13,14,15)

scaled_vector <- function(vector){
 (vector-mean(vector))/(sd(vector))}

#Works with vector
scaled_vector(vector)
```

     [1] -1.5075567 -1.2060454 -0.9045340 -0.6030227 -0.3015113  0.0000000
     [7]  0.3015113  0.6030227  0.9045340  1.2060454  1.5075567

``` r
#Check with a new vector set
Other <- c(100,120,140,150)
scaled_vector(Other)
```

    [1] -1.2402159 -0.3382407  0.5637345  1.0147221
