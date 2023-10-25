# Mid-semester check-in: Part I

0.  Load libraries

``` r
rm(list=ls())
library(tidyverse) 
library(dplyr)
library(nycflights13)
```

1.  Calculate the average and standard deviation of flight delays for
    each airline, *counting only those flights that were delayed longer
    than an hour*.

``` r
 #Easy way, using just arrival delays
 flightstats_Arrival<- flights |>
  filter(!is.na(arr_delay), arr_delay>= 60)|>
  group_by(carrier)|>
  summarize("Mean Delay" = mean(arr_delay), "STD" = sd(arr_delay))
  
 #Overkill way, using both arrival and departure delays
 flightstats_Delay<- flights |>
   filter(!is.na(arr_delay), !is.na(dep_delay), arr_delay >=60 | dep_delay >= 60)|>
   pivot_longer(cols = contains("delay"), names_to= "Arrival or Departure", values_to = "Time")|>
   group_by(carrier)|>
   summarize("Mean Delay" = mean(Time), "STD" = sd(Time))
```

2.  Identify the 5 flights (i.e., unique combination of `carrier` and
    `flight`) that are most frequently delayed more than a half hour.

<!-- -->

3.  Make a plot of the distribution of flight times for each airline.
    The plot should show summary statistics in some way (e.g. median,
    upper and lower quartiles; you can choose which summary statistics
    are best) as well as individual data points. Order the x axis in
    order of median flight time, from highest on the left to lowest on
    the right.
