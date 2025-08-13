# Block 2 — Random Numbers vs Random Variates

- **Random numbers**: Uniform(0,1) values from the generator.
- **Random variates**: values transformed to follow a target distribution.

**Examples**
```r
U <- runif(5)
X_uniform <- 40 + 20 * U                 # Uniform(40,60)
lambda <- 0.2
X_exp <- -log1p(-U) / lambda             # Exponential(lambda)
```
