---
tags: FMS
---

# CH07 The Neyman Pearson Lemma and UMP tests
## 7.1 Concepts
### 7.1.1 Randomized Tests
Let $\mathcal{P}:=\left\{P_{\theta}: \theta \in \Theta\right\}$ be a family of probability measures. Let $\Theta_{0} \subset \Theta$, $\Theta_{1} \subset \Theta$, and $\Theta_{0} \cap \Theta_{1}=\emptyset$. Based on observations $X \in \mathcal{X}$, with distribution $P \in \mathcal{P}$, we consider the general testing problem for $H_{0}: \theta \in \Theta_{0}$, against $H_{1}: \theta \in \Theta_{1}$.

A possibly randomized test is some function $\phi: \mathcal{X} \rightarrow[0,1]$. Fix some $\alpha \in$ $[0,1]$. We say that $\phi$ is a test at level $\alpha$ if $$\sup _{\theta \in \Theta_{0}} E_{\theta} \phi(X) \leq \alpha$$

### 7.1.2 The Power of Test
The power function of the test employed is defined by: $$\beta(\theta):=P_{\theta}\left( \text{of rejecting } H_{0} \text{ by the test } \varphi \right)=E_{\theta}[\phi(T)]$$

#### Risk
We consider testing $H_{0}: \theta=\theta_{0}$ against the alternative $H_{1}: \theta=\theta_{1}$.

Define the risk $R(\theta, \phi)$ of a test $\phi$ as the probability of error of first and second kind: $$R(\theta, \phi):=\left\{\begin{array}{lll}
E_{\theta} \phi(X) &= \text{type I error}, & \theta=\theta_{0} \\
1-E_{\theta} \phi(X) &= \text{type II error}, & \theta=\theta_{1}
\end{array}\right.$$

### 7.1.3 Neyman Pearson Test
We consider testing $H_{0}: \theta=\theta_{0}$ against the alternative $H_{1}: \theta=\theta_{1}$.

We let $p_{0}\left(p_{1}\right)$ be the density of $P_{\theta_{0}}\left(P_{\theta_{1}}\right)$ with respect to some dominating measure $\nu$ (for example $\nu=P_{\theta_{0}}+P_{\theta_{1}}$ ). A Neyman Pearson test is $$\phi_{\mathrm{NP}}:=\left\{\begin{array}{ll}
1 & \text { if } p_{1} / p_{0}>c \\
q & \text { if } p_{1} / p_{0}=c \\
0 & \text { if } p_{1} / p_{0}<c
\end{array}\right.$$ Here $0 \leq q \leq 1$, and $0 \leq c<\infty$ are given constants.

### 7.1.4 UMP Test
A test $\phi$ is called Uniformly Most Powerful (UMP) if
- $\phi$ has level $\alpha$,
- for all tests $\phi^{\prime}$ with level $\alpha$, it holds that $E_{\theta} \phi^{\prime}(X) \leq E_{\theta} \phi(X) \quad \forall \theta \in \Theta_{1}$.

:::warning
**Remark**
UMP Test is the best test among all tests with level of significance $\leq \alpha$:
- Its level of significance is $\alpha$
- It has the smallest type II error for all $\theta \in \Theta_{1}$
:::

### 7.1.5 UMPU Test
> **Inspiration:** Uniformly most powerful tests do not always exist. We therefore restrict attention to a smaller class of tests, and look for uniformly most powerful tests in the smaller class.

#### 7.1.5.1 Unbiased Test
A test $\phi$ is called unbiased if $$E_{\theta_1} \phi(X) \geqslant\operatorname{level}(\phi) \quad \forall \theta_{1} \in \Theta_{1}$$

#### 7.1.5.2 UMPU Test
A test $\phi$ is called Uniformly Most Powerful Unbiased (UMPU) if
- $\phi$ has level $\alpha$,
- $\phi$ is unbiased,
- for all unbiased tests $\phi^{\prime}$ with level $\alpha$, one has $E_{\theta} \phi^{\prime}(X) \leq E_{\theta} \phi(X) \quad \forall \theta \in \Theta_{1}$.

## 7.2 Lemmas and Theorems
### Lemma 7.1.1: Neyman-Pearson Lemma
We consider testing $H_{0}: \theta=\theta_{0}$ against the alternative $H_{1}: \theta=\theta_{1}$.

Let $\phi$ be some test. We have $$R\left(\theta_{1}, \phi_{\mathrm{NP}}\right)-R\left(\theta_{1}, \phi\right) \leqslant c\left[R\left(\theta_{0}, \phi\right)-R\left(\theta_{0}, \phi_{\mathrm{NP}}\right)\right]$$ or $$\left[R\left(\theta_{1}, \phi\right)-R\left(\theta_{1}, \phi_{\mathrm{NP}}\right)\right] \geqslant c\left[R\left(\theta_{0}, \phi_{\mathrm{NP}}\right)-R\left(\theta_{0}, \phi\right)\right]$$

#### Proof
$$\begin{aligned}  &R\left(\theta_{1}, \phi_{\mathrm{NP}}\right)-R\left(\theta_{1}, \phi\right) \text{(take expct)}\\
=& \int\left(\phi-\phi_{\mathrm{NP}}\right) p_{1} \\
=& \int_{p_{1} / p_{0}>c}\left(\phi-\phi_{\mathrm{NP}}\right) p_{1}+\int_{p_{1} / p_{0}=c}\left(\phi-\phi_{\mathrm{NP}}\right) p_{1}+\int_{p_{1} / p_{0}<c}\left(\phi-\phi_{\mathrm{NP}}\right) p_{1} \\
\leq & c \int_{p_{1} / p_{0}>c}\left(\phi-\phi_{\mathrm{NP}}\right) p_{0}+c \int_{p_{1} / p_{0}=c}\left(\phi-\phi_{\mathrm{NP}}\right) p_{0}+c \int_{p_{1} / p_{0}<c}\left(\phi-\phi_{\mathrm{NP}}\right) p_{0} \\
=& c\left[R\left(\theta_{0}, \phi\right)-R\left(\theta_{0}, \phi_{\mathrm{NP}}\right)\right]\end{aligned}
$$

:::warning
**Remark:**
NP Lemma means that a Neyman-Pearson test is better than any other test at level $\alpha$ in terms of risks. When you increase the Type I error of NP test ($R(\theta_0, \phi_{NP})$), then its Type II error $R(\theta_1, \phi_{NP})$ will decrease.
:::

### Theorem 7.3.1: UMP tests for exponential families
We now study the situation where $\Theta$ is an interval in $\mathbb{R}$, and the testing problem is $H_{0}: \theta \leq \theta_{0}$ against $H_{1}: \theta>\theta_{0}$.

Suppose that $\mathcal{P}$ is a one-dimensional exponential family $$p_{\theta}(x)=\exp [c(\theta) T(x)-d(\theta)] h(x)$$

1. **$c(\theta)$ is a strictly increasing function of $\theta$**: **Thus $\beta(\theta)$ is increasing in $\theta$**. Then a UMP test $\phi$ is $$\phi(T(x)):= \begin{cases}1 & \text { if } T(x)>t_{0} \\ q & \text { if } T(x)=t_{0} \\ 0 & \text { if } T(x)<t_{0}\end{cases}$$ where $q$ and $t_{0}$ are chosen in such a way that $E_{\theta_{0}} \phi(T)=\alpha$.
2. **$c(\theta)$ is a strictly decreasing function of $\theta$**: **Thus $\beta(\theta)$ is decreasing in $\theta$**. Then a UMP test $\phi$ is $$\phi(T(x)):= \begin{cases}1 & \text { if } T(x)<t_{0} \\ q & \text { if } T(x)=t_{0} \\ 0 & \text { if } T(x)>t_{0}\end{cases}$$ where $q$ and $t_{0}$ are chosen in such a way that $E_{\theta_{0}} \phi(T)=\alpha$.

:::warning
**Remark**
If the testing problem is $H_{0}: \theta \geq \theta_{0}$ against $H_{1}: \theta < \theta_{0}$, then it is exactly the other way around.

:::

#### Discrete Proof for the power function $\beta(\theta) = E_{\theta} \phi(T)$ is increasing
We have $P (T=t) = \exp [c(\theta) t-d(\theta)] \sum\limits_{x: T(x)=t}h(x)$. 
For $\tilde{\theta}>\theta$, we construct $$\frac{P_{\tilde{\theta}}(T=t)}{P_{\theta}(T=t)} = \exp[(c(\tilde{\theta}) - c(\theta))t - (d(\tilde{\theta}) - d(\theta))]$$ which increases in $t$.

![](https://i.imgur.com/xpd8wyU.png =600x)

Case I: $1 =\sum_{t} P_\tilde{\theta}(T=t)<\sum_{t} P_{\theta}(T=t)=1$ reaches contradiction. (and also case III which works the other way around). So case 2 is the only possible situation. 

Define a point $s_{0}$ where the two densities cross: $$\left\{\begin{array}{ll}\frac{P_{\tilde{\theta}}(T=t)}{P_{\theta}(T=t)} \leq 1 & \text { for } t \leq s_{0} \\\frac{P_{\tilde{\theta}}(T=t)}{P_{\theta}(T=t)} > 1 & \text { for } t \geq s_{0} \\\end{array} .\right.$$ Thus $$\begin{aligned}E_{\tilde{\theta}} \phi(T)-E_{\theta} \phi(T) &=\sum_{t} \phi(t)\left[P_{\tilde{\theta}}(t)-P_{\theta}(t)\right] \\ &= \sum_{t\leq s_0} \underbrace{\phi(t)}_{\leq \phi(s_0)}\underbrace{ \left[P_{\tilde{\theta}}(t)-P_{\theta}(t)\right]}_{\leq 0} + \sum_{t\geq s_0} \underbrace{\phi(t)}_{\geq \phi(s_0)} \underbrace{\left[P_{\tilde{\theta}}(t)-P_{\theta}(t)\right]}_{\geq 0} \\ & \geq \phi(s_0)\sum_{t\leq s_0} \left[P_{\tilde{\theta}}(t)-P_{\theta}(t)\right] + \phi(s_0)\sum_{t\geq s_0}\left[P_{\tilde{\theta}}(t)-P_{\theta}(t)\right] \\ &= \phi(s_0)\sum_{t}\left[P_{\tilde{\theta}}(t)-P_{\theta}(t)\right] \\ &= 0\end{aligned}$$ i.e. $$E_{\tilde{\theta}} \phi(T) \geqslant E_{\theta} \phi(T) \text { for } \tilde{\theta} >\theta$$ But then$$\sup _{\theta \leq \theta_{0}} \beta(\theta)=\beta\left(\theta_{0}\right)=\alpha$$ Hence, $\phi$ has level $\alpha$. Because any other test $\phi^{\prime}$ with level $\alpha$ must have $E_{\theta_{0}} \phi^{\prime}(X) \leq \alpha$ (NP Lemma), we conclude that $\phi$ is UMP.

### Theorem 7.5.1 UMPU Test for two-sided problems in exp family
We consider testing $H_{0}: \theta=\theta_{0}$, against $H_{1}: \theta \neq \theta_{0} .$

Suppose $\mathcal{P}$ is a one-dimensional exponential family:$$\frac{d P_{\theta}}{d \nu}(x):=p_{\theta}(x)=\exp [c(\theta) T(x)-d(\theta)] h(x),$$ with $c(\theta)$ strictly increasing in $\theta$. Then a UMPU test is $$\phi(T(x)):=\left\{\begin{array}{ll}
1 & \text { if } T(x)<t_{L} \text { or } T(x)>t_{R} \\
q_{L} & \text { if } T(x)=t_{L} \\
q_{R} & \text { if } T(x)=t_{R} \\
0 & \text { if } t_{L}<T(x)<t_{R}
\end{array},\right.$$ where the constants $t_{R}, t_{L}, q_{R}$ and $q_{L}$ are chosen in such a way that$$E_{\theta_{0}} \phi(X)=\alpha,\left.\frac{d}{d \theta} E_{\theta} \phi(X)\right|_{\theta=\theta_{0}}=0 .$$

:::warning
**Note** 
Let $\phi_{R}$ a right-sided test as defined Theorem 7.3.1 with level at most $\alpha$ and $\phi_{L}$ be the similarly defined left-sided test. Then $\beta_{R}(\theta)=E_{\theta} \phi_{R}(T)$ is strictly increasing, and $\beta_{L}(\theta)=E_{\theta} \phi_{L}(T)$ is strictly decreasing. The two-sided test $\phi$ of Theorem 7.5.1 is a superposition of two one-sided tests.
:::

## 7.4 Examples
### Ex 7.2.1: NP Test on Binomial Distribution
:::warning
**Remark**
Which also showcased that it is UMP for exp family.
:::

#### 7.2.1.1 Simple Hypothesis
$X \sim B(n, \theta)$. We want to test, at level $\alpha$, the hypothesis $$H_{0}: \theta=\frac{1}{2}=: \theta_{0},$$ against the alternative $$H_{1}: \theta=\frac{1}{4}=: \theta_{1}$$ Consider the randomized test $$\phi(T):= \begin{cases}1 & \text { if } p_1/p_0 <t_{0} \\ q & \text { if } p_1/p_0=t_{0} \\ 0 & \text { if } p_1/p_0>t_{0}\end{cases}$$ where $q \in(0,1)$, and where $t_{0}$ is the critical value of the test. The constants $q$ and $t_{0} \in\{0, \ldots, n\}$ are chosen in such a way that the probability of rejecting $H_{0}$ when it is in fact true, is equal to $\alpha$: $$P_{\theta_{0}}\left(H_{0} \text { rejected }\right)=P_{\theta_{0}}\left(T \leq t_{0}-1\right)+q P_{\theta_{0}}\left(T=t_{0}\right):=\alpha$$ Because $\phi=\phi_{\mathrm{NP}}$ is the Neyman Pearson test, it is the most powerful test (at level $\alpha$ ). The power of the test is $\beta\left(\theta_{1}\right)$, where$$\beta(\theta):=E_{\theta} \phi(T)$$

#### 7.2.1.2 Composite Hypothesis (One-sided)
Consider now testing $H_{0}: \theta_{0}=\frac{1}{2}$, against $H_{1}: \theta<\frac{1}{2}$.

In Problem 1 , the construction of the test $\phi$ is independent of the value $\theta_{1}<\theta_{0}$. So $\phi$ is most powerful for all $\theta_{1}<\theta_{0}$. We say that $\phi$ is uniformly most powerful for the alternative $H_{1}: \theta<\theta_{0}$.

#### 7.2.1.3 Composite Hypothesis (Two-sided)
We now want to test $H_{0}: \theta \geq \frac{1}{2}$, against the alternative $H_{1}: \theta<\frac{1}{2}$.

Recall the function $$\beta(\theta):=E_{\theta} \phi_{NP}(T)$$ The level of $\phi$ is defined as$$\sup _{\theta \geq 1 / 2} \beta(\theta) $$ We have$$
\begin{aligned}
\beta(\theta) &=P_{\theta}\left(T \leq t_{0}-1\right)+q P_{\theta}\left(T=t_{0}\right) \\
&=(1-q) P_{\theta}\left(T \leq t_{0}-1\right)+q P_{\theta}\left(T \leq t_{0}\right)
\end{aligned}$$ Observe that if $\theta_{1}<\theta_{0}$, small values of $T$ are more likely under $P_{\theta_{1}}$ than under $P_{\theta_{0}}$: $$P_{\theta_{1}}(T \leq t)>P_{\theta_{0}}(T \leq t), \forall t \in\{0,1, \ldots, n\}$$ Thus, $\beta(\theta)$ is a decreasing function of $\theta$. It follows that the level of $\phi$ is $$=\sup _{\theta \geq \frac{1}{2}} \beta(\theta)=\beta\left(\frac{1}{2}\right)=\alpha$$ Hence, $\phi$ is uniformly most powerful for $H_{0}: \theta \geq \frac{1}{2}$ against $H_{1}: \theta<\frac{1}{2}$.

### Ex 7.3.1: Test for the variance of the normal distribution
Let $X_{1}, \ldots, X_{n}$ be an i.i.d. sample from the $\mathcal{N}\left(\mu_{0}, \sigma^{2}\right)$-distribution, with $\mu_{0}$ known, and $\sigma^{2}>0$ unknown. We want to test $H_{0}: \sigma^{2} \leq \sigma_{0}^{2}$, against $H_{1}: \sigma^{2}>\sigma_{0}^{2}$. The density of the sample is $$ \mathbf{p}_{\sigma^{2}}\left(x_{1}, \ldots, x_{n}\right)=\exp \left[-\frac{1}{2 \sigma^{2}} \sum_{i=1}^{n}\left(x_{i}-\mu_{0}\right)^{2}-\frac{n}{2} \log \left(2 \pi \sigma^{2}\right)\right]$$ Thus, we may take $$ c\left(\sigma^{2}\right)=-\frac{1}{2 \sigma^{2}}$$ and $$ T(\mathbf{X})=\sum_{i=1}^{n}\left(X_{i}-\mu_{0}\right)^{2}$$ The function $c\left(\sigma^{2}\right)$ is strictly increasing in $\sigma^{2}$. So we let $\phi$ be the test which rejects $H_{0}$ for large values of $T(\mathbf{X})$. Note that under $H_{0}$, the statistic $T(\mathbf{X}) / \sigma_{0}^{2}$ has a $\chi^{2}$-distribution with $n$ degrees of freedom, the $\chi_{n}^{2}$-distribution (see Section 12.2 for a definition). So we can find the critical value from the quantile of the $\chi_{n}^{2}$-distribution.

### Ex 7.5.1 Two-sided test for the mean of the normal distribution
Let $X_{1}, \ldots, X_{n}$ be an i.i.d. sample from the $\mathcal{N}\left(\mu, \sigma_{0}^{2}\right)$-distribution, with $\mu \in \mathbb{R}$ unknown, and with $\sigma_{0}^{2}$ known. We consider testing
$H_{0}: \mu=\mu_{0}$,
against
$H_{1}: \mu \neq \mu_{0} .$
A sufficient statistic is $T:=\sum_{i=1}^{n} X_{i}$. We have, for $t_{L}<t_{R}$,
$$
\begin{aligned}
E_{\mu} \phi(T) &=\mathbb{P}_{\mu}\left(T>t_{R}\right)+\mathbb{P}_{\mu}\left(T<t_{L}\right) \\
&=\mathbb{P}_{\mu}\left(\frac{T-n \mu}{\sqrt{n} \sigma_{0}}>\frac{t_{R}-n \mu}{\sqrt{n} \sigma_{0}}\right)+\mathbb{P}_{\mu}\left(\frac{T-n \mu}{\sqrt{n} \sigma_{0}}<\frac{t_{L}-n \mu}{\sqrt{n} \sigma_{0}}\right) \\
&=1-\Phi\left(\frac{t_{R}-n \mu}{\sqrt{n} \sigma_{0}}\right)+\Phi\left(\frac{t_{L}-n \mu}{\sqrt{n} \sigma_{0}}\right)
\end{aligned}
$$
where $\Phi$ is the standard normal distribution function. To avoid confusion with the test $\phi$, we denote the standard normal density in this example by $\dot{\Phi}$. Thus, $$
\frac{d}{d \mu} E_{\mu} \phi(T)=\frac{n}{\sqrt{n} \sigma_{0}} \dot{\Phi}\left(\frac{t_{R}-n \mu}{\sqrt{n} \sigma_{0}}\right)-\frac{n}{\sqrt{n} \sigma_{0}} \dot{\Phi}\left(\frac{t_{L}-n \mu}{\sqrt{n} \sigma_{0}}\right)
$$
So putting
$$
\left.\frac{d}{d \mu} E_{\mu} \phi(T)\right|_{\mu=\mu_{0}}=0
$$
gives
$$
\dot{\Phi}\left(\frac{t_{R}-n \mu_{0}}{\sqrt{n} \sigma_{0}}\right)=\dot{\Phi}\left(\frac{t_{L}-n \mu_{0}}{\sqrt{n} \sigma_{0}}\right)
$$
or
$$
\left(t_{R}-n \mu_{0}\right)^{2}=\left(t_{L}-n \mu_{0}\right)^{2} .
$$
We take the solution $\left(t_{L}-n \mu_{0}\right)=-\left(t_{R}-n \mu_{0}\right)$, (because the solution $\left(t_{L}-n \mu_{0}\right)=\left(t_{R}-n \mu_{0}\right)$ leads to a test that always rejects, and hence does not have level $\alpha$, as $\alpha<1$ ). Plugging this solution back in gives
$$
\begin{aligned}
E_{\mu_{0}} \phi(T) &=1-\Phi\left(\frac{t_{R}-n \mu_{0}}{\sqrt{n} \sigma_{0}}\right)+\Phi\left(-\frac{t_{R}-n \mu_{0}}{\sqrt{n} \sigma_{0}}\right) \\
&=2\left(1-\Phi\left(\frac{t_{R}-n \mu_{0}}{\sqrt{n} \sigma_{0}}\right)\right) .
\end{aligned}
$$
The requirement $E_{\mu_{0}} \phi(T)=\alpha$ gives us
$$
\Phi\left(\frac{t_{R}-n \mu_{0}}{\sqrt{n} \sigma_{0}}\right)=1-\alpha / 2,
$$
and hence
$$
t_{R}-n \mu_{0}=\sqrt{n} \sigma_{0} \Phi^{-1}(1-\alpha / 2), t_{L}-n \mu_{0}=-\sqrt{n} \sigma_{0} \Phi^{-1}(1-\alpha / 2) .
$$