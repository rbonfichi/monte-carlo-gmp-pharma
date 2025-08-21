# Chapter 2 – Random Numbers vs. Random Variates

Monte Carlo simulations require *randomness*, but not all randomness is the same.  
In this chapter, we clarify a crucial distinction:

---

## 🎲 Random Numbers
- **Definition:** Numbers generated without a predictable pattern, typically in the range [0, 1].  
- **Source:** In practice, they are produced by a *pseudo-random number generator* (PRNG), which is deterministic but sufficiently random for most statistical simulations.

- **Example in R:**
  ```r
  runif(5)  # Generates 5 random numbers between 0 and 1
  ```

**Key Point:** These are “raw” random values — they are not yet tied to any specific probability distribution.

## 📈 Random Variates

- **Definition:** Values drawn from a specific probability distribution, obtained by transforming random numbers.  
- **Key Point:** Random variates represent **real-world data models** (e.g., assay values, tablet weights).

- **Example:** Transforming random numbers into normally distributed values.

- **Example in R:**
  ```r
  rnorm(5, mean = 100, sd = 15)  # 5 normal variates with mean 100, sd 15
  ```

## 🔄 From Numbers to Variates

<p align="center">
  <img src="../images/random_numbers_to_variates.png" alt="Figure 2.1 – Random Numbers to Random Variates" width="70%">
  <br>
  <em>Figure 2.1 – Transformation process: from raw uniform random numbers to model-based random variates.</em>
</p>

1. Generate uniform random numbers.

2. Apply a transformation (inverse CDF or algorithm) to match the target distribution.

3. Obtain random variates that reflect the desired model.

**Example in R – Transforming Uniform → Normal**
```r
u <- runif(1000)
x <- qnorm(u, mean = 50, sd = 5)

hist(x,
     main = "Normal Variates from Uniform Random Numbers",
     xlab = "Value",
     col = "lightblue",
     border = "white")
```
➡️ What happens here?

1. We first generate 1,000 **uniform random numbers** between 0 and 1.  
2. We then apply the **inverse Normal CDF** (`qnorm`) to transform them into values that follow a Normal distribution (mean = 50, sd = 5).  
3. The histogram shows that the values now follow the familiar bell-shaped curve.  

> 🔎 **Note – What is the inverse Normal CDF?**  
> The inverse Normal CDF (also called the **quantile function**) tells us:  
> *“Given a probability p, which value x of the Normal distribution has that cumulative probability?”*  
> For example, the 0.975 quantile of a standard Normal distribution is 1.96 — meaning 97.5% of values lie below 1.96.

This demonstrates the core idea:  

- **Uniform random numbers** are the raw material.  
- **Random variates** are shaped into a distribution that models real-world phenomena (e.g., tablet weight around 50 mg).  

<p align="center">
  <img src="../images/random_uniform_to_normal.png" alt="Figure 2.2 – Transforming Uniform Random Numbers into Normal Variates" width="70%">
  <br>
  <em>Figure 2.2 – Transforming Uniform Random Numbers into Normal Variates (mean = 50, sd = 5)</em>
</p>

## 💊 Why It Matters in Pharma

In pharmaceutical applications:

- **Random Numbers** simulate uncertainty in a general sense, without context.  
- **Random Variates** simulate actual process or measurement data (e.g., tablet weight, assay results).  
- Using the wrong one may lead to unrealistic or misleading outcomes.  

👉 This distinction is fundamental: **all Monte Carlo simulations in GMP contexts are ultimately based on random variates, not raw random numbers.**  
This foundation is essential for moving forward. In the next chapter, we will explore the most common probability distributions used in pharmaceutical applications.

---

[← Previous: Introduction](chapter01_intro.md) | [▲ back to top](../#table-of-contents) | [Next → Simple Distributions](chapter03_distributions.md)
