[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

**Exercise:** In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.

In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use `scipy.stats.norm.cdf`.

```
five10_cm = 177.8
six1_cm = 185.4

five10_pRank = dist.cdf(five10_cm)
six1_pRank = dist.cdf(six1_cm)

solution = six1_pRank - five10_pRank
print(f"Solution: {solution * 100:.2f}%")
```

**```Solution: 34.21%```**
