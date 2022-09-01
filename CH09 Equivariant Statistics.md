---
tags: FMS
---

# CH09 Equivariant Statistics
## 9.1 Concepts
> In this section we abbreviate location equivariance (invariance) to simply equivariance (invariance), and we assume throughout that the loss $L(\theta, a)$ is invariant.

### 9.1.1 Equivariance
A ==statistic== $T=T(\mathbf{X})$ is called ==location equivariant== if for all constants $c \in \mathbb{R}$ and all $\mathbf{x}=\left(x_{1}, \ldots, x_{n}\right)$, $$T\left(x_{1}+c, \ldots, x_{n}+c\right)=T\left(x_{1}, \ldots, x_{n}\right)+c$$

### 9.1.2 Invariance
A ==loss function== $L(\theta, a)$ is called location invariant if for all $c \in \mathbb{R}$, $$L(\theta+c, a+c)=L(\theta, a),(\theta, a) \in \mathbb{R}^{2}$$ 

#### Maximal Invariant Statistics
A map $\mathbf{Y}: \mathbb{R}^{n} \rightarrow \mathbb{R}^{n}$ is called maximal invariant if $\mathbf{Y}(\mathbf{x})=\mathbf{Y}\left(\mathbf{x}^{\prime}\right) \Leftrightarrow \exists c \in \mathbb{R}: \mathbf{x}=\mathbf{x}^{\prime}+c .$
(The constant c may depend on $\mathbf{x}$ and $\mathbf{x}^{\prime}$ )

### 9.1.3 UMRE Estimator
An equivariant statistic $T$ is called uniform minimum risk equivariant (UMRE) if $$R(\theta, T)=\min _{d \text { equivariant }} R(\theta, d), \forall \theta,$$ or equivalently, $$R(0, T)=\min _{d \text { equivariant }} R(0, d)$$

## 9.2 Corollaries and Lemmas
### Corollary 9.1.1 (For location model)
If $T$ is equivariant (and $L(\theta, a)$ is invariant), then $$
\begin{aligned}R(\theta, T) &=E_{\theta} L(\theta, T(\mathbf{X}))=E_{\theta} L(0, T(\mathbf{X})-\theta) \\&=E_{\theta} L(0, T(\mathbf{X}-\theta))=E_{\theta} L_{0}[T(\varepsilon)]
\end{aligned}$$ where $L_{0}[a]:=L(0, a)$ and $\varepsilon:=\left(\epsilon_{1}, \ldots, \epsilon_{n}\right)$. 

Because the distribution of $\varepsilon$ does not depend on $\theta$, we conclude that ==the risk does not depend on $\theta$.== 

We may therefore omit the subscript $\theta$ in the last expression: $$R(\theta, T)=E L_{0}[T(\varepsilon)]$$ Since for $\theta=0$, we have the equality $\mathbf{X}=\varepsilon$ we may alternatively write $$R(\theta, T)=E_{0} L_{0}[T(\mathbf{X})]=R(0, T)$$

### Theorem 9.1.1 Construction of UMRE Estimator
Let $Y_{i}:=X_{i}-X_{n}, i=1, \ldots, n, \mathbf{Y}:=\left(Y_{1}, \ldots, Y_{n}\right)$, and define $$T^{*}(\mathbf{Y}):=\arg \min _{v} E\left[L_{0}\left(v+\epsilon_{n}\right) \mid \mathbf{Y}\right]$$ Moreover, let $$T^{*}(\mathbf{X}):=T^{*}(\mathbf{Y})+X_{n}$$ Then $T^{*}$ is UMRE.

#### 1. Lemma 9.1.1 Equivariance of the estimator
Let $Y_{i}:=X_{i}-X_{n}, i=1, \ldots, n$, and $\mathbf{Y}:=\left(Y_{1}, \ldots, Y_{n}\right) .$ We have $T$ equivariant $\Leftrightarrow T(\mathbf{X})=T(\mathbf{Y})+X_{n}$

#### 2. Corollary 9.1.2 Quadratic loss: the Pitman estimator
If we take quadratic loss $$L(\theta, a):=(a-\theta)^{2},$$ we get $L_{0}[a]=a^{2}$, and so, for $\mathbf{Y}=\mathbf{X}-X_{n}$, $$\begin{aligned}
T^{*}(\mathbf{Y}) &=\arg \min _{v} E\left[\left(v+\epsilon_{n}\right)^{2} \mid \mathbf{Y}\right] \\ &=-E\left(\epsilon_{n} \mid \mathbf{Y}\right)\end{aligned}$$ and hence $$T^{*}(\mathbf{X})=X_{n}-E\left(\epsilon_{n} \mid \mathbf{Y}\right)$$ This estimator is called the Pitman estimator.

#### 3. Lemma 9.1.2 Analytical Form of the Pitman estimator
Let $\mathbf{p}_{0}$ be the density of $\varepsilon=\left(\epsilon_{1}, \ldots, \epsilon_{n}\right)$ w.r.t. Lebesgue measure. Then a UMRE statistic is $$T^{*}(\mathbf{X})=\frac{\int z \mathbf{p}_{0}\left(X_{1}-z, \ldots, X_{n}-z\right) d z}{\int \mathbf{p}_{0}\left(X_{1}-z, \ldots, X_{n}-z\right) d z}$$

### Theorem 9.1.2 Construction of UMRE Estimator using Equivariant estimator
Suppose that $d(\mathbf{X})$ is equivariant. Let $\mathbf{Y}:=\mathbf{X}-d(\mathbf{X})$, and $$T^{*}(\mathbf{Y}):=\arg \min _{v} E\left[L_{0}(v+d(\varepsilon)) \mid \mathbf{Y}\right]$$ Then $$T^{*}(\mathbf{X}):=T^{*}(\mathbf{Y})+d(\mathbf{X}) $$ is UMRE.

#### 1. Lemma: Equivariance
Let $d(X)$ equivariant, and $Y=X-d(X)$. Then $T$ equivariant $\Leftrightarrow T(X)=T(Y)+d(X)$

#### 2. Quadratic loss
For quadratic loss $\left(L_{0}[a]=a^{2}\right)$, the definition of $T^{*}(\mathbf{Y})$ in the above theorem is $$ T^{*}(\mathbf{Y})=-E(d(\varepsilon) \mid \mathbf{Y})=-E_{0}(d(\mathbf{X}) \mid \mathbf{X}-d(\mathbf{X})),$$ so that $$T^{*}(\mathbf{X})=d(\mathbf{X})-E_{0}(d(\mathbf{X}) \mid \mathbf{X}-d(\mathbf{X}))$$

### Basu's Lemma
Let $X$ have distribution $P_{\theta}, \theta \in \Theta$. Suppose $T$ is sufficient and complete, and that $Y=Y(X)$ has a distribution that does not depend on $\theta$. Then, for all $\theta, T$ and $Y$ are independent under $P_{\theta}$.

:::warning
**Remark**
Basu's lemma is intriguing: it proves a probabilistic property (independence)
via statistical concepts.
:::

#### Proof. 
Let $A$ be some measurable set, and $$h(T):=P(Y \in A \mid T)-P(Y \in A)$$ Notice that indeed, $P(Y \in A \mid T)$ does not depend on $\theta$ because $T$ is sufficient. and $P(Y \in A)$ is by definition independent of $\theta$. Because $$E_{\theta} h(T)=0, \forall \theta,$$ we conclude from the completness of $T$ that $$h(T)=0, P_{\theta}-\text { a.s. }, \forall \theta,$$ in other words, $$ P(Y \in A \mid T)=P(Y \in A), P_{\theta}-\text { a.s., } \forall \theta$$ Since $A$ was arbitrary, we thus have that the conditional distribution of $Y$ given $T$ is equal to the unconditional distribution: $$P(Y \in \cdot \mid T)=P(Y \in \cdot), P_{\theta}-\text { a.s., } \forall \theta,$$ that is, for all $\theta, T$ and $Y$ are independent under $P_{\theta}$.

### 9.1.4 Construction of UMRE via sufficient and complete unbiased statistic
Suppose statistic $T$: $\left.\begin{array}{l}\text { unbiased } \\ \text { sufficient } \\ \text { complete } \\ \text { equivariant }\end{array}\right\} \Rightarrow T$ UMRE

#### Proof Sketch
$$
T^{*}(\mathbf{X})=d(\mathbf{X})-E_{0}(d(\mathbf{X}) \mid \mathbf{X}-d(\mathbf{X}))
$$ 
Unbiasedness leads to $E_{0} T=0$ and hence $E_{\theta}(T)=\theta$ $\forall \theta$. According to Basu's lemma, $Y=X-T(X)$ & $T(X)$ are independent. Thus $$ E_{0}(T(\mathbf{X}) \mid \mathbf{X}-T(\mathbf{X}))=E_{0} T(\mathbf{X})=0$$ So then $T$ is UMRE.

## 9.4 Examples
### Ex 9.1.1 UMRE for Uniform distribution with unknown midpoint
Suppose $X_{1}, \ldots, X_{n}$ are i.i.d. Uniform $[\theta-1 / 2, \theta+1 / 2], \theta \in \mathbb{R}$. Then $$\begin{gathered}p_{0}(x)=1\{|x| \leq 1 / 2\} . \\\max _{1 \leq i \leq n}\left|x_{i}-z\right| \leq 1 / 2 \Leftrightarrow x_{(n)} \mid-1 / 2 \leq z \leq x_{(1)}+1 / 2\end{gathered} $$ We have $$
\mathbf{p}_{0}\left(x_{1}-z, \ldots, x_{n}-z\right)=1\left\{x_{(n)}-1 / 2 \leq z \leq x_{(1)}+1 / 2\right\}$$ Thus, writing $$T_{1}:=X_{(n)}-1 / 2, T_{2}:=X_{(1)}+1 / 2$$ the UMRE estimator (against quadratic loss) $T^{*}$ is $$T^{*}=\left(\int_{T_{1}}^{T_{2}} z d z\right) /\left(\int_{T_{1}}^{T_{2}} d z\right)=\frac{T_{1}+T_{2}}{2}=\frac{X_{(1)}+X_{(n)}}{2}$$

### Ex 9.1.2 UMRE estimator for the mean of the normal distribution: $\sigma^{2}$ known

Let $X_{1}, \ldots, X_{n}$ be independent $\mathcal{N}\left(\theta, \sigma^{2}\right)$, with $\sigma^{2}$ known. Then $T:=\bar{X}$ is sufficient and complete, and moreover, the distribution of $\mathbf{Y}:=\mathbf{X}-\bar{X}$ does not depend on $\theta$. So by Basu's lemma, $\bar{X}$ and $\mathbf{X}-\bar{X}$ are independent. Hence, $\bar{X}$ is UMRE.

:::warning
**Remark**
- Indeed, Basu's lemma is peculiar: $\bar{X}$ and $\mathbf{X}-\bar{X}$ of course remain independent if the mean $\theta$ is known and/or the variance $\sigma^{2}$ is unknown! (independence does not rely on what params you know or not)
- As a by-product, one concludes the independence of $\bar{X}$ and the sample variance $S^{2}=\sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2} /(n-1)$, because $S^{2}$ is a function of $\mathbf{X}-\bar{X}$.

:::
