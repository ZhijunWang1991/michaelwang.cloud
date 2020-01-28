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
比如在表格的数据中 ：
![](/cn/2020-01-28-fooddataR_files/significant.PNG)；
又比如在图片中：
![](/cn/2020-01-28-fooddataR_files/sig_picture.jpg)。

   所以最好的代码就是既可以算出平均值/标准差，又可以分组标注出显著性差异，一段代码如下：


```r
##For significant ANOVA

#library
library(multcomp)
```

```
## Loading required package: mvtnorm
```

```
## Loading required package: survival
```

```
## Loading required package: TH.data
```

```
## Loading required package: MASS
```

```
## 
## Attaching package: 'TH.data'
```

```
## The following object is masked from 'package:MASS':
## 
##     geyser
```

```r
##set workspace
basefolder <- 'C:/Users/wang298/OneDrive - WageningenUR/Banana/paper2/data_analysis/'
setwd(paste0(basefolder,file.path('carotene')))


##load dataset
peel <- read.csv("carotene_peel.csv")
View(peel)
##ANOVA 
Carotene <- peel$Carotene
Farm <- peel$Farm

aggregate(Carotene, by =list(Farm), FUN=mean)
```

```
##    Group.1         x
## 1      CO1 1.7722643
## 2      CR1 1.5552997
## 3      CR2 1.6959400
## 4      CR3 1.5939059
## 5      DR1 0.5916084
## 6      DR2 1.2911703
## 7      EC1 0.6326465
## 8      EC2 0.9055603
## 9      PA1 1.4218027
## 10     PE1 1.2938576
```

```r
aggregate(Carotene, by =list(Farm), FUN=sd)
```

```
##    Group.1          x
## 1      CO1 0.14870994
## 2      CR1 0.57342218
## 3      CR2 0.13151390
## 4      CR3 0.15907280
## 5      DR1 0.13377849
## 6      DR2 0.21904799
## 7      EC1 0.12347390
## 8      EC2 0.15066340
## 9      PA1 0.34283921
## 10     PE1 0.09672653
```

```r
fit <- aov(Carotene ~ Farm)
summary(fit)
```

```
##             Df Sum Sq Mean Sq F value Pr(>F)    
## Farm         9 16.430  1.8256   29.25 <2e-16 ***
## Residuals   90  5.618  0.0624                   
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

```r
TukeyHSD(fit)
```

```
##   Tukey multiple comparisons of means
##     95% family-wise confidence level
## 
## Fit: aov(formula = Carotene ~ Farm)
## 
## $Farm
##                 diff         lwr         upr     p adj
## CR1-CO1 -0.216964592 -0.57948382  0.14555464 0.6410044
## CR2-CO1 -0.076324317 -0.43884355  0.28619491 0.9995528
## CR3-CO1 -0.178358362 -0.54087759  0.18416087 0.8465227
## DR1-CO1 -1.180655863 -1.54317509 -0.81813663 0.0000000
## DR2-CO1 -0.481093997 -0.84361323 -0.11857477 0.0016620
## EC1-CO1 -1.139617753 -1.50213698 -0.77709852 0.0000000
## EC2-CO1 -0.866703928 -1.22922316 -0.50418470 0.0000000
## PA1-CO1 -0.350461572 -0.71298080  0.01205766 0.0668434
## PE1-CO1 -0.478406685 -0.84092592 -0.11588745 0.0018121
## CR2-CR1  0.140640275 -0.22187896  0.50315951 0.9600442
## CR3-CR1  0.038606230 -0.32391300  0.40112546 0.9999986
## DR1-CR1 -0.963691272 -1.32621050 -0.60117204 0.0000000
## DR2-CR1 -0.264129406 -0.62664864  0.09838983 0.3598243
## EC1-CR1 -0.922653161 -1.28517239 -0.56013393 0.0000000
## EC2-CR1 -0.649739337 -1.01225857 -0.28722011 0.0000040
## PA1-CR1 -0.133496980 -0.49601621  0.22902225 0.9713791
## PE1-CR1 -0.261442094 -0.62396132  0.10107714 0.3744682
## CR3-CR2 -0.102034045 -0.46455328  0.26048519 0.9956703
## DR1-CR2 -1.104331546 -1.46685078 -0.74181232 0.0000000
## DR2-CR2 -0.404769680 -0.76728891 -0.04225045 0.0165341
## EC1-CR2 -1.063293436 -1.42581267 -0.70077420 0.0000000
## EC2-CR2 -0.790379611 -1.15289884 -0.42786038 0.0000000
## PA1-CR2 -0.274137255 -0.63665649  0.08838198 0.3079358
## PE1-CR2 -0.402082368 -0.76460160 -0.03956314 0.0178085
## DR1-CR3 -1.002297502 -1.36481673 -0.63977827 0.0000000
## DR2-CR3 -0.302735636 -0.66525487  0.05978360 0.1858546
## EC1-CR3 -0.961259391 -1.32377862 -0.59874016 0.0000000
## EC2-CR3 -0.688345566 -1.05086480 -0.32582634 0.0000009
## PA1-CR3 -0.172103210 -0.53462244  0.19041602 0.8720448
## PE1-CR3 -0.300048323 -0.66256755  0.06247091 0.1955965
## DR2-DR1  0.699561866  0.33704263  1.06208110 0.0000006
## EC1-DR1  0.041038111 -0.32148112  0.40355734 0.9999977
## EC2-DR1  0.313951935 -0.04856730  0.67647117 0.1489971
## PA1-DR1  0.830194292  0.46767506  1.19271352 0.0000000
## PE1-DR1  0.702249178  0.33972995  1.06476841 0.0000005
## EC1-DR2 -0.658523755 -1.02104299 -0.29600452 0.0000028
## EC2-DR2 -0.385609931 -0.74812916 -0.02309070 0.0277624
## PA1-DR2  0.130632426 -0.23188681  0.49315166 0.9751769
## PE1-DR2  0.002687312 -0.35983192  0.36520654 1.0000000
## EC2-EC1  0.272913824 -0.08960541  0.63543306 0.3140426
## PA1-EC1  0.789156181  0.42663695  1.15167541 0.0000000
## PE1-EC1  0.661211067  0.29869184  1.02373030 0.0000026
## PA1-EC2  0.516242357  0.15372313  0.87876159 0.0005189
## PE1-EC2  0.388297243  0.02577801  0.75081647 0.0258570
## PE1-PA1 -0.127945114 -0.49046434  0.23457412 0.9783825
```

```r
par(mar=c(5,4,6,2))
tuk <- glht(fit,linfct= mcp(Farm="Tukey"))
plot(cld(tuk,level=.05),col="lightgrey")
```

```
## Warning in RET$pfunction("adjusted", ...): Completion with error > abseps

## Warning in RET$pfunction("adjusted", ...): Completion with error > abseps

## Warning in RET$pfunction("adjusted", ...): Completion with error > abseps

## Warning in RET$pfunction("adjusted", ...): Completion with error > abseps

## Warning in RET$pfunction("adjusted", ...): Completion with error > abseps

## Warning in RET$pfunction("adjusted", ...): Completion with error > abseps
```

<img src="/cn/2020-01-28-fooddataR_files/figure-html/CaroteneANOVA-1.png" width="672" />

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following object is masked from 'package:MASS':
## 
##     select
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
table <- group_by(peel, peel$Farm) %>%
  summarise(
    count = n(),
    mean = mean(Carotene, na.rm = TRUE),
    sd = sd(Carotene, na.rm = TRUE)
  )
```

