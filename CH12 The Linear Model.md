---
tags: FMS
---

# CH12 The Linear Model
## 12.1 Concepts
### 12.1.1 Least Square Estimator
- **Definition**: Suppose $X$ has rank $p$. One calls $$
\hat{\beta}:=\arg \min _{b \in \mathbb{R}^{p}}\|Y-X b\|_{2}^{2}$$ the least squares estimator.

:::warning
1. The least squares $\hat{\beta}$ is obtained by best linear approx (linear regression) of $Y$ on $X$.
2. Settings: 
$$X:=\left(\begin{array}{cccc}
1 & x_{1,2} & \cdots & x_{1, p} \\
1 & x_{2,2} & \cdots & x_{2, p} \\
\vdots & \vdots & \ddots & \vdots \\
1 & x_{n, 2} & \cdots & x_{n, p}
\end{array}\right)$$$$
Y=\left(\begin{array}{c}
Y_{1} \\
\vdots \\
Y_{n}
\end{array}\right)
$$

:::
- **Solution of LSE**: If $X$ has rank $p$, the matrix $X^{T} X$ has an inverse $\left(X^{T} X\right)^{-1}$ and we get$$\hat{\beta}=\left(X^{T} X\right)^{-1} X^{T} Y$$
:::warning
**Remark**
- **Normal equations**: $$X^{T}(Y-X \hat{\beta})=0$$
- **Projection Interpretation:** This process is equivalent to minimizing the distance between $Y$ and the space $\left\{X b: b \in \mathbb{R}^{p}\right\}$ spanned by the columns of $X$, which is achieved by projecting $Y$ on this space.
:::

## 12.2 Lemmas
### Definition
For $f=E Y$ we let $\beta^{*}:=\left(X^{T} X\right)^{-1} X^{T} f$ and we call $X \beta^{*}$ the best linear approximation of $f$.


### Lemma 12.3.1: Zero Average, Homogeneous Variance
Suppose $E \epsilon \epsilon^{T}=\sigma^{2} I$ where $\epsilon:=Y-f$. Then

(i) $E \hat{\beta}=\beta^{*}, \operatorname{Cov}(\hat{\beta})=\sigma^{2}\left(X^{T} X\right)^{-1}$,
(ii) $E\left\|X\left(\hat{\beta}-\beta^{*}\right)\right\|_{2}^{2}=\sigma^{2} p$,
(iii) $E\|X \hat{\beta}-f\|_{2}^{2}=\underbrace{\sigma^{2} p}_{\begin{array}{c}\text { estimation } \\ \text { error }\end{array}}+\underbrace{\left\|X \beta^{*}-f\right\|_{2}^{2}}_{\begin{array}{c}\text { misspecification } \\ \text { error }\end{array}}$.

:::warning
**Remark:** The misspecification error $\left\|X \beta^{*}-f\right\|_{2}^{2}$ comes from the possible misspecification of the linear model. That is, $f$ need not be a linear combination of the columns of $X$. One sometimes also calls $\left\|X \beta^{*}-f\right\|_{2}^{2}$ the approximation error. The estimation error is here the variance term $\sigma^{2} p$.
:::

### Lemma 12.3.2: Add Normal Distrib (Complete Gauss-Markov) Assumption
> Definition of Chi-Square Distribution: Let $Z_{1}, \ldots, Z_{p}$ be i.i.d. $\mathcal{N}(0,1)$-distributed. Define the $p$-vector
$$
Z:=\left(\begin{array}{c}
Z_{1} \\
\vdots \\
Z_{p}
\end{array}\right)
$$
Then $Z$ is $\mathcal{N}(0, I)$-distributed, with $I$ the $p \times p$ identity matrix. Then: $$
\|Z\|_{2}^{2} \sim \chi_{p}^{2}
$$


Suppose $\epsilon:=Y-f \sim \mathcal{N}\left(0, \sigma^{2} I\right)$. Then we have

(i) $\hat{\beta}-\beta^{*} \sim \mathcal{N}\left(0, \sigma^{2}\left(X^{T} X\right)^{-1}\right)$,
(ii) $\frac{\left\|X\left(\hat{\beta}-\beta^{*}\right)\right\|_{2}^{2}}{\sigma^{2}} \sim \chi_{p}^{2}$ where $\chi_{p}^{2}$ is $\chi^{2}$-distributed with $p$ degrees of freedom

:::warning
**Remark:** More generally, many estimators are approximately normally distributed (for example the sample median) and many test statistics have approximately a $\chi^{2}$ null-distribution (the **null distribution** is the [probability distribution](https://www.wikiwand.com/en/Probability_distribution "Probability distribution") of the [test statistic](https://www.wikiwand.com/en/Test_statistic "Test statistic") when the [null hypothesis](https://www.wikiwand.com/en/Null_hypothesis "Null hypothesis") is true) (for example the $\chi^{2}$ goodness-of-fit statistic). This phenomenon occurs because many models can in a certain sense be approximated by the linear model and many minus log-likelihoods resemble the least squares loss function (see Chapter 14). Understanding the linear model is a first step towards understanding a wide range of more complicated models.
:::




## 12.3 Key Takeaways & Common Tricks
1. Check [Linear Algebra & Matrix Caculus](/rEihCvcfSBO6r_ZtfIPW8g)
2. Use the linearity of multivariate normal distribution and the projection matrix form