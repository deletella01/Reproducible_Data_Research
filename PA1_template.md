---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---
## Author: Bamidele Tella

## Loading and preprocessing the data
1. First, we unzip and extract the dataset to the directory folder. Then we load the csv file to R.
2. The data is save to a variable vector.  

```r
unzip(zipfile = "./activity.zip") 
ActivityData<- read.csv("./activity.csv")
```

## What is mean total number of steps taken per day?

1. A base plot histogram is made to show the frequency of total steps taken per day. This is done by taking the sum of steps of all interval in the day and plotting the result in a histogram.

```r
AveTotalsteps<-data.frame(tapply(ActivityData$steps, ActivityData$date, sum, na.rm=TRUE))
colnames(AveTotalsteps) <- "Total_Steps_per_Day"
hist(AveTotalsteps$Total_Steps_per_Day, main="A Histogram of Total Daily Steps",xlab = "Average Total Daily Steps",ylim = c(0,30))
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
dev.copy(png,file='myfigure1.png')
```

```
## png 
##   3
```

```r
dev.off() 
```

```
## png 
##   2
```

2. The mean of steps taken per day is calculated, followed my the median of total steps taken.

```r
meanSteps<-data.frame(tapply(ActivityData$steps, ActivityData$date, mean, na.rm=TRUE))
colnames(meanSteps) <- "Mean-Steps-per-Day"
meanSteps
```

```
##            Mean-Steps-per-Day
## 2012-10-01                NaN
## 2012-10-02          0.4375000
## 2012-10-03         39.4166667
## 2012-10-04         42.0694444
## 2012-10-05         46.1597222
## 2012-10-06         53.5416667
## 2012-10-07         38.2465278
## 2012-10-08                NaN
## 2012-10-09         44.4826389
## 2012-10-10         34.3750000
## 2012-10-11         35.7777778
## 2012-10-12         60.3541667
## 2012-10-13         43.1458333
## 2012-10-14         52.4236111
## 2012-10-15         35.2048611
## 2012-10-16         52.3750000
## 2012-10-17         46.7083333
## 2012-10-18         34.9166667
## 2012-10-19         41.0729167
## 2012-10-20         36.0937500
## 2012-10-21         30.6284722
## 2012-10-22         46.7361111
## 2012-10-23         30.9652778
## 2012-10-24         29.0104167
## 2012-10-25          8.6527778
## 2012-10-26         23.5347222
## 2012-10-27         35.1354167
## 2012-10-28         39.7847222
## 2012-10-29         17.4236111
## 2012-10-30         34.0937500
## 2012-10-31         53.5208333
## 2012-11-01                NaN
## 2012-11-02         36.8055556
## 2012-11-03         36.7048611
## 2012-11-04                NaN
## 2012-11-05         36.2465278
## 2012-11-06         28.9375000
## 2012-11-07         44.7326389
## 2012-11-08         11.1770833
## 2012-11-09                NaN
## 2012-11-10                NaN
## 2012-11-11         43.7777778
## 2012-11-12         37.3784722
## 2012-11-13         25.4722222
## 2012-11-14                NaN
## 2012-11-15          0.1423611
## 2012-11-16         18.8923611
## 2012-11-17         49.7881944
## 2012-11-18         52.4652778
## 2012-11-19         30.6979167
## 2012-11-20         15.5277778
## 2012-11-21         44.3993056
## 2012-11-22         70.9270833
## 2012-11-23         73.5902778
## 2012-11-24         50.2708333
## 2012-11-25         41.0902778
## 2012-11-26         38.7569444
## 2012-11-27         47.3819444
## 2012-11-28         35.3576389
## 2012-11-29         24.4687500
## 2012-11-30                NaN
```

```r
medianSteps<- median(AveTotalsteps$Total_Steps_per_Day)
```
The median steps taken is 10395.

## What is the average daily activity pattern?

1. A time series plot is made to show the relationship between the 5-minute interval of the day and the average number of steps taken daily, across all days.

```r
AveStepsPerInterval<-with(ActivityData,tapply(steps,interval,mean,na.rm=TRUE))
minuteInterval<-unique(ActivityData$interval)
AveStepsInterval<-data.frame(cbind(AveStepsPerInterval,minuteInterval))

plot(AveStepsInterval$minuteInterval,AveStepsInterval$AveStepsPerInterval,type = "l",xlab = "5 minute Intervals",
     ylab = "Average Steps",main = "A Plot of Average Steps per Interval")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
dev.copy(png,file='myfigure2.png')
```

```
## png 
##   3
```

```r
dev.off()
```

```
## png 
##   2
```

2. The interval with the maximum average steps taken across all days was also calculated.

```r
MaxIntervalAverage<-AveStepsInterval[which.max(AveStepsInterval$AveStepsPerInterval),]
```
The maximum average steps taken across all days is 206.1698113, recorded at an interval of 835

## Imputing missing values

1. The number of missing values is calculated to be able to determine the amount of effect the missing values have on the result.

```r
missingValues<-is.na(ActivityData$steps)
sum(missingValues)
```

```
## [1] 2304
```

2. The average mean daily is used as a strategy to account for missing values, hence each missing value is replaced by its day average. 

3. A new data set was created from our original data set, with the mean accounted for in this data set.


```r
ActivityData2<-ActivityData
index<-which(is.na(ActivityData2$steps))
len<-length(index)
AveSteps<-with(ActivityData2,tapply(steps,date,mean,na.rm=TRUE))
na<-mean(AveSteps, na.rm = TRUE)
for (i in 1:len) {
        ActivityData2[index[i],1]<-na
}        
AveTotalsteps2<-data.frame(tapply(ActivityData2$steps, ActivityData2$date, sum, na.rm=TRUE))
colnames(AveTotalsteps2) <- "Total_Steps_per_Day"
AveTotalsteps2
```

```
##            Total_Steps_per_Day
## 2012-10-01            10766.19
## 2012-10-02              126.00
## 2012-10-03            11352.00
## 2012-10-04            12116.00
## 2012-10-05            13294.00
## 2012-10-06            15420.00
## 2012-10-07            11015.00
## 2012-10-08            10766.19
## 2012-10-09            12811.00
## 2012-10-10             9900.00
## 2012-10-11            10304.00
## 2012-10-12            17382.00
## 2012-10-13            12426.00
## 2012-10-14            15098.00
## 2012-10-15            10139.00
## 2012-10-16            15084.00
## 2012-10-17            13452.00
## 2012-10-18            10056.00
## 2012-10-19            11829.00
## 2012-10-20            10395.00
## 2012-10-21             8821.00
## 2012-10-22            13460.00
## 2012-10-23             8918.00
## 2012-10-24             8355.00
## 2012-10-25             2492.00
## 2012-10-26             6778.00
## 2012-10-27            10119.00
## 2012-10-28            11458.00
## 2012-10-29             5018.00
## 2012-10-30             9819.00
## 2012-10-31            15414.00
## 2012-11-01            10766.19
## 2012-11-02            10600.00
## 2012-11-03            10571.00
## 2012-11-04            10766.19
## 2012-11-05            10439.00
## 2012-11-06             8334.00
## 2012-11-07            12883.00
## 2012-11-08             3219.00
## 2012-11-09            10766.19
## 2012-11-10            10766.19
## 2012-11-11            12608.00
## 2012-11-12            10765.00
## 2012-11-13             7336.00
## 2012-11-14            10766.19
## 2012-11-15               41.00
## 2012-11-16             5441.00
## 2012-11-17            14339.00
## 2012-11-18            15110.00
## 2012-11-19             8841.00
## 2012-11-20             4472.00
## 2012-11-21            12787.00
## 2012-11-22            20427.00
## 2012-11-23            21194.00
## 2012-11-24            14478.00
## 2012-11-25            11834.00
## 2012-11-26            11162.00
## 2012-11-27            13646.00
## 2012-11-28            10183.00
## 2012-11-29             7047.00
## 2012-11-30            10766.19
```

4. A base plot histogram is plotted to show the total steps taken daily with the missing values accounted for. The relative mean and median of the new data set were also calculated to also account for the missing value.

```r
hist(AveTotalsteps2$Total_Steps_per_Day, xlab = "Total Steps Without Missing Values", ylab = "Frequency",main = "Total Number of Steps per Day with Missing Values Excluded")
```

![](PA1_template_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

```r
dev.copy(png,file='myfigure3.png')
```

```
## png 
##   3
```

```r
dev.off()
```

```
## png 
##   2
```

```r
meanSteps2<-data.frame(tapply(ActivityData2$steps, ActivityData2$date, mean, na.rm=TRUE))
colnames(meanSteps2) <- "Mean-Steps-per-Day"
meanSteps2
```

```
##            Mean-Steps-per-Day
## 2012-10-01         37.3825996
## 2012-10-02          0.4375000
## 2012-10-03         39.4166667
## 2012-10-04         42.0694444
## 2012-10-05         46.1597222
## 2012-10-06         53.5416667
## 2012-10-07         38.2465278
## 2012-10-08         37.3825996
## 2012-10-09         44.4826389
## 2012-10-10         34.3750000
## 2012-10-11         35.7777778
## 2012-10-12         60.3541667
## 2012-10-13         43.1458333
## 2012-10-14         52.4236111
## 2012-10-15         35.2048611
## 2012-10-16         52.3750000
## 2012-10-17         46.7083333
## 2012-10-18         34.9166667
## 2012-10-19         41.0729167
## 2012-10-20         36.0937500
## 2012-10-21         30.6284722
## 2012-10-22         46.7361111
## 2012-10-23         30.9652778
## 2012-10-24         29.0104167
## 2012-10-25          8.6527778
## 2012-10-26         23.5347222
## 2012-10-27         35.1354167
## 2012-10-28         39.7847222
## 2012-10-29         17.4236111
## 2012-10-30         34.0937500
## 2012-10-31         53.5208333
## 2012-11-01         37.3825996
## 2012-11-02         36.8055556
## 2012-11-03         36.7048611
## 2012-11-04         37.3825996
## 2012-11-05         36.2465278
## 2012-11-06         28.9375000
## 2012-11-07         44.7326389
## 2012-11-08         11.1770833
## 2012-11-09         37.3825996
## 2012-11-10         37.3825996
## 2012-11-11         43.7777778
## 2012-11-12         37.3784722
## 2012-11-13         25.4722222
## 2012-11-14         37.3825996
## 2012-11-15          0.1423611
## 2012-11-16         18.8923611
## 2012-11-17         49.7881944
## 2012-11-18         52.4652778
## 2012-11-19         30.6979167
## 2012-11-20         15.5277778
## 2012-11-21         44.3993056
## 2012-11-22         70.9270833
## 2012-11-23         73.5902778
## 2012-11-24         50.2708333
## 2012-11-25         41.0902778
## 2012-11-26         38.7569444
## 2012-11-27         47.3819444
## 2012-11-28         35.3576389
## 2012-11-29         24.4687500
## 2012-11-30         37.3825996
```

```r
medianSteps2<- median(AveTotalsteps2$Total_Steps_per_Day)
```
The new median is calculated to be 1.0766189\times 10^{4}.

## Are there differences in activity patterns between weekdays and weekends?
1. A new factor of the weekdays and weekends, was created. 

Make a panel plot containing a time series plot (i.e. type = "l") of the
5-minute interval (x-axis) and the average number of steps taken, averaged
across all weekday days or weekend days (y-axis). The plot should look
something like the following, which was creating using simulated data


```r
ActivityData2$date <- as.Date(strptime(ActivityData2$date, format="%Y-%m-%d"))
ActivityData2$day <- weekdays(ActivityData2$date)
for (i in 1:nrow(ActivityData2)) {
        if (ActivityData2[i,]$day %in% c("Saturday","Sunday")) {
                ActivityData2[i,]$day<-"weekend"
        }
        else{
                ActivityData2[i,]$day<-"weekday"
        }
}
```

2. A plot using the ggplot2 system was used to created a visualization of the average steps over the different interval, taken by weekdays and weekends.

```r
stepsByDay <- aggregate(ActivityData2$steps ~ ActivityData2$interval + ActivityData2$day, ActivityData2, mean)
colnames(stepsByDay)<-c("Interval","Day","Steps")
library(ggplot2)
gStepsbyDay <- ggplot(stepsByDay,aes(Interval,Steps)) 
gStepsbyDay<-gStepsbyDay + geom_line() + facet_grid(Day~.)
gStepsbyDay<-gStepsbyDay + labs(xlab="Interval",ylab="Average Number of Steps")
gStepsbyDay
```

![](PA1_template_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

```r
dev.copy(png,file='myfigure4.png')
```

```
## png 
##   3
```

```r
dev.off()
```

```
## png 
##   2
```
