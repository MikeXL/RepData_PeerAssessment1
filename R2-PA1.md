---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
    theme: paper
    includes:
      in_header: ga_track.html
---
## Introduction
It is now possible to collect a large amount of data about personal movement using activity monitoring devices such as a Fitbit, Nike Fuelband, or Jawbone Up. These type of devices are part of the “quantified self” movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. But these data remain under-utilized both because the raw data are hard to obtain and there is a lack of statistical methods and software for processing and interpreting the data.

This assignment makes use of data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.

The data for this assignment can be downloaded from the course web site:

Dataset: [Activity monitoring data][1] [52K]
The variables included in this dataset are:

steps: Number of steps taking in a 5-minute interval (missing values are coded as \color{red}{\verb|NA|}NA)
date: The date on which the measurement was taken in YYYY-MM-DD format
interval: Identifier for the 5-minute interval in which measurement was taken
The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this dataset.

## Load necessary libraries

```r
library(dplyr)
library(tidyr)
```

## Loading and preprocessing the data

```r
data.url  <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
data.file <- "data/activity.zip"
download.file(data.url, data.file)
csv.file = as.character(unzip(data.file, list=T)$Name)
df <- read.csv(unzip(data.file, csv.file), header=T, sep=",")
```


## What is mean total number of steps taken per day?

1. Calculate the total number of steps taken per day  

```r
df.agg <- df %>% 
            drop_na() %>% 
            group_by(date) %>% 
            summarise(steps_total  = sum(steps), 
                      steps_mean   = mean(steps), 
                      steps_median = median(steps)
                    )
```
2. Histogram of the total number of steps taken each day  


```r
hist(df.agg$steps_mean, main="Histogram of the total number of steps taken each day", xlab=NA)
```

![](R2-PA1_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

3. Calculate and report the mean and median of the total number of steps taken per day  


```r
head(df.agg)
```

```
## # A tibble: 6 x 4
##   date       steps_total steps_mean steps_median
##   <fct>            <int>      <dbl>        <dbl>
## 1 2012-10-02         126      0.438            0
## 2 2012-10-03       11352     39.4              0
## 3 2012-10-04       12116     42.1              0
## 4 2012-10-05       13294     46.2              0
## 5 2012-10-06       15420     53.5              0
## 6 2012-10-07       11015     38.2              0
```

## What is the average daily activity pattern?
4. Time series plot of the average number of steps taken  

```r
plot(df.agg$steps_mean ~ as.Date(df.agg$date), type="l", xlab=NA, ylab=NA, main = "average steps taken daily", frame=F, axes = T, col="#66cc00", cex.lab=.25)
```

![](R2-PA1_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?



[1]: https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip
