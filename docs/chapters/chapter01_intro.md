# Chapter 1 – Introduction

Monte Carlo methods are **powerful simulation tools** widely used in engineering, finance, and the **pharmaceutical industry**.  
In this chapter, you will:

- **Understand** what Monte Carlo simulation is.
- Learn how it can be applied in **GMP** and **pharma operations**.
- See a **simple example** to build intuition.

---

## 1️⃣ What is Monte Carlo Simulation?

Monte Carlo simulation is a **computational method** that uses **random sampling** to estimate numerical results.  
It is especially useful when:

1. **Analytical solutions** are hard or impossible to obtain.
2. The system is **too complex** for exact formulas.
3. You want to **model uncertainty** and see the range of possible outcomes.

---

## 2️⃣ Why Monte Carlo in Pharma?

In the **pharmaceutical** and **GMP** context, Monte Carlo simulation can help:

- **Estimate** the probability of *out-of-specification* (OOS) results.
- **Predict** process capability with uncertainty.
- **Support** regulatory decisions with quantitative evidence.

---

## 📊 A Simple Example in R

Let’s say we want to model the variation in an **assay result** that is normally distributed with  
a **mean** of 98.0 and a **standard deviation** of 0.4.

```r
set.seed(123)
x <- rnorm(10000, mean = 98.0, sd = 0.4)
mean(x)
sd(x)
```
---
[▲ back to top](../#table-of-contents) | [Next → Random Numbers vs. Random Variates](chapter02_random-variates.md)
