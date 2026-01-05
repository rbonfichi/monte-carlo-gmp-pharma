# Chapter 16 — Decision and Risk

Monte Carlo simulation is not only a computational tool — it is a **decision-making aid**.  
In GMP environments, it can quantify the probability of failing specifications, the impact of process changes, and the effectiveness of corrective actions.

---

## 🎯 1. From Simulation to Decisions

Simulation results should feed directly into **risk-based decision-making**:

- **Accept the process** if risk is within agreed thresholds.
- **Mitigate variability** if risk is above thresholds but controllable.
- **Reject or re-design** the process if unacceptable risk remains.

We denote by **p_out** the probability of OOS (Out of Specification), i.e.  
the proportion of simulated batches falling outside the specification limits.  
This notation will be used consistently throughout this chapter.

> 📌 **Example (Case Study 1 — API Assay):**
>  Simulation showed p_out ≈ 15% and Cpk ≈ 0.43, clearly beyond acceptable GMP thresholds.
>  Decision: process redesign or immediate CAPA required.

---

## 📉 2. Risk Metrics

Typical risk metrics from simulation output:

- **Probability of OOS** (`p_out`): proportion of simulated batches outside specifications.
- **Capability indices** (e.g., Cpk): quantify process centering and spread relative to specifications.
- **Tail probabilities**: probability mass in the extreme quantiles (e.g., 0.1% tails of the distribution).
 
*Note: In GMP decision-making, capability indices such as Cpk should be interpreted with caution when the distribution is skewed or non-normal.  
Monte Carlo simulations allow the use of **percentile-based capability measures**, which are often more robust and transparent for regulatory discussions.*

### 📦 Percentile-based Capability Indices (Alternative to Cpk)

Traditional capability indices such as Cpk assume that data follow a **normal distribution**.  
However, in GMP contexts, distributions are often skewed or heavy-tailed (e.g., dissolution, microbiology).

An alternative is to use **percentile-based capability measures**, which rely directly on quantiles of the simulated distribution.  
Instead of asking *“does ±3σ fit inside the specs?”*, we check where the **extreme percentiles** fall relative to the specification limits.

**Mini-example (Case Study 1 — API Assay):**

```r
set.seed(123)
quantile(Assay, probs = c(0.00135, 0.5, 0.99865))
# Example output (simulated):
#   0.135%     50%   99.865% 
#    95.2     99.7    104.3
```
- The extreme quantiles (0.135% and 99.865%) fall **outside** 98–102%.
- Conclusion: the process is **not capable**, without assuming normality.

*Benefit*: This approach is **robust** and more transparent for regulatory discussions,
because it shows directly how the simulated data compare with specifications.

**R Example:**
```r
set.seed(123)
p_out <- mean(Assay < 98 | Assay > 102)
Cpk   <- min((102 - mean(Assay)) / (3 * sd(Assay)),
             (mean(Assay) - 98) / (3 * sd(Assay)))

quantile(Assay, probs = c(0.001, 0.999))
```
---

> 📌 **Example (Case Study 2 — Dissolution):**
> Simulation focuses on % dissolved at 30 minutes (see [Chapter 8](chapter08_case-study2.md)).
> Tail probability (e.g., worst 0.1% of units falling below 75% dissolution) can guide acceptance.

## 🔄 3. What-if Scenarios

Monte Carlo enables **scenario analysis**:

- Adjust mean or variability (simulate process improvements)
- Change specification limits (regulatory or contractual)
- Add measurement uncertainty

**R Example:**

*(Variables `API_LabelClaim` and `Purity` are defined as in Chapter 5 examples.)*

```r
set.seed(123)
# Simulate reduced variability
sd_new <- 1.0
API_weight_new <- rnorm(N, mean = 101, sd = sd_new)
Assay_new <- (API_weight_new / API_LabelClaim) * Purity * 100
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

> ⚠️ **Note**: These thresholds (e.g., p_out ≤ 0.1%, Cpk ≥ 1.33)  
> are common industry practices but **not regulatory requirements**.  
> Acceptance limits must be defined within the company’s Quality System,  
> considering product criticality and regulatory expectations.

These thresholds **transform raw statistics into actionable decisions.**

---

## 📌 5. GMP Interpretation

- **Low p_out + High Cpk** → continue as planned.
- **Moderate p_out or marginal Cpk** → investigate and mitigate sources of variation.
- **High p_out or Low Cpk** → reject process or redesign.

*💡 This structured approach aligns with **ICH Q9(R1) (Quality Risk Management, 2023 revision)**,  
which emphasizes the quantification of risk rather than relying solely on qualitative scoring.  
This quantitative view strengthens the evidence base for regulatory inspections.*

Additional regulatory documents also emphasize the role of quantitative methods:  
- **ICH Q14 (Analytical Procedure Development, 2023)**,  
- **USP <1220> (Analytical Procedure Lifecycle, 2022)**.  
These guidelines reinforce the importance of simulation and quantitative risk assessment in pharmaceutical decision-making.

---

## 6. Modular Integration of Case Studies

Each Case Study provides a worked example of applying this framework:

- **Case Study 1: API Assay** → high OOS probability → reject/redesign.
- **Case Study 2: Dissolution** (see [Chapter 8](chapter08_case-study2.md)) → interpret % release distributions and tail risks.
- **Case Study 3: From 3 Batches to Continuous Confidence** (see [Chapter 9](chapter09_case-study3.md)) → bridging PPQ to CPV via Monte Carlo & Bootstrap.
- **Case Study 4: Capability Indices in Pharma** (see [Chapter 10](chapter10_case-study4.md)) → using nonparametric bootstrap to derive defensible Ppk estimates with few, skewed data.
- **Case Study 5: Predictive Stability with Monte Carlo** (see [Chapter 11](chapter11_case-study5.md)) → forecasting stability outcomes of new batches, anchoring predictions to early data.

**Further Case Studies (planned, non-exhaustive):**
- **Sampling & Acceptance Plans** — attributes/variables (ISO 2859-1, ISO 3951-1), OC curves via simulation.
- **Microbiology (Low Counts)** — Poisson/Negative Binomial/ZIP, tolerance intervals, rare-event probabilities.
- **Measurement Uncertainty & Guard-Banding** — decision rules under metrological uncertainty (one-sided/two-sided specs).
- **Stability — tolerance intervals and advanced applications** — extending predictive stability (Case Study 5) to tolerance intervals.
- **Fill-Weight/Volume** — one-sided compliance and lot conformance risk.

This modular design allows an organization to gradually build a **library of risk-based simulations**, providing a consistent and scalable knowledge base that supports GMP decision-making across different applications.

---

*The next chapter consolidates these insights, summarizing the main conclusions and outlining practical next steps.*

[← Previous: Chapter 15 — Case Study 9 — Monte Carlo Measurement Uncertainty & Risk of Non-Compliance](chapter15_case-study9.md) | [▲ Chapter Index](../index.md#table-of-contents) | [Next → Chapter 17 — Conclusions and Next Steps](chapter17_conclusions-nextsteps.md)
