---
title: "Pushups Study — Final Write-Up"
author: Giovanni Asencio
output: html_document
---

```{r}
library(tidyverse)
library(tigerstats)

push <- read.csv("pushups.csv")
head(push)
```

# 1. Introduction

The goal of this study is to determine whether line players and skill players differ in the average number of pushups they can complete.

**H₀:** μ_line = μ_skill  
**Hₐ:** μ_line ≠ μ_skill  

# 2. Data Description

The dataset contains two variables:  
- *position* (line or skill)  
- *pushups* (number performed)

There are 30 total observations.

# 2.1 Graphical Summary

```{r}
boxplot(push$pushups ~ push$position,
        col = c("lightblue","lightgreen"),
        xlab = "Player Type",
        ylab = "Number of Pushups",
        main = "Pushups by Player Type")
```

# 2.2 Numerical Summary

```{r}
push %>% group_by(position) %>%
  summarise(
    min = min(pushups),
    max = max(pushups),
    mean = mean(pushups),
    sd = sd(pushups)
  )
```

# 3. Statistical Test — Two-Sample t-test

```{r}
t.test(pushups ~ position, data = push)
```

# 4. Results and Conclusions

The t-test shows a **very small p-value**, indicating strong evidence that the two means differ. Skill players complete more pushups on average than line players.

We therefore **reject H₀** and conclude that skill players perform significantly more pushups than line players.
