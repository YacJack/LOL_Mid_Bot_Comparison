# LOL_Mid_Bot_Comparison

by Shuang Wu (shw076@ucsd.edu) , Yacheng Xiao (yaxiao@ucsd.edu)

---

## Introduction

"This is the version of AD, AD loses, the game is lost" 
We hear these voices all the time when we play League of Legends with our friends. But is the bottom lane really the key to the outcome of the game? In other words, compared to other lanes such as the jungler and the middle lane, is the bottom lane really usually the most Carry? Compared with the bottom lane, the middle lane often goes to various lanes to help, and the existence of the middle lane is also key to the game. 
As one of the tests to see if the bot lane is the most Carry route, we decided to compare the bot lane and the mid lane which will carry more. As one of the most competitive leagues, we selected the data of the 2022 LCK game to compare kills. Death, assists and DR, KDA, damage taken/damage per gold to compare which lane is more Carry. In this dataset, we have 1868 rows in total, which includes mid and bot position only. DR represents for Dominance Ratio, calculated by (2*Kills + Assists) / 3*Deaths, which is a comprehensive way to view excellence according to players. KDA is calculated by Kills + Assists / Deaths.

---

## Cleaning and EDA
### Univariate Analysis
<iframe src="assets/kills.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/golddiffat15.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/DR.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis
<iframe src="assets/goldvsxp.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/posvsgold.html" width=800 height=600 frameBorder=0></iframe>


### Interesting Aggregates

---

## Assessment of Missingness

Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using

```py
print(counts[['Quarter', 'Count']].head().to_markdown(index=False))
```

| Quarter     |   Count |
|:------------|--------:|
| Fall 2020   |       3 |
| Winter 2021 |       2 |
| Spring 2021 |       6 |
| Summer 2021 |       4 |
| Fall 2021   |      55 |

---

## Hypothesis Testing


---
