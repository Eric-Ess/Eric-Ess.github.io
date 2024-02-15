---
layout: post
title: Plotting growth
subtitle: Tuesday
tags: Thesis
comments: true
---
plotting some growth. here is the code
```{r}
#retrieve csv
size_data <- read.csv("~/project-gigas-carryover/lifestage_carryover/data/size/gigas-lengths.csv")
#filtering/grouping
i_treatment_data <- size_data[size_data$init.treat == "treatment", ]
i_control_data <- size_data[size_data$init.treat == "control", ]
#getting R to read dates as dates
i_treatment_data$dates <- as.Date(i_treatment_data$Date, format= "%m/%d/%Y")
i_control_data$dates <- as.Date(i_control_data$Date, format= "%m/%d/%Y")
size_data$dates <- as.Date(size_data$Date, format= "%m/%d/%Y")
#specifying the order of months
month_order <- c("Oct", "Nov", "Jan")
i_treatment_data$month <- factor(i_treatment_data$month, levels = month_order)
i_control_data$month <- factor(i_control_data$month, levels = month_order)
#plotting
library(ggplot2)
ggplot(i_treatment_data, aes(month)) +
    geom_boxplot(aes(y= length, colour= life.stage))+
    facet_grid(~life.stage)+
    ggtitle("Treatment Tank")+
    ylab("Mean Length (mm)")+
    xlab("Month")

ggplot(i_control_data, aes(month)) +
    geom_boxplot(aes(y= length, colour= life.stage)) +
    facet_grid(~life.stage)+
    ggtitle("Control Tank")+
    ylab("Mean Length (mm)")+
    xlab("Month")

#percent mortality
total_dead <- length(size_data[size_data$notes == "dead 1-31-24" & size_data$month == "Jan", ]$tag)
total_juvenile_t <- length(i_treatment_data[i_treatment_data$life.stage == "juvenile", ]$tag)
mortality/total_j_t
#juveniles are the only ones that  died as far as i know.
```
mortality/total_j_t comes out to 0.1416667 <br><br>

![](https://github.com/Eric-Ess/Eric-Ess.github.io/blob/master/post_images/021324/control-growth.png?raw=true)

![](https://github.com/Eric-Ess/Eric-Ess.github.io/blob/master/post_images/021324/treatment-growth.png?raw=true)
