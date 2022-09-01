---
tags: FMS
---

# CH11 Proving Admissibility and Minimaxity
## 11.1 Concepts
### 11.1.1 Minimaxity and Admissiability
- **Minimaxity**: $T$ is minimax if $\forall T^{\prime}$, $$\sup _{\theta} R(\theta, T) \leq \sup _{\theta} R\left(\theta, T^{\prime}\right)$$ or equivalentlly, $$
\sup _{\theta} R(\theta, T)=\inf _{T^{\prime}} \sup _{\theta} R\left(\theta, T^{\prime}\right)$$ 
:::warning
Minimaxity concerns the best ($\inf$) statistic/decision $(T/d)$ in the worst possible case $(\sup R)$.
:::
- **Admissibility**: $T$ is ==inadmissible== if $\exists T^{\prime}$: $$\forall \theta, R\left(\theta, T^{\prime}\right) \leq R(\theta, T) \text { and } \\\exists \theta, R\left(\theta, T^{\prime}\right)<R(\theta, T)$$

### 11.1.2 Bayes and Extended Bayes Estimator
- **Bayes (Minimal Bayes Risk)**: $T$ is Bayes if $\forall T^{\prime}$: $$r_{w}(T) \leq r_{w}\left(T^{\prime}\right)$$
- **Extended Bayes**: A statistic $T$ is called extended Bayes if there exists a sequence of prior densities $\left\{w_{m}\right\}_{m=1}^{\infty}$ (w.r.t. dominating measures that are allowed to depend on $m$), such that $$r_{w_{m}}(T)-\inf _{T^{\prime}} r_{w_{m}}\left(T^{\prime}\right) \rightarrow 0 \text { as } m \rightarrow \infty$$ 
:::warning
Especially in cases where one wants to use the uniform distribution as prior, but cannot do so because $\Theta$ is not bounded, the notion extended Bayes is useful.
:::


## 11.2 Lemmas
### Schematic Diagram
![FMS-CH11](https://s2.loli.net/2022/01/08/omsW1TpzdnBDOJi.png)

### Lemma 11.1.1: Proving Minimaxity

Suppose $T$ is a statistic with risk $R(θ,T) = R(T)$ not depending on $\theta$. Then

(i) **$T$ admissible $\Rightarrow$ $T$ minimax**,
(ii) **$T$ Bayes $\Rightarrow$ $T$ minimax**, and in fact more generally,
(iii) **$T$ extended Bayes $\Rightarrow$ $T$ minimax**.


### Lemma 11.2.1: Proving Admissibility for Bayes Estimator
> **Regularity**: the parameter space is assumed to be an open subset of a topological space, so that we can consider open neighborhoods of members of $\Theta$, and continuous functions on $\Theta$. We moreover restrict ourselves to statistics $T$ with $R(θ,T) < \infty$, so that $P_{\theta}$-a.s. indicates $\forall \theta, R\left(\theta, T^{\prime}\right)=R(\theta, T)$


Suppose that the statistic $T$ is Bayes for the prior density $w$. Then (i) or (ii) below are sufficient conditions for the admissibility of $T$:

(i) The statistic $T$ is the **unique Bayes decision** (i.e., $r_w(T) = r_w(T′)$ implies that $\forall \theta$, $T=T'$ $P_\theta$-almost surely),
(ii) **For all $T′$, $R(\theta,T′)$ is continuous in $\theta$**, and moreover, **for all open $U \subset \Theta$, the prior probability $\Pi(U):=\int_{U} w(\vartheta) d \mu(\vartheta)$ of $U$ is strictly positive**


### Lemma 11.2.2 Proving Admissibility for Extended Bayes Estimator
> **Regularity**: the parameter space is assumed to be an open subset of a topological space, so that we can consider open neighborhoods of members of $\Theta$, and continuous functions on $\Theta$. We moreover restrict ourselves to statistics $T$ with $R(θ,T) < \infty$, so that $P_{\theta}$-a.s. indicates $\forall \theta, R\left(\theta, T^{\prime}\right)=R(\theta, T)$

Suppose the statistic $T$ is Extended Bayes, and that **for all $T′$, $R(\theta,T′)$ is continuous in $\theta$**. In fact assume, **for all open $U \subset \Theta$**, $$\frac{r_{w_{m}}(T)-\inf _{T^{\prime}} r_{w_{m}}\left(T^{\prime}\right)}{\Pi_{m}(U)} \rightarrow 0$$ **as $m \rightarrow \infty$**. Here $\Pi_{m}(U):=\int_{U} w_{m}(\vartheta) d \mu_{m}(\vartheta)$ is the probability of $U$ under the prior $\Pi_{m}$. 

Then $T$ is admissible.


## 11.3 Key Takeaways & Common Tricks
1. Proving admissibility usually starts with ==supposing inadmissibility== which followed by ==the rebuttal method==.
2. ==Usually in this chapter, we inspect Bayes risk, which is bounded by supremum risk== (supremum is irrelevant to the param and the prior integrates to 1): $$\begin{aligned}r_{w}\left(T^{\prime}\right) &=\int R\left(\vartheta, T^{\prime}\right) w(\vartheta) d \mu(\theta) \\& \leqslant \int \sup _{\vartheta} R\left(\vartheta, T^{\prime}\right) w(\vartheta) d \mu(\theta) \\ &=\sup _{\vartheta} R\left(\vartheta, T^{\prime}\right)\end{aligned}$$
3. For extended Bayes, we usually suppose for simplicity that a ==Bayes decision $T_m$ for the prior $w_m$ exists for all $m$==, i.e. $$r_{w_{m}}\left(T_{m}\right)=\inf _{T^{\prime}} r_{w_{m}}\left(T^{\prime}\right), m=1,2, \ldots$$ and evaluate the discrepency between $T$ and $T_m$.
4. When using quadratic loss, the risk is MSE, which can be ==decomposed into $Bias^2 + Var$==.
5. How to ==leverage the assumption of open set when proving admissibility==: $T$ is inadmissible. Then, for some $T^{\prime}, R\left(\theta, T^{\prime}\right) \leq R(\theta, T)$ for all $\theta$, and, for some $\theta_{0}, R\left(\theta_{0}, T^{\prime}\right)<R\left(\theta_{0}, T\right)$, so that for some $\epsilon > 0$, open neighborhood $U \subset \Theta$ of $\theta_{0}$, $$R\left(\vartheta, T^{\prime}\right) \leq R(\vartheta, T)-\epsilon, \vartheta \in U$$, and then integrate on the two partitions $$r_{w}\left(T^{\prime}\right)=\int_{U} R\left(\vartheta, T^{\prime}\right) w(\vartheta) d \nu(\vartheta)+\int_{U^{c}} R\left(\vartheta, T^{\prime}\right) w(\vartheta) d \nu(\vartheta)$$, from which we get $$r_{w}(T^{\prime})\leq r_{w}(T)-\epsilon \Pi(U)$$

## 11.4 Examples
### Ex 11.1.1: Minimax estimator for Binomial distribution
(See Ex 10.5.2 and conjugate priors)

### Ex 11.2.1: Admissible estimators for the normal mean
Let $X$ be $N(\theta,1)$-distributed, $\theta \in \Theta:=\mathbb{R}$ and $R(\theta, T):=E_{\theta}(T-\theta)^{2}$ be the quadratic risk. 

We consider estimators of the form $$T =aX+b, \quad a>0, b\in R$$ $T$ is admissible if and only if one of the following cases hold 
(i) $a<1$, 
(ii) $a=1$ and $b=0$.

#### Key Points
- **Necessity**: $\Rightarrow$ is evaluated by the inadmissibility of the complement setting (nonsensical situations given the variance=1)
- **Sufficiency**: 
    - (i) Unique Bayes:
        - Normal Prior: $\theta \sim \mathcal{N}\left(c, \tau^{2}\right)$
        - Prove $E_{X}\left(T(X)-T^{\prime}(X)\right)^{2}=0$
        - Use [Lemma 11.2.1](#Lemma-1121-Proving-Admissibility-for-Bayes-Estimator)
    - (ii) Extended Bayes ($a=1$ will make $\tau^2 \rightarrow \infty$, i.e. a uniform prior)
        - Normal Prior: $w_m \sim \mathcal{N}\left(0, m\right)$
        - Set $U=(u, u+h)$, with $u$ and $h>0$ fixed.
        - Take first-order Taylor item, with a positive residue
        - Use [Lemma 11.2.2](#Lemma-1122-Proving-Admissibility-for-Extended-Bayes-Estimator)