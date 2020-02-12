---
title: R学习进展
author: Jon
date: '2020-02-12'
slug: rnotebook
categories:
  - R
tags:
  - data science
---
1. Some function to manage the R workSpace

##change the working direction
setwd()

##show the current working direction
getwd()

##save images
save.image("myfile")
png("filename.png")


2. creat a matrix

y <- matrix(1:20, nrow = 5, ncol = 4)

y


3. input excel or csv files

library(readxl)
dataset <- read_excel("direction")

dataset <- read.csv2("direction")




