# RepData_PeerAssessment1
---
title: "Peer Assessment 1"
author: "Hector A.  Tinoco"
date: "Sunday, March 15, 2015"
output: html_document
---

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r}
## Reading Data
setwd("C:/Users/Tinoco/Google Drive/2. Research (Current)/(2015) Especialization in Data Science_/5. Reproducible Research/Week 2/repdata-data-activity")  
Data <- read.csv("activity.csv", colClasses = "character")

## Extracting Data
Data2<-Data
Data2[is.na(Data[,1]),1]<-0
Data2[,1]<-as.numeric(Data2[,1])

#Questions

Q1=tapply(Data2$steps,Data2$date,sum)

hist(Q1,freq=TRUE,breaks=dim(Q1), col="red", xlab="Mean of steps by Day",
ylab="Frequency of Steps", main="Mean of Steps")

#Mean

Q2=tapply(Data2$steps,Data2$date,mean)
X2=(1:dim(Q2))*5

# Median
Q3=tapply(Data2$steps,Data2$date,median)

Q2
Q3

```


```{r simulation}

## Series Plot

plot(X2,Q2,xlab="Time intervals",ylab="Mean of steps daily")

## Maximun Value in X
XmaxV<-X2[Q2==max(Q2)]


```
The time interval that contains the maximum step is 'r XmaxV'

```{r}
##Number of Missing values
N<-rep(1,length(Data[,1]))
Nt<-sum(N[is.na(Data[,1])])

```
Total number of missing values 'r Nt'

```{r}


A=names(Q1)

for(i in 1:length(Q2)){
Data2[(Data[,2]==A[i])&(is.na(Data[,1])),1]<-as.numeric(Q2[i])
}

#Mean Data3

Q4=tapply(Data2$steps,Data2$date,mean)
X2=(1:dim(Q4))*5

# Median Data 3
Q5=tapply(Data2$steps,Data2$date,median)

## Total Steps
Q6=tapply(Data2$steps,Data2$date,sum)

hist(Q6,freq=TRUE,breaks=length(Q6), col="red",xlab=" New Histogram of Means of steps by Day",
ylab="Frequency of Steps", main="Mean of Steps")

```

