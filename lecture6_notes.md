# Lecture-6 次梯度

- 定义

对于一个凸且可微的函数$f(x)$，恒有$f(y)\geq f(x)+\nabla f(x)^T(y-x),\forall x,y\in dom(f)$

,在次梯度的条件下，我们记为$f(y)\geq f(x)+g^T(y-x),\forall x,y\in dom(f)$，其中$g$就被称为次梯度，也就是说，直线$f(x)+g^T(y-x)$位于函数$f(x)$的下方。

![image-20201023002511441](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201023002511441.png)

对于上图，如果$x\neq0$,，则$g=sign(x)$；否则对于$x=0$的情况，g可以是$[-1,1]$区间里的任意一个数。

- 次微分

一个凸函数的所有次梯度集合为次微分，即$\partial f(x)=\{g\in \mathbb{R}^n:g\ is\ a \ subgradient \ of \ f\ at \ x\}$，换个写的方式就是$\partial f(x)=\{g|f(y)\geq f(x)+g^T(y-x)，\forall y \in dom(f)\}$。

很明显，我们可以发现，$\partial f(x)$就是很多个half-space的交集，故对于任意一个函数$f(x)$，不管它是不是凸的，它的次微分必然是凸的。

- 次微分的一些性质
  - 和微分一样的性质：加法法则，乘法法则，链式求导；
  - 有限pointwise maximum：

  如果$f(x)=max\{f_i(x)\},i=1,2,...,m$,则有$\partial f(x)=conv(\bigcup_{i\in I(x)}\partial f_i(x) )$,其中$I(x)=\{i|f_i(x)=f(x)\}$，即在$x$处激活的那些函数索引值。而$conv(C)$表示C组成的凸包(convex hull)，凸包的定义为$\operatorname{conv} C=\left\{\theta_{1} x_{1}+\ldots+\theta_{k} x_{k} \mid x_{i} \in C, \theta_{i} \geq 0, i=1, \ldots, k, \theta_{1}+\ldots+\theta_{k}=1\right\}$

- 次梯度下，函数的最优条件

对于随便一个函数$f(x)$，$f(x^*)=min_x(f(x)) \iff 0 \in \partial f(x^*)$

- Lasso example

$\min _{\beta \in \mathbb{R}^{p}} \frac{1}{2}\|y-X \beta\|_{2}^{2}+\lambda\|\beta\|_{1}$，其中$y \in \mathbb{R}^{n}, X \in \mathbb{R}^{n \times p},\lambda \geq0$，根据次梯度下的最优条件知：

$0 \in \partial\left(\frac{1}{2}\|y-X \beta\|_{2}^{2}+\lambda\|\beta\|_{1}\right)$

$\Longleftrightarrow 0 \in-X^{T}(y-X \beta)+\lambda \partial\|\beta\|_{1}$
$\Longleftrightarrow \quad X^{T}(y-X \beta)=\lambda v$

$v_{i} \in\left\{\begin{array}{ll}\{1\} & \text { if } \quad \beta_{i}>0 \\ \{-1\} & \text { if } \quad \beta_{i}<0, \quad i=1, \ldots p \\ {[-1,1]} & \text { if } \quad \beta_{i}=0\end{array}\right.$

我们不妨记$X_i$为$X$矩阵的列向量，于是次梯度的最优条件也就是说，只要满足下面的条件即可：

$\left\{\begin{array}{ll}X_{i}^{T}(y-X \beta)=\lambda \cdot \operatorname{sign}\left(\beta_{i}\right) & \text { if } \beta_{i} \neq 0 \\ \left|X_{i}^{T}(y-X \beta)\right| \leq \lambda & \text { if } \beta_{i}=0\end{array}\right.$

上述条件其实也并不能帮助我们直接得到lasso的解析解，但倒是为我们提供了一个评估lasso的条件，即在当前某个解$\beta$的条件下，如果$\left|X_{i}^{T}(y-X \beta)\right| < \lambda$，那么我们就可以知道$\beta_i=0$。

- Soft-thresholding 的例子

Soft-thresholding 就是lasso中的$X=I$时的情况,那么根据次梯度下的最优条件，我们可以知道最优解满足下面的条件：

$\left\{\begin{array}{ll}y_{i}-\beta_{i}=\lambda \cdot \operatorname{sign}\left(\beta_{i}\right) & \text { if } \beta_{i} \neq 0 \\ \left|y_{i}-\beta_{i}\right| \leq \lambda & \text { if } \beta_{i}=0\end{array}\right.$

而Soft-thresholding 问题的解析解为$\beta=S_\lambda(y)$，其中：

$\left[S_{\lambda}(y)\right]_{i}=\left\{\begin{array}{ll}y_{i}-\lambda & \text { if } y_{i}>\lambda \\ 0 & \text { if }-\lambda \leq y_{i} \leq \lambda, \quad i=1, \ldots n \\ y_{i}+\lambda & \text { if } y_{i}<-\lambda\end{array}\right.$

不妨可以check一下上述解析解是否满足最优条件，显然是满足的。