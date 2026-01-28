---
title: Exact Permutation Tests
draft: false
tags:
  - component
cssclasses:
aliases:
---
course: "Math 185 – Computational Statistics"  
tags: [statistics, hypothesis-testing, exact-tests, permutation-tests]

## Clinical Trials

Clinical trials are research studies performed on people that aim to evaluate medical, surgical, or behavioral interventions. Typical research questions include:

- Is a new treatment safe and effective?
    
- Is a new treatment more effective and/or less harmful than the standard treatment?
    

### Example: Response Rate of a New Pain Drug

Suppose a new pain drug is tested to determine whether the response rate is **at least 85%**.

We test:

$$  
H_0: p = 0.85 \quad \text{vs.} \quad H_1: p \neq 0.85  
$$

#### One-sided vs Two-sided Tests

There is long-standing debate in clinical research regarding whether hypothesis tests should be one-sided or two-sided.

- **One-sided tests** are sometimes argued for when only improvement is of interest.
    
- **Two-sided tests** account for the possibility that a treatment may perform worse than expected.
    

Because adverse or unexpected effects are rarely impossible, the modern consensus in medical research favors **two-sided hypothesis tests**.

---

## Exact Binomial Test

Suppose:

- $n = 19$ patients are enrolled
    
- $X$ = number of positive responses
    
- Observed $X = 18$
    

Under the null hypothesis:

$$  
X \sim \text{Binomial}(n=19, p=0.85)  
$$

Exact binomial tests are used instead of normal approximations when sample sizes are small or when guarantees on coverage are needed.

---

## Exact Confidence Intervals (Clopper–Pearson)

Clopper and Pearson (1934) defined an **exact** $(1-\alpha)$ confidence interval for $p$ by inverting two one-sided binomial tests.

The interval $(p_\ell, p_u)$ satisfies:

$$  
\sum_{k=0}^{x} \binom{n}{k} p_u^k (1 - p_u)^{n-k} = \frac{\alpha}{2}  
$$

$$  
\sum_{k=x}^{n} \binom{n}{k} p_\ell^k (1 - p_\ell)^{n-k} = \frac{\alpha}{2}  
$$

with:

- $p_\ell = 0$ if $x = 0$
    
- $p_u = 1$ if $x = n$
    

This method guarantees **at least** $1-\alpha$ coverage.

---

## Two-Sample Binomial Problem

We compare two treatments:

|Outcome|Control (0)|Treatment (1)|Total|
|---|---|---|---|
|Success|$Y_0$|$Y_1$|$Y$|
|Failure|$n_0-Y_0$|$n_1-Y_1$|$n-Y$|
|Total|$n_0$|$n_1$|$n$|

Where:

$$  
Y_0 \sim \text{Binomial}(n_0, p_0), \quad Y_1 \sim \text{Binomial}(n_1, p_1)  
$$

We test:

$$  
H_0: p_0 = p_1  
$$

---

## Fisher’s Exact Test

### Fisher’s Tea Drinker Example

A British woman claimed she could tell whether milk or tea was poured first.

|Guess \ True|Milk|Tea|Total|
|---|---|---|---|
|Milk|3|1|4|
|Tea|1|3|4|
|Total|4|4|8|

Under the null hypothesis of independence, the table follows a **hypergeometric distribution** conditional on the margins.

$$  
P(Y_0 = k) = \frac{\binom{n_0}{k} \binom{n_1}{Y-k}}{\binom{n}{Y}}  
$$

The p-value is computed by summing probabilities of tables that are **at least as extreme** as the observed one.

For this example:

$$  
p\text{-value} = \frac{\binom{4}{3}\binom{4}{1} + \binom{4}{4}\binom{4}{0}}{\binom{8}{4}} \approx 0.243  
$$

---

## Effect Size Measures

Let group 0 be the control and group 1 be treated.

- **Risk Difference**:  
    $$  
    \Delta = p_1 - p_0  
    $$
    
- **Risk Ratio (RR)**:  
    $$  
    RR = \frac{p_1}{p_0}  
    $$
    
- **Odds Ratio (OR)**:  
    $$  
    OR = \frac{p_1(1-p_0)}{p_0(1-p_1)}  
    $$
    

Properties:

- $p_1 = p_0 \iff RR = 1 \iff OR = 1$
    
- When outcomes are rare, $OR \approx RR$
    

---

## Fisher’s Exact Test for $r \times c$ Tables

For an $r \times c$ contingency table with fixed margins:

$$  
P(K_{11}=k_{11},\dots,K_{rc}=k_{rc}) = \frac{\prod_i R_i! \prod_j C_j!}{n! \prod_{i,j} k_{ij}!}  
$$

A table is considered **as extreme** if its probability is less than or equal to the observed table’s probability.

The number of possible tables grows rapidly with $r$, $c$, and $n$.

---

## Permutation Tests (Two-Sample)

Let:

$$  
X_1,\dots,X_n \sim F_X, \quad Y_1,\dots,Y_m \sim F_Y  
$$

We test:

$$  
H_0: F_X = F_Y \quad \text{vs.} \quad H_1: F_X \succeq F_Y  
$$

A simple test statistic is:

$$  
T = \bar X - \bar Y  
$$

### Permutation Principle

Under $H_0$, the pooled sample

$$  
Z = {X_1,\dots,X_n, Y_1,\dots,Y_m}  
$$

is **exchangeable**. For any permutation $\pi$:

$$  
T_\pi = T(Z_{\pi(1)},\dots,Z_{\pi(n)}; Z_{\pi(n+1)},\dots,Z_{\pi(n+m)})  
$$

The permutation p-value is:

$$  
p = \frac{#{\pi : T_\pi \ge T_{obs}}}{(n+m)!}  
$$

---

## Approximate Permutation Test

Because $(n+m)!$ can be enormous, we approximate using $B$ random permutations:

1. Compute $T_{obs}$
    
2. For $b = 1,\dots,B$:
    
    - Sample a random permutation $\pi_b$
        
    - Compute $T_{\pi_b}$
        
3. Estimate:
    

$$  
\hat p = \frac{#{b : T_{\pi_b} \ge T_{obs}} + 1}{B + 1}  
$$

---

## Permutation t-Test

Assume:

$$  
H_0: \mu_X = \mu_Y \quad \text{vs.} \quad H_1: \mu_X \neq \mu_Y  
$$

with equal variances.

The test statistic:

$$  
T = \frac{\bar X - \bar Y}{s_p\sqrt{1/n + 1/m}}  
$$

where:

$$  
s_p^2 = \frac{(n-1)s_X^2 + (m-1)s_Y^2}{n+m-2}  
$$

If normality holds:

$$  
T \sim t_{n+m-2}  
$$

Otherwise, the permutation distribution provides a valid alternative.

---

## Permutation Tests for Independence

Let $(X_1,Y_1),\dots,(X_n,Y_n) \sim F_{X,Y}$.

We test:

$$  
H_0: F_{X,Y} = F_X F_Y  
$$

Under $H_0$, permuting the $Y$ values breaks any dependence while preserving marginal distributions.

For permutation $\pi$:

$$  
T_\pi = T((X_1,Y_{\pi(1)}),\dots,(X_n,Y_{\pi(n)}))  
$$

The p-value is:

$$  
p = \frac{#{\pi : T_\pi \ge T_{obs}}}{n!}  
$$

---

## Summary

- Exact tests avoid asymptotic approximations
    
- Fisher’s exact test conditions on margins
    
- Permutation tests rely on exchangeability
    
- Approximate permutation tests scale to large samples
    
- These methods are especially valuable in small-sample settings