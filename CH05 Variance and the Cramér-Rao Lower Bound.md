---
tags: FMS
---

# CH05 Bias, Variance and the Cramér-Rao Lower Bound
## 5.1 Concepts
### 5.1.1 Unbiased Estimator
Let $T: \mathcal{X} \rightarrow \mathbb{R}$ be an estimator of $g(\theta)$. The bias of $T=T(X)$ is $$\operatorname{bias}_{\theta}(T):=E_{\theta} T-g(\theta)$$ The estimator $T$ is called unbiased if $$\operatorname{bias}_{\theta}(T)=0, \forall \theta$$ Thus, unbiasedness means that there is no systematic error: $E_{\theta} T=g(\theta)$. We require this for all $\theta$.

:::warning
**Remark**
We conclude that requiring unbiasedness can have disadvantages: unbiased estimators do not always exist, and if they do, they can be nonsensical. Moreover, the property of unbiasedness is not preserved under taking nonlinear transformations.
:::

### 5.1.2 Mean Square Error
The mean square error of $T$ is $$\operatorname{MSE}_{\theta}(T):=E_{\theta}(T-g(\theta))^{2}$$

### 5.1.3 Complete Estimator
A sufficient statistic $S$ is called complete if we have the following implication: $$E_{\theta} h(S)=0, \forall \theta \Rightarrow h(S)=0, P_{\theta}-a . s ., \forall \theta$$ Here, $h$ is a function of $S$ not depending on $\theta$.

### 5.1.4 UMVU Estimator
An unbiased estimator $T^{*}$ is called UMVU (Uniform Minimum Variance Unbiased) if for any other unbiased estimator $T$, $$
\operatorname{var}_{\theta}\left(T^{*}\right) \leq \operatorname{var}_{\theta}(T), \forall \theta$$

### 5.1.5 Score function and Fisher information
- **Condition I:** The set $$A:=\left\{x: p_{\theta}(x)>0\right\}$$ does not depend on $\theta$.
- **Condition II:** (Differentiability in $L_{2}$ ) For all $\theta$ and for a function $s_{\theta}: \mathcal{X} \rightarrow \mathbb{R}$ satisfying $$I(\theta):=E_{\theta} s_{\theta}^{2}(X)<\infty,$$ it holds that $$\lim _{h \rightarrow 0} E_{\theta}\left(\frac{p_{\theta+h}(X)-p_{\theta}(X)}{h p_{\theta}(X)}-s_{\theta}(X)\right)^{2}=0$$

If I and II hold, we call $$s_{\theta}(x):=\frac{d}{d \theta} \log p_{\theta}(x)$$ the score function, and $$I(\theta):=E_{\theta} s_{\theta}^{2}(X)$$ the Fisher information for estimating $\theta$.

:::warning
**Remark** 
- As already noted, if $p_{\theta}(x)$ is differentiable for all $x$, we can take (under regularity conditions) $$s_{\theta}(x):=\frac{d}{d \theta} \log p_{\theta}(x)=\frac{\dot{p}_{\theta}(x)}{p_{\theta}(x)}$$ where $$\dot{p}_{\theta}(x):=\frac{d}{d \theta} p_{\theta}(x)$$
- Under regularity, $$E_{\theta}(\dot{s}_{\theta}(x)) = -I(\theta)$$
- Suppose $X_{1}, \ldots, X_{n}$ are i.i.d. with density $p_{\theta}$, and $s_{\theta}=\dot{p}_{\theta} / p_{\theta}$ exists. The joint density is $$\mathbf{p}_{\theta}(\mathbf{x})=\prod_{i=1}^{n} p_{\theta}\left(x_{i}\right),$$ so that (under conditions I and II) the score function for $n$ observations is $$\mathbf{s}_{\theta}(\mathbf{x})=\sum_{i=1}^{n} s_{\theta}\left(x_{i}\right)$$ The Fisher information ==for $n$ observations== is thus $$\mathbf{I}(\theta)=\operatorname{Var}_{\theta}\left(\mathbf{s}_{\theta}(\mathbf{X})\right)=\sum_{i=1}^{n} \operatorname{Var}_{\theta}\left(s_{\theta}\left(X_{i}\right)\right)=n I(\theta)$$
:::

### 5.1.6 CRLB
We call $$\dot{g}^{2}(\theta) / I(\theta), \theta \in \Theta$$ the Cramer Rao lower bound (CRLB) (for estimating $g(\theta)$ ).


## 5.2 Lemmas and Theorems
### Lemma 5.2.1 Bias-Variance Decomp
We have the following decomposition for the mean square error: $$\operatorname{MSE}_{\theta}(T)=\operatorname{bias}_{\theta}^{2}(T)+\operatorname{var}_{\theta}(T)$$

#### Proof 
Write $E_{\theta}T:=q(\theta)$. Then $$\begin{aligned}
E_{\theta}(T-g(\theta))^{2} &=\underbrace{E_{\theta}(T-q(\theta))^{2}}_{=\operatorname{var}_{\theta}(T)}+\underbrace{(q(\theta)-g(\theta))^{2}}_{=\operatorname{bias}_{\theta}^{2}(T)} \\
&+2(q(\theta)-g(\theta)) \underbrace{E_{\theta}(T-q(\theta))}_{=0} .
\end{aligned}$$

### Lemma 5.2.2 Iterative variance Lemma
Let $Y$ and $Z$ be two random variables. Then $$\operatorname{var}(Y)=\operatorname{var}(E(Y \mid Z))+E \operatorname{var}(Y \mid Z)$$

:::warning
**Remark**
- var = var btwn groups + averaging variance among groups
- By conditioning on $S$, "superfluous" variance in the sample is killed.
:::

#### Proof
Use Iterative expectation lemma. It holds that $$\begin{aligned}
\operatorname{var}(E(Y \mid Z)) &=E[E(Y \mid Z)]^{2}-[E(E(Y \mid Z))]^{2} \\
&=E[E(Y \mid Z)]^{2}-[E Y]^{2}\end{aligned} $$ and $$\begin{gathered}
E \operatorname{var}(Y \mid Z)=E\left[E\left(Y^{2} \mid Z\right)-[E(Y \mid Z)]^{2}\right] \\=E Y^{2}-E[E(Y \mid Z)]^{2}\end{gathered} $$ Hence, when adding up, the term $E[E(Y \mid Z)]^{2}$ cancels out, and what is left over is exactly the variance $$\operatorname{var}(Y)=E Y^{2}-[E Y]^{2}$$

### Lemma 5.3.1: The Lehmann-Scheffé Lemma
Let $T$ be an unbiased estimator of $g(\theta)$, with, for all $\theta$, finite variance. Moreover, let $S$ be sufficient and complete. Then $T^{*}:=E(T \mid S)$ is a (unique) UMVU.

:::warning
**Remark**
Let $S$ be sufficient and complete and $T^{\prime}\left(S\right) \in \mathbb{R}$, then $T^{\prime}$ is a UMVU estimator of $E_{\theta} T^{\prime}$

:::

#### Proof
Suppose that $T$ is unbiased, and that $S$ is sufficient. Let $$T^{*}:=E(T \mid S)$$ The distribution of $T$ given $S$ does not depend on $\theta$, so $T^{*}$ is also an estimator. 

Moreover, it is unbiased: by the iterated expectations lemma $$E_{\theta} T^{*}=E_{\theta}(E(T \mid S))=E_{\theta} T=g(\theta)$$

By iterative variance Lemma $$\operatorname{Var}(T) = \operatorname{Var}(E(T|S)) + E(\operatorname{Var}(T|S)) = \operatorname{Var}(T^*) + E(\operatorname{Var}(T|S)) \geqslant \operatorname{Var}(T^*)$$ Thus $T^*$ has smaller variance than $T$.

Let $T'$ be another (arbitary) unbiased estimator of $g(\theta)$. Define $T^{*^\prime}(S) = E(T'|S)$, which is also an unbiased estimator and has smaller variance than $T'$. If we have $$E_{\theta}\left(T^{*^\prime}(S)-T^{\prime}(S)\right)=0, \forall \theta$$ Because $S$ is complete, this implies $$T^{*}=T^{*^\prime}, P_{\theta}-a . s .$$ Thus $T^*$ is (unique) UMVU.

### Lemma 5.4.1 Completeness for exponential families
Let for $\theta \in \Theta$, $$p_{\theta}(x)=\exp \left[\sum_{j=1}^{k} c_{j}(\theta) T_{j}(x)-d(\theta)\right] h(x)$$ Consider the set $$\mathcal{C}:=\left\{\left(c_{1}(\theta), \ldots, c_{k}(\theta)\right): \theta \in \Theta\right\} \subset \mathbb{R}^{k}$$ Suppose that $\mathcal{C}$ is truly $k$-dimensional (that is, not of dimension smaller than $k)$, i.e., it contains an open ball in $\mathbb{R}^{k}$. (Or an open cube $\prod_{j=1}^{k}\left(a_{j}, b_{j}\right)$.) Then $S:=\left(T_{1}, \ldots, T_{k}\right)$ is complete.

### Lemma 5.5.1 Score Function
Assume Conditions I and II in 5.1.5. Then $$E_{\theta} s_{\theta}(X)=0, \forall \theta$$

#### Proof
Under $P_{\theta}$, we only need to consider values $x$ with $p_{\theta}(x)>0$, that is, we may freely divide by $p_{\theta}$, without worrying about dividing by zero. Observe that $$E_{\theta}\left(\frac{p_{\theta+h}(X)-p_{\theta}(X)}{p_{\theta}(X)}\right)=\int_{A}\left(p_{\theta+h}-p_{\theta}\right) d \nu=0$$ since densities integrate to 1, and both $p_{\theta+h}$ and $p_{\theta}$ vanish outside $A$. Thus by Jensen's Inequality, $$\begin{aligned}
\left|E_{\theta} s_{\theta}(X)\right|^{2} &=\left|E_{\theta}\left(\frac{p_{\theta+h}(X)-p_{\theta}(X)}{h p_{\theta}(X)}-s_{\theta}(X)\right)\right|^{2} \\
& \leq E_{\theta}\left(\frac{p_{\theta+h}(X)-p_{\theta}(X)}{h p_{\theta}(X)}-s_{\theta}(X)\right)^{2} \rightarrow 0
\end{aligned}$$

### Theorem 5.5.1 (The Cramér-Rao lower bound) 
Suppose Conditions I and II are met, and that $T$ is an unbiased estimator of $g(\theta)$ with finite variance. Then $g(\theta)$ has a derivative, $\dot{g}(\theta):=d g(\theta) / d \theta$, equal to $$\dot{g}(\theta)=\operatorname{Cov}\left(T, s_{\theta}(X)\right)$$ Moreover, $$\operatorname{Var}_{\theta}(T) \geq \frac{\dot{g}^{2}(\theta)}{I(\theta)}, \forall \theta$$

:::warning
**Remark: biased version**
Let $T$ be a possibly biased estimator y $g(\theta)$. Define $E_{\theta} T=: q(\theta)$. Then $$\operatorname{MSE}_{\theta}(T) \geqslant \frac{[\dot{q}(\theta)]^{2}}{I(\theta)}+(q(\theta)-g(\theta))^{2}$$
:::


#### Proof
We first show differentiability of $g .$ As $T$ is unbiased, we have $$\begin{aligned}\frac{g(\theta+h)-g(\theta)}{h} 
&=\frac{E_{\theta+h} T(X)-E_{\theta} T(X)}{h} \\ 
&=\frac{1}{h} \int T\left(p_{\theta+h}-p_{\theta}\right) d \nu \\
&=\int \frac{T\left(p_{\theta+h}-p_{\theta}\right)p_{\theta}}{hp_{\theta}}  d\nu \\
&=\int \left[ \frac{T\left(p_{\theta+h}-p_{\theta}\right)p_{\theta}}{hp_{\theta}} - Ts_{\theta}p_{\theta} + Ts_{\theta}p_{\theta} \right]  d \nu\\
&=\underbrace{\int\left[ \frac{T\left(p_{\theta+h}-p_{\theta}\right)p_{\theta}}{hp_{\theta}} - Ts_{\theta}p_{\theta} \right]  d \nu}_{(i)} + \underbrace{\int Ts_{\theta}p_{\theta}  d \nu}_{(ii)}\\
\end{aligned}$$ For $(i)$, $$\begin{aligned}
(i)^2 &= \left( \int\left[ T \left( \frac{\left(p_{\theta+h}-p_{\theta}\right)}{hp_{\theta}} - s_{\theta} \right) \right] p_{\theta} d \nu \right)^2 \\ 
&\underbrace{\leqslant \left(\int T^{2} p_{\theta}\right) \cdot \left(\int\left(\frac{p_{\theta+h}-p_{\theta}}{h p_{\theta}}-s_{\theta}\right)^{2} p_{\theta}\right)}_{\text{by Cauchy-Schwarz Inequality}}\\ 
&= \underbrace{\operatorname{Var}_{\theta}(T)}_{\text{finite}} \cdot \underbrace{E_{\theta}\left(\frac{p_{\theta+h}(X)-p_{\theta}(X)}{h p_{\theta}(X)}-s_{\theta}(X)\right)^{2}}_{\xrightarrow{h \rightarrow 0} 0} \\
&\xrightarrow{h \rightarrow 0} 0
\end{aligned}$$ For $(ii)$: $$\int Ts_{\theta}p_{\theta}  d \nu = E_{\theta}(T\cdot s_{\theta}) = \operatorname{Cov}(T,s_{\theta})$$ Thus $$ \dot{g}(\theta) = \lim\limits_{h\rightarrow 0} \frac{g(\theta+h)-g(\theta)}{h} = \operatorname{Cov}(T,s_{\theta})$$ By Cauchy-Schwarz,$$\begin{aligned}
\dot{g}^{2}(\theta) &=\left(\operatorname{cov}_{\theta}\left(T, s_{\theta}(X)\right)\right)^{2} \\ & \leq \operatorname{var}_{\theta}(T) \operatorname{var}_{\theta}\left(s_{\theta}(X)\right)=\operatorname{var}_{\theta}(T) I(\theta)\end{aligned}$$

### Lemma 5.6.1 CRLB can only be reached by exp fam.
Assume Conditions I and II, with $s_{\theta}=\dot{p}_{\theta} / p_{\theta}$. Suppose $T$ is unbiased for $g(\theta)$, and that $T$ reaches the Cramér Rao lower bound. Then $\left\{P_{\theta}: \theta \in \Theta\right\}$ forms a one-dimensional exponential family: there exist functions $c(\theta), d(\theta)$, and $h(x)$ such that for all $\theta$, $$p_{\theta}(x)=\exp [c(\theta) T(X)-d(\theta)] h(x), x \in \mathcal{X}$$ Moreover, $c(\theta)$ and $d(\theta)$ are differentiable, say with derivatives $\dot{c}(\theta)$ and $\dot{d}(\theta)$ respectively. We furthermore have the equality $$g(\theta)=\dot{d}(\theta) / \dot{c}(\theta), \forall \theta$$

### Theorem 5.7.1 CRLB in higher dimension
The Fisher information matrix is $$I(\theta)=E_{\theta} s_{\theta}(X) s_{\theta}^{T}(X)=\operatorname{Cov}_{\theta}\left(s_{\theta}(X)\right)$$ Let $T$ be an unbiased estimator of $g(\theta)$. Then, under regularity conditions, $$\operatorname{Var}_{\theta}(T) \geq \dot{g}(\theta)^T I(\theta)^{-1} \dot{g}(\theta)$$

#### Corollary 5.7.1
$\operatorname{Cov}_{\theta}(T) \geq I(\theta)^{-1}$, that is, $\operatorname{Cov}_{\theta}(T)-I(\theta)^{-1}$ is positive semidefinite