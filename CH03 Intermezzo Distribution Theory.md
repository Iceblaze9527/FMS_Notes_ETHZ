---
tags: FMS
---

# CH03 Intermezzo: Distribution Theory
## 3.1 Concepts
### 3.1.1 Conditional Density and Expcts
#### Cond Density
The conditional density of $X$ given $Y=y$ is $$f_{X}(x \mid y):=\frac{f_{X, Y}(x, y)}{f_{Y}(y)}, x \in \mathbb{R}^{n}$$ Thus, we have $$f_{Y}(y \mid x)=f_{X}(x \mid y) \frac{f_{Y}(y)}{f_{X}(x)},(x, y) \in \mathbb{R}^{n+m}$$ and $$f_{X}(x)=\int f_{X}(x \mid y) f_{Y}(y) d y, x \in \mathbb{R}^{n}$$

#### Cond Expct
Let $g: \mathbb{R}^{n} \times \mathbb{R}^{m} \rightarrow \mathbb{R}$ be some function. The conditional expectation of $g(X, Y)$ given $Y=y$ is $$E[g(X, Y) \mid Y=y]:=\int f_{X}(x \mid y) g(x, y) d x$$ Note thus that $$E\left[g_{1}(X) g_{2}(Y) \mid Y=y\right]=g_{2}(y) E\left[g_{1}(X) \mid Y=y\right]$$ Notation We define the random variable $E[g(X, Y) \mid Y]$ as $$E[g(X, Y) \mid Y]:=h(Y),$$ where $h(y)$ is the function $h(y):=E[g(X, Y) \mid Y=y]$.

### 3.1.2 Multinomial Distribution
We say that the random vector $\left(N_{1}, \ldots, N_{k}\right)$ has the multinomial distribution with parameters $n$ and $p_{1}, \ldots, p_{k}\left(\right.$ with $\left.\sum_{j=1}^{k} p_{j}=1\right)$, if for all $\left(n_{1}, \ldots, n_{k}\right) \in\{0, \ldots, n\}^{k}$, with $n_{1}+\cdots+n_{k}=n$, it holds that $$P\left(N_{1}=n_{1}, \ldots, N_{k}=n_{k}\right)=\left(\begin{array}{cc}n & \\ n_{1} & \cdots & n_{k}
\end{array}\right) p_{1}^{n_{1}} \cdots p_{k}^{n_{k}}$$ Here $$\left(\begin{array}{c}n \\ n_{1} \cdots n_{k}\end{array}\right):=\frac{n !}{n_{1} ! \cdots n_{k} !}$$

### 3.1.3 The Poisson distribution
A random variable $X \in\{0,1, \ldots\}$ has the Poisson distribution with parameter $\lambda>0$, if for all $x \in\{0,1, \ldots\}$ $$P(X=x)=\mathrm{e}^{-\lambda} \frac{\lambda^{x}}{x !}$$

### 3.1.4 Characteristic Function: Fourier Transformation of Mass/Density Function
$$\left\{\begin{array}{l}
\varphi_{X}: \mathbb{R} \rightarrow \mathbb{C} \\
\varphi_{X}(t)=\mathrm{E}\left[e^{i t X}\right]=\int_{\mathbb{R}} e^{i t x} d F_{X}(x)=\int_{\mathbb{R}} e^{i t x} f_{X}(x) d x
\end{array}\right.
$$

- Correspondence btwn c.f. $\mathbb{E}(e^{itX})$ and d.f $F(\cdot)$ is unique
- $\mathcal{\varphi}_{\sum_{i}X}(t) = \prod_{i}\varphi_X(t)$ (Convolution Theorem: Proved by Fubini's Theorem)

:::warning
**How to compute the distrib of summed independent r.v.'s:**
- Calculate/Lookup their characteristic funcs
- Calculate their products
- Look up which distribution has this characteristic function
:::

## 3.2 Lemmas
### Lemma 3.1.1: Iterated expectations lemma
It holds that $$E[E[g(X, Y) \mid Y]]=E g(X, Y)$$

#### Proof
Define $$ h(y):=E[g(X, Y) \mid Y=y] $$ Then $$ \begin{aligned} E h(Y) &=\int h(y) f_{Y}(y) d y=\int E[g(X, Y) \mid Y=y] f_{Y}(y) d y \\
&=\iint g(x, y) f_{X, Y}(x, y) d x d y=E g(X, Y)
\end{aligned}$$

### Lemma 3.2.1 The marginal distribution of Multinomial Distribution
Suppose $X$ follows multinomial distribution. The marginal distribution of $X$ is the Binomial $\left(n, p_{1}\right)$-distribution. 

#### Proof
For $x \in\{0, \ldots, n\}$, we have $$\begin{aligned}
P(X=x) &=\sum_{y=0}^{n-x} P(X=x, Y=y, Z=n-x-y) \\ &=\sum_{y=0}^{n-x}\left(\begin{array}{c}n \\ x y n-x-y\end{array}\right) p_{1}^{x} p_{2}^{y}\left(1-p_{1}-p_{2}\right)^{n-x-y} \\&=\left(\begin{array}{l}
n \\x\end{array}\right) p_{1}^{x} \sum_{y=0}^{n-x}\left(\begin{array}{c}
n-x \\ y \end{array}\right) p_{2}^{y}\left(1-p_{1}-p_{2}\right)^{n-x-y} \\
&=\left(\begin{array}{l}n \\ x \end{array}\right) p_{1}^{x}\left(1 - p_{1}\right)^{n-x}\end{aligned} $$

### Lemma 3.3.1 The distribution of the sum of two Possion r.v.'s
Suppose $X$ and $Y$ are independent, and that $X$ has the Poisson $(\lambda)$ distribution, and $Y$ the Poisson( $\mu$ )-distribution. Then $Z:=X+Y$ has the Poisson $(\lambda+\mu)$-distribution.

#### Proof
For all $z \in\{0,1, \ldots\}$, we have $$\begin{aligned}
P(Z=z) &=\sum_{x=0}^{z} P(X=x, Y=z-x) \\
&=\sum_{x=0}^{z} P(X=x) P(Y=z-x) \\
&=\sum_{x=0}^{z} \mathrm{e}^{-\lambda} \frac{\lambda^{x}}{x !} \mathrm{e}^{-\mu} \frac{\mu^{z-x}}{(z-x) !} \\
&=\mathrm{e}^{-(\lambda+\mu)} \frac{1}{z !} \sum_{x=0}^{z}\left(\begin{array}{l}z \\x
\end{array}\right) \lambda^{x} \mu^{z-x} \\
&=\mathrm{e}^{-(\lambda+\mu)} \frac{(\lambda+\mu)^{z}}{z !}
\end{aligned}$$

### Lemma 3.3.2 The distribution of the sum of multiple Possion r.v.'s
Let $X_{1}, \ldots, X_{n}$ be independent, and (for $i=1, \ldots, n$ ), let $X_{i}$ have the Poisson $\left(\lambda_{i}\right)$-distribution. Define $Z:=\sum_{i=1}^{n} X_{i}$. Let $z \in\{0,1, \ldots\}$. Then the conditional distribution of $\left(X_{1}, \ldots, X_{n}\right)$ given $Z=z$ is the multinomial distribution with parameters $z$ and $p_{1}, \ldots, p_{n}$, where$$p_{j}=\frac{\lambda_{j}}{\sum_{i=1}^{n} \lambda_{i}}, j=1, \ldots, n$$

#### Proof
First note that $Z$ is Poisson $\left(\lambda_{+}\right)$-distributed, with $\lambda_{+}:=\sum_{i=1}^{n} \lambda_{i}$. Thus, for all $\left(x_{1}, \ldots, x_{n}\right) \in\{0,1, \ldots, z\}^{n}$ satisfying $\sum_{i=1}^{n} x_{i}=z$, we have $$\begin{aligned}
P\left(X_{1}=x_{1}, \ldots, X_{n}=x_{n} \mid Z=z\right) &=\frac{P\left(X_{1}=x_{1}, \ldots, X_{n}=x_{n}\right)}{P(Z=z)} \\
&=\frac{\prod_{i=1}^{n}\left(\mathrm{e}^{-\lambda_{i}} \lambda_{i}^{x_{i}} / x_{i} !\right)}{\mathrm{e}^{-\lambda_{+} \lambda_{+}^{z} / z !}} \\
&=\left(\begin{array}{c}
z \\
x_{1} \cdots x_{n}
\end{array}\right)\left(\frac{\lambda_{1}}{\lambda_{+}}\right)^{x_{1}} \cdots\left(\frac{\lambda_{n}}{\lambda_{+}}\right)^{x_{n}} .
\end{aligned}$$

### Lemma 3.4.1 The distribution of the maximum of two random variables
Let $X_{1}$ and $X_{2}$ be independent and both have distribution $F$. Suppose that $F$ has density $f$ w.r.t. Lebesgue measure. Let $$Z:=\max \left\{X_{1}, X_{2}\right\}$$ The distribution function of $Z$ is $F^{2}$. Moreover, $Z$ has density $f_{Z}(z)=2 F(z) f(z), z \in \mathbb{R}$

#### Proof. 
We have for all $z$, $$\begin{aligned} P(Z \leq z) &=P\left(\max \left\{X_{1}, X_{2}\right\} \leq z\right) \\ &=P\left(X_{1} \leq z, X_{2} \leq z\right)=F^{2}(z)\end{aligned}$$ If $F$ has density $f$, then (Lebesgue)-almost everywhere, $$f(z)=\frac{d}{d z} F(z)$$ So the derivative of $F^{2}$ exists almost everywhere, and $$\frac{d}{d z} F^{2}(z)=2 F(z) f(z)$$

#### Corollary
The conditional distribution function of $X_{1}$ given $Z=z$ is$$
F_{X_{1}}\left(x_{1} \mid z\right)= \begin{cases}\frac{F\left(x_{1}\right)}{2 F(z)}, & x_{1}<z \\ 1, & x_{1} \geq z\end{cases}$$ Note thus that this distribution has a jump of size $\frac{1}{2}$ at $z$.

## 3.3 Key Takeaways & Common Tricks


## 3.4 Examples
### Example 3.2.1 Histograms
Let $X_{1}, \ldots, X_{n}$ be i.i.d. copies of a random variable $X \in \mathbb{R}$ with distribution $F$, and let $\underline{-\infty=a_{0}<a_{1}<\cdots<a_{k-1}<a_{k}=\infty}$. Define, for $j=1, \ldots, k$,
$$
\left\{\begin{aligned}
p_{j} &:=P\left(X \in\left(a_{j-1}, a_{j}\right]\right)=F\left(a_{j}\right)-F\left(a_{j-1}\right), \\
\frac{N_{j}}{n} &:=\frac{\#\left\{X_{i} \in\left(a_{j-1}, a_{j}\right]\right\}}{n}=\hat{F}_{n}\left(a_{j}\right)-\hat{F}_{n}\left(a_{j-1}\right) .
\end{aligned}\right.
$$
Then $\left(N_{1}, \ldots, N_{k}\right)$ has the Multinomial $\left(n, p_{1}, \ldots, p_{k}\right)$-distribution.