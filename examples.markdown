---
layout: page
title: Examples
usemathjax: true 
permalink: /examples/
---

## Cramér Function

**Definition:** Given a probability distribution $P$, the associated Cramér function is defined to be the convex conjugate of the log-normalizer:
 \[[ \psi^*_P(\theta) := \sup \\{ \langle y, \theta\rangle - \log M[\theta] \colon y\in \mathbb{R}^d\\} \]]
where \[[ M[\theta] = \int \exp(\langle \cdot,\theta\rangle) dP \]] is the moment-generating function of $P$.

Examples: 

| Reference Distribution $(P)$ | Cramér Rate Function $(\psi^*_P(y))$ | $\text{dom}\psi^*_P$ |
|:----------------------------:|:------------------------------------:|:--------------------:|
|  Multivariate Normal $(\mu \in \mathbb{R}^d, \Sigma \in \mathbb{S}^d, \Sigma \succ 0$)      | $\frac{1}{2}(y-\mu)^T\Sigma^{-1}(y-\mu)$                                     |   $\mathbb{R}^d$                  |
| Multivariate Normal-inverse Gaussian $(\mu,\beta \in \mathbb{R}^d, \alpha, \delta \in \mathbb{R}, \delta > 0,\\\\ \Sigma \in \mathbb{S}^d, \Sigma \succ 0, \alpha \geq \sqrt{\beta^T\Sigma \beta},\\\\ \gamma := \sqrt{\alpha^2 - \beta^T\Sigma \beta})$                             | $\alpha\sqrt{\delta^2+ (y-\mu)^T\Sigma^{-1}(y-\mu)} - \langle \beta,y-\mu \rangle - \delta \gamma$                                     |   $\mathbb{R}$                   |
| Gamma $(\alpha, \beta \in \mathbb{R}_{++})$     |  $\beta y-\alpha +\alpha\log\left(\frac{\alpha}{\beta y}\right)$            |  $\mathbb{R}_{++}$                    |
| Laplace $(\mu \in \mathbb{R}, b \in \mathbb{R}_{++})$     |  $\begin{cases} 0, &y-\mu\\\\ \sqrt{1+\rho(y)^2} -1 + \log\left( \frac{\sqrt{1+\rho(y)^2}-1}{\rho(y)^2/2}\right), &y\neq \mu \end{cases}\\\\ (\rho(y) := (y-\mu)/b)$            |  $\mathbb{R}$                    |
| Poisson $(\lambda \in \mathbb{R}_{++})$     |  $y\log(y/\lambda) - y + \lambda$            |  $\mathbb{R}_{+}$                    |

