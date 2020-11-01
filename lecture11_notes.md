# Lecture 11-通用问题的对偶

-  拉格朗日函数（Lagrangian）

对于任意一个最小化问题（不一定$f(x)$是凸的）：
$$
\min _{x} f(x)
$$
s.t.
$$
\begin{array}{ll}
h_{i}(x) \leq 0, & i=1, \ldots m \\
\ell_{j}(x)=0, & j=1, \ldots r
\end{array}
$$
我们定义拉格朗日函数为$L(x, u, v)=f(x)+\sum_{i=1}^{m} u_{i} h_{i}(x)+\sum_{j=1}^{r} v_{j} \ell_{j}(x)$，其中$u\in \mathbb{R}^m且u\geq 0,v\in\mathbb{R}^r $

显然$L(x,u,v)\leq f(x)$，因为$\sum_{i=1}^{m} u_{i} h_{i}(x)+\sum_{j=1}^{r} v_{j} \ell_{j}$肯定是$\leq$0的。

- 拉格朗日对偶函数（Lagrange dual function）

假设$C$是原问题的可行解，$f^*$是原问题的最优值，于是我们可以知道$f^{*} \geq \min _{x \in C} L(x, u, v) \geq \min _{x} L(x, u, v):=g(u, v)$

我们称作$g(u,v)$，其中$u\geq0,v\  \text{can be anything}$，是拉格朗日对偶函数，即拉格朗日函数的最小值，给出了原问题的lower bound。

- 二次型的例子

考虑以下二次型
$$
\min _{x\in \mathbb{R}^n}\frac{1}{2}x^TQx+c^Tx \\
s.t. Ax=b,x\geq 0
$$
其中$Q\succ 0$。

于是拉格朗日函数为$L(x, u, v)=\frac{1}{2} x^{T} Q x+c^{T} x-u^{T} x+v^{T}(A x-b)$

我们求拉格朗日函数的极小，即拉格朗日对偶函数:

$g(u, v)=\min _{x \in \mathbb{R}^{n}} L(x, u, v)=-\frac{1}{2}\left(c-u+A^{T} v\right)^{T} Q^{-1}\left(c-u+A^{T} v\right)-b^{T} v$

这玩意给出了最优值$f^*$的下界。

下图给出了二次型原问题和对偶问题的情况，下半个曲面就是拉格朗日对偶函数，上半个曲面就是原问题。

![image-20201101233851300](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201101233851300.png)

可以发现，对偶问题的极大刚好等于原问题的最小，这不是巧合，因为二次型满足KKT条件。

- 拉格朗日对偶问题

$$
\max _{u,v} g(u,v) \\
s.t. u\geq 0
$$

我们记$g*$为拉格朗日对偶问题的最优解，显然$f^*\geq g^*$，这也被称为弱对偶（weak duality）。

***NOTICE：即使原问题是非凸的，拉格朗日对偶问题肯定是凸的！***

通过定义，我们知道：
$$
\begin{aligned}
g(u, v) &=\min _{x}\left\{f(x)+\sum_{i=1}^{m} u_{i} h_{i}(x)+\sum_{j=1}^{r} v_{j} \ell_{j}(x)\right\} \\
&=-\quad \max _{x}\left\{-f(x)-\sum_{i=1}^{m} u_{i} h_{i}(x)-\sum_{j=1}^{r} v_{j} \ell_{j}(x)\right\} \\

\end{aligned}
$$
也就是说，拉格朗日函数就是对一堆affine函数求point-wise max，这显然是凸的！

- 非凸问题举例

假设我们有函数$f(x)=x^4-50x^2+100x$，这显然是一个非凸的函数，该问题和它的拉格朗日对偶函数图像如下：

![image-20201101235622507](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201101235622507.png)

对偶函数可以用一个close-form算出来，它给出了原问题的下界，于是对偶问题的最大值大概给出了原问题的最小值。当KKT条件满足时，二者相等，只不过在这里KKT条件不满足。

- 强对偶（strong duality）

当$f^*=g^*$时，我们称这是强对偶。什么时候才能有这么漂亮的性质呢？当满足Slater条件时！啥又是Slater条件？很简单，即：

1. 当$f(x)$是凸函数；
2. 存在一个可行解，使得$h_{1}(x)<0, \cdots h_{m}(x)<0$ and $\ell_{1}(x)=0, \cdots \ell_{r}(x)=0$，也就是不等式约束和等式约束都满足的时候。

- 对偶间隔（duality gap）

我们记$f(x)-g(u,v)$是对偶间隔，显然，$f(x)-f^*\geq f(x)-g(u,v)$，如果对偶间隔为0，那么说明$x$就是原问题的最优解了。

这玩意儿有啥用呢？主要是对一些迭代方法有用，当有一天，如果我们发现$f(x)-g(u,v)$小于某个$\epsilon$时，我们差不多可以认为$x$到了最优解。

