# Chapter 8 — Decision and Risk

Monte Carlo simulation is not only a computational tool — it is a **decision-making aid**.  
In GMP environments, it can quantify the probability of failing specifications, the impact of process changes, and the effectiveness of corrective actions.

---

## 🎯 1. From Simulation to Decisions

Simulation results should feed directly into **risk-based decision-making**:

- **Accept the process** if risk is within agreed thresholds.
- **Mitigate variability** if risk is above thresholds but controllable.
- **Reject or re-design** the process if unacceptable risk remains.

> 📌 **Example (Case Study 1 — API Assay):**
>  Simulation showed p_out ≈ 15% and Cpk ≈ 0.43, clearly beyond acceptable GMP thresholds.
>  Decision: process redesign or immediate CAPA required.

---

## 📉 2. Risk Metrics

Typical risk metrics from simulation output:

- **Probability of OOS** (`p_out`): proportion of simulated batches outside specifications.
- **Capability indices** (e.g., Cpk): quantify process centering and spread relative to specifications.
- **Tail probabilities**: probability mass in the extreme quantiles (e.g., 0.1% tails of the distribution).

**R Example:**
```r
p_out <- mean(Assay < 98 | Assay > 102)
Cpk   <- min((102 - mean(Assay)) / (3 * sd(Assay)),
             (mean(Assay) - 98) / (3 * sd(Assay)))

quantile(Assay, probs = c(0.001, 0.999))
```
---
> 📌 **Example (Case Study 2 — Dissolution, hypothetical):**
> Simulation may focus on % dissolved at 30 minutes.
> Tail probability (e.g., worst 0.1% of units falling below 75% dissolution) could guide acceptance.

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
mean(Assay_new < 98 | Assay_new > 102)
```
---
> 📌 **Example (Case Study 1 — API Assay):**
> Reducing API weight variability from sd = 1.2 → 0.8 lowered p_out from 15% to 5%.

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

## 6. Modular Integration of Case Studies

Each Case Study provides a worked example of applying this framework:

- **Case Study 1: API Assay** → high OOS probability → reject/redesign.
- **Case Study 2: Dissolution (future)** → interpret % release distributions.
- **Case Study 3: Microbiology (future)** → rare-event probabilities (Poisson).

These placeholders illustrate how new case studies can be integrated without rewriting this chapter.

---

This modular design ensures that Monte Carlo simulation supports **consistent, scalable decision-making** across different GMP applications.

[← Previous: Pharmaceutical Case Study](chapter07_case-study1.md) | [▲ back to top](../#table-of-contents) | [Next → Conclusions and Next Steps](chapter09_conclusions-nextsteps.md)
