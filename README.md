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

<iframe src="assets/damagetochampions.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis
<iframe src="assets/goldspentvsdamage.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/positionvsdamage.html" width=800 height=600 frameBorder=0></iframe>

### Interesting Aggregates
| position   |   [0, 5) |   [5, 10) |   [10, 15) |   [15, 20) |   [20, 25) |   [25, 30) |
|:-----------|---------:|----------:|-----------:|-----------:|-----------:|-----------:|
| bot        |  1.58313 |   6.46181 |    12.1394 |    16.6667 |    21.7143 |       26.5 |
| mid        |  1.49315 |   6.56433 |    12.1958 |    16.8605 |    21.2308 |       26.5 |


| position   |   [0, 5) |
|:-----------|---------:|
| bot        |  1.30037 |
| mid        |  1.33882 |
---

## **Assessment of Missingness**

We realize there's some columns includes missing value that are **not missing at random** such as "elemental drakes", "elders", "heralds".etc.  The data is extracted from Riot's database [Oracle’s Elixir](https://oracleselixir.com/tools/downloads), since the data is official League of Legends competition information. In this case, if a certain data is missing in the dataframe, it indicates that it is not recorded in Riot's database of website. Thus is **NMAR**

---

To check the Missingness dependency, we pick the one column with non-trivil missingness("golddiffat15") and use permutation test to visualize result.
<iframe src="assets/dependmissing.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/notdependmissing.html" width=800 height=600 frameBorder=0></iframe>

---

## Hypothesis Testing

In order to prevent too many assists from AOE, we decided to use DR (dominated ratio 2Kills + 1Assists/ 3Deaths) to calculate the performance of each lane. In addition, in order to prevent kills that do not match damage circumstances, and economic gaps make a difference, we will also compare DPG (Damage to hero/Money spent)

---

Our null hypothesis is: Bot lane players have the same DR (Dominance Ratio) and DPG (Damage to Champion per Gold )as the Mid lane players
μbot = μmid
Alternative: Bot lane players have better DR than the Mid lane players
μbot > μmid

Test statistics: TVD

Significance level: 0.05

---


---

# Conclusion

From both cases, From observed data and the permutation distribution we found significant level are below 0.05 which means difference in DR and DPG between mid and bot lane are not likely to occured by chance. It gives potential result that bot lane usually deal more damage and better performance than mid lane.
