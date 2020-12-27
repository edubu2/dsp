[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

## Problem

Using data from the NSFG, make a scatter plot of birth weight versus mother’s age. Plot percentiles of birth weight versus mother’s age. Compute Pearson’s and Spearman’s correlations. How would you characterize the relationship between these variables?

## Solution

My code for these solutions are [here](https://github.com/edubu2/ThinkStats2/blob/master/code/chap07ex.ipynb).

### Scatterplot

![scatterplot](https://github.com/edubu2/dsp/blob/master/lessons/statistics/images/7-1-scatter.png)

### Binned Percentiles

![binned percentiles](https://github.com/edubu2/dsp/blob/master/lessons/statistics/images/7-1-binnedPercentiles.png)

### Relationship Statistics

* **CoVariance**: 0.54
* **Pearsons's Correlation**: 0.07 
* **Spearman's Rank Correlation**: 0.09

### Interpretation

The correlation between age and baby weight is weak. We can say this after seeing no visible correlation in the scatterplot, no linear relation on the CDF figure, and finally, a Spearman's Rank Correlation of **0.09**. 
