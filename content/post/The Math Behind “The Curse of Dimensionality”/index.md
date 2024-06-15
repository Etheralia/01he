---
title: n球的体积
summary: 这篇文章是我在知乎上的文章“维数灾难背后的数学”的延伸。在这里，我将使用积分微积分和Wallis积分推导出n球的体积公式。
date: 2024-6-15

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com)'

authors:
  - 二进制何

tags:
  - Academic
  - Hugo Blox
  - Markdown
---

Welcome 👋

{{< toc mobile_only=true is_open=true >}}

# n球的体积

## 介绍

这篇文章是我在知乎上的文章“维数灾难背后的数学”的延伸。在这里，我将使用积分微积分和Wallis积分推导出n球的体积公式。

n球是将普通“球”推广到任意维度的概念。它定义为n维欧几里得空间中距离中心点（我们将考虑原点0）固定距离的点集。n球在机器学习和数据分析中具有重要应用。

n球的方程如下：

$$
x_{1}^{2}+x_{2}^{2}+\ldots+x_{N}^{2} \leq r^{2}
$$

其中r是球的半径。

## 体积公式的推导

n球最重要的性质之一是它的体积。半径为r的n球的体积公式如下：

$$
V_{N}(r)=\frac{\pi^{(N+1) / 2}}{\Gamma((N+1) / 2)} r^{N+1}
$$

其中$\Gamma$是伽马函数。在本文的其余部分，我们将推导出这个公式。

我们将单位（半径等于1）的n球定义为以下空间：$\mathcal{B}_{n}=\left\{x_{1}, \ldots, x_{m} ; \sum_{i=1}^{n} x_{i}^{2} \leq 1\right\}$

我们记$V_{n}=V_{n}(1)$为这个球的体积。更一般地，$V_{n}(R)$为半径为R的n球的体积。从现在开始，我们将使用$V_{n}$来指代单位n球的体积：

$$
V_{n}=\int_{x \in \mathcal{B}_{n}} d x_{1} d x_{2} \ldots d x_{n}
$$

首先，注意到半径为R的n球的体积是$R^{n} V_{n}$：只需在$V_{n}(R)$的表达式中使用变量变换$y_{i} \leftarrow x_{i} / R$。现在，让我们简化$V_{n}$：

$$
\begin{aligned}
V_{n} & =\int_{x_{1}^{2}+\cdots+x_{n}^{2} \leq 1} d x_{1} d x_{2} \ldots d x_{n} \\
& =\int_{x_{1}^{2} \leq 1}\left(\int_{x_{2}^{2}+\cdots+x_{n}^{2} \leq 1-x_{1}^{2}} d x_{2} \ldots d x_{n}\right) d x_{1} \\
& =\int_{x_{1}^{2} \leq 1} V_{n-1}\left(\sqrt{1-x_{1}^{2}}\right) d x_{1}
\end{aligned}
$$

我们现在可以用之前的关系替换半径为$\sqrt{1-x_{1}^{2}}$的$n-1$球的体积表达式：

$$
\begin{aligned}
V_{n} & =\int_{x_{1}^{2} \leq 1} V_{n-1}\left(\sqrt{1-x_{1}^{2}}\right) d x_{1} \\
& =V_{n-1} \int_{x_{1}^{2} \leq 1}\left(\sqrt{1-x^{2}}\right)^{n-1} d x_{1} \\
& =V_{n-1} \int_{-1}^{1}\left(\sqrt{1-x^{2}}\right)^{n-1} d x
\end{aligned}
$$

我们用变量变换$x=\cos (\theta)$（所以$d x=-\sin (\theta) d \theta$）来简化积分：

$$
\begin{aligned}
V_{n} & =V_{n-1} \int_{-1}^{1}\left(\sqrt{1-x^{2}}\right)^{n-1} d x \\
& =-V_{n-1} \int_{\pi}^{0} \sin ^{n-1}(\theta) \sin (\theta) d \theta \\
& =V_{n-1} \int_{0}^{\pi} \sin ^{n}(\theta) d \theta \\
& =2 V_{n-1} \int_{0}^{\pi / 2} \sin ^{n}(\theta) d \theta \\
& =I_{n} V_{n-1}
\end{aligned}
$$

我们记$I_{n}=2 \int_{0}^{\pi / 2} \sin ^{n}(\theta) d \theta$

注意$\int_{0}^{\pi / 2} \sin ^{n}(\theta) d \theta$是数学中著名的积分：它被称为Wallis积分，通常用$W_{n}$表示。它可以通过分部积分推导出来（我将在附录中证明这个公式）。根据n的奇偶性，积分可以表示为：

$W_{2 p}=\frac{\pi}{2} \frac{(2 p)!}{2^{2 p}(p!)^{2}}$ 和 $W_{2 p+1}=\frac{2^{2 p}(p!)^{2}}{(2 p+1)!}$

使用我们的递归关系，我们知道：$V_{n}=I_{n} I_{n-1} \ldots I_{2} V_{1}$ 而 $V_{1}=V_{1}(1)=2$（线段$[-1,1]$的长度）。

我们将利用一个非常有用的性质：

$$
I_{2 p} I_{2 p+1}=4 W_{2 p} W_{2 p+1}=\frac{\pi}{2} \frac{(2 p)!}{2^{2 p}(p!)^{2}} \frac{2^{2 p}(p!)^{2}}{(2 p+1)!}=\frac{2 \pi}{2 p+1}=\frac{\pi}{p+1 / 2}
$$

我们还需要伽马函数。你只需了解这两个表达式

$$
\Gamma(n)=(n-1)!
$$

和

$$
\Gamma(n+1 / 2)=(n-1 / 2) \times \cdots \times 1 / 2 \times \pi^{1 / 2}
$$

现在，我们可以通过分组连续项来轻松计算$V_{n}$，再次取决于n的奇偶性。

$$
\begin{aligned}
V_{2 p} & =I_{2 p} I_{2 p-1} \ldots I_{2} V_{1} \\
& =I_{2 p}\left(I_{2 p-1} I_{2 p-2}\right) \ldots\left(I_{3} I_{2}\right) \times 2 \\
& =\pi \times \frac{(2 p)!}{2^{2 p}(p!)^{2}} \times \frac{\pi}{p-1 / 2} \times \frac{\pi}{p-3 / 2} \times \cdots \times \frac{\pi}{3 / 2} \times \frac{\pi}{1 / 2} \\
& =\frac{(2 p)!}{2^{p}(p!)^{2}} \times \frac{\pi^{p}}{(2 p-1)(2 p-3) \ldots(1)} \\
\text { 如果 } n=2 p: \quad & =\frac{\pi^{p}}{2^{p}} \times \frac{(2 p)!}{(p!)^{2}} \times \frac{(2 p)(2 p-2) \ldots(4)(2)}{(2 p!)} \\
& =\frac{\pi^{p}}{2^{p}} \times \frac{(2 p)!}{(p!)^{2}} \times \frac{2^{p} p!}{(2 p)!} \\
& =\frac{\pi^{p}}{p!} \\
& =\frac{\pi^{n / 2}}{\Gamma\left(\frac{n}{2}+1\right)}
\end{aligned}
$$

如果 $n=2 p+1$，计算相对简单一些：

$$
\begin{aligned}
V_{2 p+1} & =I_{2 p+1} I_{2 p} I_{2 p-1} \ldots I_{2} V_{1} \\
& =\left(I_{2 p+1} I_{2 p}\right)\left(I_{2 p-1} I_{2 p-2}\right) \ldots\left(I_{3} I_{2}\right) \times 2 \\
& =\frac{\pi}{p+1
 / 2} \times \frac{\pi}{p-1 / 2} \times \frac{\pi}{p-3 / 2} \times \cdots \times \frac{\pi}{3 / 2} \times \frac{1}{1 / 2} \\
& =\frac{\pi^{p+\frac{1}{2}}}{(p+1 / 2)(p-1 / 2) \cdots(1 / 2) \pi^{\frac{1}{2}}} \\
& =\frac{\pi^{p+\frac{1}{2}}}{\Gamma\left(p+\frac{1}{2}+1\right)} \\
& =\frac{\pi^{n / 2}}{\Gamma\left(\frac{n}{2}+1\right)}
\end{aligned}
$$

所以我们得到了n球体积的单一公式，无论n的奇偶性如何

$$
V_{n}=V_{n}(1)=\frac{\pi^{n / 2}}{\Gamma\left(\frac{n}{2}+1\right)}
$$

并且扩展到半径为R的n球的体积为：

$$
V_{n}(R)=R^{n} V_{n}(1)=R^{n} \frac{\pi^{n / 2}}{\Gamma\left(\frac{n}{2}+1\right)}
$$

请注意，使用这个表达式，有一个非常简单的方法可以推导出n球的表面积。我们只需对半径为R的n球的体积关于R求导，就可以得到半径为R的n球的表面积：

$$
\frac{d}{d R} V_{n}(R)=n R^{n-1} V_{n}(1)=n R^{n-1} \frac{\pi^{n / 2}}{\Gamma\left(\frac{n}{2}+1\right)}
$$

特别地，半径为1的n球的表面积为：

$$
S_{n}=n \frac{\pi^{n / 2}}{\Gamma\left(\frac{n}{2}+1\right)}=\frac{2 \pi^{n / 2}}{\Gamma\left(\frac{n}{2}\right)}
$$

## 附录：Wallis积分的推导

Wallis积分定义为：

$$
W_{n}=\int_{0}^{\pi / 2} \sin ^{n}(\theta) d \theta
$$

我们将使用分部积分推导递归公式。

$$
\begin{aligned}
W_{n} & =\int_{0}^{\pi / 2} \sin ^{n}(\theta) d \theta \\
& =\int_{0}^{\pi / 2} \sin ^{n-2}(\theta)\left(1-\cos ^{2}(\theta)\right) d \theta \\
& =W_{n-2}-\int_{0}^{\pi / 2} \sin ^{n-2}(\theta) \cos ^{2}(\theta) d \theta \\
& =W_{n-2}-\left(\left[\frac{\sin ^{n-1}(\theta)}{n-1} \cos (\theta)\right]_{0}^{\pi / 2}-\frac{1}{n-1} \int_{0}^{\pi / 2}-\sin ^{n-1}(\theta) \sin (x) d \theta\right) \\
& =W_{n-2}-\frac{1}{n-1} W_{n}
\end{aligned}
$$

我们得出结论：

$$
W_{n}=\frac{n-1}{n} W_{n-2}
$$

我们现在可以根据n的奇偶性区分两种情况：

- 如果 $n=2 p$，我们有：

$$
W_{2 p}=\frac{2 p-1}{2 p} W_{2 p-2}=\frac{2 p-1}{2 p} \frac{2 p-3}{2 p-2} \cdots \frac{1}{2} W_{0}=\frac{2 p-1}{2 p} \frac{2 p-3}{2 p-2} \cdots \frac{1}{2} \frac{\pi}{2}=\frac{\pi}{2} \frac{(2 p)!}{2^{2 p}(p!)^{2}}
$$

我们通过在分母和分子中乘以$2 p(2 p-2) \ldots 2$来使$(2 p)!$出现，并将分母的每一项因数化为2。

- 类似地，如果 $n=2 p+1$，我们有：

$$
W_{2 p+1}=\frac{2 p}{2 p+1} W_{2 p-1}=\frac{2 p}{2 p+1} \frac{2 p-2}{2 p-1} \ldots \frac{2}{3} W_{1}=\frac{2 p}{2 p+1} \frac{2 p-2}{2 p-1} \ldots \frac{2}{3} \frac{2}{1}=\frac{2^{2 p}(p!)^{2}}{(2 p+1)!}
$$

我们得出结论

$$
W_{2 p}=\frac{\pi}{2} \frac{(2 p)!}{2^{2 p}(p!)^{2}}
$$

$$
W_{2 p+1}=\frac{2^{2 p}(p!)^{2}}{(2 p+1)!}
$$

