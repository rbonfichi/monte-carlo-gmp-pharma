# Chapter 2 – Random Numbers vs. Random Variates

Monte Carlo simulations require *randomness*, but not all randomness is the same.  
In this chapter, we clarify a crucial distinction:

---

## 🎲 Random Numbers
- **Definition:** Numbers generated without a predictable pattern, usually between 0 and 1.
- **Source:** Often produced by a *pseudo-random number generator* (PRNG) in software.
- **Example in R:**
  ```r
  runif(5)  # Generates 5 random numbers between 0 and 1
  ```

**Key Point:** These are “raw” random values — they are not yet tied to any specific probability distribution.

## 📈 Random Variates

- **Definition:** Values drawn from a specific probability distribution using random numbers as input.

- **Example:** Transforming random numbers into normally distributed values.

- **Example in R:**
  ```r
  rnorm(5, mean = 100, sd = 15)  # 5 normal variates with mean 100, sd 15
  ```

- **Key Point:** Random variates are random numbers mapped to a model of the real world.

## 🔄 From Numbers to Variates

1. Generate uniform random numbers.

2. Apply a transformation (inverse CDF or algorithm) to match the target distribution.

3. Obtain random variates that reflect the desired model.

**Example in R – Transforming Uniform → Normal**
```r
u <- runif(1000)
x <- qnorm(u, mean = 50, sd = 5)  # Convert uniform to normal
hist(x, main = "Normal Variates from Uniform Random Numbers")
```

## 💊 Why It Matters in Pharma

In pharmaceutical applications:

- **Random Numbers** simulate uncertainty without a specific context.

- **Random Variates** simulate actual process or measurement data (e.g., tablet weight, assay results).

- Using the wrong one may lead to unrealistic results.

---

[← Previous: Introduction](chapter01_intro.md) | [▲ back to top](../#table-of-contents) | [Next → Simple Distributions](chapter03_distributions.md)
