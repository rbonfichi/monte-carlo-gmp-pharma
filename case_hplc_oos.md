# Example — HPLC Result and OOS Probability

Assume Normal variation: μ=100%, σ=1.2%, specs 97–103.
```r
set.seed(123)
X <- rnorm(2e5, 100, 1.2)
mean(X<97 | X>103)
```
![Histogram](../images/hplc_oos_example.png)
