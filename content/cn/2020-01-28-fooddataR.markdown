---
title: R与显著性分析
author: ''
date: '2020-01-28'
slug: fooddataR
categories:
  - R
tags:
  - data science
---
1. R的帮助
   为什么需要用到R语言？最直接的原因是数据可视化的需要。目前我本人常用的主成分分析，判别分析，显著性差异分析，相关性分析等作图都是使用R语言。
   数据发掘甚至机器学习也可以用到R语言，但我目前的水平还达不到。
2. 怎样使用R做显著性分析？
   显著性分析最直接的用处是标注显著性差异，
比如在表格的数据中 ：![](/cn/2020-01-21-Rnote_files/significant.PNG)；
又比如在图片中：![](/cn/2020-01-21-Rnote_files/sig_picture.jpg)。
   所以最好的代码就是既可以算出平均值/标准差，又可以分组标注出显著性差异，一段代码如下：

#load library
library(multcomp)

##set workspace
basefolder <- 'C:/data_analysis/'
setwd(paste0(basefolder,file.path('carotene')))


##load dataset
peel <- read.csv("carotene_peel.csv")
View(peel)
##ANOVA 
Carotene <- peel$Carotene
Farm <- peel$Farm

aggregate(Carotene, by =list(Farm), FUN=mean)
aggregate(Carotene, by =list(Farm), FUN=sd)

fit <- aov(Carotene ~ Farm)
summary(fit)
TukeyHSD(fit)
par(mar=c(5,4,6,2))
tuk <- glht(fit,linfct= mcp(Farm="Tukey"))
plot(cld(tuk,level=.05),col="lightgrey")


library(dplyr)
table <- group_by(peel, peel$Farm) %>%
  summarise(
    count = n(),
    mean = mean(Carotene, na.rm = TRUE),
    sd = sd(Carotene, na.rm = TRUE)
  )
   
   
