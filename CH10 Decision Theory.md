---
tags: FMS
---

# CH10 Decision Theory
## 10.1 Concepts
### 10.1.1 Risk
- **Loss Function**: A loss function is a map $$L: \Theta \times \mathcal{A} \rightarrow \mathbb{R}$$ with $L(\theta, a)$ being the loss when the parameter value is $\theta$ and one takes action $a$.
- **Risk**: Expected Loss $$R(\theta, d):=E_{\theta} L(\theta, d), \theta \in \Theta$$

:::warning
**Note**
- The best decision $d$ is the one with the smallest risk $R(\theta, d)$. However, $\theta$ is not known. Thus, if we compare two decision functions $d_{1}$ and $d_{2}$, we may run into problems because the risks are not comparable.
:::

### 10.1.2 Admissibility
A decision $d^{\prime}$ is called strictly better than $d$ if $$R\left(\theta, d^{\prime}\right) \leq R(\theta, d), \forall \theta,$$ and $$\exists \theta: R\left(\theta, d^{\prime}\right)<R(\theta, d)$$ When there exists a $d^{\prime}$ that is strictly better than $d$, then $d$ is called inadmissible.

:::warning
**Illustration**
![](https://i.imgur.com/y9tEKZA.png =400x)

**Note**
We note that to show that a decision $d$ is inadmissible, it suffices to find a strictly better $d^{\prime}$. On the other hand, to show that $d$ is admissible, one has to verify that there is no strictly better $d^{\prime}$. So in principle, one then has to take all possible $d^{\prime}$ into account.
:::

### 10.1.3 Minimaxity
A decision $d$ is called minimax if $$\sup _{\theta} R(\theta, d)=\inf _{d^{\prime}} \sup _{\theta} R\left(\theta, d^{\prime}\right)$$

:::warning
**Illustration**
![](https://i.imgur.com/lUfWawG.png =400x)

:::

### 10.1.4 Bayes Estimator
#### 10.1.4.1 Prior Density
Let $w(\theta), \theta \in \Theta$ such that $$\left\{\begin{array}{ll}\sum_{\theta \in \Theta} w(\theta)=1 &\text{ discrete case} \\ \int_{\Theta} w(\theta) d \theta=1 &\text{ cont. case} \end{array}\right.$$

#### 10.1.4.2 Bayes Risk
Expected Risk (integrate the parameter out) $$r_{w}(d)= (\sum_{\theta\in\Theta}) \int_{\Theta} R(\vartheta, d) w(\vartheta) d \mu(\vartheta)$$

#### 10.1.4.3 Bayes Estimator
$$
d_{\text {Bayes }}=\arg \min _{d^{\prime}} r_{w}\left(d^{\prime}\right)
$$

#### 10.1.4.4 Posterior
We now think of $p_{\theta}$ as the density of $X$ given the value of $\theta$ (likelihood). We write it as $$p_{\theta}(x)=p(x \mid \theta), x \in \mathcal{X} .$$ Moreover, we define the marginal density (evidence) $$p(\cdot):=\int_{\Theta} p(\cdot \mid \vartheta) w(\vartheta) d \mu(\vartheta)$$ The a posteriori density of $\theta$ is $$w(\vartheta \mid x)=p(x \mid \vartheta) \frac{w(\vartheta)}{p(x)}, \vartheta \in \Theta, x \in \mathcal{X}$$

#### 10.1.4.5 MAP
The maximum a posteniori $\theta_{MAP}(x)=\arg \max_{\theta \in \Theta} w(\theta \mid x)$

## 10.2 Lemmas
### Lemma 10.2.1: Not using the data at all is admissible
#### Domination
Let $P$ and $Q$ be probability measures on the same measurable space. Then $P$ dominates $Q$ if for all measurable $B, P(B)=0$ implies $Q(B)=0$.
Let $L(\theta, a):=|g(\theta)-a|^{r}$ and $d(X):=g\left(\theta_{0}\right)$, where $\theta_{0}$ is some fixed given value.

Assume that $P_{\theta_{0}}$ dominates $P_{\theta}$ for all $\theta$. Then $d$ is admissible.

#### Proof
Suppose that $d^{\prime}$ is better than $d$. Then we have $$E_{\theta_{0}}\left|g\left(\theta_{0}\right)-d^{\prime}(X)\right|^{r} \leq E_{\theta_{0}}\left|g\left(\theta_{0}\right)-d(X)\right|^{r} = 0$$ This implies that$$ d^{\prime}(X)=g\left(\theta_{0}\right), P_{\theta_{0}}-\text { almost surely } $$ i.e. $$P_{\theta_{0}}\left(d^{\prime}(X) \neq g\left(\theta_{0}\right)\right)=0$$ the assumption that $P_{\theta_{0}}$ dominates $P_{\theta}, \forall \theta$, implies now $$P_{\theta}\left(d^{\prime}(X) \neq g\left(\theta_{0}\right)\right)=0, \forall \theta$$ That is, for all $\theta, d^{\prime}(X)=g\left(\theta_{0}\right), P_{\theta}$-almost surely, and hence, for all $\theta, R\left(\theta, d^{\prime}\right)=$ $R(\theta, d)$. So $d^{\prime}$ is not strictly better than $d$. We conclude that $d$ is admissible.

### Lemma 10.2.2 A Neyman Pearson test is admissible
Consider testing $H_{0}: \theta=\theta_{0}$ against the alternative $H_{1}: \theta=\theta_{1}$. Define the risk $R(\theta, \phi)$ of a test $\phi$ as the probability of error of first and second kind: $$ R(\theta, \phi):=\left\{\begin{array}{ll} E_{\theta} \phi(X), & \theta=\theta_{0} \\ 1-E_{\theta}\phi(X), & \theta=\theta_{1} \end{array} .\right.$$ We let $p_{0}\left(p_{1}\right)$ be the density of $P_{\theta_{0}}\left(P_{\theta_{1}}\right)$ with respect to some dominating measure $\nu$ (for example $\nu=P_{\theta_{0}}+P_{\theta_{1}}$ ). A Neyman Pearson test is (see Section 7.1) $$\phi_{\mathrm{NP}}:=\left\{\begin{array}{ll}
1 & \text { if } p_{1} / p_{0}>c \\
q & \text { if } p_{1} / p_{0}=c \\
0 & \text { if } p_{1} / p_{0}<c \\
\end{array} .\right.$$ Here $0 \leq q \leq 1$, and $0 \leq c<\infty$ are given constants.

Suppose ==$R\left(\theta_{1}, \phi_{NP}\right)\neq 0$== Then $\phi_{NP}$ is admissible.

#### Proof using NP Lemma
1. Suppose $R\left(\theta_{0}, \phi\right)<R\left(\theta_{0}, \phi_{\mathrm{NP}}\right)$. Then from the Neyman Pearson Lemma, we know that either $R\left(\theta_{1}, \phi\right)>R\left(\theta_{1}, \phi_{\mathrm{NP}}\right)$ (i.e., then $\phi$ is not better then $\phi_{\mathrm{NP}}$ ), or $c=0$. But when $c=0$, it holds that $R\left(\theta_{1}, \phi_{\mathrm{NP}}\right)=0$.
2. Similarly, suppose that $R\left(\theta_{1}, \phi\right)<R\left(\theta_{1}, \phi_{\mathrm{NP}}\right)$. Then it follows from the Neyman Pearson Lemma that $R\left(\theta_{0}, \phi\right)>R\left(\theta_{0}, \phi_{\mathrm{NP}}\right)$, because we assume $c<\infty$.

Thus no $\phi$ is strictly better than $\phi_{NP}$ in either case, i.e. $\phi_{NP}$ is admissible.

:::warning
**Illustration:** $S:=\left\{\left(\begin{array}{l}R\left(\theta_{0}, \phi\right) \\ R\left(\theta_{1}, \phi\right)\end{array}\right): \phi \text { test statistic}\right\}$, $C[0,1]^{2}$
![](https://i.imgur.com/fG3EUTQ.png =200x)

:::

### Lemma 10.3.1 Minimax Neyman Pearson test
Let $S=\left\{\left(\begin{array}{l}R\left(\theta_{0}, \phi\right) \\ R\left(\theta_{1}, \phi\right)\end{array}\right): \phi \in \mathcal{F}\right\}$. Note that $S$ is convex since $\phi_{\mathrm{NP}}$ is linear. 

A Neyman Pearson test $\phi_{\mathrm{NP}}$ is minimax, ==if and only if $R\left(\theta_{0}, \phi_{\mathrm{NP}}\right)=$ $R\left(\theta_{1}, \phi_{\mathrm{NP}}\right)$==. 

#### Proof using NP Lemma
Let $\phi$ be a test, and write for $j=0,1$, $$r_{j}:=R\left(\theta_{j}, \phi_{\mathrm{NP}}\right), r_{j}^{\prime}=R\left(\theta_{j}, \phi\right)$$ 

1. ==Suppose that $r_{0}=r_{1}$ and that $\phi_{\mathrm{NP}}$ is not minimax.== Then, for some test $\phi$, $$\max _{j} r_{j}^{\prime}<\max _{j} r_{j}$$ This implies that both $$r_{0}^{\prime}<r_{0}, r_{1}^{\prime}<r_{1}$$ and by the Neyman Pearson Lemma, this is not possible.
2. Suppose $r_{0}<r_{1}$, for a convex set $S$ we can find a test $\phi$ with $r_{0}<r_{0}^{\prime}<r_{1}$ and $r_{1}^{\prime}<r_{1}$. So then $\phi_{\mathrm{NP}}$ is not minimax. 
3. Similarly if $r_{0}>r_{1}$.

:::warning
**Illustration**
![](https://i.imgur.com/mlWf3hT.png =200x)

:::

### Lemma 10.4.1 Bayes Estimator as test statistic
Consider again the testing problem $H_{0}: \theta=\theta_{0}$ against the alternative $H_{1}: \theta=\theta_{1}$. Let $w\left(\theta_{0}\right)=w_{0}, w\left(\theta_{1}\right)=w_{1}=1-w_{0}$, and risk $R\left(\theta_{0},\phi\right)=E_{\theta_{0}} \phi(X)$, $R\left(\theta_{1}, \phi\right)=1-E_{\theta_1} \phi(X)$. Thus Bayes risk: $$r_{w}(\phi):=w_{0} R\left(\theta_{0}, \phi\right)+w_{1} R\left(\theta_{1}, \phi\right)$$ A Bayes test is therefore: $$\phi_{\text {Bayes }}=\left\{\begin{array}{ll}
1 & \text { if } p_{1} / p_{0}>w_{0} / w_{1} \\
q & \text { if } p_{1} / p_{0}=w_{0} / w_{1} \\
0 & \text { if } p_{1} / p_{0}<w_{0} / w_{1}
\end{array} \right.$$

#### Proof
$$\begin{aligned}r_{w}(\phi) &=w_{0} \int \phi p_{0}+w_{1}\left(1-\int \phi p_{1}\right) \\&=\int \phi\left(w_{0} p_{0}-w_{1} p_{1}\right)+w_{1}
\end{aligned} $$ So we choose $\phi \in[0,1]$ to minimize $\phi\left(w_{0} p_{0}-w_{1} p_{1}\right)$. This is done by taking $$\phi= \begin{cases}1 & \text { if } w_{0} p_{0}-w_{1} p_{1}<0 \\ q & \text { if } w_{0} p_{0}-w_{1} p_{1}=0 \\ 0 & \text { if } w_{0} p_{0}-w_{1} p_{1}>0\end{cases}
$$ 
where for $q$ we may take any value between 0 and 1 .

#### Corollary
Bayes risk is large if the two densities are close to each other: $$r_{w}\left(\phi_{Bayes}\right)=\frac{1-\int\left|w_{0} p_{0}-w_{1}p_{1}\right|}{2}$$

:::warning
**Illustration**
![](https://i.imgur.com/cG2bM2m.png =600x)
:::

### Lemma 10.5.1 Bayesian Decision using the data
Let $X$ have distribution $P \in \mathcal{P}:=\left\{P_{\theta}: \theta \in \Theta\right\}$. Suppose $\mathcal{P}$ is dominated by a ($\sigma$-finite) measure $\nu$. Let prior distribution $\Pi$ on $\Theta$ have density with respect to some dominating measure $\mu$.

==Given the data $X=x$==, consider $\theta$ as a random variable with posterior density $w(\vartheta \mid x)$. Let $$l(x, a):=E_{x}[L(\theta, a) \mid X=x]=\int_{\Theta} L(\vartheta, a) w(\vartheta \mid x) d \mu(\vartheta),$$ and $$ d(x):=\arg \min _{a} l(x, a)$$ Then $d$ is Bayes decision $d_{\text {Bayes }}$.

#### Proof
$\begin{aligned} r_{w}\left(d^{\prime}\right) &=\int_{\Theta} R\left(\vartheta, d^{\prime}\right) w(\vartheta) d \mu(\vartheta) \\ 
&=\int_{\Theta} E_{\theta}\left(L(\vartheta, d^{\prime})\right) w(\vartheta) d \mu(\vartheta)\\
&=\underbrace{\int_{\Theta}\left[\int_{\mathcal{X}} L\left(\vartheta, d^{\prime}(x)\right) \underbrace{p(x \mid \vartheta)}_{\text{p.d.f, by def}} d \nu(x)\right] w(\vartheta) d \mu(\vartheta)}_{\text{by interchageability of the integral}} \\ 
&=\int_{\mathcal{X}}\left[\int_{\Theta}L\left(\vartheta, d^{\prime}(x)\right) \underbrace{w(\vartheta \mid x) p(x) }_{\text{by Bayes' Rule}} d \mu(\vartheta)\right] d \nu(x) \\ 
&=\int_{\mathcal{X}} l\left(x, d^{\prime}(x)\right) p(x) d \nu(x) \\ 
& \geq \int_{\mathcal{X}} l(x, d(x)) p(x) d \nu(x) \\ &=r_{w}(d) . \end{aligned}$

### Corollary 10.5.1 Bayesian Decision only depends on sufficient staistics
Let $S$ be sufficient. Then $d_{Bayes}(x)$ depends only on $S$

#### Proof
The Bayes decision is $$d_{\text {Bayes }}(X)=\arg \min _{a \in \mathcal{A}} l(X, a)$$ where $$\begin{aligned}l(x, a)&=E_{x}(L(\theta, a) \mid X=x)\\
&=\int _{\Theta}L(\vartheta, a)w(\vartheta \mid x) d \mu(\vartheta)\\
&=\int_{\Theta} L(\vartheta, a) \frac{p(x\mid\vartheta) w(\vartheta)}{p(x)} d \mu(\vartheta) \\
&\propto \int_{\Theta} L(\vartheta, a) p(x\mid\vartheta) w(\vartheta) d \mu(\vartheta)\\
&\propto \int_{\Theta} L(\vartheta, a) \underbrace{g_{\vartheta}(S(x))h(x)}_{\text{by factorization theorem}} w(\vartheta) d \mu(\vartheta)  \end{aligned}$$ So $$ d_{\text {Bayes }}(X)=\arg \min _{a \in \mathcal{A}} \int_{\Theta} L(\vartheta, a) g_{\vartheta}(S(X)) w(\vartheta) d \mu(\vartheta) $$which only depends on the sufficient statistic $S$.

### Lemma 10.5.2 Bayes estimator for quadratic loss is the expct of the posterior
Consider the case $\mathcal{A}=\mathbb{R}$ and $\Theta \subseteq \mathbb{R}$. Let $L(\theta, a):=|\theta-a|^{2}$. Then $$d_{\text {Bayes }}(X)=E(\theta \mid X)$$ and for a Bayesian estimator T$$r_{w}\left(T^{\prime}\right)=r_w(T)+E\left[T(X)-T^{\prime}(X)\right]^{2}$$

#### Proof
$$\ell(x, a)=E\left[(\theta-a)^{2} \mid X=x\right]$$ 
Since $$\arg \min _{a \in \mathbb{R}} E(Z-a)^{2}=E Z
$$ use Lemma 10.5.1 $$ d_{\text{Bayes}}(x) = \arg\min _{a \in \mathbb{R}} \ell(x, a)=E(\theta \mid X=x)
$$

![](https://i.imgur.com/Ixm2sOS.jpg =600x)

## 10.3 Key Takeaways & Common Tricks
:::danger

:::


## 10.4 Examples
### 10.4.1 Loss function and risks
#### Ex 10.1.1 Estimation 
In the case of estimating a parameter of interest $g(\theta) \in \mathbb{R}$, the action space is $\mathcal{A}=\mathbb{R}$ (or a subset thereof). Important loss functions are then $$L(\theta, a):=w(\theta)|g(\theta)-a|^{r},$$where $w(\cdot)$ are given non-negative weights and $r \geq 0$ is a given power. The risk is then $$R(\theta, d)=w(\theta) E_{\theta}|g(\theta)-d(X)|^{r} .$$ A special case is taking $w \equiv 1$ and $r=2$. Then $L(\theta, a)=(g(\theta)-a)^{2}$ is called quadratic loss and $$R(\theta, d)=E_{\theta}|g(\theta)-d(X)|^{2}$$ is called the mean square error.

#### Example 10.1.2 Tests 
Consider testing the hypothesis $H_{0}: \theta \in \Theta_{0}$ against the alternative $H_{1}: \theta \in \Theta_{1}$. Here, $\Theta_{0}$ and $\Theta_{1}$ are given subsets of $\Theta$ with $\Theta_{0} \cap \Theta_{1}=\emptyset$. As action space, we take $\mathcal{A}=\{0,1\}$, and as loss
$$ L(\theta, a):=\left\{\begin{array}{ll} 1 & \text { if } \theta \in \Theta_{0} \text { and } a=1 \\ c & \text { if } \theta \in \Theta_{1} \text { and } a=0 \\ 0 & \text { otherwise }\end{array} .\right. $$ Here $c>0$ is some given constant. Then $$R(\theta, d)=\left\{\begin{array}{ll}P_{\theta}(d(X)=1) & \text { if } \theta \in \Theta_{0} \\ P_{\theta}(d(X)=0) & \text { if } \theta \in \Theta_{1} \\0 & \text { otherwise }\end{array}\right.
$$
Thus, the risks correspond to the error probabilities (type I and type II errors).

### 10.4.2 Bayes Estimators (using posterior and conjugate priors)
#### Ex 10.5.1 Bayes test revisited
For the testing problem $H_{0}: \theta=\theta_{0}$ against the alternative $H_{1}: \theta=\theta_{1}$, with loss function $$L\left(\theta_{0}, a\right):=a, L\left(\theta_{1}, a\right):=1-a, a \in\{0,1\},$$ we have $$l(x, \phi)=\phi w_{0} p_{0}(x) / p(x)+(1-\phi) w_{1} p_{1}(x) / p(x)$$ Thus, $$\arg \min _{\phi} l(\cdot, \phi)=\left\{\begin{array}{ll}
1 & \text { if } w_{1} p_{1}>w_{0} p_{0} \\
q & \text { if } w_{1} p_{1}=w_{0} p_{0} \\
0 & \text { if } w_{1} p_{1}<w_{0} p_{0}
\end{array} .\right.$$

#### Ex 10.5.4.1 Poisson with Gamma prior
Suppose that given $\theta, X$ has Poisson distribution with parameter $\theta$, and that $\theta$ has the Gamma $(k, \lambda)$-distribution. The density of $\theta$ is then $$ w(\vartheta)=\lambda^{k} \vartheta^{k-1} \mathrm{e}^{-\lambda \vartheta} / \Gamma(k)$$ where $$\Gamma(k)=\int_{0}^{\infty} \mathrm{e}^{-z} z^{k-1} d z$$ The $\operatorname{Gamma}(k, \lambda)$ distribution has mean $$E \theta=\int_{0}^{\infty} \vartheta w(\vartheta) d \vartheta=\frac{k}{\lambda} .$$ The a posteriori density is then $$\begin{aligned}w(\vartheta \mid x) & \propto p(x \mid \vartheta) w(\vartheta) \\& \propto \mathrm{e}^{-\vartheta(1+\lambda)} \vartheta^{k+x-1} \end{aligned} $$ We recognize $w(\vartheta \mid x)$ as the density of the $\operatorname{Gamma}(k+x, 1+\lambda)$-distribution. Bayes estimator with quadratic loss is thus $$E(\theta \mid X)=\frac{k+X}{1+\lambda}$$,The maximum a posteriori estimator is $$\frac{k+X-1}{1+\lambda}$$

#### Ex 10.5.2 Binomial distibution with Beta prior
Suppose that $X$ is binomial $(n, \theta)$ and that $\theta$ has the $\operatorname{Beta}(r, s)$ prior$$w(\vartheta)=\frac{\Gamma(r+s)}{\Gamma(r) \Gamma(s)} \vartheta^{r-1}(1-\vartheta)^{s-1}, 0<\vartheta<1 .
$$ $$\theta \mid X=x \sim \operatorname{Beta}(x+r, n-x+s)$$ Bayes estimator under quadratic loss is the posterior expectation $$E(\theta \mid X)=\frac{X+r}{n+r+s}$$ special case: $r=s=1$ (uniform distrib.) $$E(\theta \mid X) =\frac{x+1}{n+2}
$$

:::warning
**Remark:**
- The posterior expct is a good estimator of $\theta_{\text{MAP}}$
- If $\theta \sim \operatorname{Unif}(\theta)$ Then $\theta_{\text {MAP }}=\theta_{\text {MLE}}$
:::

#### Example 10.5.3 Normal distribution with normal prior 
Let $X \sim \mathcal{N}(\theta, 1)$ and $\theta \sim \mathcal{N}\left(c, \tau^{2}\right)$ for some $c$ and $\tau^{2}$. We have $$\begin{aligned}
w(\vartheta \mid x) &=\frac{p(x \mid \vartheta) w(\vartheta)}{p(x)} \\
& \propto \phi(x-\vartheta) \phi\left(\frac{\vartheta-c}{\tau}\right) \\
& \propto \exp \left[-\frac{1}{2}\left\{(x-\vartheta)^{2}+\frac{(\vartheta-c)^{2}}{\tau^{2}}\right\}\right] \\
& \propto \exp \left[-\frac{1}{2}\left\{\vartheta-\frac{\tau^{2} x+c}{\tau^{2}+1}\right\}^{2} \frac{1+\tau^{2}}{\tau^{2}}\right] .
\end{aligned}$$ We conclude that Bayes estimator for quadratic loss is $$T_{\text {Bayes }}=E(\theta \mid X)=\frac{\tau^{2} X+c}{\tau^{2}+1}$$