Reproducible Research: Peer Assessment 1
========================================================

The following libraries need to be instaled before running the code:

```r
library(lattice)
library(xtable)
library(plyr)
```


## Loading and preprocessing the data

Unzip, load and arrange data over the file **activity.zip** into a dataframe 
named **act**. Create new variable **fdate** that has the measurements date in 
POSIXct format.


```r
unzip("activity.zip")
act <- read.csv("activity.csv")
act$fdate <- as.POSIXct(strptime(act$date, "%Y-%m-%d"))
dly <- ddply(act, ~date, summarise, Mean = mean(steps, na.rm = T), Median = median(steps, 
    na.rm = T), Steps = sum(steps, na.rm = T))
```




## What is mean total number of steps taken per day?

The following plot shows that most days have a near 10k valid step samples, 
but there are several of days (16% approx.) between 0 and 2k.


```r
histogram(~Steps, data = dly, breaks = 8, main = "Distribution of Steps per Day")
```

![plot of chunk stepshist](figure/stepshist.png) 




```r
names(dly) <- c("Measurement Date", "Daily Mean (Steps)", "Daily Median (Steps)", 
    "Total Daily (Steps)")
print(xtable(dly), type = "html", align = rep("c", 3), include.rownames = F, 
    html.table.attributes = "border = '1'")
```

<!-- html table generated in R 3.0.3 by xtable 1.7-3 package -->
<!-- Wed May 14 23:29:49 2014 -->
<TABLE border = '1'>
<TR> <TH> Measurement Date </TH> <TH> Daily Mean (Steps) </TH> <TH> Daily Median (Steps) </TH> <TH> Total Daily (Steps) </TH>  </TR>
  <TR> <TD> 2012-10-01 </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD align="right">   0 </TD> </TR>
  <TR> <TD> 2012-10-02 </TD> <TD align="right"> 0.44 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 126 </TD> </TR>
  <TR> <TD> 2012-10-03 </TD> <TD align="right"> 39.42 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 11352 </TD> </TR>
  <TR> <TD> 2012-10-04 </TD> <TD align="right"> 42.07 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 12116 </TD> </TR>
  <TR> <TD> 2012-10-05 </TD> <TD align="right"> 46.16 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 13294 </TD> </TR>
  <TR> <TD> 2012-10-06 </TD> <TD align="right"> 53.54 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 15420 </TD> </TR>
  <TR> <TD> 2012-10-07 </TD> <TD align="right"> 38.25 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 11015 </TD> </TR>
  <TR> <TD> 2012-10-08 </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD align="right">   0 </TD> </TR>
  <TR> <TD> 2012-10-09 </TD> <TD align="right"> 44.48 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 12811 </TD> </TR>
  <TR> <TD> 2012-10-10 </TD> <TD align="right"> 34.38 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 9900 </TD> </TR>
  <TR> <TD> 2012-10-11 </TD> <TD align="right"> 35.78 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10304 </TD> </TR>
  <TR> <TD> 2012-10-12 </TD> <TD align="right"> 60.35 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 17382 </TD> </TR>
  <TR> <TD> 2012-10-13 </TD> <TD align="right"> 43.15 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 12426 </TD> </TR>
  <TR> <TD> 2012-10-14 </TD> <TD align="right"> 52.42 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 15098 </TD> </TR>
  <TR> <TD> 2012-10-15 </TD> <TD align="right"> 35.20 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10139 </TD> </TR>
  <TR> <TD> 2012-10-16 </TD> <TD align="right"> 52.38 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 15084 </TD> </TR>
  <TR> <TD> 2012-10-17 </TD> <TD align="right"> 46.71 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 13452 </TD> </TR>
  <TR> <TD> 2012-10-18 </TD> <TD align="right"> 34.92 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10056 </TD> </TR>
  <TR> <TD> 2012-10-19 </TD> <TD align="right"> 41.07 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 11829 </TD> </TR>
  <TR> <TD> 2012-10-20 </TD> <TD align="right"> 36.09 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10395 </TD> </TR>
  <TR> <TD> 2012-10-21 </TD> <TD align="right"> 30.63 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 8821 </TD> </TR>
  <TR> <TD> 2012-10-22 </TD> <TD align="right"> 46.74 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 13460 </TD> </TR>
  <TR> <TD> 2012-10-23 </TD> <TD align="right"> 30.97 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 8918 </TD> </TR>
  <TR> <TD> 2012-10-24 </TD> <TD align="right"> 29.01 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 8355 </TD> </TR>
  <TR> <TD> 2012-10-25 </TD> <TD align="right"> 8.65 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 2492 </TD> </TR>
  <TR> <TD> 2012-10-26 </TD> <TD align="right"> 23.53 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 6778 </TD> </TR>
  <TR> <TD> 2012-10-27 </TD> <TD align="right"> 35.14 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10119 </TD> </TR>
  <TR> <TD> 2012-10-28 </TD> <TD align="right"> 39.78 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 11458 </TD> </TR>
  <TR> <TD> 2012-10-29 </TD> <TD align="right"> 17.42 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 5018 </TD> </TR>
  <TR> <TD> 2012-10-30 </TD> <TD align="right"> 34.09 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 9819 </TD> </TR>
  <TR> <TD> 2012-10-31 </TD> <TD align="right"> 53.52 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 15414 </TD> </TR>
  <TR> <TD> 2012-11-01 </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD align="right">   0 </TD> </TR>
  <TR> <TD> 2012-11-02 </TD> <TD align="right"> 36.81 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10600 </TD> </TR>
  <TR> <TD> 2012-11-03 </TD> <TD align="right"> 36.70 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10571 </TD> </TR>
  <TR> <TD> 2012-11-04 </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD align="right">   0 </TD> </TR>
  <TR> <TD> 2012-11-05 </TD> <TD align="right"> 36.25 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10439 </TD> </TR>
  <TR> <TD> 2012-11-06 </TD> <TD align="right"> 28.94 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 8334 </TD> </TR>
  <TR> <TD> 2012-11-07 </TD> <TD align="right"> 44.73 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 12883 </TD> </TR>
  <TR> <TD> 2012-11-08 </TD> <TD align="right"> 11.18 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 3219 </TD> </TR>
  <TR> <TD> 2012-11-09 </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD align="right">   0 </TD> </TR>
  <TR> <TD> 2012-11-10 </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD align="right">   0 </TD> </TR>
  <TR> <TD> 2012-11-11 </TD> <TD align="right"> 43.78 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 12608 </TD> </TR>
  <TR> <TD> 2012-11-12 </TD> <TD align="right"> 37.38 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10765 </TD> </TR>
  <TR> <TD> 2012-11-13 </TD> <TD align="right"> 25.47 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 7336 </TD> </TR>
  <TR> <TD> 2012-11-14 </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD align="right">   0 </TD> </TR>
  <TR> <TD> 2012-11-15 </TD> <TD align="right"> 0.14 </TD> <TD align="right"> 0.00 </TD> <TD align="right">  41 </TD> </TR>
  <TR> <TD> 2012-11-16 </TD> <TD align="right"> 18.89 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 5441 </TD> </TR>
  <TR> <TD> 2012-11-17 </TD> <TD align="right"> 49.79 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 14339 </TD> </TR>
  <TR> <TD> 2012-11-18 </TD> <TD align="right"> 52.47 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 15110 </TD> </TR>
  <TR> <TD> 2012-11-19 </TD> <TD align="right"> 30.70 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 8841 </TD> </TR>
  <TR> <TD> 2012-11-20 </TD> <TD align="right"> 15.53 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 4472 </TD> </TR>
  <TR> <TD> 2012-11-21 </TD> <TD align="right"> 44.40 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 12787 </TD> </TR>
  <TR> <TD> 2012-11-22 </TD> <TD align="right"> 70.93 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 20427 </TD> </TR>
  <TR> <TD> 2012-11-23 </TD> <TD align="right"> 73.59 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 21194 </TD> </TR>
  <TR> <TD> 2012-11-24 </TD> <TD align="right"> 50.27 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 14478 </TD> </TR>
  <TR> <TD> 2012-11-25 </TD> <TD align="right"> 41.09 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 11834 </TD> </TR>
  <TR> <TD> 2012-11-26 </TD> <TD align="right"> 38.76 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 11162 </TD> </TR>
  <TR> <TD> 2012-11-27 </TD> <TD align="right"> 47.38 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 13646 </TD> </TR>
  <TR> <TD> 2012-11-28 </TD> <TD align="right"> 35.36 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 10183 </TD> </TR>
  <TR> <TD> 2012-11-29 </TD> <TD align="right"> 24.47 </TD> <TD align="right"> 0.00 </TD> <TD align="right"> 7047 </TD> </TR>
  <TR> <TD> 2012-11-30 </TD> <TD align="right">  </TD> <TD align="right">  </TD> <TD align="right">   0 </TD> </TR>
   </TABLE>




## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?


```r
# plot(cars)
```

