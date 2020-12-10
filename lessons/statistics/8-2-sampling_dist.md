[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77) (scoring)

## Problem

Exercise: In games like hockey and soccer, the time between goals is roughly exponential. So you could estimate a team’s goal-scoring rate by observing the number of goals they score in a game. This estimation process is a little different from sampling the time between goals, so let’s see how it works.

Write a function that takes a goal-scoring rate, lam, in goals per game, and simulates a game by generating the time between goals until the total time exceeds 1 game, then returns the number of goals scored.

Write another function that simulates many games, stores the estimates of lam, then computes their mean error and RMSE.

Is this way of making an estimate biased?

## Solution

```
def SimulateGames(m=10, lam=2):
    estimates = []
    for _ in range(m):
        sample_lam = SimulateGame(lam)
        estimates.append(sample_lam)
        
    mean_error = estimation.MeanError(estimates, lam)
    rmse = estimation.RMSE(estimates, lam) 
    
    print(f"""Mean Error: {mean_error:.2f}
RMSE: {rmse:.2f}""")
    
SimulateGames()

num_games = [10, 50, 100, 1000, 10000, 100000]
for m in num_games:
    print(m)
    SimulateGames(n=m)
    print("\n")
```

**Results**:

This is an unbiased method because the mean error is small and decreases as m increases.

Sample size:  10

Mean Error: 0.30

RMSE: 1.52
_________________
Sample size:  50

Mean Error: 0.02

RMSE: 1.35
_________________
Sample size:  100

Mean Error: 0.18

RMSE: 1.48
_________________
Sample size:  1000

Mean Error: 0.04

RMSE: 1.41
_________________
Sample size:  10000

Mean Error: 0.00

RMSE: 1.42
_________________
Sample size:  100000

Mean Error: 0.01

RMSE: 1.42
