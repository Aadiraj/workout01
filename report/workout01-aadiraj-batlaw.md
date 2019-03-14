workout01-aadiraj-batlaw
================
Aadiraj Batlaw

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
shots <- read.csv("../data/shots-data.csv", stringsAsFactors = F)
two_point <- select(filter(shots, shot_type == "2PT Field Goal"), name, shot_made_flag)

two_points = two_point %>%
  group_by(name) %>%
  summarise(total = n(), made = sum(shot_made_flag == "shot_yes")) 
two_points <- arrange(mutate(two_points, perc_made = made/total), desc(perc_made))

three_point <- select(filter(shots, shot_type == "3PT Field Goal"), name, shot_made_flag)
three_points = three_point %>%
  group_by(name) %>%
  summarise(total = n(), made = sum(shot_made_flag == "shot_yes")) 
three_points <- arrange(mutate(three_points, perc_made = made/total), desc(perc_made))

overall <- select(shots, name, shot_made_flag)
overall_points = overall %>%
  group_by(name) %>%
  summarise(total = n(), made = sum(shot_made_flag == "shot_yes")) 
overall_points <- arrange(mutate(overall_points, perc_made = made/total), desc(perc_made))
```

Article: Analyzing and Comparing Shooting Statistics of Five Golden State Warriors Players
==========================================================================================

Introduction and Motivation
---------------------------

In this article, we will be analyzing the shooting statistics of 5 players of the Golden State Warriors team. These players are believed to be one of (if not the) best players on the team, so after our analysis we would like to discover if we can determine which shooting statistics lead these players to success, and what statistics make one player more successful over the other.

Background
----------

First, let us examine our players. Our first player is Andre Iguodala. Andre Iguodala is a 35 year old, 6 foot 6, 215 lb Shooting Guard/Small Forward for the Golden State Warriors. He began his career in basketball in 2004, and joined the Golden State Warriors in 2013. <img src="../images/andre.jgp" width="80%" style="display: block; margin: auto;" /> Our second player is Draymond Green. Draymond Green is a 29 year old, 6 foot 7, 230 lb Power Forward for the Golden State Warriors. He joined the Golden State Warriors in 2012, beginning his career in basketball. Our third player is Kevin Durant. Kevin Durant is a 30 year old, 6 foot 9, 240 lb Small Forward/Power Forward for the Golden State Warriors. He began his career in basketball in 2007, and joined the Golden State Warriors in 2016. Our fourth player is Klay Thompson. Klay Thompson is a 29 year old, 6 foot 7, 215 lb Shooting Guard for the Golden State Warriors. He joined the Golden State Warriors in 2011, beginning his career in basketball. Last but certainly not least, we have Stephen Curry, arguably the best player in the NBA right now. Stephen Curry is a 30 year old, 6 foot 3, 190 lb Point Guard for the Golden State Warriors. He joined the Golden State Warriors in 2011, beginning his career in basketball.
