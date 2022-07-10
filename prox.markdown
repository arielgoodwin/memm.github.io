---
layout: page
title: Proximal Operators 
usemathjax: true 
permalink: /prox/
---

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

**Proximal operators for the Normal Linear Model $(h = \frac{1}{2}\lVert\cdot \rVert^2)$**
 
| Reference Distribution | Proximal Operator | 
|:----------------------------:|:------------------------------------:|
|  Multivariate Normal $(\mu \in \mathbb{R}^d, \Sigma \in \mathbb{S}^d, \Sigma \succ 0$)      | $x^+ = (tI +\Sigma)^{-1}(\Sigma\bar{x}+t\mu)$|| Multivariate Normal-inverse Gaussian $(\mu,\beta \in \mathbb{R}^d, \alpha, \delta \in \mathbb{R}, \delta > 0,\\\\ \Sigma \in \mathbb{S}^d, \Sigma \succ 0, \alpha \geq \sqrt{\beta^T\Sigma \beta},\\\\ \gamma := \sqrt{\alpha^2 - \beta^T\Sigma \beta})$             | x^+ = (I+\rho\Sigma^{-1})^{-1}(t\beta+\bar{x}+\rho\Sigma^{-1}\mu), \text{ where } \rho \in \mathbb{R}\_+\colon\\\\ (\rho\delta)^2 + \lVert (\rho^{-1}I+\Sigma^{-1})^{-1}(t\beta +\bar{x} - \mu\rVert\_{\Sigma^{-1}}^2 = (\alpha t)^2$|

