
# A/B Testing - Lab

## Introduction

In this lab, you'll go through a sample process of designing an experiment.

## Objectives
You will be able to:

* Design, structure, and run an A/B test


## The Scenario

You've been tasked with designing an experiment to test whether a new email template will be more effective for your company's marketing team. The current template has a 5% response rate, which has outperformed numerous other templates in the past. As a result of some very poor performance from some of these alternative templates, the company is both excited to test this new design that was developed internally, and nervous about losing sales, if it is not to work out. As a result, they are looking to determine how many individuals they will need to serve the new email template to in order to detect a 1% performance increase (or drop).


## Step 1: State the Null Hypothesis, $H_0$

State your null hypothesis here (be sure to make it quantitative as before)

h_0 : the probability of success for the new email template is .05

## Step 2: State the Alternative Hypothesis, $H_1$

State your alternative hypothesis here (be sure to make it quantitative as before)

h_1 : the probability of success for the new email template is > .06 

(<.04 would also result in the same equations we saw previously)

## Step 3: Define Alpha and Beta

Now define what alpha and beta you believe might be appropriate for this scenario.
To start, we may arbitrarily set alpha and beta to .01, indicating that we wish to minimally open ourselves up to type I and type II errors. Later, we will be able to adapt these, if sample sizes turn out to be impractically large.


```python
alpha = .01
beta = .01
```

## Step 4: Calculate N

Calculating n requires us to know the variance. In this case, we will have a binomial variable (they either respond to the email or don't) and thus the variance, can be calculated with a standard formula: $n\bullet p\bullet(1-p)$ however, this also requires knowledge of p, the probability of response from the updated template. After conducting a limited sample however, we can extrapolate more and detemine if we have sufficient evidence or not.


...So, after an initial trial of 35 individuals, you have a total of 2 responses. 

Is this sufficient evidence to refute the null hypothesis stated above?


```python
#Your code for testing the null hypothesis here

import scipy.stats as st

def compute_n(alpha, beta, mu_0, mu_1, var):
    z_alpha = st.norm.ppf(alpha)
    z_beta = st.norm.ppf(beta)
    num = ((z_alpha+z_beta)**2)*var
    den = (mu_1 - mu_0)**2
    return num/den

alpha = .01 #Part of A/B test design
beta = .01 #Part of A/B test design
mu_0 = .05 #Part of A/B test design
mu_1 = .06 #Part of A/B test design
var = 35 *(2/35)*(1-2/35) #sample variance using binomial variance formula

compute_n(alpha, beta, mu_0, mu_1, var)
```




    408211.46565667057



### Your answer here: is there sufficient data to refute the null hypothesis? [Yes/No]
No: Current calculations show we would have to conduct a much much larger sample of over 400K to achieve the desired accuracy based on our initial sample.

## Experimenting With New Test Designs
If we relax alpha and beta to .05, each (opening ourselves up to a higher probability of making type I and type II errors), how much would our required sample size drop?


```python
#Your code here
alpha = .05 #Part of A/B test design
beta = .05 #Part of A/B test design
mu_0 = .05 #Part of A/B test design
mu_1 = .06 #Part of A/B test design
var = 35 *(2/35)*(1-2/35) #sample variance using binomial variance formula

compute_n(alpha, beta, mu_0, mu_1, var)
```




    204075.27768034008



### Your answer here: how much would required sample size drop based on the new formulation?
The sample size would still need to be quite large; over 200K, but has been cut roughly in have by relaxing alpha and beta both .05.

## Summary

In this lab, you practiced designing an intial experiment and then refined the parameters of the experiment based on an initial sample to determine feasability.
