[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

The distribution of income is famously skewed to the right. In this exercise, we’ll measure how strong that skew is.
The Current Population Survey (CPS) is a joint effort of the Bureau of Labor Statistics and the Census Bureau to study income and related variables. Data collected in 2013 is available from http://www.census.gov/hhes/www/cpstables/032013/hhinc/toc.htm. I downloaded `hinc06.xls`, which is an Excel spreadsheet with information about household income, and converted it to `hinc06.csv`, a CSV file you will find in the repository for this book. You will also find `hinc2.py`, which reads this file and transforms the data.

The dataset is in the form of a series of income ranges and the number of respondents who fell in each range.
* The lowest range includes respondents who reported annual household income 'Under \$5000'.
* The highest range includes respondents who made '\$250,000 or more.'

To estimate mean and other statistics from these data, we have to make some assumptions about the lower and upper bounds, and how the values are distributed in each range. `hinc2.py` provides `InterpolateSample`, which shows one way to model this data. It takes a `DataFrame` with a column, `income`, that contains the upper bound of each range, and `freq`, which contains the number of respondents in each frame.

It also takes `log_upper`, which is an assumed upper bound on the highest range, expressed in `log10` dollars. The default value, `log_upper=6.0` represents the assumption that the largest income among the respondents is $10^6$, or one million dollars.

`InterpolateSample` generates a pseudo-sample; that is, a sample of household incomes that yields the same number of respondents in each range as the actual data. It assumes that incomes in each range are equally spaced on a `log10` scale.


## Solution

### Upper-Bound = \$1,000,000 or \$10^6

```
mean = RawMoment(cdf.Values(), 1)
median = cdf.Value(0.5)

skew = Skewness(cdf.Values())
p_skew = PearsonMedianSkewness(cdf.Values())
below_mean = cdf.Prob(mean)

print(f"""Mean: {mean:.2f}
Median: {median:.2f}
Skewness: {skew:.2f}
Pearson's Skewness: {p_skew:.2f}
Percent Below Mean: {below_mean*100:.2f}""")
```

**Output**:

```
Mean: 74268.05
Median: 51226.45
Skewness: 4.95
Pearson's Skewness: 0.74
Percent Below Mean: 65.99
```

All of this is based on an assumption that the highest income is one million dollars, but that's certainly not correct.  What happens to the skew if the upper bound is 10 million?

Without better information about the top of this distribution, we can't say much about the skewness of the distribution.

### Upper-Bound = \$10,000,000 or \$10^7

```
# Solution goes here
log_upper = 7.0
log_sample = InterpolateSample(income_df, log_upper=log_upper)
sample = np.power(10, log_sample)
cdf = thinkstats2.Cdf(sample)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Household income ($)',
               ylabel='CDF')

mean = RawMoment(cdf.Values(), 1)
median = cdf.Value(0.5)

skew = Skewness(cdf.Values())
p_skew = PearsonMedianSkewness(cdf.Values())
below_mean = cdf.Prob(mean)

print(f"""Mean: {mean:.2f}
Median: {median:.2f}
Skewness: {skew:.2f}
Pearson's Skewness: {p_skew:.2f}
Percent Below Mean: {below_mean*100:.2f}""")
```

**Output**:

```
Mean: 124273.48
Median: 51226.45
Skewness: 11.60
Pearson's Skewness: 0.39
Percent Below Mean: 85.66
```

### Explained:

When the upper bound on the highest range is set to one million, or $10^6, the skewness is 4.95. The percent of the sample below the mean is 65.99%.

When we change that to $10^7, or 10 million, the skew jumps significantly to 11.60. What happens to the mean was even more suprising, jumping from about 74k to 124k. That brought the percent of the sample below the mean annual income to a suprisingly-high **85.66%**.

Keep in mind that we need to take this with a grain of salt. We don't have the real data about the top of this distribution.
