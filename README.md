Turn in one copy for each group. If group members are not present in class they will be required to complete their own lab to receive credit. Please turn in **both a DOC or PDF file and your R Markdown script**. 

## Lab Overview
This lab is extremely open ended with the goal of creating data visualization with `ggplot2`. For each figure, include a 2-3 sentence description.

## Question 1 (5 points)

Create a better (or new) version of your final figure from Lab 2.

```
library(tidyverse)
mt_ppp <- read_csv('https://raw.githubusercontent.com/stat408/Lab2/master/MT_PPP.csv')
```


## Question 2 (10 points)

Create at least two figures from the OkCupid dataset, see additional details below. Note, this lab will also get you thinking about data wrangling / manipulation.


#### Description
R package of cleaned profile data from "OkCupid Profile Data for Introductory Statistics and Data Science Courses": 59,946 OkCupid users who were living within 25 miles of San Francisco, had active profiles on June 26, 2012, were online in the previous year, and had at least one picture in their profile. The original data, publication, code, and codebook can be found at [https://github.com/rudeboybert/JSE_OkCupid](https://github.com/rudeboybert/JSE_OkCupid).

#### References
Albert Y. Kim, Adriana Escobedo-Land (2015). OkCupid Profile Data for Introductory Statistics and Data Science Courses. Journal of Statistics Education, 23(2). [http://www.amstat.org/publications/jse/v23n2/kim.pdf](http://www.amstat.org/ publications/jse/v23n2/kim.pdf).

```
library(okcupiddata)
data(profiles)
```

