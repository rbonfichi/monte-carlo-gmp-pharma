# Chapter 4 — The Transfer Equation (Model)

A transfer equation links uncertain inputs to an output: `Y = f(X1, X2, …)`. 

**Example — Concentration**
`C = W / V` with `W ~ N(98.5, 0.5^2)` and `V ~ N(10.0, 0.1^2)`.
```r
set.seed(123)
W <- rnorm(1e4, 98.5, 0.5)
V <- rnorm(1e4, 10.0, 0.1)
C <- W / V
summary(C)
```

---
[← Previous: Simple Distributions](chapter03_distributions.md) | [▲ back to top](../#table-of-contents) | [Next → A Complete Simulation in R](chapter05_full-simulation.md)
