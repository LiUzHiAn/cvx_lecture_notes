# Lecture 10-线性规划的对偶

-  原问题（primal problem）

给定$c \in \mathbb{R}^{n}, A \in \mathbb{R}^{m \times n}, b \in \mathbb{R}^{m}, G \in \mathbb{R}^{r \times n}, h \in \mathbb{R}^{r}$，我们定义原问题（primal problem）为:
$$
\min_{x \in \mathbb{R}^{n}} c^{T} x
$$
s.t.
$$
\begin{array}{l}
A x=b \\
G x \leq h
\end{array}
$$
对于上式，做以下操作：

$$u^T(Ax-b)=0,\text{for any}\  u\\v^T(Gx-h)\leq 0 , \text{for}\ v\geq 0  $$

两式相加，得$\left(-A^{T} u-G^{T} v\right)^{T} x \geq-b^{T} u-h^{T} v$

- 对偶问题（dual problem）

我们令$c=-A^{T} u-G^{T} v$,于是原问题的对偶问题为：
$$
\max _{u \in \mathbb{R}^{m}, v \in \mathbb{R}^{r}}-b^{T} u-h^{T} v
$$
s.t.
$$
\begin{array}{l}
-A^{T} u-G^{T} v=c \\
v \geq 0
\end{array}
$$
***对原问题求极小可以转化为对对偶问题求极大。***

- max-flow/min-cut问题

参考[Ryan Tibshirani-lecture-slides](http://www.stat.cmu.edu/~ryantibs/convexopt-F15/lectures/11-dual-gen.pdf)

