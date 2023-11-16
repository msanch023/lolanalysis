# Does winning become more likely with a winning top laner?
### By Marco Sanchez

This is a website containing the report for a project done in DSC 80 at UCSD 
where I cleaned, performed exploratory data analysis, assessed missingness, and
conducted a hypothesis test.

## **Introduction**

The data set I used was taken from HYPERLINK and contains information on 
professional league of legends matches from 2022. This data set contains 149401
rows and 56 columns. There are 12 rows per game with 10 of the rows containing 
information about the players and the last 2 containing information about 
the teams in the match.

### **Question to be Explored**

The question I explored was whether having a top laner who was winning at 15 
minutes would make winning the game more likely. I decided to explore this question 
because, out of the 5 lanes in league of legends, most would agree that the top 
lane is the most isolated lane and hardest to carry the game from. Top lane also 
happens to be the most snowballable lane. This means that once either of the 
laners get ahead the lane becomes very uneven in favor of the laner who is ahead.
We define who is ahead at any given time during laning phase by who has more gold.

### **Description of Columns**

By simplifying the data down to 8 columns and around 21000 rows, I had all the 
data I would need in order to answer whether winning became more likely when 
the top laner was fed.

**Columns Used**



`gameid` -> Unique game identifier <br />
`position` -> Position being played, in this case only `top` is kept
`champion` -> Character being played	
`result` -> `1` if the match was won and `0` if the match was lost
`goldat15` -> The total amount of gold the player has gathered at 15 minutes 
`opp_goldat15` -> The total amount of gold the opponent has gathered at 15 minutes
`golddiffat15` -> The differential in gold between the two players
`winning_lane` -> `True` if the player has more gold and `False` if the opponent has more gold



## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

### Univariate

### Bivariate 

