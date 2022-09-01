---
tags: FMS
---

# CH08 Comparison of Estimators
## Lemma 8.3.1: [Rao Blackwell Lemma](https://www.wikiwand.com/en/Rao%E2%80%93Blackwell_theorem)
Let $S=S(X)$ be sufficient. Knowing the sufficient statistic $S$ one can forget about the original data $X$ without loosing information. Suppose that $S$ is sufficient for $\theta$. Suppose moreover that the action space $\mathcal{A} \subset \mathbb{R}^{p}$ is convex, and that for each $\theta$, the map $a \mapsto L(\theta, a)$ is convex. Let $d: \mathcal{X} \rightarrow \mathcal{A}$ be a decision, and define $d^{\prime}(s):=$ $E(d(X) \mid S=s)$ (assumed to exist). Then $$R\left(\theta, d^{\prime}\right) \leq R(\theta, d), \forall \theta$$

### Proof
Jensen's inequality says that for a convex function $g$, $$E(g(X)) \geq g(E(X))$$ Hence, $\forall \theta$, $$\begin{aligned}
E(L(\theta, d(X)) \mid S=s) & \geq L(\theta, E(d(X) \mid S=s)) \\
&=L\left(\theta, d^{\prime}(s)\right)
\end{aligned}$$ By the iterated expectations lemma, we arrive at $$\begin{aligned}
R(\theta, d) &=E_{\theta} L(\theta, d(X)) \\
&=E_{\theta} E(L(\theta, d(X)) \mid S) \\
& \geq E_{\theta} L\left(\theta, d^{\prime}(S)\right) \\
&=R(\theta, d')
\end{aligned}$$

:::warning
**Remark**
In statistics, the Rao-Blackwell theorem, sometimes referred to as the Rao-Blackwell-Kolmogorov theorem, is a result which characterizes the transformation of an arbitrarily crude estimator into an estimator that is optimal by the mean-squared-error criterion or any of a variety of similar criteria.

**Why sufficiency:** Generally, the conditional expected value of one function of these data given another function of these data does depend on $\theta$, but the very definition of sufficiency given above entails that this one does not.

**Lemma 8.2.1 vs Rao-Blackwell Lemma**
Lemma 8.2.1 | Rao-Blackwell Lemma
-- | --
$\mathrm{R}(\theta, d(X_{s}^{*})) = \mathrm{R}(\theta, d(X))$ | $R\left(\theta, E(d(X)\mid S=s)\right) \leqslant R(\theta, d(X))$
$d(X_{s}^{*}) = d(X^{*}({S(X)}))$ is a r.v. | Not Random
stays constant (equality) | can improve (inequality)
no cond required | convex decision set and loss func
:::

## Ex 8.3.1 Mean square error
Let $T$ be an estimator of $g(\theta) \in \mathbb{R}$ and let
$$
R(\theta, T):=\mathbb{E}_{\theta}(T(X)-g(\theta))^{2}=: \operatorname{MSE}_{\theta}(T) .
$$
Let $S$ be sufficient and $\tilde{T}:=\mathbb{E}(T \mid S)$. Then by the Rao-Blackwell Lemma
$$
R(\theta, \tilde{T}) \leq R(\theta, T) \forall \theta .
$$
The mean square error can be decomposed in the variance term and the squared bias term. Since $\mathbb{E} \tilde{T}=\mathbb{E} T$ by the iterated expectations lemma, we thus have
$$
\operatorname{var}_{\theta}(\tilde{T}) \leq \operatorname{var}_{\theta}(T), \forall \theta .
$$
Compare with Lemma 5.2.2 and the result of Lehmann-Scheffé in Section 5.3.