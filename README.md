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

By simplifying the data down to 6 columns and around 21000 rows, I had
all the data I would need in order to answer whether winning became more
likely when the top laner was fed.

**Columns Used** <br />
`result` -\> `1` if the match was won and `0` if the
match was lost<br /> `champion` -\> The character that the player was using
`goldat15` -\> The total amount of gold the player
has gathered at 15 minutes <br /> `opp_goldat15` -\> The total amount of
gold the opponent has gathered at 15 minutes<br /> `golddiffat15` -\>
The differential in gold between the two players<br /> `winning_lane`
-\> `1` if the player has more gold and `0` if the opponent has more
gold<br />

## **Data Cleaning and Exploratory Data Analysis**

### **Data Cleaning**

When cleaning the data I decided to keep only the rows relevant to top
lane and the gold information of the two players.

I started by removing all columns besides `position`, `champion`, `result`,
`goldat15`, `opp_goldat15`, and `golddiffat15`. After I had isolated the
6 columns that I would need, I filtered out all of the roles that werent
top. Once that was done I dropped the position column since the position
filtering was already done. I then checked for any missing values and
removed the rows that contained any. Lastly I created a new column
called `winning_lane` which contains either `1` or `0` for whether the
laner was winning or losing. I decided to replace `True` and `False`
with `1` and `0` because I liked the binary look better.


Here is the head of the data frame

| position   | champion   |   result |   goldat15 |   opp_goldat15 |   golddiffat15 |   winning_lane |
| top        | Renekton   |        0 |       5025 |           4634 |            391 |              1 |
| top        | Gragas     |        1 |       4634 |           5025 |           -391 |              0 |
| top        | Gragas     |        0 |       4673 |           6157 |          -1484 |              0 |
| top        | Gangplank  |        1 |       6157 |           4673 |           1484 |              1 |
| top        | Renekton   |        1 |       5856 |           4952 |            904 |              1 |







### **Univariate**

<iframe src="assets/uniHist.html" width=800 height=600 frameBorder=0></iframe>

This histogram provides a visual representation of the amount of gold that top 
laners have collected by 15 minutes which tends to be around 4000 to 6000 gold.

### **Bivariate**

<iframe src="assets/biBox.html" width=800 height=600 frameBorder=0></iframe>

This box plot shows the gold diff at 15 minutes and whether they won or not. As 
you can see there is not much of a difference in whether the gold lead helps 
the top laner win or not.

<iframe src="assets/biScatter.html" width=800 height=600 frameBorder=0></iframe>

This scatter plot shows how much gold a top laner has at 15 minutes and the gold 
difference between them and their opponent. I included this one because I thought 
it was interesting.

### **Interesting Aggregates**

|   result |   mean |   median |     std |   min |   max |
|        0 | 5071.8 |     5009 | 603.128 |  2806 |  8288 |
|        1 | 5401.1 |     5290 | 703.966 |  3062 |  9854 |


This `groupby()` shows that when the top laners are winning they generally have 
more gold than their opponents. While the gold differences dont seem like much, in 
league of legends even a 200 gold lead can mean a won or lost fight. 


## **Assessment of Missingness**

### **NMAR Analysis**

Due to the way the data is presented I believe that there is are columns in the 
dataset that are NMAR (not missing at random). A good example is how the gold 
information for some of the players was missing but the gold information for 
other players in the same game was present. There are also some games where the 
gold information is completely missing for players but the it is present for 
the teams overall. This points towards the possibility that the missingness 
depends on the column itself and not another column. Some data that might suggest 
that the data is MAR (missing at random) would be if it was missing based on the 
role being played or the league the match was being played in.

### **Missingness Dependency**

To test if the missingness in one of the columns might be NMAR or MAR I took 
`opp_goldat15` and tested whether its missingness depended on `results` or 
`champion`. 

My permutation tests found that with a p-value of 0.4595404595404595 
for the dependency of `opp_goldat15` on `result` there is no evidence to conclude 
that `opp_goldat15` depends on `result`. Therefore in this case we fail to reject 
the null hypothesis.

|        0 |        1 |   Total |
| 0.500094 | 0.499906 |       1 |
| 0.5      | 0.5      |       1 |
| 0.50008  | 0.49992  |       1 |

<iframe src="assets/empDist.html" width=800 height=600 frameBorder=0></iframe>


For the second part of the permutation tests I tested whether `opp_goldat15` was 
independent from `champion`. With a p-value of 0.000999000999000999 for the 
independence of `opp_goldat15` from `champion` there is evidence to conclude that 
`opp_goldat15` is not independent from `champion` and therefore we reject the 
null hypothesis.

For this table I only included the first 10 champions since there are more than 160 champions in the game

|     Aatrox |      Ahri |      Akali |      Akshan |    Alistar |      Amumu |      Anivia |       Annie |   Aphelios |       Ashe|
| 0.0118615  | 0.0227448 | 0.012868   | 0.00179663  | 0.00576616 | 0.00385665 | 0.000442103 | 0.000112877 |  0.0302229 | 0.00366852 |
| 0.00830126 | 0.028862  | 0.00951072 | 0.000604728 | 0.0117097  | 0.00307861 | 5.49753e-05 | 0.000109951 |  0.0459593 | 0.00153931 |
| 0.0113414  | 0.0236386 | 0.0123775  | 0.00162249  | 0.00663454 | 0.00374297 | 0.000385542 | 0.00011245  |  0.0325221 | 0.00335743 |

<iframe src="assets/empDist2.html" width=800 height=600 frameBorder=0></iframe>


## **Hypothesis Testing**






