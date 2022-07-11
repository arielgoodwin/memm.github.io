---
layout: page
title: Proximal Operators 
usemathjax: true 
permalink: /prox/
---
<p style="text-align: center;">
[Energy](#energy) [Boltzmann-Shannon Entropy](#bsentropy) [Burg Entropy](#burg)
</p>

Consider the additive composite model \[[ \min \\{ f(x) + g(x) \colon x\in \mathbb{R}^d\\}\]]
where $f\colon \mathbb{R}^d \to (-\infty,+\infty]$ and $g\colon \mathbb{R}^d \to (-\infty,+\infty]$ are proper, closed, and convex functions. A variety of statistical estimation problems are encompassed by this model, and a particular method for solving this minimization is the
**Bregman Proximal Gradient (BPG) Algorithm**. The essential components of this method are a choice of **smooth adaptable kernel** and the definition of the **Bregman proximal operator**.

**Definition:** Let $f\colon \mathbb{R}^d \to (-\infty, +\infty]$ be a proper, closed function which is continuously differentiable on
$\text{int(dom}f)$. Then a
function $h\colon \mathbb{R}^d\to (-\infty, +\infty]$ of Legendre type$^1$ is a **smooth adaptable kernel** with respect to $f$ if 
dom $h \subseteq $ dom $f$ and there exists a constant $L > 0$ such that $Lh - f$ is convex.


**Definition:** Let $g\colon \mathbb{R}^d \to (-\infty, +\infty]$ and $h\colon \mathbb{R}^d\to (-\infty, +\infty]$ be two functions, where
the former is proper and closed while the latter is of Legendre type. Then the **Bregman proximal operator** is defined as 
\[[\text{prox}\_g^h(\bar{x}) := \text{argmin}\\{g(x) + h(x) - h(\bar{x}) - \langle \nabla h(\bar{x}), x-\bar{x}\rangle \colon x \in \mathbb{R}^d\\}\]]

Then a fruitful approach for solving the additive composite problem is to find $h$ that is smooth adaptable with respect to $f$ and simultaneously admits a computationally efficient proximal operator with respect to $g$. This leads to the following algorithm.

> Bregman Proximal Gradient (BPG) Algorithm <br> Initialization. Set $t\in (0,1/L]$ and $x^0 \in \text{int(dom}h)$<br> Procedure. For $k=0,1,2,...:$ \[[ x^{k+1} = \text{prox}\_{tg}^h(\nabla h^*(\nabla h(x^k)-t\nabla f(x^k)))\]]

Here we compile Bregman proximal operators for the Cramér functions of several popular distributions, with different choices of the smooth
adaptable kernel $h$. 

<a name="energy"></a>
# Smooth Adaptable Kernel: Energy $(h(x) = \frac{1}{2}\lVert x \rVert^2)$

| Reference Distribution | Proximal Operator | 
|:----------------------------:|:------------------------------------:|
|  Multivariate Normal $(\mu \in \mathbb{R}^d, \Sigma \in \mathbb{S}^d, \Sigma \succ 0$)| $x^+ = (tI +\Sigma)^{-1}(\Sigma\bar{x}+t\mu)$|
| Multivariate Normal-inverse Gaussian $(\mu,\beta \in \mathbb{R}^d, \alpha, \delta \in \mathbb{R}, \delta > 0,\\\\ \Sigma \in \mathbb{S}^d, \Sigma \succ 0, \alpha \geq \sqrt{\beta^T\Sigma \beta},\\\\ \gamma := \sqrt{\alpha^2 - \beta^T\Sigma \beta})$ | $x^+ = (I+\rho\Sigma^{-1})^{-1}(t\beta+\bar{x}+\rho\Sigma^{-1}\mu), \text{ where } \rho \in \mathbb{R}\_+\colon\\\\ (\rho\delta)^2 + \lVert (\rho^{-1}I+\Sigma^{-1})^{-1}(t\beta +\bar{x} - \mu\rVert\_{\Sigma^{-1}}^2 = (\alpha t)^2$|
|Gamma $(\alpha, \beta \in \mathbb{R}\_{++})$ | $x^+ = (\bar{x} - t\beta +\sqrt{(\bar{x}-t\beta)^2 + 4t\alpha})/2$|
|Laplace $(\mu \in \mathbb{R}, b \in \mathbb{R}\_{++})$| $x^+ = \begin{cases}\mu, &\bar{x} = \mu\\\\ \mu+b\rho,&\bar{x}\neq \mu\end{cases}\\\\ \text{ where } \rho \in \mathbb{R}\colon \alpha\_1\rho^3 + \alpha\_2\rho^2 +\alpha\_3\rho + \alpha\_4 = 0,\\\\ \text{ with } \alpha\_1 = (b/t)^2b^2, \alpha\_2 = 2(b/t)^2b(\mu-\bar{x}),\\\\ \alpha\_3 = (b/t)^2(\mu -\bar{x})^2 - 2(b/t)b -1, \alpha\_4 = -2(b/t)(\mu-\bar{x})$|
| Poisson $(\lambda \in \mathbb{R}_{++})$     | $x^+ \in \mathbb{R}\_+ \colon \log(x^+/\lambda) + (x^+-\bar{x})/t=0$|
| Multinomial $(p\in \Delta\_d, n\in \mathbb{N})$      | $x^+ \in n\Delta\_d\cap I(p) \colon (x\_i^+ -\bar{x}\_i)/t + \log\left(\frac{x\_i^+}{np\_i}\right)+1 +\lambda = 0$|
| Negative Multinomial $\\\\ (p \in [0,1)^d, x_0\in \mathbb{R}\_{++},\\\\ p_0 := 1-\sum\_{i=1}^{d}p_i)$      | $x^+\in\mathbb{R}\_+^d\cap I(p)\colon \log\left(\frac{x\_i^+}{p\_i\rho(x^+)}\right)+1 +(x\_i^+-\bar{x}\_i)/t = \frac{\bar{x}\_i+x\_0}{\rho(x^+)},\\\\ \text{where } \rho(x^+) := x\_0 + \sum\_{i=1}^d x\_i^+$|
| Discrete Uniform $(a,b\in \mathbb{Z}, a\leq b, \mu := (a+b)/2,\\\\ n := b-a+1)$      | $x^+ = \bar{x}-t\theta^+ \text{ where } \theta^+ = 0 \text{ if } \bar{x} = (a+b)/2, \\\\ \text{otherwise: }\theta^+ \in \mathbb{R}\setminus\\{0\\}:\\\\ t(\theta^+ -\bar{x}/t) + \frac{(b+1)e^{(b+1)\theta^+}-ae^{a\theta^+}}{e^{(b+1)\theta^+}-e^{a\theta^+}} = \frac{e^{\theta^+}}{e^{\theta^+}-1}$|
| Continuous Uniform $(a,b\in \mathbb{R}, a\leq b, \mu := (a+b)/2)$      | $x^+ = \bar{x}-t\theta^+ \text{ where } \theta^+ = 0 \text{ if } \bar{x} = (a+b)/2, \\\\ \text{otherwise: }\theta^+ \in \mathbb{R}\setminus\\{0\\}:\\\\ t(\theta^+ -\bar{x}/t) + \frac{ae^{a\theta^+}-be^{b\theta^+}}{e^{a\theta^+}-e^{b\theta^+}} = \frac{1}{\theta^+}$|
|  Logistic $(\mu \in \mathbb{R}, s\in \mathbb{R}_{++})$      | $x^+ = \bar{x} -t\theta^+ \text{ where } \theta^+ = 0 \text{ if } \bar{x} = \mu,\\\\ \text{otherwise: }\theta^+ \in \mathbb{R}\setminus\\{0\\}:\\\\ t\theta^+ + \frac{1}{\theta^+} + \frac{\pi s}{\tan(-\pi s \theta^+)} = \bar{x}-\mu$|

<a name="bsentropy"></a>
# Smooth Adaptable Kernel: Boltzmann-Shannon Entropy $(h(x) = -\sum\_{i=1}^d \log(x\_i))$

| Reference Distribution | Proximal Operator | 
|:----------------------------:|:------------------------------------:|
|  Multivariate Normal $(\mu, \sigma \in \mathbb{R}, \sigma > 0$)| $x^+ = ((t/\sigma)\mu -1/\bar{x} + \sqrt{((t/\sigma)\mu - 1/\bar{x})^2+4(t/\sigma)})/(2t/\sigma)$|
| Normal-inverse Gaussian $(\mu,\alpha,\beta,\delta \in \mathbb{R}, \delta > 0,\\\\ \alpha \geq \|\beta\|, \gamma := \sqrt{\alpha^2 - \beta^2})$ | $x^+ \in \mathbb{R}\_{++}: \\\\ t\alpha(x^+ - \mu)x^+ = ((t\beta -1/\bar{x})x^+ +1)\sqrt{\delta^2+(x^+-\mu)^2}$|
| Multivariate Normal-inverse Gaussian $(\mu,\beta \in \mathbb{R}^d, \alpha, \delta \in \mathbb{R}, \delta > 0,\\\\ \Sigma \in \mathbb{S}^d, \Sigma \succ 0, \alpha \geq \sqrt{\beta^T\Sigma \beta},\\\\ \gamma := \sqrt{\alpha^2 - \beta^T\Sigma \beta})$                            | $x\_i^+ = (w\_i +\rho \mu\_i + \sqrt{(w\_i +\rho\mu\_i)^2 + 4\rho}/(2\rho),\\\\ \text{with } w\_i=t\beta\_i -1/\bar{x}\_i \text{ and } \rho \in\mathbb{R}\_+ :\\\\ (\rho \delta)^2 + \frac{1}{4\sigma}\sum\_{i=1}^d(w\_i + \sqrt{(w\_i+\mu\_i\rho)^2+4\rho})^2 = (\alpha t/\sigma)^2$ |
|Gamma $(\alpha, \beta \in \mathbb{R}\_{++})$ | $x^+ = \bar{x}(t\alpha + 1)/(\bar{x}t\beta +1)$|
|Laplace $(\mu \in \mathbb{R}, b \in \mathbb{R}\_{++})$| $x^+ = \begin{cases}\mu, &\bar{x} = \mu\\\\ \mu+b\rho,&\bar{x}\neq \mu\end{cases}\\\\ \text{ where } \rho \in \mathbb{R}\_{++}\setminus\\{\mu/b\\}\colon \alpha\_1\rho^3 + \alpha\_2\rho^2 +\alpha\_3\rho + \alpha\_4 = 0,\\\\ \text{ with } \alpha\_1 = b^2((b/\bar{x})^2-t^2), \alpha\_2 = 2b(\mu((b/\bar{x})^2-t^2)-b^2(t+1)/\bar{x}),\\\\ \alpha\_3 = b^2((1-\mu/\bar{x})^2 + 2t(1-2\mu/\bar{x}))-t^2\mu^2 , \alpha\_4 = 2tb\mu(1-\mu/\bar{x})$|
| Poisson $(\lambda \in \mathbb{R}_{++})$     | $x^+ \in \mathbb{R}\_+ \colon t\log(x^+/\lambda) = \frac{1}{x^+} - \frac{1}{\bar{x}}$|
| Multinomial $(p\in \text{ri}\Delta\_d, n\in \mathbb{N})$      | $x^+ \in \text{ri}n\Delta\_d \colon t\left[\log\left(\frac{x\_i^+}{np\_i}\right)+1 \right] = \lambda + \frac{1}{x\_i^+} - \frac{1}{\bar{x}\_i}$|
| Negative Multinomial $\\\\ (p \in (0,1)^d, x_0\in \mathbb{R}\_{++},\\\\ p_0 := 1-\sum\_{i=1}^{d}p_i)$      | $x^+\in\mathbb{R}\_{++}\colon  t\log\left(\frac{x\_i^+}{p\_i\rho(x^+)}\right)+t  = t\frac{x\_i^+ +x\_0}{\rho(x^+)}+ \frac{1}{x\_i^+}-\frac{1}{\bar{x}\_i},\\\\ \text{where } \rho(x^+) := x\_0 + \sum\_{i=1}^d x\_i^+$|
| Discrete Uniform $(a,b\in \mathbb{Z}, a\leq b, \mu := (a+b)/2,\\\\ n := b-a+1)$      | $x^+ = \bar{x}/(t\bar{x}\theta^+ +1) \text{ where } \theta^+ = 0 \text{ if } \bar{x} = (a+b)/2, \\\\ \text{otherwise: }\theta^+ \in \mathbb{R}\setminus\\{0\\}:\\\\ \frac{(b+1)e^{(b+1)\theta^+}-ae^{a\theta^+}}{e^{(b+1)\theta^+}-e^{a\theta^+}} = \frac{e^{\theta^+}}{e^{\theta^+}-1} + \frac{\bar{x}}{t\bar{x}\theta^+ +1}$|
| Continuous Uniform $(a,b\in \mathbb{R}, a\leq b, \mu := (a+b)/2)$      | $x^+ = \bar{x}/(t\bar{x}\theta^+ +1) \text{ where } \theta^+ = 0 \text{ if } \bar{x} = (a+b)/2, \\\\ \text{otherwise: }\theta^+ \in \mathbb{R}\setminus\\{0\\}:\\\\ \frac{be^{b\theta^+}-ae^{a\theta^+}}{e^{b\theta^+}-e^{a\theta^+}} = \frac{1}{\theta^+} + \frac{\bar{x}}{t\bar{x}\theta^+ +1}$|
|  Logistic $(\mu \in \mathbb{R}, s\in \mathbb{R}_{++})$      | $x^+ = \bar{x}/(t\bar{x}\theta^+ +1) \text{ where } \theta^+ = 0 \text{ if } \bar{x} = \mu,\\\\ \text{otherwise: }\theta^+ \in \mathbb{R}\setminus\\{0\\}:\\\\ \frac{1}{\theta^+} + \frac{\pi s}{\tan(-\pi s \theta^+)} + \mu = \frac{\bar{x}}{\bar{x}t\theta^+ +1}$|


# Smooth Adaptable Kernel: Burg Entropy $(h(x) = \sum\_{i=1}^d x\_i\log x\_i)$
<a name="burg"></a>
