## Introduction

It is now possible to collect a large amount of data about personal
movement using activity monitoring devices such as a
[Fitbit](http://www.fitbit.com), [Nike
Fuelband](http://www.nike.com/us/en_us/c/nikeplus-fuelband), or
[Jawbone Up](https://jawbone.com/up). These type of devices are part of
the "quantified self" movement -- a group of enthusiasts who take
measurements about themselves regularly to improve their health, to
find patterns in their behavior, or because they are tech geeks. But
these data remain under-utilized both because the raw data are hard to
obtain and there is a lack of statistical methods and software for
processing and interpreting the data.

This project makes use of data from a personal activity monitoring
device. This device collects data at 5 minute intervals through out the
day. The data consists of two months of data from an anonymous
individual collected during the months of October and November, 2012
and include the number of steps taken in 5 minute intervals each day.

This project analysis can viewed at https://rpubs.com/Deletella01/639255

## Data

The data for this assignment can be downloaded from the course web
site:

* Dataset: [Activity monitoring data](https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip) [52K]

The variables included in this dataset are:

* **steps**: Number of steps taking in a 5-minute interval (missing
    values are coded as `NA`)

* **date**: The date on which the measurement was taken in YYYY-MM-DD
    format

* **interval**: Identifier for the 5-minute interval in which
    measurement was taken




The dataset is stored in a comma-separated-value (CSV) file and there
are a total of 17,568 observations in this
dataset.


## Assignment

This assignment will be described in multiple parts. The report written
answers the questions detailed below. Ultimately, the entire assignment
was completed in a **single R markdown** document that was 
processed by **knitr** and transformed into an HTML file.

Throughout the report, the code that was used to generate the output 
presented were always included. When writing code chunks in the R markdown
document, `echo = TRUE` was used so that someone else will be able to
read the code.


### Loading and preprocessing the data

All the code Shown includes:

1. Loading the data (i.e. `read.csv()`).

2. Processing/transforming the data into a format suitable for the analysis.


### What is mean total number of steps taken per day?

For this part of the assignment,the missing values in
the dataset were ignored.

1. A histogram of the total number of steps taken each day was made.

2. The **mean** and **median** of the total number of steps taken per day was calculated and reported.


### What is the average daily activity pattern?

1. A time series plot (i.e. `type = "l"`) of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis) was made.

2. The maximum number of steps for every 5-minute interval, on average across all the days in the dataset.


### Imputing missing values

Note that there are a number of days/intervals where there are missing
values (coded as `NA`). The presence of missing days may introduce
bias into some calculations or summaries of the data.

1. The total number of missing values in the dataset (i.e. the total number of rows with `NA`s) was calculated and reported.

2. A strategy for filling in all of the missing values in the dataset was devised.

3. A new dataset that is equal to the original dataset but with the missing data filled in, was created.

4. A histogram of the total number of steps taken each day was made and the **mean** and **median** total number of steps taken per day was Calculated and reported. The goal here is to find the impact of imputing missing data on the estimates of the total daily number of steps.


### Are there differences in activity patterns between weekdays and weekends?

For this part, the `weekdays()` function were of some help here. The dataset with the filled-in missing valueswas used for this part.

1. A new factor variable in the dataset with two levels was created, "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.

2. A panel plot containing a time series plot (i.e. `type = "l"`) of the 5-minute interval (x-axis) and the average number of steps taken was made, averaged across all weekday days or weekend days (y-axis). 


