# Chapter 1 — What is the Monte Carlo Method?

**Core idea.** Repeat a computation many times with random inputs to approximate a quantity of interest.

**π toy example**
```r
set.seed(123)
N <- 1e4
x <- runif(N, -1, 1)
y <- runif(N, -1, 1)
inside <- (x^2 + y^2) <= 1
4 * mean(inside)
```
**Key takeaways**
- Law of large numbers: estimates stabilize as N grows.
- Monte Carlo is a numerical method, not a theorem: it trades computation for algebra.

---
[▲ back to top](../#table-of-contents) | [Next → Random Numbers vs. Random Variates](chapter02_random-variates.md)
