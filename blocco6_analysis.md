# Block 6 — Analysis of Results

- Descriptives (mean, SD, quantiles)
- %OOS vs specs
- Capability (Cp, Cpk)
- Optional: bootstrap CI for the mean

```r
LSL <- 9.6; USL <- 10.4
mu <- mean(C); s <- sd(C)
p_OOS <- mean(C<LSL | C>USL)
Cp  <- (USL-LSL)/(6*s)
Cpk <- min(USL-mu, mu-LSL)/(3*s)
```
