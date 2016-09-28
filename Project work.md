---
Title: SI- Part 1
author: "ranata"
date: "Saturday, January 24, 2015"
output: pdf_document
---

Overview:

In this project we will investigate the exponential distribution in R and compare it with the Central Limit Theorem. We will set lambda -- the rate parameter as 0.2 for all of the simulations. We will do a thousand simulation for this purpose. 

The objective of this exercise is to illustrate via simulation and associated explanatory text the properties of the distribution of the mean of 40 exponentials. We will:
1. Show the sample mean and compare it to the theoretical mean of the distribution.
2. Show how variable the sample is (via variance) and compare it to the theoretical variance of the distribution.
3. Show that the distribution is approximately normal.


```r
# Lets create a dataframe of 1000 simulations of sample means and explore the properties of the distribution formed by these means (which will be our random variables)

rmeans = data.frame(X = sapply(1:1000, function(X) {mean(rexp(40, 0.2))}))

# Let's view some records
head(rmeans)
```

```
##          X
## 1 4.888287
## 2 6.163391
## 3 4.532909
## 4 3.296561
## 5 5.097907
## 6 4.730967
```


Question 1

```r
# Theoretical Mean of the distribution is 1/lambda = 5
# Mean of the the random variables of means (rmeans)

mean(rmeans$X)
```

```
## [1] 4.972535
```
We see that the means of the exponential of 1000 simulations center around the theoretical mean 1/lambda = 5


Question 2

```r
# Theoretical variance of the distribution (1/lambda^2)/40 = .625
# Variance of the the random variables of means (rmeans)
var(rmeans$X)
```

```
## [1] 0.6188022
```
Again, we see that the variance of the means of the exponential of 1000 simulations is very close to the the theoretical variance (1/lambda^2)/40 = .625

Question 3

```r
library(ggplot2)
ggplot(data = rmeans, aes(x = X)) + 
    geom_histogram(aes(y=..density..), fill = I('steelblue'), 
                   binwidth = 0.30, color = I('white')) + geom_density(aes(colour="Mean Distribution"), size=1.5) + 
    stat_function(fun = dnorm, aes(colour='Normal Distribution'), size=1.5, arg = list(mean = 5, sd = sd(rmeans$X))) + labs(title="Distribution of a large collection of random exponentials\n vs \n Distribution of a large collection of means") + labs(x="Mean of Samples", y="Frequency")
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png) 

The Graph suggests that the distribution of a large collection of random exponentials centers around distribution of a large collection of means both of which are approximately normal.
