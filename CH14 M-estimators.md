---
tags: FMS
---

# CH14 M-estimators
## 14.1 Concepts
### 14.1.1 M-estimators
- **Loss Function**: Let, for each $c \in \Gamma$, be defined some loss function $\rho_{c}(X)$. These are for instance constructed as in Chapter 10: we let $L(\theta, a)$ be the loss when taking action $a$. Then, we fix some decision $d(x)$, and rewrite $$L(\theta, d(x)):=\rho_{c}(x)$$
- **Theoretical Risk**: Assuming the loss $L$ depends only on $\theta$ via the parameter of interest $\gamma=g(\theta)$. We now require that the theoretical risk $$\mathcal{R}(c):=E_{\theta} \rho_{c}(X)$$ 
- **Theoretical Risk Minimizer**: The risk is minimized at the value $c=\gamma$ i.e., $$\gamma=\arg \min _{c \in \Gamma} E_{\theta} \rho_{c}(X)=\arg \min _{c \in \Gamma} \mathcal{R}(c)$$ Alternatively, given $\rho_{c}$, one may view the above equation as the definition of $\gamma$.
- **The Empirical Risk**: $$\hat{\mathcal{R}}_{n}(c):=\frac{1}{n} \sum_{i=1}^{n} \rho_{c}\left(X_{i}\right), c \in \Gamma$$
- **The Empirical Risk Minimizer / M-estimator**: $\hat{\gamma}_{n}$ of $\gamma$ is defined as $$\hat{\gamma}_{n}:=\arg \min _{c \in \Gamma} \frac{1}{n} \sum_{i=1}^{n} \rho_{c}\left(X_{i}\right)=\arg \min _{c \in \Gamma} \hat{\mathcal{R}}_{n}(c)$$ The "M" in "M-estimator" stands for Minimizer (or - take minus signs - Maximizer).

### 14.1.2 Z-estimators
- **The Derivative of the Loss Function**: If $c \mapsto \rho_{c}(x)$ is differentiable for all $x$, we write$$\psi_{c}(x):=\dot{\rho}_{c}(x):=\frac{\partial}{\partial c} \rho_{c}(x)$$ 
- **The Derivative of the Theoretical Risk**: Assuming we may interchange differentiation and taking expectations, we have $$\dot{\mathcal{R}}(c)=E_{\theta} \psi_{c}(X)$$
- **Zero Point of the Derivative**: This implies the theoretical risk minimizer satisfies $$\dot{\mathcal{R}}(\gamma)=0$$
- **The Derivative of the Empirical Risk:** If $\rho_{c}(x)$ is differentiable in $c$ for all $x$, then $$\dot{\hat{\mathcal{R}}}_{n}(c)=\frac{\partial}{\partial c} \frac{1}{n} \sum_{i=1}^{n} \rho_{c}\left(X_{i}\right)=\frac{1}{n} \sum_{i=1}^{n} \psi_{c}\left(X_{i}\right)$$ 
- **The Z-estimator:** The Z-estimator $\hat{\gamma}_{n}$ of $\gamma$ (assumed to exist) is defined as a solution of the equations $$\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0$$ The "Z" in "Z-estimator" stands for Zero.

### 14.1.3 Asymptotic Relative Efficiency
Definition 14.6.1 Let $T_{n, 1}$ and $T_{n, 2}$ be two estimators of $\gamma$, that satisfy $$\sqrt{n}\left(T_{n, j}-\gamma\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, V_{\theta, j}\right), j=1,2$$ Then $$\mathrm{e}_{2: 1}:=\frac{V_{\theta, 1}}{V_{\theta, 2}}$$ is called the asymptotic relative efficiency of $T_{n, 2}$ with respect to $T_{n, 1}$. 

If $e_{2: 1}>1$, the estimator $T_{n, 2}$ is asymptotically more efficient than $T_{n, 1}$. An asymptotic $(1-\alpha)$-confidence interval for $\gamma$ based on $T_{n, 2}$ is then narrower than the one based on $T_{n, 1}$

:::warning
The $(1-\alpha)$-confidence interval of $T_{n, 1}$ is $$\hat{\gamma}_{n_{1}} \pm \sqrt{\frac{V_{\theta, 1}}{n_{1}} \Phi^{-1}\left(1-\frac{\alpha}{2}\right)}$$ given a known $V_{\theta, 1}$. Thus, $T_{n, 2}$ achieves the same length of $(1-\alpha)$-confidence interval by using less samples. Efficiency is the reciprocal ratio of the two sample sizes. Thus is independent of the level of CI
:::

## 14.2 Lemmas & Theorems (for consistency and asymptotic normality & linearity)
> **Inspiration**: By the law of large numbers, averages converge to expectations. So the M-estimator (Z-estimator) does make sense. However, consistency and further properties are not immediate, because we actually need convergence the averages to expectations over a range of values $c \in \Gamma$ simultaneously. This is the topic of **empirical process theory**.
> 
> **Notations:** Suppose $$\hat{P}_{n}(A)=\frac{1}{n} \sum_{i=1}^{n} 1_{A}\left(x_{i}\right) \quad A \subset \mathscr{X}$$ Let $f: x \rightarrow \mathbb{R}$, define $$\hat{P}_{n} f:=\frac{1}{n} \sum_{i=1}^{n} f\left(x_{i}\right) \\ P f:=E f(x) \\ \hat{P}_{n} f-P f:=\left(\hat{P}_{n}-P\right) f$$

### 14.2.0 Summary
#### 0.1 Intuitive Interpretation of the lemmas and the theorems
:::warning
**Lemma 14.2.1: Sufficient conditions for the uniform in $c$ convergence of $\hat{\mathcal{R}}_{n}(c)$ to $\mathcal{R}(c)$**
- Param space: $\Gamma$ is compact
- Loss Function: $c \mapsto \rho_{c}(x)$ is continuous in $c$ for all $x$
- $E_{\theta}\left(\sup _{c \in \Gamma}\left|\rho_{c}(x)\right|\right)<\infty$: ![](https://i.imgur.com/QZN7Fqm.png =200x)
:::

:::warning
**Theorem 14.2.1: Uniform Convergence Leads to Consistency**

If the empirical risk uniformly (in proba) converges to theoretical risk,
then the emipirical risk minimizer (M-estimator) is consistent, i.e. its theoretical risk asymptotically in proba converges to the minimal theoretical risk.
::: 

:::warning
**Theorem 14.2.2: Easier proof of 14.2.1 for the one-dimensional case using Z-estimator**
- Param space: $\Gamma \subset \mathbb{R}$ (no need to be compact!)
- Deriv of loss function: $\psi_{c}(x)$ is continuous in $c$ for all $x$
- $E_{\theta}\left|\psi_{c}\right|<\infty, \forall c$
- $\exists \delta>0$ such that ![](https://i.imgur.com/D3YGEhs.png =300x)
Then for n large enough, $\mathbb{P}_{\theta}$ (forcing stronger convexity), there is a solution $\hat{\gamma}_{n}$ of $\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0$, and this solution $\hat{\gamma}_{n}$ is consistent.
:::

:::warning
**Theorem 14.3.1: Asymptotic Normality and Linearity of Z-estimators**

- $\hat{\gamma}_{n}$ be the Z-estimator of $\gamma$. 
- $\hat{\gamma}_{n}$ is a consistent estimator of $\gamma$
- The empirical process $\nu_{n}(c):=\sqrt{n}\left(\hat{P}_{n}-P_{\theta}\right) \psi_{c}=\sqrt{n}\left(\dot{\hat{\mathcal{R}}}_{n}(c)-\dot{\mathcal{R}}(c)\right), c \in \Gamma$ is asymptotically continuous at $\gamma$: for all (possibly random) sequences $\left\{\gamma_{n}\right\}$ in $\Gamma$, with $\left\|\gamma_{n}-\gamma\right\|=o_{\mathbf{P}_{\theta}}(1)$, we have $\left|\nu_{n}\left(\gamma_{n}\right)-\nu_{n}(\gamma)\right|=o_{\mathbf{P}_{\theta}}(1)$
- Assume $p \times p$ Hessian matrix $M_{\theta}:=\left.\frac{\partial}{\partial c^{T}} \dot{\mathcal{R}}(c)\right|_{c=\gamma}$, and $M_{\theta}^{-1}$ exists (which amounts to assuming that $\gamma$, as a solution to $\dot{\mathcal{R}}(\gamma)=0$, is well-identified.)
- $J_{\theta}:=P_{\theta} \psi_{\gamma} \psi_{\gamma}^{T}$ exists

Then $\hat{\gamma}_{n}$ is asymptotically linear, with influence function $$l_{\theta}=-M_{\theta}^{-1} \psi_{\gamma}$$ thus aysmp normal $$\sqrt{n}\left(\hat{\gamma}_{n}-\gamma\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, V_{\theta}\right),$$ with $$V_{\theta}=M_{\theta}^{-1} J_{\theta} M_{\theta}^{-1}$$
:::

#### 0.2 Proof Strategy
:::warning
**Lemma 14.2.1: Sufficient conditions for the uniform in $c$ convergence of $\hat{\mathcal{R}}_{n}(c)$ to $\mathcal{R}(c)$**

finite $\varepsilon-$ bracketing sets

:::

:::warning
**Theorem 14.2.1: Uniform Convergence Leads to Consistency**
Insertion method. Use the fact that the theoretical minimizer is the global minimum of the theoretical risk, and the same goes for the empirical counterpart. The difference is bounded by what the uniform convergence suggests (twice the sup)
:::

:::warning
**Theorem 14.2.2: Easier proof of 14.2.1 for the one-dimensional case using Z-estimator**

The (strong) law of large numbers
The continuous mapping theorem
:::

:::warning
**Theorem 14.3.1: Asymptotic Normality and Linearity of Z-estimators**
Insertion method. Use the fact that $\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0, \dot{\mathcal{R}}(\gamma)=0$ and insert $\dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right)$

$$\begin{aligned}
0 &=\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right) \\
&=\nu_{n}\left(\hat{\gamma}_{n}\right) / \sqrt{n}+\dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right)-\dot{\mathcal{R}}(\gamma) \\
&=:(i)+(ii)\end{aligned}$$ for (i) we use the asymptotic continuity; $$(i) =\dot{\hat{\mathcal{R}}}_{n}(\gamma)+o_{\mathbf{P}_{\theta}}(1 / \sqrt{n})$$ for (ii) we use the differentiability (first-order Taylor Expansion)
$$(ii) =M_{\theta}\left(\hat{\gamma}_{n}-\gamma\right)+o\left(\left\|\gamma_{n}-\gamma\right\|\right)
$$ By the CLT, $\dot{\hat{\mathcal{R}}}_{n}(\gamma)=\mathcal{O}_{\mathbf{P}_{\theta}}(1 / \sqrt{n})$, thus $\left\|\hat{\gamma}_{n}-\gamma\right\|=\mathcal{O}_{\mathbf{P}_{\theta}}(1 / \sqrt{n})$ Hence$$0=\dot{\hat{\mathcal{R}}}_{n}(\gamma)+M_{\theta}\left(\hat{\gamma}_{n}-\gamma\right)+o_{\mathbf{P}_{\theta}}(1 / \sqrt{n})
$$
:::


### Theorem 14.2.1: Uniform Convergence Leads to Consistency
Suppose the uniform convergence$$\sup _{c \in \Gamma}\left|\hat{\mathcal{R}}_{n}(c)-\mathcal{R}(c)\right| \stackrel{\mathbb{P}_{\theta}}{\rightarrow} 0$$ Then $$\mathcal{R}\left(\hat{\gamma}_{n}\right) \stackrel{\mathbb{P}_{\theta}}{\rightarrow} \mathcal{R}(\gamma)$$ i.e. M-estimators are consistent.

#### Proof 
$$\begin{aligned}
0 & \leqslant R\left(\hat{\gamma}_{n}\right)-R(\gamma)\\
  & = -\left[\hat{R}_{n}\left(\hat{\gamma}_{n}\right)-R\left(\hat{\gamma}_{n}\right)\right]+\left[\hat{R}_{n}(\gamma)-R(\gamma)\right]+ \underbrace{\hat{R}_{n}\left(\hat{\gamma}_{n}\right)-\hat{R}_{n}(\gamma)}_{\leqslant 0} \\
  & \leqslant 2 \sup _{c}\left|\hat{R}_{n}(c)-R(c)\right| \stackrel{\mathbb{P}}{\rightarrow} 0
\end{aligned}
$$

### Lemma 14.2.1: Sufficient conditions for the uniform in $c$ convergence of $\hat{\mathcal{R}}_{n}(c)$ to $\mathcal{R}(c)$
> **Well-Separatedness:** We will need that convergence of to the minimum value also implies convergence of the arg min, i.e., convergence of the location of the minimum. To this end, we present the following definition. 
$\gamma$ of $\mathcal{R}(c)$ is called well-separated if for all $\epsilon>0$, $$\inf \{\mathcal{R}(c): c \in \Gamma,\|c-\gamma\|>\epsilon\}>\mathcal{R}(\gamma)$$ If $\gamma$ is well-separated, $\mathcal{R}\left(\hat{\gamma}_{n}\right) \stackrel{\mathbb{P}_{\theta}}{\rightarrow} \mathcal{R}(\gamma)$ implies $\hat{\gamma}_{n} \stackrel{\mathbb{P}_{\theta}}{\rightarrow} \gamma$. 
An example of $\gamma$ not being well-separated: ![gamma-not-well-sep](https://i.imgur.com/E6MYH06.png =300x)
**Regularity**: For consistency the assumption of a compact parameter space $\Gamma$ can often be omitted if $c \mapsto \rho_{c}$ is convex.

Suppose that $\Gamma$ is compact, that $c \mapsto \rho_{c}(x)$ is continuous for all $x$, and that$$E_{\theta}\left(\sup _{c \in \Gamma}\left|\rho_{c}(x)\right|\right)<\infty$$ Then we have the uniform convergence $$\sup _{c \in \Gamma}\left|\hat{\mathcal{R}}_{n}(c)-\mathcal{R}(c)\right| \stackrel{\mathbb{P}_{\theta}}{\rightarrow} 0$$

#### A bare-handed, classical, yet elegant proof featuring combinatorial arguments
- **Bracketing Sets**: If $\Gamma$ is finite, the uniform convergence natually holds; for infinite $\Gamma$, we use a set of 'bracketing' sets to approximate since it is compact. We will show that $\forall \varepsilon>0$, $\exists$ a finite "bracketing set" $\left\{\left[f_{j}^{L}, f_{j}^{U}\right]\right\}_{j=1}^{N}$ where $f_{j}^{L}, f_{j}^{U}: x \rightarrow \mathbb{R}$, such that $$\begin{aligned} & f_{j}^{U} \geqslant f_{j}^{L} \\ & P\left(f_{j}^{U}-f_{j}^{L}\right) \leqslant \varepsilon\end{aligned}$$ and $\forall c \in \Gamma, \exists j \in\{1 \dots N\}$ such that $$f_{j}^{L} \leqslant \rho_{c} \leqslant f_{j}^{U}$$ Then $$\begin{aligned}\left(\hat{P}_{n}-P\right) \rho_{c} & \leqslant \hat{P}_{n} f_{j}^{U}-P f_{j}^{U}+\underbrace{P\left(f_{j}^{U}-\rho_{c}\right)}_{\leqslant \varepsilon} \\
& \geqslant \hat{P}_{n} f_{j}^{L}-P f_{j}^{L}+\underbrace{P\left(f_{j}^{L}-\rho_{c}\right)}_{\geqslant-\varepsilon} \\ \Rightarrow \sup _{c}\left|\left(\hat{P}_{n}-P\right)\rho_{c}\right| & \leqslant \underbrace{\max _{1 \leqslant j \leqslant N} \max \left\{\left|\left(\hat{P}_{n}-P\right) f_{j}^{L}\right|,\left|\left(\hat{P}_{n}-P\right) f_{j}^{U}\right|\right\}}_{\stackrel{\mathbb{P}}{\rightarrow} 0 \quad \text{since it is finite number}} + \varepsilon\end{aligned}$$ Intuitive Illustration: ![](https://i.imgur.com/W3flbHM.png =300x)
- **Construction of finite $\varepsilon$ - bracketing sets**: Let $\delta>0$ and $w(\cdot, \delta, c)=\underset{\tilde{c} \in \Gamma:\|\tilde{c}-c\| < \delta}{\sup }\left|\rho_{c}-\rho_{\tilde{c}}\right|$ $$\overset{(ii)}{\Rightarrow} \lim\limits_{\delta \downarrow 0} w(x,\delta,c)=0 \quad \forall x, \forall c \overset{(iii)}{\Rightarrow} \lim\limits_{\delta \downarrow 0} P_{w}(\cdot, \delta, c)=0 \quad \forall c$$ $\Rightarrow \forall \varepsilon>0 , \exists \delta_{c},$ such that $$P_{w}\left(\cdot, \delta_{c}, c\right)\leqslant \frac{\varepsilon}{2}$$ Let
$$B_{c}:=\left\{\tilde{c} \in \Gamma:\|\tilde{c}-c\|<\delta_{c}\right\}$$ Then $\left\{B_{c}: c \in \Gamma\right\}$ is a covering of $\Gamma$ by open sets. Since $\Gamma$ is compact, there exists finite sub-covering $$B_{c_{1}} \ldots B_{c_{N}}$$ Let $c \subset \Gamma$ arbitrary, then $\exists$ $j: c \in B_{c_{j}}:$ $$\begin{aligned}\rho_{c} & \leqslant \rho_{c_{j}}+w\left(\cdot, \delta_{c_{j}}, c_{j}\right):=f_{j}^{U} \\& \geqslant \rho_{c_{j}}-w\left(\cdot, \delta_{c_{j}}, c_{j}\right):=f_{j}^{L}\end{aligned}$$ Thus $$
P\left(f_{j}^{U}-f_{j}^{L}\right)=2 P w\left(\cdot, \delta_{cj}, c_{j}\right) \leqslant \varepsilon
$$

### Theorem 14.2.2 Easier proof for the one-dimensional case using Z-estimator
> **Inspiration**: The above theorem directly uses the definition of the M-estimator, and does not rely on having an explicit expression available. There are situations where an explicit expression is indeed not possible. This problem can be circumvented by using the result below for Z-estimators. To prove consistency of a Z-estimator of a one-dimensional parameter is relatively easy.

Suppose that $\Gamma \subset \mathbb{R}$ and that $\psi_{c}(x)$ is continuous in $c$ for all $x$. Assume moreover that $$E_{\theta}\left|\psi_{c}\right|<\infty, \forall c,$$ and that $\exists \delta>0$ such that $$
\begin{aligned}
&\dot{R}(c)>0 \quad c \in(\gamma, \gamma+\delta) \\
&\dot{R}(c)<0 \quad c \in(\gamma-\delta, \gamma) \\
&\dot{R}(\gamma)=0
\end{aligned}$$ Then $$\mathbb{P}\left(\exists \hat{\gamma}_{n}: \dot{\hat{R}_{n}}\left(\hat{\gamma}_{n}\right)=0\right) \xrightarrow[]{n\rightarrow\infty} 1$$ and $$\left\|\hat{\gamma}_{n}-\gamma\right\|=\mathcal{o}_{\mathbb{P}}(1)$$ i.e. $\hat{\gamma}_{n}$ is consistent.

#### Proof
Let $0<\epsilon<\delta$ be arbitrary. By the (strong) law of large numbers, $\mathbb{P}_{\theta}$-a.s. for $n$ sufficiently large, $$\dot{\hat{\mathcal{R}}}_{n}(\gamma+\epsilon)>0, \dot{\hat{\mathcal{R}}}_{n}(\gamma-\epsilon)<0$$ The continuity of $c \mapsto \psi_{c}$ implies that then $\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0$ for some $\left|\gamma_{n}-\gamma\right|<\epsilon$.

### Theorem 14.3.1 Asymptotic Normality and Linearity of Z-estimators
Denote now $$\nu_{n}(c):=\sqrt{n}\left(\hat{P}_{n}-P_{\theta}\right) \psi_{c}=\sqrt{n}\left(\dot{\hat{\mathcal{R}}}_{n}(c)-\dot{\mathcal{R}}(c)\right), c \in \Gamma$$ The stochastic process $$\left\{\nu_{n}(c): c \in \Gamma\right\}$$ is called the empirical process indexed by c. The empirical process is called asymptotically continuous at $\gamma$ if for all (possibly random) sequences $\left\{\gamma_{n}\right\}$ in $\Gamma$, with $\left\|\gamma_{n}-\gamma\right\|=o_{\mathbf{P}_{\theta}}(1)$, we have $$\left|\nu_{n}\left(\gamma_{n}\right)-\nu_{n}(\gamma)\right|=o_{\mathbf{P}_{\theta}}(1)$$ Also, we assume that $$M_{\theta}:=\left.\frac{\partial}{\partial c^{T}} \dot{\mathcal{R}}(c)\right|_{c=\gamma}$$ exists. It is a $p \times p$ matrix. We require it to be of full rank, which amounts to assuming that $\gamma$, as a solution to $\dot{\mathcal{R}}(\gamma)=0$, is well-identified. 

Let $\hat{\gamma}_{n}$ be the Z-estimator of $\gamma$. Suppose that $\hat{\gamma}_{n}$ is a consistent estimator of $\gamma$, and that $\nu_{n}$ is asymptotically continuous at $\gamma$. Suppose moreover $M_{\theta}^{-1}$ exists, and also $$J_{\theta}:=P_{\theta} \psi_{\gamma} \psi_{\gamma}^{T}$$ Then $\hat{\gamma}_{n}$ is asymptotically linear, with influence function $$l_{\theta}=-M_{\theta}^{-1} \psi_{\gamma}$$

#### Corollary 14.3.1 
Under the conditions of Theorem 14.3.1$$\sqrt{n}\left(\hat{\gamma}_{n}-\gamma\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, V_{\theta}\right),$$ with $$V_{\theta}=M_{\theta}^{-1} J_{\theta} M_{\theta}^{-1}$$ which is usually called "sandwich formula"

#### Proof Sketch
By definition, $$\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right)=0, \dot{\mathcal{R}}(\gamma)=0$$
So we have $$\begin{aligned}
0 &=\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right) \\
&=\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right) - \dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right) + \dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right)\\
&=\dot{\hat{\mathcal{R}}}_{n}\left(\hat{\gamma}_{n}\right) - \dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right) + \dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right) -\dot{\mathcal{R}}(\gamma) \\
&=\nu_{n}\left(\hat{\gamma}_{n}\right) / \sqrt{n}+\dot{\mathcal{R}}\left(\hat{\gamma}_{n}\right)-\dot{\mathcal{R}}(\gamma) \\
&=:(i)+(ii)\end{aligned}$$ for (i) we use the asymptotic continuity; 
for (ii) we use the differentiability (first-order Taylor Expansion)
By the CLT, $\dot{\hat{\mathcal{R}}}_{n}(\gamma)=\mathcal{O}_{\mathbf{P}_{\theta}}(1 / \sqrt{n})$, thus $\left\|\hat{\gamma}_{n}-\gamma\right\|=\mathcal{O}_{\mathbf{P}_{\theta}}(1 / \sqrt{n})$ i.e. $$0=\dot{\hat{\mathcal{R}}}_{n}(\gamma)+M_{\theta}\left(\hat{\gamma}_{n}-\gamma\right)+o_{\mathbf{P}_{\theta}}(1 / \sqrt{n})$$ Thus $$
\left(\hat{\gamma}_{n}-\gamma\right)=-\hat{P}_{n} M^{-1} \psi_{\gamma}+o_{\mathbf{P}_{\theta}}(1 / \sqrt{n})$$

### Lemma 14.8.1 Log-likelihood ratio is an an asymptotic pivot
Suppose that $\mathcal{P}=\left\{P_{\theta}: \theta \in \Theta\right\}$ has $\Theta \subset \mathbb{R}^{p}$, and that $\mathcal{P}$ is dominated by some $\sigma$-finite measure $\nu$. Let $p_{\theta}:=d P_{\theta} / d \nu$ denote the densities, and let $$\hat{\theta}_{n}:=\arg \max _{\vartheta \in \Theta} \sum_{i=1}^{n} \log p_{\vartheta}\left(X_{i}\right)$$ be the MLE. Assume enough regularity such as existence of derivatives and interchanging integration and differentiation. Define now the twice log-likelihood ratio $$2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta):=2 \sum_{i=1}^{n}\left[\log p_{\hat{\theta}_{n}}\left(X_{i}\right)-\log p_{\theta}\left(X_{i}\right)\right]$$ Under regularity conditions, $2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta)$ is an asymptotic pivot for $\theta$. Its asymptotic distribution is again the $\chi^{2}$-distribution with $p$ degrees of freedom: $$2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \chi_{p}^{2}, \quad \forall \theta $$ 

#### Corollary
For the simple hypothesis $H_{0}: \theta=\theta_{0}$, we can use $2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}\left(\theta_{0}\right)$ as test statistic: reject $H_{0}$ if$$
2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}\left(\theta_{0}\right)>G_{p}^{-1}(1-\alpha),$$ where $G_{p}$ is the distribution function of the $\chi_{p}^{2}$-distribution. This test has approximately level $\alpha$ as was shown in Lemma 14.8.1.

:::warning
**Remark**
A practical advantage of log-likelihood ratio is that it is self-normalizing: one does not need to explicitly estimate asymptotic (co-)variances. (compared to the results of Section 14.7 where we need to obtain the inversion of fisher information as the asymptotic covariance)
:::

### Lemma 14.10.1 Likelihood ratio tests
Consider now the hypothesis $H_{0}: R(\theta)=0$, where $$R(\theta)=\left(\begin{array}{c}R_{1}(\theta) \\ \vdots \\ R_{q}(\theta)\end{array}\right)$$ are $q$ restrictions on $\theta$ (with $R: \mathbb{R}^{p} \rightarrow \mathbb{R}^{q}$ a given function). (or the dim of null hypothesis space is $p-q$ ). Let $\hat{\theta}_{n}$ be the unrestricted MLE, that is$$\hat{\theta}_{n}=\arg \max _{\vartheta \in \Theta} \sum_{i=1}^{n} \log p_{\vartheta}\left(X_{i}\right)$$ Moreover, let $\hat{\theta}_{n}^{0}$ be the restricted MLE, defined as $$\hat{\theta}_{n}^{0}=\arg \max _{\vartheta \in \Theta: R(\vartheta)=0} \sum_{i=1}^{n} \log p_{\vartheta}\left(X_{i}\right)$$ Let$$\mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-\mathcal{L}_{n}\left(\hat{\theta}_{n}^{0}\right)=\sum_{i=1}^{n}\left[\log p_{\hat{\theta}_{n}}\left(X_{i}\right)-\log p_{\hat{\theta}_{n}^{0}}\left(X_{i}\right)\right]$$ be the log-likelihood ratio for testing $H_{0}: R(\theta)=0$.

Under regularity conditions, and if $H_{0}: R(\theta)=0$ holds, we have$$2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}\left(\hat{\theta}_{n}^{0}\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \chi_{q}^{2}$$

## 14.3 Examples
### Ex 14.0: M-estimators: Discussion of Least Absolute Deviation
:::warning
**Remark**: Sometimes the loss function mey not be differentiable, but the risks are still differentiable (since you take the integral)
:::

### Ex 14.1 MLE as special case of M-estimation
With $\rho_{\tilde{\theta}}(x)=-\log p_{\tilde{\theta}}(x)$ the M-estimator is the maximum likelihood estimator
$$
\begin{aligned}
\hat{\theta} &=\arg \min _{\tilde{\theta} \in \Theta} \mathcal{L}_{\mathbf{X}}(\tilde{\theta}) \\
&=\arg \min _{\tilde{\theta} \in \Theta} \frac{1}{n} \sum_{i=1}^{n}\left(-\log p_{\tilde{\theta}}\left(X_{i}\right)\right) .
\end{aligned}
$$

### Ex 14.4 Asymptotic normality of the MLE
In this section, we show that, under regularity conditions, the MLE is asymptotically normal with asymptotic covariance matrix the inverse of the Fisher information matrix $I(\theta)$. $$\sqrt{n}\left(\hat{\theta}_{n}-\theta\right) \stackrel{\mathcal{D}_{\theta}}{\longrightarrow} \mathcal{N}\left(0, I^{-1}(\theta)\right)$$

### Ex 14.6.1: Asymptotic Relative Efficiency of Sample Mean and Sample Median
Let $\mathcal{X}=\mathbb{R}$, and $F$ be the distribution function of $X$. Suppose that $F$ is symmetric around the parameter of interest $\mu$. In other words, $$F(\cdot)=F_{0}(\cdot-\mu),$$ where $F_{0}$ is symmetric around zero. We assume that $F_{0}$ has finite variance $\sigma^{2}$, and that is has density $f_{0}$ w.r.t. Lebesgue measure, with $f_{0}(0)>0$. Take $T_{n, 1}:=\bar{X}_{n}$, the sample mean, and $T_{n, 2}:=\hat{F}_{n}^{-1}(1 / 2)$, the sample median. Then $V_{\theta, 1}=\sigma^{2}$ and $V_{\theta, 2}=1 /\left(4 f_{0}^{2}(0)\right)$ (the latter being derived from the conclusion of the ==Huber Loss Estimator==). So $$\mathrm{e}_{2:1}=4 \sigma^{2} f_{0}^{2}(0)$$ Whether the sample mean is the winner, or rather the sample median, depends thus on the distribution $F_{0}$.

### Ex 14.9 MLE for the multinomial distribution
Let $X_{1}, \ldots, X_{n}$ be i.i.d. copies of $X$, where $X \in\{1, \ldots, k\}$ is a label, with $$P_{\theta}(X=j):=\pi_{j}, j=1, \ldots, k$$ where the probabilities $\pi_{j}$ are positive and add up to one: $\sum_{j=1}^{k} \pi_{j}=1$, but are assumed to be otherwise unknown. Then there are $p:=k-1$ unknown parameters, say $\theta=\left(\pi_{1}, \ldots, \pi_{k-1}\right)$. Define $N_{j}:=\#\left\{i: X_{i}=j\right\}$. Note that $\left(N_{1}, \ldots, N_{k}\right)$ has a multinomial distribution with parameters $n$ and $\left(\pi_{1}, \ldots, \pi_{k}\right)$.

#### Lemma 14.9.1 
For each $j=1, \ldots, k$, the MLE of $\pi_{j}$ is $$\hat{\pi}_{j}=\frac{N_{j}}{n}$$

:::warning
**Proof Sketch**
The log-densities can be written as$$\log p_{\theta}(x)=\sum_{j=1}^{k} 1\{x=j\} \log \pi_{j},$$ so that $$\sum_{i=1}^{n} \log p_{\theta}\left(X_{i}\right)=\sum_{j=1}^{k} N_{j} \log \pi_{j}$$ Putting the derivatives with respect to $\theta=\left(\pi_{1}, \ldots, \pi_{k-1}\right)$, (with $\pi_{k}=1-$ $\sum_{j=1}^{k-1} \theta_{j}$ ) to zero gives, $$\frac{N_{j}}{\hat{\pi}_{j}}-\frac{N_{k}}{\hat{\pi}_{k}}=0$$
:::

#### Lemma 14.9.2 
The Fisher information is $$I(\theta)=\left(\begin{array}{ccc}
\frac{1}{\pi_{1}} & \cdots & 0 \\\vdots & \ddots & \vdots \\0 & \cdots & \frac{1}{\pi_{k-1}}\end{array}\right)+\frac{1}{\pi_{k}} \iota \iota^{T}$$ where $\iota$ is the $(k-1)$-vector $\iota:=(1, \ldots, 1)^{T}$.

#### Conclusion
$$Z_{n, 1}(\theta)=n\left(\hat{\theta}_{n}-\theta\right)^{T} I(\theta)\left(\hat{\theta}_{n}-\theta\right) = \sum_{j=1}^{k} \frac{\left(N_{j}-n \pi_{j}\right)^{2}}{n \pi_{j}}$$ This is called the Pearson's chi-square $$\sum \frac{(\text { observed }-\text { expected })^{2}}{\text { expected }}
$$ $$Z_{n, 2}(\gamma):=n\left(\hat{\theta}_{n}-\theta\right)^{T} \hat{I_n}(\theta)\left(\hat{\theta}_{n}-\theta\right) = \sum_{j=1}^{k} \frac{\left(N_{j}-n \pi_{j}\right)^{2}}{N_{j}}$$ This is called the Pearson's chi-square$$\sum \frac{(\text { observed }-\text { expected })^{2}}{\text { observed }}$$ Finally, the log-likelihood ratio pivot is
$$2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta)=2 \sum_{j=1}^{k} N_{j} \log \left(\frac{\hat{\pi}_{j}}{\pi_{j}}\right) .
$$ 
The approximation $\log (1+x) \approx x-x^{2} / 2$ shows that $2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta) \approx Z_{n, 2}(\theta)$. 

The three asymptotic pivots $Z_{n, 1}(\theta), Z_{n, 2}(\theta)$ and $2 \mathcal{L}_{n}\left(\hat{\theta}_{n}\right)-2 \mathcal{L}_{n}(\theta)$ are each asymptotically $\chi_{k-1}^{2}$-distributed under $\mathbb{P}_{\theta}$.


