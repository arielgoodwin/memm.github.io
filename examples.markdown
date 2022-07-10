---
layout: page
title: Cramér Functions
usemathjax: true 
permalink: /examples/
---

**Definition:** Given a probability distribution $P$ on $\Omega$, the associated **Cramér rate function** is defined to be the convex conjugate of the log-normalizer:
 \[[ \psi^*_P(\theta) := \sup \\{ \langle y, \theta\rangle - \log M[\theta] \colon y\in \mathbb{R}^d\\} \]]
where \[[ M[\theta] = \int\_{\Omega} \exp(\langle \cdot,\theta\rangle) dP \]] is the moment-generating function of $P$.

**Table 1: Cramér rate functions for several popular parameterized distributions**
 
| Reference Distribution $(P)$ | Cramér Rate Function $(\psi^*_P(y))$ | $\text{dom}\psi^*_P$ |
|:----------------------------:|:------------------------------------:|:--------------------:|
|  Multivariate Normal $(\mu \in \mathbb{R}^d, \Sigma \in \mathbb{S}^d, \Sigma \succ 0$)      | $\frac{1}{2}(y-\mu)^T\Sigma^{-1}(y-\mu)$                                     |   $\mathbb{R}^d$                  |
| Multivariate Normal-inverse Gaussian $(\mu,\beta \in \mathbb{R}^d, \alpha, \delta \in \mathbb{R}, \delta > 0,\\\\ \Sigma \in \mathbb{S}^d, \Sigma \succ 0, \alpha \geq \sqrt{\beta^T\Sigma \beta},\\\\ \gamma := \sqrt{\alpha^2 - \beta^T\Sigma \beta})$                             | $\alpha\sqrt{\delta^2+ (y-\mu)^T\Sigma^{-1}(y-\mu)} - \langle \beta,y-\mu \rangle - \delta \gamma$                                     |   $\mathbb{R}$                   |
| Gamma $(\alpha, \beta \in \mathbb{R}_{++})$     |  $\beta y-\alpha +\alpha\log\left(\frac{\alpha}{\beta y}\right)$            |  $\mathbb{R}_{++}$                    |
| Laplace $(\mu \in \mathbb{R}, b \in \mathbb{R}_{++})$     |  $\begin{cases} 0, &y-\mu\\\\ \sqrt{1+\rho(y)^2} -1 + \log\left( \frac{\sqrt{1+\rho(y)^2}-1}{\rho(y)^2/2}\right), &y\neq \mu \end{cases}\\\\ (\rho(y) := (y-\mu)/b)$            |  $\mathbb{R}$                    |
| Poisson $(\lambda \in \mathbb{R}_{++})$     |  $y\log(y/\lambda) - y + \lambda$            |  $\mathbb{R}_{+}$                    |
| Multinomial $(p\in \Delta_d, n\in \mathbb{N})$      |  $\sum_{i=1}^dy_i\log\left(\frac{y_i}{n p_i}\right)$            |  $n\Delta_d \cap I(p)$                    |
| Negative Multinomial $\\\\ (p \in [0,1)^d, y_0\in \mathbb{R}\_{++},\\\\ p_0 := 1-\sum\_{i=1}^{d}p_i)$      |  $\sum_{i=0}^dy_i\log\left(\frac{y_i}{p_i \bar{y}}\right) \;\; (\bar{y}:= \sum_{i=0}^dy_i)$            |  $\mathbb{R}^d_{+} \cap I(p)$                    |
| Discrete Uniform $(a,b\in \mathbb{Z}, a\leq b, \mu := (a+b)/2,\\\\ n := b-a+1)$      |  $\begin{cases} 0, &y-\mu\\\\ (y-\mu)\theta - \log\left(\frac{e^{(b-\mu +1)\theta}-e^{(a-\mu)\theta}}{n(e^{\theta}-1)}\right), &y\neq \mu \end{cases}\\\\ \text{where } \theta \in \mathbb{R} \colon y + \frac{e^\theta}{e^\theta -1} = \frac{(b+1)e^{(b+1)\theta}-ae^{a\theta}}{e^{(b+1)\theta}-e^{a\theta}}$            |  $[a,b]$                    |
| Continuous Uniform $\\\\(a,b\in \mathbb{R}, a< b, \mu := (a+b)/2)$      |  $\begin{cases} 0, &y-\mu\\\\ (y-\mu)\theta - \log\left(\frac{e^{(b-\mu)\theta}-e^{(a-\mu)\theta}}{(b-a)\theta}\right), &y\neq \mu \end{cases}\\\\ \text{where } \theta \in \mathbb{R} \colon y + \frac{1}{\theta} = \frac{be^{b\theta}-ae^{a\theta}}{e^{b\theta}-e^{a\theta}}$            |  $(a,b)$                    |
|  Logistic $(\mu \in \mathbb{R}, s\in \mathbb{R}_{++})$      |  $\begin{cases} 0, &y-\mu\\\\ (y-\mu)\theta - \log\left(B(1-s\theta,1+s\theta)\right), &y\neq \mu \end{cases}\\\\ \text{where } \theta \in \mathbb{R}_+ \colon y -\mu = \frac{1}{\theta} + \frac{\pi s}{\tan(-\pi s\theta)}$            |  $\mathbb{R}$                    |

Note: 
- Chi-squared, Erlang, and Exponential distributions are special cases of the Gamma distribution
- Binomial, Bernoulli, and Categorical distributions are special cases of the Multinomial distribution
- Negative Binomial and (Shifted) Geometric distributions are special cases of the Negative Multinomial Distribution


