# Block 5 — Complete Simulation in R

Step-by-step example for `C = W/V`.
```r
set.seed(123)
N <- 10000
W <- rnorm(N, 98.5, 0.5)
V <- rnorm(N, 10.0, 0.1)
C <- W / V
mean(C); sd(C); quantile(C, c(.025,.975))
```
Plot a histogram and overlay mean/quantiles.
