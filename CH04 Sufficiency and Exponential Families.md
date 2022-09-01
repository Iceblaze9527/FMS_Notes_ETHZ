---
tags: FMS
---

# CH04 Sufficiency and Exponential Families
## 4.1 Concepts
### 4.1.1 Sufficiency
We call $S$ sufficient for $\theta \in \Theta$ if for all $\theta$, and all possible $s$, the conditional distribution $$P_{\theta}(X \in \cdot \mid S(X)=s)$$ does not depend on $\theta$.

:::warning
**Remark**
The gist of sufficiency: losslessness. We can regenerate new samples that have the exact same distrib as previous ones by knowing sufficient statistic only
:::

### 4.1.2 Exp fam.
A $k$-dimensional exponential family is a family of distributions $\left\{P_{\theta}: \theta \in \Theta\right\}$, dominated by some $\sigma$-finite measure $\nu$, with densities $p_{\theta}=d P_{\theta} / d \nu$ of the form $$p_{\theta}(x)=\exp \left[\sum_{j=1}^{k} c_{j}(\theta) T_{j}(x)-d(\theta)\right] h(x)$$ 

:::warning
**Note** 
- In case of a $k$-dimensional exponential family, the $k$-dimensional statistic $S(X)=\left(T_{1}(X), \ldots, T_{k}(X)\right)$ is sufficient for $\theta$.
- If $X_{1}, \ldots, X_{n}$ is an i.i.d. sample from a $k$-dimensional exponential family, then the distribution of $\mathbf{X}=\left(X_{1}, \ldots, X_{n}\right)$ is also in a $k$-dimensional exponential family. The density of $\mathbf{X}$ is then (for $\mathbf{x}:=\left(x_{1}, \ldots, x_{n}\right)$ ),  $$\mathbf{p}_{\theta}(\mathbf{x})=\prod_{i=1}^{n} p_{\theta}\left(x_{i}\right)=\exp \left[\sum_{j=1}^{k} n c_{j}(\theta) \bar{T}_{j}(\mathbf{x})-n d(\theta)\right] \prod_{i=1}^{n} h\left(x_{i}\right)$$where, for $j=1, \ldots, k$,$$\bar{T}_{j}(\mathbf{x})=\frac{1}{n} \sum_{i=1}^{n} T_{j}\left(x_{i}\right)$$ Hence $S(\mathbf{X})=\left(\bar{T}_{1}(\mathbf{X}), \ldots, \bar{T}_{k}(\mathbf{X})\right)$ is then sufficient for $\theta$.
- The functions $\left\{T_{j}\right\}$ and $\left\{c_{j}\right\}$ are not uniquely defined.

:::

#### Canonical Form
We call $\left\{P_{\theta}: \theta \in \Theta\right\}$ an exponential family in canonical form, if $$p_{\theta}(x)=\exp \left[\sum_{j=1}^{k} \theta_{j} T_{j}(x)-d(\theta)\right] h(x)$$ Note that $d(\theta)$ is the normalizing constant $$d(\theta)=\log \left(\int \exp \left[\sum_{j=1}^{k} \theta_{j} T_{j}(x)\right] h(x) d \nu(x)\right)$$

## 4.2 Lemmas and Theorems
### Theorem 4.2.1 (Factorization Theorem of Neyman) 
Suppose $\left\{P_{\theta}: \theta \in \Theta\right\}$ is dominated by a $\sigma$-finite measure $\nu$. Let $p_{\theta}:=d P_{\theta} / d \nu$ denote the densities. Then $S$ is sufficient for $\theta$ if and only if one can write $p_{\theta}$ in the form $$p_{\theta}(x)=g_{\theta}(S(x)) h(x), \forall x, \theta$$ for some functions $g_{\theta}(\cdot) \geq 0$ and $h(\cdot) \geq 0$.

:::warning
**Corollary 4.2.1**
The likelihood is $L_{X}(\theta)=p_{\theta}(X)=g_{\theta}(S) h(X)$. Hence, the maximum likelihood estimator $\hat{\theta}=\arg \max _{\theta} L_{X}(\theta)=\arg \max _{\theta} g_{\theta}(S)$ depends only on the sufficient statistic $S$.
:::

#### Proof in the discrete case. 
Suppose $X$ takes only the values $a_{1}, a_{2}, \ldots \forall \theta$ (so we may take $\nu$ to be the counting measure). Let $Q_{\theta}$ be the distribution of $S$ : $$Q_{\theta}(s):=\sum_{j: S\left(a_{j}\right)=s} P_{\theta}\left(X=a_{j}\right)$$ The conditional distribution of $X$ given $S$ is $$P_{\theta}(X=x \mid S=s)=\frac{P_{\theta}(X=x)}{Q_{\theta}(s)}, S(x)=s$$ ( $\Rightarrow$ ) If $S$ is sufficient for $\theta$, the above does not depend on $\theta$, but is only a function of $x$, say $h(x)$. So we may write for $S(x)=s$, $$P_{\theta}(X=x)=P_{\theta}(X=x \mid S=s) Q_{\theta}(S=s)=h(x) g_{\theta}(s),$$ with $g_{\theta}(s)=Q_{\theta}(S=s)$.

( $\Leftarrow$ ) Inserting $p_{\theta}(x)=g_{\theta}(S(x)) h(x)$, we find $$Q_{\theta}(s)=g_{\theta}(s) \sum_{j: S\left(a_{j}\right)=s} h\left(a_{j}\right),$$ This gives in the formula for $P_{\theta}(X=x \mid S=s)$, $$P_{\theta}(X=x \mid S=s)=\frac{h(x)}{\sum_{j: S\left(a_{j}\right)=s} h\left(a_{j}\right)}$$

### Lemma 4.5.1 The mean and variance of statistics in exp fam (in canonical form)
We have (under regularity)$$ E_{\theta} T(X)=\dot{d}(\theta),\operatorname{Cov}_{\theta}(T(X))=\ddot{d}(\theta)$$

#### Proof 
By the definition of $d(\theta)$, we find $$\begin{aligned}
\dot{d}(\theta) &=\frac{\partial}{\partial \theta} \log \left(\int \exp \left[\theta T(x)\right] h(x) d \nu(x)\right) \\
&=\frac{\int \exp \left[\theta T(x)\right] T(x) h(x) d \nu(x)}{\int \exp \left[\theta T(x)\right] h(x) d \nu(x)} \\
&=\int \exp \left[\theta T(x)-d(\theta)\right] T(x) h(x) d \nu(x) \\
&=\int p_{\theta}(x) T(x) d \nu(x)=E_{\theta} T(X)
\end{aligned}$$ 

and (omitting the integration $x$ variable to shorten the expressions) $$\begin{aligned}\ddot{d}(\theta) 
&=\frac{\int \exp \left[\theta T\right] T^2 h }{\int \exp \left[\theta T\right] h } -\frac{\left(\int \exp \left[\theta T\right] T h \right)^2}{\left(\int \exp \left[\theta T\right] h\right)^{2}} \\
&=\int \exp \left[\theta T-d(\theta)\right] T^2 h -\left(\int \exp \left[\theta T-d(\theta)\right] T h \right)^2\\
&=\int T^2 p_{\theta} -\left(\int p_{\theta} T \right)\left(\int p_{\theta} T \right) \\
&=E_{\theta} T^2(X) -\left(E_{\theta} T(X)\right)^2 \\
&=\operatorname{Cov}_{\theta}(T(X))
\end{aligned}$$

### Lemma 4.8 The mean and variance of statistics in exp fam (general case, proved using score func)
In the special case that $\left\{P_{\theta}: \theta \in \Theta\right\}$ is a one-dimensional exponential family, the densities are of the form $$p_{\theta}(x)=\exp [c(\theta) T(x)-d(\theta)] h(x)$$ Hence $$s_{\theta}(x)=\dot{c}(\theta) T(x)-\dot{d}(\theta)$$ The equality $E_{\theta} s_{\theta}(X)=0$ implies that $$E_{\theta} T(X)=\frac{\dot{d}(\theta)}{\dot{c}(\theta)},$$ One moreover has $$\dot{s}_{\theta}(x)=\ddot{c}(\theta) T(x)-\ddot{d}(\theta)$$ Hence, the inequality $\operatorname{var}_{\theta}\left(s_{\theta}(X)\right)=-E_{\theta} \dot{s}_{\theta}(X)$ implies $$\begin{aligned} \left[\dot{c}(\theta)\right]^{2} \operatorname{var}_{\theta}(T(X)) &=-\ddot{c}(\theta) E_{\theta} T(X)+\ddot{d}(\theta) \\
&=\ddot{d}(\theta)-\frac{\dot{d}(\theta)}{\dot{c}(\theta)} \ddot{c}(\theta)
\end{aligned}$$

:::warning
**Remark**
In addition, it follows that $$I(\theta)=\ddot{d}(\theta)-\frac{\dot{d}(\theta)}{\dot{c}(\theta)} \ddot{c}(\theta)$$ The Fisher information for estimating $\gamma=c(\theta)$ is $$I_{0}(\gamma)=\ddot{d}_{0}(\gamma)=\frac{I(\theta)}{[\dot{c}(\theta)]^{2}}$$
:::