# Chapter 5 – A Complete Simulation in R

Now that we know about **random variates**, **distributions**, and the **transfer equation**,  
let’s put it all together into a **full Monte Carlo simulation**.

---

## 🎯 Scenario

We want to simulate the **assay** of a tablet to assess if the process meets specifications:  
**LSL = 98.0%**, **USL = 102.0%**.

Inputs:

1. `API_weight` → Normally distributed (mean = 101 mg, sd = 2 mg)  
2. `Tablet_weight` → Normally distributed (mean = 250 mg, sd = 5 mg)  
3. `Purity` → Uniform distribution (min = 0.98, max = 1.00)

Transfer Equation:

\[
Assay(\%) = \frac{API\_weight}{Tablet\_weight} \times Purity \times 100
\]

`Assay(%) = (API_weight / Tablet_weight) * Purity * 100`

---

## 💻 R Code

```r
set.seed(123)

# 1. Number of simulations
N <- 10000

# 2. Random inputs
API_weight    <- rnorm(N, mean = 101, sd = 2)
Tablet_weight <- rnorm(N, mean = 250, sd = 5)
Purity        <- runif(N, min = 0.98, max = 1.00)

# 3. Transfer equation
Assay <- (API_weight / Tablet_weight) * Purity * 100

# 4. Save histogram
png("full_simulation_assay.png", width = 800, height = 600)
hist(Assay,
     main = "Simulated Assay (%)",
     xlab = "Assay %",
     col = "lightblue",
     border = "white")
abline(v = c(98, 102), col = "red", lwd = 2, lty = 2)
dev.off()

# 5. Probability of being out of spec
p_out <- mean(Assay < 98 | Assay > 102)
p_out
```

---

## 📊 Expected Output
- **Histogram** with vertical red dashed lines at 98% and 102% to mark specifications.

- Printed `p_out` → probability of being out of specification.

<p align="center"> <img src="../images/full_simulation_assay.png" alt="Full Simulation Assay" width="500"> </p>

---

## 💊 Interpretation
If `p_out` is **very low** (e.g., < 0.1%), the process is highly capable.

If `p_out` is **significant**, we may need to:

- Reduce input variability,
- Adjust process targets,
- Improve measurement accuracy.

---

[← Previous: The Transfer Equation](chapter04_transfer-equation.md) | [▲ back to top](../#table-of-contents) | [Next → Analysis of Results](chapter06_analysis.md)
