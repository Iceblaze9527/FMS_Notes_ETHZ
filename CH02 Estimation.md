---
tags: FMS
---

# CH02 Estimation
## 2.1 Concepts
### 2.1.1 The empirical distrib
Let $X_{1}, \ldots, X_{n}$ be real-valued observations. An example of a nonparametric estimator is the empirical distribution function $$\hat{F}_{n}(\cdot):=\frac{1}{n} \#\left\{X_{i} \leq \cdot, 1 \leq i \leq n\right\}$$ This is an estimator of the theoretical distribution function $$F(\cdot):=P(X \leq \cdot)$$ (SLLN ensures asymptotic equivalence)

Let now $\mathscr{X}$ general. The empirical distribution is $\hat{P}_{n}(A):=\frac{1}{n} \sum_{i=1}^{n} 1_{A}\left(X_{i}\right), \quad A \subset \mathscr{X}$, by LLN, $\hat{P}_{n}(A) \approx P(A), \forall A$ as $n\rightarrow \infty$, thus $\hat{P}_{n}$ is an estimator of $P$

### 2.1.2 Plug-in methods

### 2.1.3 Method of Moments
Let $X \in \mathbb{R}$ and suppose (say) that the parameter of interest is $\theta$ itself, and that $\Theta \subset \mathbb{R}^{p}$. Let $\mu_{1}(\theta), \ldots, \mu_{p}(\theta)$ denote the first $p$ moments of $X$ (assumed to exist), i.e., $$\mu_{j}(\theta)=E_{\theta} X^{j}=\int x^{j} d F_{\theta}(x), j=1, \ldots, p$$ Also assume that the map $$m: \Theta \rightarrow \mathbb{R}^{p}$$ defined by $$m(\theta)=\left[\mu_{1}(\theta), \ldots, \mu_{p}(\theta)\right]$$ has an inverse $$m^{-1}\left(\mu_{1}, \ldots, \mu_{p}\right)$$ for all $\left[\mu_{1}, \ldots, \mu_{p}\right] \in \mathcal{M}$ (say). We estimate the $\mu_{j}$ by their sample counterparts $$\hat{\mu}_{j}:=\frac{1}{n} \sum_{i=1}^{n} X_{i}^{j}=\int x^{j} d \hat{F}_{n}(x), j=1, \ldots, p$$ When $\left[\hat{\mu}_{1}, \ldots, \hat{\mu}_{p}\right] \in \mathcal{M}$ we can plug them in to obtain the estimator $$\hat{\theta}:=m^{-1}\left(\hat{\mu}_{1}, \ldots, \hat{\mu}_{p}\right)$$

:::warning
**Remark**
- In some cases, we don't need to know the form of p.d.f., that is, we don't need a statistical model, to derive moment estimator
- Moment estimation may not be unique (as lower the order as possible)
- Moment estimation may not have closed form solution: numerical method
- Moment estimation may not exist
- Origin moments (in our case) are unbiased
- Many moment estimates are asymptotically unbiased
- **Consistency**
    - Sample origin moments and sample center moments are strongly consistent (SLLN)
    - If $G(\cdot)$ is continuous, then $\hat{g}(\boldsymbol{X})$ is strongly consistent
- **Asymptotic normality**
    - Under some regularity conditions, $\hat{g}(\boldsymbol{X})$ is consistent asymptotic normal estimate

:::

### 2.1.4 Maximum Likelihood
The likelihood function (with data $\mathbf{X}=\left(X_{1}, \ldots, X_{n}\right)$ ) is the function $L_{\mathbf{X}}: \Theta \rightarrow \mathbb{R}$ given by $$L_{\mathbf{X}}(\vartheta):=\prod_{i=1}^{n} p_{\vartheta}\left(X_{i}\right), \vartheta \in \Theta$$ The MLE (maximum likelihood estimator) is $$\hat{\theta}:=\arg \max _{\vartheta \in \Theta} L_{\mathbf{X}}(\vartheta)$$

:::warning
**Remark**
- Alternatively, we may write the MLE as the maximizer of the log-likelihood $$\hat{\theta}=\arg \max _{\vartheta \in \Theta} \log L_{\mathbf{X}}(\vartheta)=\arg \max _{\vartheta \in \Theta} \sum_{i=1}^{n} \log p_{\vartheta}\left(X_{i}\right)$$ The log-likelihood is generally mathematically more tractable.
- The likelihood function may have local maxima. Moreover, the MLE is not always unique, or may not exist (for example, the likelihood function may be unbounded)
- **Invariance property of MLEs:** If $\hat{\theta}$ is the MLE of $\theta$, then for any function $g(\theta)$, the MLE of $g(\theta)$ is $g(\hat{\theta})$.
- **Consistency:** no easy task, see Sec 14.2
- **Aysmptotic Normality:** see Sec 14.4
- If the statistical model is a good approximation, MLE is often more efficient than the moment estimator
:::


## 2.2 Lemmas
### Lemma 2.4.1 Maximum likelihood is a plug-in method
> First, as noted above, the MLE maximizes the log-likelihood. We may of course normalize the $\log$-likelihood by $1 / n$ :$$\hat{\theta}=\arg \max _{\vartheta \in \Theta} \frac{1}{n} \sum_{i=1}^{n} \log p_{\vartheta}\left(X_{i}\right)$$ Replacing the average $\sum_{i=1}^{n} \log p_{\vartheta}\left(X_{i}\right) / n$ in (2.2) by its theoretical counterpart $E_{\theta} \log p_{\vartheta}(X)$ gives $$\arg \max _{\vartheta \in \Theta} E_{\theta} \log p_{\vartheta}(X)$$ which is indeed equal to the parameter $\theta$ we are trying to estimate.

We have
$$\theta=\arg \max _{\vartheta \in \Theta} E_{\theta} \log p_{\vartheta}(X)
$$

#### Proof
By the (Jensen's) inequality $\log x \leq x-1, x>0$, for all $\vartheta \in \Theta$ $$E_{\theta} \log \frac{p_{\vartheta}(X)}{p_{\theta}(X)} \leq E_{\theta}\left(\frac{p_{\vartheta}(X)}{p_{\theta}(X)}-1\right)=0$$

:::warning
**Remark**
- Some care has to be taken, not to divide by zero! This can be handled e.g., by assuming that the support $\left\{x: p_{\theta}(x)>0\right\}$ does not depend on $\theta$.
:::

### Lemma 14.1.1 Alteranative proof of Lemma 2.4.1 using KL-info
KL info (relative entropy): $$K(\vartheta \mid \theta)=E_{\theta} \log \frac{P_{\theta}(x)}{P_{\vartheta}(x)}$$

**Restatement:** The function $\mathcal{R}(\tilde{\theta})=-E_{\theta} \log p_{\tilde{\theta}}(X)$ is minimized at $\tilde{\theta}=\theta:$ $$
\theta=\arg \min _{\tilde{\theta}} \mathcal{R}(\tilde{\theta})$$

#### Proof 
We will show that $$K(\tilde{\theta} \mid \theta) \geq 0$$ This follows from Jensen's inequality. Since the log-function is concave, $$\begin{aligned}
K(\tilde{\theta} \mid \theta) &=-E_{\theta} \log \left(\frac{p_{\tilde{\theta}}(X)}{p_{\theta}(X)}\right) \\
& \geq-\log \left(E_{\theta}\left(\frac{p_{\tilde{\theta}}(X)}{p_{\theta}(X)}\right)\right) \\&=-\log 1=0\end{aligned}$$


## 2.3 Examples