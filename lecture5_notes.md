# Lecture-5 Gradient Descent

- 优化的目标

最小化一个无约束的、可微的、凸的$f(x)$，其中$dom(f)=\mathbb R^n$

- 梯度下降法

选择一个初始的$x^{(0)}$,迭代过程为$x^{k}=x^{(k-1)}-t_k \nabla{f}(x^{(k-1)}) $，迭代的停止条件需要手动给定。对于标准二次型而言，常用的停止条件为$||\nabla{f}(x)||<\epsilon$，因为梯度快要接近为0时，也就意味着快到达了最优解。

- 牛顿法

$f(y) \approx f(x)+\nabla f(x)^{T}(y-x)+\frac{1}{2 t}\|y-x\|_{2}^{2}$，相当于用当前点的二阶泰勒展开近似$f(x)$，然后利用二次型有解析解的特点，直接定位到局部最优点，作为下一次迭代的位置，即$x^{+}=\arg \min _{y} f(x)+f(x)+\nabla f(x)^{T}(y-x)+\frac{1}{2 t}\|y-x\|_{2}^{2}$，其中$\frac{1}{t}=\nabla^2f(x)$

![image-20201022231948008](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201022231948008.png)

- Backtracking line search

这个东西的思想其实很简单，只要找到一个能让$f(x)$在$x$附近能下降的点$x^{+}$即可。首先，对于任意一个凸函数，由其一阶条件可知：
$$
f(y)\geq \nabla f(x)^T(y-x)+f(x), \forall x,y \in dom(f)
$$
换个在梯度下减法中的写法（把$y$替换成$x+t\Delta x$）,上式为：
$$
f(x+t\Delta x)\geq t \nabla f(x)^T\Delta x+f(x), \forall x,y \in dom(f)
$$
Backtracking line search的流程如下：

只要 $f(x+t \Delta x)>f(x)+\alpha t \nabla f(x)^{T} \Delta x $ 成立，我们就不断减小t，即$t:=\beta t$，通常$\alpha$取值为0.5即可。一旦上述不等式不成立，就停止。

![image-20201022233837839](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201022233837839.png)

- exact line search

在搜索步长时，backtracking line search不一定是是最优的（通常情况下总不是最优的），所以我们希望找到每一步最优的那个步长，即所谓的exact line search，为：

$$t=\arg \min _{s \geq 0} f(x-s \nabla f(x))$$，但这个minimization不一定很好做，对于二次型这种倒是容易，但对于其他的复杂凸函数很难求，所以实际上很少用。

- 最速下降法

根据一阶泰勒展开知，$f(x+v)\approx \hat{f}(x+v)=f(x)+\nabla f(x)^Tv$,我们称$\nabla f(x)^Tv$为方向导数，如果方向导数是小于0的，那么$v$的方向就是函数下降的方向，现在我们的目标是，能不能一次就找到使得函数值下降最多的那个点？为方便处理，不妨将$v$的长度固定为1，即$\Delta x_{nsd}=argmin\{\nabla f(x)^Tv| \space ||v||=1\}$,然后用这个方向$v$作为descent methd中的方向，再去line search即可。

- 二次型最优化问题的收敛性分析

见Boyd 9.1.2和bilibili中科大凸优化课程视频。

