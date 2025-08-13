# Block 8 — Decision and Risk

Use a risk threshold to drive decisions.
```r
threshold <- 0.005   # 0.5%
accept <- (p_OOS < threshold)
```
What-if analysis: shift μ, inflate σ, adjust specs, recompute p_OOS.
