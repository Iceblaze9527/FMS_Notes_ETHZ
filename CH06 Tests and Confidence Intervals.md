---
tags: FMS
---

# CH06 Tests and Confidence Intervals
## 6.1 Concepts
### 6.1.1 Non-randomized Tests
Let $\gamma_{0} \in \Gamma$ and $\alpha \in[0,1]$ be given. A (non-randomized) test at level $\alpha$ for the hypothesis $$H_{0}: \gamma=\gamma_{0}$$ is a statistic $$\phi\left(X, \gamma_{0}\right) \in\{0,1\}$$ such that $$P_{\theta}\left(\phi\left(X, \gamma_{0}\right)=1\right) \leq \alpha$$ for all $\theta \in\{\vartheta$ : $\left.g(\vartheta)=\gamma_{0}\right\}$. 

We often omit the dependence of $\phi$ on $\gamma_{0}$, i.e., we write $\phi(X):=\phi\left(X, \gamma_{0}\right)$.

:::warning
**Note** 
Typically a test $\phi$ is based on a test statistic $T$, i.e. it is of the form $$\phi(X)=\left\{ \begin{array}{ll}
1 & \text { if } T(X)>c \\
0 & \text { else }
\end{array}\right.$$ The constant $c$ is called the critical value.
:::

### 6.1.2 Pivot
To test $$H_{0}: \gamma=\gamma_{0}$$, we look for a pivot. This is a function $Z(\mathbf{X}, \gamma)$ depending on the data $\mathbf{X}$ and on the parameter $\gamma$, such that for all $\theta \in \Theta$, the distribution$$\mathbb{P}_{\theta}(Z(\mathbf{X}, g(\theta)) \leq \cdot)=: G(\cdot)$$ does not depend on $\theta$. 

#### Asymptotic pivot 
Let $Z_{n}\left(X_{1}, \ldots, X_{n}, \gamma\right)$ be some function of the data and the parameter of interest, defined for each sample size $n$. We call $Z_{n}\left(X_{1}, \ldots, X_{n}, \gamma\right)$ an asymptotic pivot if for all $\theta \in \Theta$, $$\lim _{n \rightarrow \infty} \mathbb{P}_{\theta}\left(Z_{n}\left(X_{1}, \ldots, X_{n}, \gamma\right) \leq \cdot\right)=G(\cdot),$$ at all continuity points of $G$, where the limit $G$ does not depend on $\theta$.

:::warning
**Note**
We note that to find a pivot is unfortunately not always possible. However, if we do have a pivot $Z(\mathbf{X}, \gamma)$ with distribution $G$, we can compute its quantile functions $$q_{L}:=q_{\text {sup }}^{G}\left(\frac{\alpha}{2}\right), q_{R}:=q_{\text {inf }}^{G}\left(1-\frac{\alpha}{2}\right)$$ and the test $$\phi\left(\mathbf{X}, \gamma_{0}\right):=\left\{\begin{array}{ll}1 & \text { if } Z\left(\mathbf{X}, \gamma_{0}\right) \notin\left[q_{L}, q_{R}\right] \\
0 & \text { else } \end{array} \right.$$
Then the test has level $\alpha$ for testing $H_{\gamma_{0}}$, with $\gamma_{0}=g\left(\theta_{0}\right)$ :$$\begin{gathered}
\left.\mathbb{P}_{\theta_{0}}\left(\phi\left(\mathbf{X}, g\left(\theta_{0}\right)\right)=1\right)=\mathbb{P}_{\theta_{0}}\left(Z\left(\mathbf{X}, g\left(\theta_{0}\right)\right)>q_{R}\right)+\mathbb{P}_{\theta_{0}}\left(Z(\mathbf{X}), g\left(\theta_{0}\right)\right)<q_{L}\right) \\
=1-G\left(q_{R}\right)+G\left(q_{L}-\right) \leq 1-\left(1-\frac{\alpha}{2}\right)+\frac{\alpha}{2}=\alpha .
\end{gathered}$$
:::


### 6.1.3 Confidence Sets and Confidence Interval
#### 6.1.3.1 Confidence Sets
A subset $I=I(\mathbf{X}) \subset \Gamma$, depending (only) on the data $\mathbf{X}=$ $\left(X_{1}, \ldots, X_{n}\right)$, is called a confidence set for $\gamma$, at level $1-\alpha$, if $$\mathbb{P}_{\theta}(\gamma \in I) \geq 1-\alpha, \forall \theta \in \Theta$$

#### 6.1.3.2 Confidence Interval
A confidence interval is of the form $$I:=[\underline{\gamma}, \overline{\gamma}], $$ where the boundaries $\underline{\gamma}=\underline{\gamma}(\mathbf{X})$ and $\overline{\gamma}=\overline{\gamma}(\mathbf{X})$ depend (only) on the data $\mathbf{X}$.

#### 6.1.3.3 Equivalence (duality) confidence sets and tests
**confidence sets <- tests**
Let for each $\gamma_{0} \in \mathbb{R}, \phi\left(\mathbf{X}, \gamma_{0}\right) \in\{0,1\}$ be a test at level $\alpha$ for the hypothesis $H_{\gamma_{0}}: \gamma=\gamma_{0}$Thus, we reject $H_{\gamma_{0}}$ if and only if $\phi\left(\mathbf{X}, \gamma_{0}\right)=1$, and$$
\mathbb{P}_{\theta: \gamma=\gamma_{0}}\left(\phi\left(\mathbf{X}, \gamma_{0}\right)=1\right) \leq \alpha $$ Then $$I(\mathbf{X}):=\{\gamma: \phi(\mathbf{X}, \gamma)=\mathbf{0}\}$$ is a $(1-\alpha)$-confidence set for $\gamma$.

**confidence sets -> tests**
Conversely, if $I(\mathbf{X})$ is a $(1-\alpha)$-confidence set for $\gamma$, then, for all $\gamma_{0}$, the test $\phi\left(\mathbf{X}, \gamma_{0}\right)$ defined as $$\phi\left(\mathbf{X}, \gamma_{0}\right)= \begin{cases}1 & \text { if } \gamma_{0} \notin I(\mathbf{X}) \\ 0 & \text { else }\end{cases}$$ is a test at level $\alpha$ of $H_{\gamma_{0}}$.

:::warning
**Remark**
When comparing confidence intervals, the aim is usually to take the one with smallest length on average (keeping the level at $1-\alpha$ ). In the case of tests, we look for the one with maximal power. 
:::

## 6.2 Examples
### Ex 6.2.1: Location Model
As example, consider again the location model (Section 1.3). Let $$\Theta:=\left\{\theta=\left(\mu, F_{0}\right), \mu \in \mathbb{R}, F_{0} \in \mathcal{F}_{0}\right\}$$ with $\mathcal{F}_{0}$ a subset of the collection of symmetric distributions (see (1.2)). Let $\hat{\mu}$ be an equivariant estimator, that is: the distribution of $\hat{\mu}-\mu$ does not depend on $\mu$ (see Chapter 9 for the formal definition of equivariance).

#### 6.2.1.1 $\mathcal{F}_{0}:=\left\{F_{0}\right\}$ is a single (known) distribution
We take $$Z(\mathbf{X}, \mu):=\hat{\mu}-\mu$$ as pivot. By the equivariance, this pivot has distribution $G$ depending only on $F_{0}$.

#### 6.2.1.2 $\mathcal{F}_{0}:=\left\{F_{0}(\cdot)=\Phi(\cdot / \sigma): \sigma>0\right\}$
We choose $\hat{\mu}:=\bar{X}_{n}$ where $\bar{X}_{n}=$ $\sum_{i=1}^{n} X_{i} / n$ is the sample mean. As pivot, we take $$ Z(\mathbf{X}, \mu):=\frac{\sqrt{n}\left(\bar{X}_{n}-\mu\right)}{S_{n}},$$ where $S_{n}^{2}=\sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2} /(n-1)$ is the sample variance. Then $G$ is the Student distribution with $n-1$ degrees of freedom.

#### 6.2.1.3 $\mathcal{F}_{0}:=\left\{F_{0}\right.$ symmetric and continuous at $\left.x=0\right\}$
We let the pivot be the sign test statistic:$$Z(\mathbf{X}, \mu):=\sum_{i=1}^{n} 1\left\{X_{i} \geq \mu\right\} $$Then $G$ is the $\operatorname{Binomial}(n, p)$ distribution, with parameter $p=1 / 2$.

#### 6.2.1.4 $\mathcal{F}_{0}:=\left\{F_{0}: \int x d F_{0}(x)=0, \int x^{2} d F_{0}(x)<\infty\right\}$

$$Z_{n}\left(X_{1}, \ldots, X_{n}, \mu\right):=\frac{\sqrt{n}\left(\bar{X}_{n}-\mu\right)}{S_{n}}
$$
is an asymptotic pivot, with limiting distribution $G=\Phi$.

### Ex 6.5.1: Student's Test
> **Two-sample problem:** We assume that the data are realizations of two independent samples, say $\mathbf{X}=\left(X_{1}, \ldots, X_{n}\right)$ and $\mathbf{Y}=\left(Y_{1}, \ldots, Y_{m}\right)$, where $X_{1}, \ldots, X_{n}$ are i.i.d. with distribution function $F_{X}$, and $Y_{1}, \ldots, Y_{m}$ are i.i.d. with distribution function $F_{Y}$. The distribution functions $F_{X}$ and $F_{Y}$ may be in whole or in part unknown. The testing problem is: $H_{0}: F_{X}=F_{Y}$ against a one- or two-sided alternative.

#### Assumption
- The data come from a normal distribution.
- The variance of $F_{X}$ and $F_{Y}$ are equal.
$$F_{X} \sim \mathcal{N}\left(\mu, \sigma^{2}\right) \\ F_{Y} \sim \mathcal{N}\left(\mu+\gamma, \sigma^{2}\right) \\ H_{0}: \gamma=0=: \gamma_{0}
$$

#### Pivot Construction 
The pooled sample variance $$S^{2}:=\frac{1}{m+n-2}\left\{\sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2}+\sum_{j=1}^{m}\left(Y_{j}-\bar{Y}\right)^{2}\right\}$$ Thus $$Z(\mathbf{X}, \mathbf{Y}, \gamma):=\sqrt{\frac{n m}{n+m}}\left(\frac{\bar{Y}-\bar{X}-\gamma}{S}\right) \sim T_{m+n-2}$$ 

#### Test Statistic
As test statistic for $H_{0}: \gamma=0$, we therefore take $$T:=Z(\mathbf{X}, \mathbf{Y}, 0)$$ The one-sided test at level $\alpha$, for $H_{0}: \gamma=0$ against $H_{1}: \gamma<0$, is $$\phi(\mathbf{X}, \mathbf{Y}):=\left\{\begin{array}{ll}
1 & \text { if } T<-t_{n+m-2}(1-\alpha) \\
0 & \text { if } T \geq-t_{n+m-2}(1-\alpha)
\end{array}\right.$$


### Ex 6.5.2 Wilcoxon Test
> **Two-sample problem:** We assume that the data are realizations of two independent samples, say $\mathbf{X}=\left(X_{1}, \ldots, X_{n}\right)$ and $\mathbf{Y}=\left(Y_{1}, \ldots, Y_{m}\right)$, where $X_{1}, \ldots, X_{n}$ are i.i.d. with distribution function $F_{X}$, and $Y_{1}, \ldots, Y_{m}$ are i.i.d. with distribution function $F_{Y}$. The distribution functions $F_{X}$ and $F_{Y}$ may be in whole or in part unknown. The testing problem is: $H_{0}: F_{X}=F_{Y}$ against a one- or two-sided alternative.

#### Assumption
- $F_{X}$ and $F_{Y}$ are continuous, but otherwise unknown. The model class for both $F_{X}$ and $F_{Y}$ is thus$$\mathcal{F}:=\{\text { all continuous distributions }\}$$ The continuity assumption ensures that all observations are distinct, that is, there are no ties. We can then put them in strictly increasing order.
- $F_{y}(\cdot)=F_{x}(\cdot-r) \quad H_{0}: \gamma=\gamma_{0}=0$

#### Pivot Construction
Let $N=n+m$ and $Z_{1}, \ldots, Z_{N}$ be the pooled sample $$Z_{i}:=X_{i}, i=1, \ldots, n, Z_{n+j}:=Y_{j}, j=1, \ldots, m$$ Define $$R_{i}:=\operatorname{rank}\left(Z_{i}\right), i=1, \ldots, N$$ and let$$Z_{(1)}<\cdots<Z_{(N)}$$ be the order statistics of the pooled sample (so that $\left.Z_{i}=Z_{\left(R_{i}\right)}(i=1, \ldots, n)\right)$.

#### Test Statistic
The Wilcoxon test statistic is $$T=T^{\text {Wilcoxon }}:=\sum_{i=1}^{n} R_{i} .$$ One may check that this  test statistic $T$ can alternatively be written as $$T=\#\left\{Y_{j}<X_{i}\right\}+\frac{n(n+1)}{2}$$ Under $H_{0}: F_{X}=F_{Y}$, the vector of ranks $\left(R_{1}, \ldots, R_{n}\right)$ has the same distribution as $n$ random draws without replacement from the numbers $\{1, \ldots, N\}$. 

The null-distribution of $T$ does not depend on $F_{X}$ or $F_{Y}$. It does however depend on the sample sizes $n$ and $m$.

#### Small Samples
- Under $H_{0}$, the joint sample are i.i.d., and let $N=m+n$, then the joint distribution of $R_{1}, \cdots, R_{n}$ is $$P\left(R_{1}=r_{1}, \cdots, R_{n}=r_{n}\right)= \begin{cases}\frac{1}{N(N-1) \cdots(N-n+1)}, & r_{1}, \cdots, r_{n} \leq N, \\ 0, & \text { otherwise }\end{cases}$$ where $r_{i}$ 's are natural numbers and not equal to each other.
- Under $H_{0}, E(T)=n(N+1) / 2$, and $T$ will take values around its mean.
- Rejection region at level of significance $\alpha$ is$$\begin{gathered}
D=\left\{\left(X_{1}, \cdots, X_{m} ; Y_{1}, \cdots, Y_{n}\right): T \leq c \text { or } T \geq d\right\} \\
\alpha=P\left(T \leq c \text { or } T \geq d \mid H_{0}\right)
\end{gathered}$$
- If $m, n$ are small, $c, d$ can be found in existing table.

#### Large Samples
- If $m, n$ are large enough - using CLT. Under $H_{0}$,$$T^{*}=\frac{T-n(N+1) / 2}{\sqrt{m n(N+1) / 12}} \frac{d}{m, n \rightarrow \infty} N(0,1)$$
- Rejection region with level of significance approximately $\alpha$ is $$D=\left\{\left(X_{1}, \cdots, X_{m} ; Y_{1}, \cdots, Y_{n}\right):\left|T^{*}\right|>z_{\alpha / 2}\right\}$$
- Approximately P-value: let $w^{*}$ be the observed value of $W^{*}$, $$p=P\left(|N(0,1)|>T^{*}\right)$$
- Similar arguments can be used to test $$\begin{array}{ll}
H_{0}: \theta \leq 0 \longleftrightarrow H_{1}: \theta>0 . & T^{*} \geq d_{1} \\
H_{0}: \theta \geq 0 \longleftrightarrow H_{1}: \theta<0 . & T^{*} \leq c_{1}
\end{array}$$

### 6.5.3 Comparison of Student's test and Wilcoxon's test
Because Wilcoxon's test is only based on the ranks, and does not rely on the assumption of normality, it lies at hand that, when the data are in fact normally distributed, Wilcoxon's test will have less power than Student's test. The loss of power is however small.

Asymptotic Relative Efficiency $\approx N^{\text {Student }} / N^{\text {Wilcoxon }}$, where $N^{\text {Student }}$ ( $N^{\text {Wilcoxon }}$ ) be the number of observations needed to reach power $\beta$ using Student's (Wilcoxon's) test.

One can show that $N^{\text {Student }} / N^{\text {Wilcoxon }}$ is approximately $.95$ when the normal model is correct. For a large class of distributions, the ratio $N^{\text {Student }} / N^{\text {Wilcoxon }}$ ranges from $.85$ to $\infty$, that is, when using Wilcoxon one generally has very limited loss of efficiency as compared to Student, and one may in fact have a substantial gain of efficiency.