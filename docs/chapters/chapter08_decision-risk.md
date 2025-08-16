# Chapter 8 — Decision and Risk

Monte Carlo simulation is not only a computational tool — it is a **decision-making aid**.  
In GMP environments, it can quantify the probability of failing specifications, the impact of process changes, and the effectiveness of corrective actions.

---

## 🎯 1. From Simulation to Decisions

Simulation results should feed directly into **risk-based decision-making**:

- **Accept the process** if risk is within agreed thresholds.
- **Mitigate variability** if risk is above thresholds but controllable.
- **Reject or re-design** the process if unacceptable risk remains.

---

## 📉 2. Risk Metrics

Typical risk metrics from simulation output:

- **Probability of OOS** (`p_out`):  
  Proportion of simulated batches outside specifications.

- **Capability indices** (e.g., Cpk):  
  Quantify process centering and spread relative to specifications.

- **Tail probabilities**:  
  Probability of extreme events (e.g., worst 0.1% of the distribution).

**R Example:**
```r
# Assuming Assay from previous simulation
p_out <- mean(Assay < 98 | Assay > 102)
Cpk   <- min((102 - mean(Assay)) / (3 * sd(Assay)),
             (mean(Assay) - 98) / (3 * sd(Assay)))

quantile(Assay, probs = c(0.001, 0.999))  # extreme tails
```

---

## 🔄 3. What-if Scenarios

Monte Carlo enables **scenario analysis**:

- Adjust mean or variability (simulate process improvements)
- Change specification limits (regulatory or contractual)
- Add measurement uncertainty

**R Example:**
```r
# Simulate reduced variability
sd_new <- 1.0
API_weight_new <- rnorm(N, mean = 101, sd = sd_new)
Assay_new <- (API_weight_new / Tablet_weight) * Purity * 100
mean(Assay_new < 98 | Assay_new > 102)  # new p_out
```

---

## 🧮 4. Decision Thresholds

Before running simulations, define:
- **Acceptance threshold for p_out** (e.g., ≤ 0.1%)
- **Target Cpk** (e.g., ≥ 1.33)
- **Regulatory or internal tolerances**

These thresholds **transform raw statistics into actionable decisions.**

---

## 📌 5. GMP Interpretation

- **Low p_out + High Cpk** → continue as planned.
- **Moderate p_out or marginal Cpk** → investigate and mitigate sources of variation.
- **High p_out or Low Cpk** → reject process or redesign.

*💡 This structured approach aligns with ICH Q9 (Quality Risk Management) principles and supports regulatory inspections.*

---

This decision-oriented use of Monte Carlo simulation allows pharmaceutical companies to move from descriptive statistics to actionable risk control.

---
[← Previous: Pharmaceutical Case Study](chapter07_case-pharma.md) | [▲ back to top](../#table-of-contents) [Next → Conclusions-Next Steps](chapter09_conclusions-nrxtsteps.md)
