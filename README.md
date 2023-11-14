# Does winning become more likely with a winning top laner?

This is a website containing the report for a project done in DSC 80 at UCSD 
where I cleaned, performed exploratory data analysis, assessed missingness, and
conducted a hypothesis test.

## Introduction

The data set I used was taken from HYPERLINK and contains information on 
professional league of legends matches from 2022. This data set contains 149401
rows and 56 columns. There are 12 rows per game with 10 of the rows containing 
information about the players and the last 2 containing information about the 
the teams in the match.

The question I explored was whether having a top laner who was winning at 15 
minutes make winning the game more likely. I decided to explore this question 
because, out of the 5 lanes in league of legends, most would agree that the top 
lane is the most isolated lane and hardest to carry the game from. Top lane also 
happens to be the most snowballable lane. This means that once either of the 
laners get ahead the lane becomes very uneven in favor of the laner who is ahead.
We define who is ahead at any given time during laning phase by who has more gold.

### test3