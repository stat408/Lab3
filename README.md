# Lab3

Turn in one copy for each group. Please turn in **both an HTML/PDF/DOC file and your R Markdown script**. Students not attending class will need to complete the lab on their own.

## Lab Overview

For this lab we will focus on writing functions and applying those functions to a data frame containing trip information from Uber. This data was compiled by 538.com and used in several stories including [https://fivethirtyeight.com/features/uber-is-serving-new-yorks-outer-boroughs-more-than-taxis-are/](https://fivethirtyeight.com/features/uber-is-serving-new-yorks-outer-boroughs-more-than-taxis-are/). More information about the data can be found at [https://github.com/fivethirtyeight/uber-tlc-foil-response](https://github.com/fivethirtyeight/uber-tlc-foil-response), but the data has been cleaned for you.

The entire lab will be worth 20 points. Clarity of code, including comments and interpretable variables names, along with thoughtful writing with an emphasis on concise interpretations will be considered when grading. 

## Questions
Answer the following questions in this R Markdown document. Please include code where necessary.


Download the Uber dataset, available at: [http://math.montana.edu/ahoegh/teaching/stat408/datasets/UberMay2014.csv](http://math.montana.edu/ahoegh/teaching/stat408/datasets/UberMay2014.csv). This file contains the trip start time for Uber pickups in New York City during the first week of May, 2014. 

```{r}
library(readr)
uber <- read.csv('http://math.montana.edu/ahoegh/teaching/stat408/datasets/UberMay2014.csv', stringsAsFactors = F)
```
Note using `read_csv` will import the TimeStamp variable as a time object and will require different functions in part 1.


### 1. Writing functions
#### a. (3 points)
We would like to identify which day of the week Uber makes the most pickups. Given that May 1, 2014 is a Thursday, we want a function that:

- takes the date (day in May 2014) and
- returns the day of the week. 

Finish the documentation for this function.
```{r}
FindDay <- function(day){
  # finds ... 
  # ARGS:
  # Returns:
  modulo.date <- day %% 7
  key <- cbind(0:6, c('Wednesday','Thursday','Friday','Saturday','Sunday','Monday','Tuesday'))
  if (day > 31 | day <= 0) stop('Please enter a valid date as a numeric value')
  return(key[key[,1] == modulo.date, 2])
}
```


We can verify this works by running the code inline. So the day for May 8 can be found by executing the code `FindDay(8)` in R. Thus May 8 is a `r FindDay(8)`.

#### b. (5 points)
We are also interested in knowing which block of time has the most trips. Note that these times are in military time, where 0 = midnight and 20 = 8 PM. Write a function called `FindTime()` that:

- takes an input time as hh:mm ("12:21") and 
-returns the following blocks of time:

    - "late night": after 22 - to 4
    - "morning": after 4 -  to 10
    - "midday": after 10 - to 16
    - "evening": after 16 -  to 22

I have given you a head start, as the code strips the hour out of the time stamp.
```{r}
FindHour <- function(time.in){
  # Function to find hour from time in 'hh:mm' format
  # ARGS: time as string with 'hh:mm'
  # Returns: hour as numeric value
  hour <- strsplit(time.in,':')[[1]][1]
  hour <- as.numeric(hour)
  return(hour)
}
```

For example running `FindHour('04:37')` will return `r FindHour('04:37')`

Now complete the function below and include documentation

```{r}
FindTime <- function(time.in){
  # Function to 
  # ARGS: time as string with 'hh:mm'
  # Returns: 
  hour <- FindHour(time.in)
  if (hour < 4) {
    return('Morning')
  } else if (hour >= 4){
    return('Not Morning')
  }
}
```
Demonstrate this works by showing `FindTime('04:37')` and `FindTime('23:12')`

### 2. Computing Counts

#### a. (5 points)
Implement your day of week function on the uber data set to count the number of trips for each day of the week. Print a table showing the total number of trips for each day.
```{r}
library(dplyr)
# create additional column with week day info
uber$weekday <- sapply(uber$Day, FindDay)
```


#### b. (5 points)
Implement your time of day function on the uber data set to the count the number of trips for each time period. Print a table showing the total number of trips per time period.

### 3. Summarizing Data 

#### a. (1 points)
Summarize your findings in 3a and 3b. Do they match your expectations, why or why not?

#### b. (1 points)
In a broader sense, how can these results be used to infer about general Uber trends, for instance in other places or during more recent time periods?
