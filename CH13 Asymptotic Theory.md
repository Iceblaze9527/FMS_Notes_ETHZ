---
tags: FMS
---

# CH13 Asymptotic Theory
## 13.1 Concepts
### 13.1.1 [Types of Convergence](https://www.wikiwand.com/zh-cn/%E9%9A%8F%E6%9C%BA%E5%8F%98%E9%87%8F%E7%9A%84%E6%94%B6%E6%95%9B?utm_source=pocket_mylist)
- **Convergence almost surely (in proba 1):** Let $\left\{Z_{n}\right\}_{n=1}^{\infty}$ and $Z$ be $\mathbb{R}^{p}$-valued random variables defined on the same probability space. We say that $Z_{n}$ converges in probability to $Z$ if$$ \mathbb{P}\left( \lim _{n \rightarrow \infty} Z_{n}=Z \right)=1$$ Notation: $Z_{n} \stackrel{a.s.}{\longrightarrow} Z$. 
- **Convergence in Probability:** Let $\left\{Z_{n}\right\}_{n=1}^{\infty}$ and $Z$ be $\mathbb{R}^{p}$-valued random variables defined on the same probability space. We say that $Z_{n}$ converges in probability to $Z$ if for all $\epsilon>0$,$$\lim _{n \rightarrow \infty} \mathbb{P}\left(\left\|Z_{n}-Z\right\|>\epsilon\right)=0$$ Notation: $Z_{n} \stackrel{\mathbb{P}}{\longrightarrow} Z$.
:::warning
**Remark:** Chebyshev’s inequality can be a tool to prove convergence in probability: For all increasing functions $\psi:[0, \infty) \rightarrow[0, \infty)$, $$
\mathbb{P}\left(\left\|Z_{n}-Z\right\| \geq \epsilon\right) \leq \frac{\mathbb{E} \psi\left(\left\|Z_{n}-Z\right\|\right)}{\psi(\epsilon)}$$
:::

- **Convergence in Distribution:** Let $\left\{Z_{n}\right\}_{n=1}^{\infty}$ and $Z$ be $\mathbb{R}^{p}$-valued random variables. We say that $Z_{n}$ converges in distribution to $Z$, if for all continuous and bounded functions $f$, $$
\lim _{n \rightarrow \infty} \mathbb{E} f\left(Z_{n}\right)=\mathbb{E} f(Z)$$Notation: $Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} Z$.
- **Convergence in Mean**: Given a real number $r \geq 1$, we say that the sequence $X_{n}$ converges in the $r$-th mean (or in the $L^{r}$-norm) towards the random variable $X$, if the $r$-th absolute moments $E\left(\left|X_{n}\right|^{r}\right)$ and $E(|X|^r)$ of $X_{n}$ and $X$ exist, and$$\lim _{n \rightarrow \infty} \mathrm{E}\left(\left|X_{n}-X\right|^{r}\right)=0$$

:::warning
**Remark:** Relationships of different convergence types: $$
\begin{array}{cccccc}
\stackrel{L^{s}}{\longrightarrow} & \stackrel{s>r\geqslant 1}{\Rightarrow} & \stackrel{L^{r}}{\longrightarrow} & & &\\
& & \Downarrow & & &\\
\stackrel{a.s.}{\longrightarrow} & \Rightarrow & \stackrel{\mathbb{P}}{\longrightarrow} & \Rightarrow & \stackrel{\mathcal{D}}{\longrightarrow} & \text{Bounded in Proba}
\end{array}$$
:::

### 13.1.2 Stochastic Order Symbols
- **Order Symbols**: Let $\left\{z_{n}\right\}$ be a collection of $\mathbb{R}^{p}$-valued vectors, and let $\left\{r_{n}\right\}$ positive constants:

| Notation | Expression | Example |
|---|---|---|
| $z_{n}=\mathcal{O}(1)$ | $\lim\limits_{n\rightarrow\infty}\sup \lVert z_n \rVert <\infty$ | $z_{n}=(-1)^{n}$ |
| $z_{n}=\mathcal{o}(1)$ | $\lim\limits_{n\rightarrow\infty} z_n = 0$ | $z_n=\frac{(-1)^{n}}{n}$ |
| $z_{n}=\mathcal{O}(r_n)$ | $z_{n}/r_n=\mathcal{O}(1)$ | $z_n=\frac{(-1)^{n}}{n} = \mathcal{O}(1/n)$  |
| $z_{n}=\mathcal{o}(r_n)$ | $z_{n}/r_n=\mathcal{o}(1)$ | $z_{n} = \frac{\sin (n)}{n^{2}} = \mathcal{o}(1/n) = \mathcal{O}(1/n^2)$|

- **Stochastic Order Symbols**: Let $\left\{Z_{n}\right\}$ be a collection of $\mathbb{R}^{p}$-valued random vectors, and let $\left\{r_{n}\right\}$ positive constants:

| Notation | Expression |
|----------|------------|
| $Z_{n}=\mathcal{O}_{\mathbf{P}}(1)$   | $\lim\limits_{M \rightarrow \infty} \limsup\limits_{n \rightarrow \infty} \mathbb{P}\left(\left\|Z_{n}\right\|>M\right)=0$ |
| $Z_{n}=\mathcal{o}_{\mathbf{P}}(1)$   | $Z_{n} \stackrel{\mathbb{P}}{\rightarrow} 0$                       |
| $Z_{n}=\mathcal{O}_{\mathbf{P}}(r_n)$ | $Z_{n}/r_n=\mathcal{O}_{\mathbf{P}}(1)$                                       |
| $Z_{n}=\mathcal{o}_{\mathbf{P}}(r_n)$ | $Z_{n}/r_n \stackrel{\mathbb{P}}{\rightarrow} 0$ |

:::warning
**Note**
1. $Z_{n}=\mathcal{O}_{\mathbf{P}}(1)$ is also called bounded in probability / uniform tightness of the sequence
2. $Z_{n}=\mathcal{o}_{\mathbf{P}}(r_n)$ is also called $Z_{n}$ is of small order $r_{n}$ in probability
:::

### 13.1.3 Consistency & Asymptoticity
- **Consistency:** A sequence of estimators $\left\{T_{n}\right\}$ of $\gamma=g(\theta)$ is called consistent if$$T_{n} \stackrel{\mathbb{P}_{\theta}}{\longrightarrow} \gamma$$
- **Asymptotic Normality:** A sequence of estimators $\left\{T_{n}\right\}$ of $\gamma=g(\theta)$ is called asymptotically normal with asymptotic covariance matrix $V_{\theta}$, if$$\sqrt{n}\left(T_{n}-\gamma\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, V_{\theta}\right)$$
- **Asymptotic Linearity:** A sequence of estimators $\left\{T_{n}\right\}$ of $\gamma=g(\theta) \in \mathbb{R}^{p}$ is called asymptotically linear if for a function $l_{\theta}: \mathcal{X} \rightarrow \mathbb{R}^{p}$, with $E_{\theta} l_{\theta}(X)=0$ and $$E_{\theta} l_{\theta}(X) l_{\theta}^{T}(X)=: V_{\theta}<\infty,$$ it holds that $$T_{n}-\gamma=\frac{1}{n} \sum_{i=1}^{n} l_{\theta}\left(X_{i}\right)+o_{\mathbf{P}_{\theta}}(1 / \sqrt{n})$$
:::warning
**Remark** 
1. For many estimators ==**asymptotic normality is a consequence of asymptotic linearity**==, that is, the estimator is approximately an average, to which we can apply the CLT.
2. We then call $l_{\theta}$ the **influence function** of (the sequence) $T_{n}$. Roughly speaking, $l_{\theta}(x)$ approximately measures the influence of an additional observation $x$ (compare with the influence function as defined in Section 8.4). 
3. The influence function can be roughly seen as a '**first-order Taylor expansion term**' of their difference when the estimator reaches the param of interest asymptotically.
:::

## 13.2 Theorems and Lemmas
### Theorem 13.1: The central limit theorem (CLT)
#### 1. One-dim CLT
Let $X_{1}, X_{2}, \ldots$ be $i . i . d .$ real-valued random variables with mean $\mu$ and variance $\sigma^{2} .$ Let $\bar{X}_{n}:=\sum_{i=1}^{n} X_{i} / n$ be the average of the first $n .$ Then by the central limit theorem $(C L T)$, $$\sqrt{n}\left(\bar{X}_{n}-\mu\right) \stackrel{\mathcal{D}}{\longrightarrow} \mathcal{N}\left(0, \sigma^{2}\right)$$ that is $$\mathbb{P}\left(\sqrt{n} \frac{\left(\bar{X}_{n}-\mu\right)}{\sigma} \leq z\right) \rightarrow \Phi(z), \forall z$$

#### 2. Multivariate CLT
Let $X_{1}, X_{2}, \ldots$ be i.i.d. copies of a random variable $X=\left(X^{(1)}, \ldots, X^{(p)}\right)^{T}$ in $\mathbb{R}^{p}$. Assume $EX := \mu=\left(\mu_{1}, \ldots, \mu_{p}\right)^{T}$ and $\Sigma:=\operatorname{Cov}(X):=E X X^{T}-\mu \mu^{T}$ exist. Then for all $a \in \mathbb{R}^{p}$, $$E a^{T} X=a^{T} \mu, \operatorname{var}\left(a^{T} X\right)=a^{T} \Sigma a$$ Define $$\bar{X}_{n}=\left(\bar{X}_{n}^{(1)}, \ldots, \bar{X}_{n}^{(p)}\right)^{T}$$ 
:::warning
**Theorem 13.1.1 (Cramér-Wold device):** Let $\left(\left\{Z_{n}\right\}, Z\right)$ be a collection of $\mathbb{R}^{p}$ valued random variables. Then$$Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} Z \Leftrightarrow a^{T} Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} a^{T} Z \quad \forall a \in \mathbb{R}^{p}$$
:::
The Cramér-Wold device therefore gives the $p$-dimensional CLT$$\sqrt{n}\left(\bar{X}_{n}-\mu\right) \stackrel{\mathcal{D}}{\longrightarrow} \mathcal{N}(0, \Sigma)$$
:::warning
**Remark**: Cramér-Wold device enables us to use one-dim argument for multivariate distributions, which is often enough.
:::

### Theorem 13.1.3: [Slutsky’s Theorem](https://www.wikiwand.com/en/Slutsky%27s_theorem)
Let $\left(\left\{Z_{n}, A_{n}\right\}, Z\right)$ be a collection of $\mathbb{R}^{p}$ valued random variables, and $a \in \mathbb{R}^{p}$ be a vector of constants. Assume that $Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} Z, A_{n} \stackrel{\mathbb{P}}{\longrightarrow} a .$ Then$$
A_{n}^{T} Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} a^{T} Z$$

#### Proof Strategy
- **Cramer-Wold Device:** $\left\|\mathbb{E} f\left(a^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z\right)\right\| \rightarrow 0$
- **Portmanteau Theorem:** set $f$ bounded and Lipschitz
:::warning
**Theorem 13.1.2 (Portmanteau Theorem):** Let $\left(\left\{Z_{n}\right\}, Z\right)$ be a collection of $\mathbb{R}^{p}$-valued random variables. Denote the distribution of $Z$ by $Q$ and let $G=Q(Z \leq \cdot)$ be its distribution function. The following statements are equivalent:
(i) $Z_{n} \stackrel{\mathcal{D}}{\longrightarrow} Z$ (i.e., $\mathbb{E} f\left(Z_{n}\right) \rightarrow \mathbb{E} f(Z) \forall f$ bounded and continuous).
(ii) $\mathbb{E} f\left(Z_{n}\right) \rightarrow \mathbb{E} f(Z) \forall f$ bounded and Lipschitz.
> A real-valued function $f$ on (a subset of) $\mathbb{R}^{p}$ is Lipschitz if for a constant $C_{L}$ and all $(z, \tilde{z})$ in the domain of $f,|f(z)-f(\tilde{z})| \leq C_{L}\|z-\tilde{z}\|$.

(iii) $\mathbb{P}\left(Z_{n} \leq z\right) \rightarrow G(z)$ for all $G$-continuity points $z$.
:::
- **Triangular Inequality:** $$\left\|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z\right)\right\| \leq\left\|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z_{n}\right)\right\|+\left\|\mathbb{E} f\left(a^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z\right)\right\|$$
- **Jensen's Inequality**: $$\left\|\mathbb{E} f\left(A_{n}^{T} Z_{n}\right)-\mathbb{E} f\left(a^{T} Z_{n}\right)\right\| \leq \mathbb{E}\left\|f\left(A_{n}^{T} Z_{n}\right)-f\left(a^{T} Z_{n}\right)\right\|$$
- Let $\epsilon>0$ and $M>0$ be arbitrary. Discuss measure $\mathbb{P}$ on $S_{n}:=\left\{\left\|Z_{n}\right\|\leqslant M, \left\|A_{n}-a\right\|\leqslant\epsilon\right\}$ and $S_{n}^{c}$

### Theorem 13.4.1: $\delta$-technique
Suppose $T_{n}$ is asymptotically linear: $$ T_{n}-g(\theta) = \frac{1}{n} \sum_{i=1}^{n} l_{\theta}\left(X_{i}\right)+\mathcal{o}_\mathbb{P}(\frac{1}{\sqrt{n}})$$ with $El_{\theta}(X)=0, \operatorname{Cov}\left(l_{\theta}(X)\right)=V_{\theta} < \infty$ 

Moreover, let $h: \mathbb{R}^{p} \rightarrow \mathbb{R}$ be differentiable at $\gamma = g(\theta)$, with derivative $\dot{h}(\gamma) \in \mathbb{R}^{p}$ $$h\left(T_{n}\right)-h(\gamma)=\frac{1}{n} \sum_{i=1}^{n} \dot{h}(\gamma)^{T} l_{\theta}\left(x_{i}\right)+\mathcal{o}_{\mathbb{P}}(\frac{1}{\sqrt{n}})$$
:::warning
**Remark:** This resembles the chain rule for computing derivatives
**Corollary 13.4.1:** Let $T_{n}$ be an asymptotically normal estimator of $\gamma=g(\theta) \in$ $\mathbb{R}^{p}$ with asymptotic covariance matrix $V_{\theta}$. Suppose $h$ is differentiable at $\gamma$. Then $h\left(T_{n}\right)$ is an asymptotically normal estimator of $h(\gamma)$ with asymptotic variance $$\sqrt{n}\left(h\left(T_{n}\right)-h(\gamma)\right) \stackrel{\mathcal{D}_{\theta}}{\rightarrow} \mathcal{N}\left(0, \dot{h}(\gamma)^{T} V_{\theta} \dot{h}(\gamma)\right)$$
:::

## 13.3 Examples
### Ex 13.3.1: Influence function of the sample average $\mu$
Assuming the entries of $X$ have finite variance, $T_{n}:=\bar{X}_{n}$, $$ T_n - g(\theta) = \bar{X}_{n} - \mu = \sum_{i=1}^{n}\left(X_{i}-\mu\right)$$ Thus, the estimator $T_n$ is a linear and hence asymptotically linear estimator of the mean $\mu$, with influence function $$l_{\theta}(x)=x-\mu$$

### Ex 13.3.2: Influence function of $\mu^2$
Assuming the entries of $X$ have variance $Var_{\theta}(X) = \sigma^2$ and finite kurtosis ($EX^4 < \infty$), the estimator $T_{n}:=\bar{X}_{n}^2$, $$T_{n}-g(\theta) =\bar{X}_{n}^{2}-\mu^{2} = 2\mu\left(\bar{X}_{n}-\mu\right)+\left(\bar{X}_{n}-\mu\right)^{2}$$ where $$\left(\bar{X}_{n}-\mu\right)^{2} = \mathcal{O}_{\mathbb{P}}(1/n) = \mathcal{o}_{\mathbb{P}}(1/\sqrt{n})$$ Thus, $T_n$ is an asymptotically linear estimator of $\mu^2$, with influence function $$l_{\theta}(x)=2\mu(x-\mu)$$ $$V_{\theta}=4 \mu^{2} \sigma^{2}$$
:::warning
**Note:** $V_{\theta} \neq \lim _{n \rightarrow \infty} \operatorname{Var}\left(\sqrt{n}\left(T_{n} - g(\theta)\right)\right) = \infty$ if $EX^4 = \infty$
:::

### Ex 13.3.3 Influence function of the sample variance
Let $X$ be real-valued, with $E_{\theta} X=: \mu, \operatorname{Var}_{\theta}(X)=: \sigma^{2}$ and $\kappa=: E_{\theta}(X-\mu)^{4}$ (assumed to exist). The sample variance is $$T_n:=\frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\bar{X}_{n}\right)^{2} = \frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2}-\left(\bar{X}_{n}-\mu\right)^{2}$$ Because by the $C L T, \bar{X}_{n}-\mu=\mathcal{O}_{\mathbf{P}_{\theta}}\left(n^{-1 / 2}\right)$, we get$$\hat{\sigma}_{n}^{2}=\frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2}+\mathcal{O}_{\mathbf{P}_{\theta}}(1/n)$$ So asymptotically one does not notice that $\mu$ is estimated, and $\hat{\sigma}_{n}^{2}$ (and also $S^{2}$ ) is asymptotically linear with influence function $$l_{\theta}(x)=(x-\mu)^{2}-\sigma^{2}$$ The asymptotic variance is $$V_{\theta}=E_{\theta}\left((X-\mu)^{2}-\sigma^{2}\right)^{2}=\kappa-\sigma^{4}$$

### Ex 13.4.x.1 Asymptotic linear estimator of the parameter of the bernoulli distribution

Suppose $X_{1}, \ldots X_{n}, \ldots$ iid, $X \sim Bernoulli(\theta)$, then $\bar{X}_{n} - \theta =\frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\theta\right)$ is asymptotically linear (normal), thus $\sqrt{n} (\bar{X_n} - \theta) \stackrel{\mathcal{D}}\rightarrow \mathcal{N}(0, \theta(1-\theta))$

We have seen before that the parameter of interest $h(\theta) = \log\frac{\theta}{1-\theta}$ has no unbiased estimator. However, we can conclude from the $\delta$-technique that the plug-in estimator $\log \frac{\bar{X}_{n}}{1-\bar{X}_{n}}$ can achieve asymptotic unbiasness: $$\sqrt{n}\left(\log \frac{\bar{X}_{n}}{1-\bar{X}_{n}}-\log \frac{\theta}{1-\theta}\right) \stackrel{\mathcal{D}}{\rightarrow} \mathcal{N}(0, 1/\theta(1-\theta))$$

Compute CRLB: $$\frac{[\dot{g(\theta)}]^2}{I(\theta)} = 1/\theta(1-\theta)$$ This means $V_\theta$ asymptotically reaches CRLB, i.e. the plug-in estimator is also asymptotically efficient!

### Ex 13.4.x.2 Variance Stablizing Transformation: use the asymptotic Normality without parameters to build CI

Find $h(\theta)$, such that $$V_{\theta} = \dot{h}(\theta)^{2}\theta(1-\theta)=1$$ This is equiv to $\dot{h}(\theta)=\frac{1}{\sqrt{\theta(1 -\theta)}}$. The solution is $$h(x)=2\arcsin (\sqrt{x})$$ i.e. $$\sqrt{n}\left(2\arcsin\left(\sqrt{\bar{x}_{n}}\right)-2 \arcsin (\sqrt{\theta})\right) \stackrel{\mathcal{D}}{\rightarrow} \mathcal{N}(0,1)$$ Thus the approx $(1-\alpha)$ confidence interval for $\theta$ is $\theta \in \sin ^{2}\left[\arcsin(\sqrt{\bar{x}_{n}}) \pm \frac{1}{2\sqrt{n}}\Phi(1-\frac{\alpha}{2})\right]$.