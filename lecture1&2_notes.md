# Lecture-1&2 凸集和凸函数

## 凸集相关

- 凸集

给定一个集合$C\sube \mathbb{R}^y$，如果有$x, y \in C \Rightarrow t x+(1-t) y \in C \text { for all } 0 \leq t \leq 1$，那么这个集合就是凸集。也就是说，集合中两个点的连线间所有的点，也都在这个集合中。

![image-20201119190710356](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201119190710356.png)

- 凸集的例子

空集、点、线、norm ball $\{x:||x||\leq r\}$,超平面$\left.\{x: a^{T} x=b\right\}$,半平面$\left\{x: a^{T} x \leq b\right\}$，多边形$\{x: A x \leq b\}$

- 锥

给定一个集合$C\sube \mathbb{R}^n$，如果有$x \in C \Rightarrow t x \in C,$ for all $t \geq 0$,那么我们就称集合$C$为一个锥。显然，锥不一定是凸的，例如下面这种情况

![image-20201119195137862](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201119195137862.png)

- 凸锥

如果一个锥是凸的，必定满足下面的性质，即，$x_{1}, x_{2} \in C \quad \Rightarrow \quad t_{1} x_{1}+t_{2} x_{2} \in C$ for all $t_{1}, t_{2} \geq 0$。

常见的几种凸锥有 norm cone$\{(x, t):\|x\| \leq t\}$、normal cone $N_{C}(x)=\left\{g: g^{T} x \geq g^{T} y,\right.$ for all $\left.y \in C\right\}$、半正定锥$S_{+}^{n}=\left\{X \in S^{n}: X \succeq 0\right\}$，其中$ X \succeq 0$是半正定矩阵的意思。

- 分割超平面理论

如果两个凸集是不相交的，那么必定存在一个超平面使得二者分开。

![image-20201119201402661](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201119201402661.png)

- 支撑超平面理论

对于一个凸集边界上的一个点，必定存在一个过改点的超平面将凸集“支撑”起来。

![image-20201119201458496](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201119201458496.png)

- 保凸变换
  - 求交集操作，两个凸集的交集还是凸集；
  - 缩放和平移操作，如果集合$C$是凸的，那么$a C+b=\{a x+b: x \in C\}$也肯定是凸的；

## 凸函数相关

- 凸函数

给定一个函数$f:\mathbb{R}^n \rightarrow \mathbb{R}$,其中$dom(f)\sube \mathbb{R}^n$,如果有$f(t x+(1-t) y) \leq t f(x)+(1-t) f(y)$ for $0 \leq t \leq 1$，那么这个函数就是凸函数。也就是这样“碗”的形状。

![image-20201119190717915](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201119190717915.png)

- 函数的凸凹性

如果一个函数$f$是凹的，那么$-f$肯定是凸的。但是！但是！反过来不一定成立，也就是说，命题“如果一个函数$f$是凸的，那么$-f$肯定是凹的”是不一定成立的。举个例子，对于affine function，它既是凹的又是凸的，带入刚才的命题会发现肯定是不对的。

- 严格凸和强凸
  - 严格凸（Strictly Convex），$f[t x+(1-t) y]<t f(x)+(1-t) f(y))$ for $x \neq y$ and $0<t<1$，即凸函数的定义等号不成立，严格不等；
  - 强凸（Strongly Convex），存在一个常数$m>0$，使得$f-\frac{m}{2}\|x\|_{2}^{2}$仍然是凸的，也就是说，原函数$f$减去二次型之后还是凸的，这说明原函数$f$凸的很厉害。

  凸、强凸、严格凸三者的凸性排序是，强凸 > 严格凸 > 凸。

- 凸函数的例子
  - 指数函数$f(x)=e^{ax},for \ any \ a$;
  - 幂函数$f(x)=x^a,a \ge1\  or \ a\le0 $，当$a\in(0,1)$时，$f(x)=x^a$是凹的；
  - $log(x)​是凹函数；
  - 仿射函数 $a^Tx+b$既是凸的又是凹的；
  - 二次型$\frac{1}{2} x^{T} Q x+b^{T} x+c$在当$Q$是半正定时是凸的；
  - 最小二乘$\|y-A x\|_{2}^{2}$必定是凸的，因为$A^TA$肯定是半正定的；
  - 支撑函数$I_{C}^{*}(x)=\max _{y \in C} x^{T} y$肯定是凸的，不管集合$C$是不是凸的；
  - 最大值函数$f(x)=\max \left\{x_{1}, \ldots x_{n}\right\}$也肯定是凸的；
  - 任何范数也都是凸的,$\|x\|_{p}=\left(\sum_{i=1}^{n} x_{i}^{p}\right)^{\frac{1}{p}}$ for $p \geq 1,\|x\|_{\infty}=\max _{i=1, \ldots n}\left|x_{i}\right|$；
  - 对一个凸集的指示函数（indicator function）是凸函数，$I_{C}(x)=\left\{\begin{array}{ll}0 & x \in C \\ \infty & x \notin C\end{array}\right.$；
- 凸函数的一些性质
  - 函数$f$是凸的，当且仅当$e p i(f)=\{(x, t) \in \operatorname{dom}(f) \times R: f(x) \leq t\}$是凸集；
  - 如果函数$f$是凸的，那么$f$的任意下水平集$\{x \in \operatorname{dom}(f): f(x) \leq t\}$都是凸集，但反过来不一定成立，比如$log(x)$的任意下水平集都是凸的，但是$log(x)$是凹函数；
  - **凸函数的一阶特性**：如果$f$是可微的，那么当且仅当$f(y) \geq f(x)+\nabla f(x)^{T}(y-x)$对任意的$x,y\in dom(f)$都成立时，$f$是凸的（意思就是说，任意点处的切线都位于函数的下方）；
  - **凸函数的二阶特性**：如果函数$f$是凸的，当且仅当$f$任意位置的二阶导数都满足$\nabla^{2} f(x) \succeq 0$（对于多元变量的情形，就是Hessian阵为半正定阵）；
  - **琴生不等式**：对于凸函数$f$，必定有$f(E[X]) \leq E[f(X)]$

- 保凸操作
  - 非负线性组合：对于$m$个凸函数$f_{1}, \ldots f_{m}$，那么对这$m$个函数的nonnegative linear combination $a_{1} f_{1}+\ldots+a_{m} f_{m}$也是凸的；
  - pointwise maximization：很简答的一个例子就是，对$m$个仿射函数求pointwise maximization；
  - 部分最小：如果$g(x,y)$是凸的，并且$C$是凸集，那么$f(x)=\min _{y \in C} g(x, y)$也是凸的；
  - 复合函数的凸性，求二阶导数去check即可；
- 一个相对复杂的例子

证明：log-sum-exp函数$g(x)=\log \left(\sum_{i=1}^{k} e^{a_{i}^{T} x+b_{i}}\right)$，for fixed $a_{i}, b_{i}, i=1, \ldots k$而言，是凸的。

证明过程：

1. 首先，我们知道仿射函数不改变函数的凸性，因此也等价于判断函数$f(x)=\log \left(\sum_{i=1}^{n} e^{x}\right)$的凸性，注意，这里的$x$是向量；
2. 然后，我们直接对$f$求二阶导数，如果二阶导数是半正定的，那么就是凸的了，很容易可以求得：$\begin{aligned} \nabla_{i} f(x) &=\frac{e^{x_{i}}}{\sum_{\ell=1}^{n} e^{x_{\ell}}} \\ \nabla_{i j}^{2} f(x) &=\frac{e^{x_{i}}}{\sum_{\ell}^{n} e^{x_{\ell}}} 1\{i=j\}-\frac{e^{x_{i}} e^{x_{j}}}{\left(\sum_{\ell=1}^{n} e^{x_{\ell}}\right)^{2}} \end{aligned}$
3. 最后，我们可以发现$\nabla^{2} f(x)=\operatorname{diag}(z)-z z^{T}$，其中$z_{i}=e^{x_{i}} /\left(\sum_{\ell=1}^{n} e^{x_{\ell}}\right)$，因此二阶Hessian阵是diagonally dominant的，必定是半正定的。

证毕。

- 凸优化问题的一般形式

$$
\min _{x \in D} f(x)
$$
subject to:
$$
\begin{array}{l}
g_{i}(x) \leq 0, i=1, \ldots m \\
h_{j}(x)=0, j=1, \ldots r
\end{array}
$$
其中$D=\operatorname{dom}(f) \cap \bigcap_{i=1}^{m} \operatorname{dom}\left(g_{i}\right) \cap \bigcap_{j=1}^{p} \operatorname{dom}\left(h_{j}\right)$，并且$g_i(x)$都是凸函数，$h_j(x)$都是仿射函数。