# **LOL_Mid_Bot_Comparison**

by Shuang Wu (shw076@ucsd.edu) , Yacheng Xiao (yaxiao@ucsd.edu)

---

## **Introduction**

### "This is the version of AD, AD loses, the game is lost" 
We hear these voices all the time when we play League of Legends with our friends. But is the bottom lane really the key to the outcome of the game? 

**In other words, compared to other lanes such as the jungler and the middle lane, is the bottom lane really usually the most Carry? Compared with the bottom lane, the middle lane often goes to various lanes to help, and the existence of the middle lane is also key to the game**. 

Here is how we define "carry":
1. The overall performance in games, represented by DR (explained below)
2. The ability to transform gold (resource) to damage

As one of the tests to see if the bot lane is the most Carry route, we decided to compare the bot lane and the mid lane which will carry more. As one of the most competitive leagues, we selected the data of the **2022 LCK game** to compare kills. Death, assists and DR, KDA, damage taken/damage per gold to compare which lane is more Carry. In this dataset, we have 1868 rows in total, which includes mid and bot position only. 

#### Some terms in columns:
1. DR represents for Dominance Ratio, calculated by *(2 x Kills + Assists) / 3 x Deaths*, which is a comprehensive way to view excellence according to players. 
2. KDA is calculated by *Kills + Assists / Deaths*.
3. DPG represents efficiency of ultilizing gold to deal damage to enemy champion.

---

## **Cleaning and EDA**
### Univariate Analysis
<iframe src="assets/goldspent.html" width=800 height=600 frameBorder=0></iframe>

This is a visual presentation for the "goldspent" variable. We can observe that the distribution of gold spent is approximately normal but slightly skewed to the right.

This makes sense because few players could spend more than 40k gold in a game.


<iframe src="assets/damagetochampions.html" width=800 height=600 frameBorder=0></iframe>

This is a visual presentation for the "damage to champions" varaible. We can observe that the distribution of damage to champions is also approximately normal and skewed to the right.

This makes sense because extremely high damage is not normal in League of Legends.

### Bivariate Analysis
<iframe src="assets/goldspentvsdamage.html" width=800 height=600 frameBorder=0></iframe>

From gold vs damage to champions scatter plot, we observe a clear positive relationship between them. 

Though the relationship is not too strong, it makes sense that with more gold, players tend to deal more damage.


<iframe src="assets/positionvsdamage.html" width=800 height=600 frameBorder=0></iframe>

From the box plot of mid and bot players' position vs damage to champions, we observe a higher median, max, min, and box range in bot lane players.

Thus, we might consider using "bot lane player carries more" as our alternative hypothesis.

### Interesting Aggregates

| position   |   [0, 5) |   [5, 10) |   [10, 15) |   [15, 20) |   [20, 25) |   [25, 30) |
|:-----------|---------:|----------:|-----------:|-----------:|-----------:|-----------:|
| bot        |  1.58313 |   6.46181 |    12.1394 |    16.6667 |    21.7143 |       26.5 |
| mid        |  1.49315 |   6.56433 |    12.1958 |    16.8605 |    21.2308 |       26.5 |

This is a pivot table for position and DR. From this table, we do not observe a significant difference between bot and mid lane players.


| position   |   [0, 5) |
|:-----------|---------:|
| bot        |  1.30037 |
| mid        |  1.33882 |

This is a pivot table for position and damage per gold. From this table, we observe a little advance of mid lane players on damage per gold compared to bot lane players.

---

## **Assessment of Missingness**

We realize there's some columns includes missing value that are **not missing at random** such as "elemental drakes", "elders", "heralds".etc.  

The data is extracted from Riot's database [Oracle’s Elixir](https://oracleselixir.com/tools/downloads), since the data is official League of Legends competition information. In this case, if a certain data is missing in the dataframe, it indicates that it is not recorded in Riot's database of website. Thus is **NMAR**.

---

#### To check the Missingness dependency, we pick the one column with non-trivil missingness("golddiffat15") and use permutation test to visualize result.

<iframe src="assets/dependmissing.html" width=800 height=600 frameBorder=0></iframe>

**Null Hypothesis: Missingness of "golddiffat15" does not depend on url**

**Alternative Hypothesis: Missingness of "golddiffat15" depends on url**

In this testing, we analyzed if url could be a depending column of the missingness of "golddiffat15".

We observed a p-value of 1 (> 0.05), which is significantly large. Thus, we fail to reject the null hypothesis and conclude that missingness of "golddiffat15" depend on url.


<iframe src="assets/notdependmissing.html" width=800 height=600 frameBorder=0></iframe>

**Null Hypothesis: Missingness of "golddiffat15" does not depend on position**

**Alternative Hypothesis: Missingness of "golddiffat15" depends on position**

In this testing, we analyzed if position could be a depending column of the missingness of "golddiffat15".
We observed a p-value of 0, which is significantly small (< 0.05). Thus, we fail to reject the null hypothesis and conclude that missingness of "golddiffat15" does not depend on position.

---

## **Hypothesis Testing**

In order to prevent too many assists from AOE (Damage that is caused by large area spell), since these kind of damage could be done easily by not even aiming, we decided to use DR (dominated ratio *2Kills + 1Assists/ 3Deaths*) to calculate the performance of each lane. 

In addition, in order to prevent kills that do not match damage circumstances, and economic gaps make a difference, we will also compare DPG (Damage to champions / Money spent)

---

**Null hypothesis: Bot lane players have the same DR (Dominance Ratio) and DPG (Damage to Champion per Gold ) as the Mid lane players**

*μbot = μmid*

**Alternative: Bot lane players have better DR and / or DPG than the Mid lane players**

*μbot > μmid*

**Test statistics: TVD**

**Significance level: 0.05**

---
<iframe src="assets/hyp1.html" width=800 height=600 frameBorder=0></iframe>

This is the visual presentation for the hypothesis testing for DR and position


<iframe src="assets/hyp2.html" width=800 height=600 frameBorder=0></iframe>

This is the visual presentation for the hypothesis testing for dpg and position

---

# **Conclusion**

From observed data and the permutation distribution we found the p-value is 0.02, which is below the significance level 0.05, which means difference in DR between mid and bot lane are not likely to occured by chance. It gives potential result that bot lane usually deal more damage and better performance than mid lane.
However, for damage per gold, we observed a p-value of 0.076, which is greater than the significance level 0.05, and we fail to reject the null hypothesis in this case and conclude that mid lane players are likely to have the same damage per gold as the bot lane players.

**By just looking at the scoreboard of a player (Kills, Assists), we might observe that bot lane players carry more, as we also carried out a testing on DR. But, in fact, for every gold the two positions earn, the damages they could produce are likely to be similar.**
**Thus, we conclude that bot lane players potentially carry more, with their potential better kills and deaths in a game; however, this carry does not necessarily indicate that bot lane players carry more in damage wise.**
