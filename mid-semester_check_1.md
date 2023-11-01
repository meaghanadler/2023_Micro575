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
    Comment: The output is the same whether answered via arrival delay
    or departure delay

``` r
glimpse(flights)
```

    Rows: 336,776
    Columns: 19
    $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2…
    $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, …
    $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, …
    $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1…
    $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849,…
    $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851,…
    $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -1…
    $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "…
    $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 4…
    $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N394…
    $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA",…
    $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD",…
    $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 1…
    $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, …
    $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6…
    $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0…
    $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 0…

``` r
#How to use reduce(rbind, by()) in a pipe?

#Based on arrival delay
filterstats_5toparr <- flights|>
  filter(!is.na(arr_delay), !is.na(dep_delay), arr_delay >=30 | dep_delay >= 30)|>
  select(carrier,flight,dep_delay,arr_delay)|>
  count(carrier,flight, sort=TRUE)|>
  head(arr_delay,n=5)

#Based on departure delay
filterstats_5topdep <- flights|>
  filter(!is.na(dep_delay), dep_delay >= 30)|>
  select(carrier,flight,dep_delay)|>
  count(carrier,flight, sort=TRUE)|>
  head(dep_delay,n=5)


#Overkill way
filterstats_5topoverkill <- flights|>
  filter(!is.na(arr_delay), !is.na(dep_delay), arr_delay >=30 | dep_delay >= 30)|>
  select(carrier,flight,dep_delay,arr_delay)|>
  pivot_longer(cols = contains("delay"), names_to= "Arrival or Departure", values_to = "Time")|>
  count(carrier,flight, sort=TRUE)|>
  head(`Most Frequently Delayed`,n=5)
```

3.  Make a plot of the distribution of flight times for each airline.
    The plot should show summary statistics in some way (e.g. median,
    upper and lower quartiles; you can choose which summary statistics
    are best) as well as individual data points. Order the x axis in
    order of median flight time, from highest on the left to lowest on
    the right.

``` r
glimpse(flights)
```

    Rows: 336,776
    Columns: 19
    $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2…
    $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, …
    $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, …
    $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1…
    $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849,…
    $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851,…
    $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -1…
    $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "…
    $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 4…
    $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N394…
    $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA",…
    $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD",…
    $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 1…
    $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, …
    $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6…
    $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0…
    $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 0…

``` r
plotdata <- flights |>
  select(carrier, flight, air_time)|>
  filter(!is.na(carrier),!is.na(flight),!is.na(air_time))|>
  group_by(carrier)

#Subset df for individual data point visualization
#reordered so that by picking every 20th its not skewing data
tenth<- plotdata |>
  with(plotdata, reorder(carrier, air_time, median))|>
  filter(row_number() %% 20 == 1)

ggplot(data=plotdata,mapping = aes(fct_reorder(.f=carrier,.x=desc(air_time),.fun=median),air_time))+
  geom_boxplot(size=0, alpha=0)+
  geom_jitter(data=tenth, aes(carrier,air_time), size=0.1,alpha=0.1)+
  xlab("Airline Carrier")+ 
  ylab("Air Time")+
  ggtitle("Distribution of flight time by airline")+
  theme_minimal()
```

![](mid-semester_check_1_files/figure-commonmark/unnamed-chunk-4-1.png)
