---
title: "Peer Assessment 1"
author: "Hector A.  Tinoco"
date: "Sunday, April 18, 2015"
output: html_document
---

```{r}
# Reading Data
setwd("C:/Users/Tinoco/Google Drive/2. Research (Current)/(2015) Courses/(2015) Especialization in Data Science_/5. Reproducible Research/Week 2/repdata-data-activity")  
Data <- read.csv("activity.csv", colClasses = "character")

# Extracting Data

Data1<-Data
Data2<-Data

## Fillling NA data with zeros 
Data2[is.na(Data[,1]),1]<-0
Data2[,1]<-as.numeric(Data2[,1])

#Questions 1

## Calculate the total number of steps taken per day?
Q1=tapply(as.numeric(Data2$steps),Data2$date,sum)

hist(Q1,freq=TRUE,breaks=dim(Q1), col="red", xlab="Total steps by Day",
     ylab="Frequency of Steps", main="Mean of Steps")

# Mean of steps by day

Q2=tapply(as.numeric(Data2$steps),Data2$date,mean)
Data2[,3]=as.numeric(Data2[,3])
X2=(1:dim(Q2))*5

# Median  of steps by day
Q3=tapply(Data2$steps,Data2$date,median)

Q2
Q3


```

```{r simulation}

## What is the average daily activity pattern?
# Series Plot

plot(X2,Q2,type = "l",xlab="Time intervals",ylab="Mean of steps daily")

## Maximun Value in X , interval
XmaxV<-X2[Q2==max(Q2)]

```

```{r simulation1}

## Series Plot

plot(X2,Q2,xlab="Time intervals",ylab="Mean of steps daily")

## Maximun Value in X
XmaxV<-X2[Q2==max(Q2)]

```

The time interval that contains the maximum step is `r XmaxV`.


```{r simulation2}

##Number of Missing values

N<-rep(1,length(Data[,1]))
Nt<-sum(N[is.na(Data[,1])])

```
Total number of missing values are `r Nt`

```{r simulation3}

A=names(Q1)

## Introducing Mean values for each Missing value
## Discriminig by Day

for(i in 1:length(Q2)){
Data1[((Data1[,2]==A[i])&(is.na(Data[,1]))),1]=as.numeric(Q2[i])
}

#Mean Data3

Q4=tapply(as.numeric(Data1$steps),Data1$date,mean)
X2=(1:length(Q4))*5

# Median Data 3
Q5=tapply(as.numeric(Data1$steps),Data1$date,median)

## Total Steps
Q6=tapply(as.numeric(Data1$steps),Data1$date,sum)

hist(Q6,freq=TRUE,breaks=(dim(Q6)-5), col="red", xlab="Total steps by Day", ylab="Frequency of Steps", main="Mean of Steps")

```

```{r simulation4}

## Data set with NA values filled with the mean 
Data1[,2]=weekdays(as.Date(Data1[,2]))
Data1[(Data1[,2]=="lunes")|(Data1[,2]=="martes")|(Data1[,2]=="miércoles")|(Data1[,2]=="jueves")|(Data1[,2]=="viernes"),2]="weekday"
Data1[(Data1[,2]=="sábado")|(Data1[,2]=="domingo"),2]="weekend"

      
## Data set with NA values filled with the mean 
Data2[,2]=weekdays(as.Date(Data2[,2]))
Data2[(Data2[,2]=="lunes")|(Data2[,2]=="martes")|(Data2[,2]=="miércoles")|(Data2[,2]=="jueves")|(Data2[,2]=="viernes"),2]="weekday"
Data2[(Data2[,2]=="sábado")|(Data2[,2]=="domingo"),2]="weekend"      

Q7=tapply(as.numeric(Data1$steps),Data1$date,sum)
Q8=tapply(as.numeric(Data2$steps),Data2$date,sum)

D1=as.numeric(Data1[Data1[,2]=="weekday",1])
X1=(1:length(D1))*5
D2=as.numeric(Data1[Data1[,2]=="weekend",1])
X2=(1:length(D2))*5

par(mfrow=c(2,1))
plot(X1,D1, type = "l", main="Plot Weekday: Time vs step",xlab="Time intervals",ylab="steps in a weekday")
plot(X2,D2, type = "l", main="Plot Weekend: Time vs disp",xlab="Time intervals",ylab="steps in a weekend")


```
