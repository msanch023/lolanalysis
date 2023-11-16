# Does winning become more likely with a winning top laner?

### By Marco Sanchez

This is a website containing the report for a project done in DSC 80 at
UCSD where I cleaned, performed exploratory data analysis, assessed
missingness, and conducted a hypothesis test.

## **Introduction**

The data set I used was taken from HYPERLINK and contains information on
professional league of legends matches from 2022. This data set contains
149401 rows and 56 columns. There are 12 rows per game with 10 of the
rows containing information about the players and the last 2 containing
information about the teams in the match.

### **Question to be Explored**

The question I explored was whether having a top laner who was winning
at 15 minutes would make winning the game more likely. I decided to
explore this question because, out of the 5 lanes in league of legends,
most would agree that the top lane is the most isolated lane and hardest
to carry the game from. Top lane also happens to be the most
snowballable lane. This means that once either of the laners get ahead
the lane becomes very uneven in favor of the laner who is ahead. We
define who is ahead at any given time during laning phase by who has
more gold.

### **Description of Columns**

By simplifying the data down to 5 columns and around 21000 rows, I had
all the data I would need in order to answer whether winning became more
likely when the top laner was fed.

**Columns Used** 
`result` -\> `1` if the match was won and `0` if the
match was lost<br /> `goldat15` -\> The total amount of gold the player
has gathered at 15 minutes <br /> `opp_goldat15` -\> The total amount of
gold the opponent has gathered at 15 minutes<br /> `golddiffat15` -\>
The differential in gold between the two players<br /> `winning_lane`
-\> `1` if the player has more gold and `0` if the opponent has more
gold<br />

## **Data Cleaning and Exploratory Data Analysis**

### **Data Cleaning**

When cleaning the data I decided to keep only the rows relevant to top
lane and the gold information of the two players.

I started by removing all columns besides `position`, `result`,
`goldat15`, `opp_goldat15`, and `golddiffat15`. After I had isolated the
5 columns that I would need, I filtered out all of the roles that werent
top. Once that was done I dropped the position column since the position
filtering was already done. I then checked for any missing values and
removed the rows that contained any. Lastly I created a new column
called `winning_lane` which contains either `1` or `0` for whether the
laner was winning or losing. I decided to replace `True` and `False`
with `1` and `0` because I liked the binary look better.

```py
print('hi')
```

### **Univariate**

### **Bivariate**
