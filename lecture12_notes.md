# Lecture 12-KKT条件

-  KKT条件（Karush-Kuhn-Tucker Condition）

对于以下general的问题：
$$
\min _{x} f(x) \\
s.t. h_i(x)\leq 0,i=1,...,m \\
l_j(x)=0,j=1,...,r \\
$$
我们定义KKT条件为：

1. stationary，$0 \in \partial f(x)+\sum_{i=1}^{m} u_{i} \partial h_{i}(x)+\sum_{j=1}^{r} v_{j} \partial \ell_{j}(x)$ ，即拉格朗日函数存在梯度为0的解；
2. complementary slackness， $u_ih_i(x)=0,\text{for all i}$，即要么不等式约束刚好值为0，或者对应的$u_i$为0，即所谓互补；
3. primal fesibility， $h_i(x)\leq0,l_j(x)=0 \text{ for all i,j}$，即带回原问题，必须是可行的；
4. dual fesibility，$u_i\geq 0, \text{for all i}$，即对偶问题中关于原问题不等式约束的变量大于0。



- 证明：强对偶条件下，原问题和对偶问题的最优解肯定是满足KKT条件的。

记$x^*,u^*,v^*$分别为原问题和对偶问题的最优解，于是有：

$\begin{aligned} f\left(x^{*}\right) &=g\left(u^{*}, v^{*}\right) \\ &=\min _{x} f(x)+\sum_{i=1}^{m} u_{i}^{*} h_{i}(x)+\sum_{j=1}^{r} v_{j}^{*} \ell_{j}(x) \\ & \leq f\left(x^{*}\right)+\sum_{i=1}^{m} u_{i}^{*} h_{i}\left(x^{*}\right)+\sum_{j=1}^{r} v_{j}^{*} \ell_{j}\left(x^{*}\right) \\ & \leq f\left(x^{*}\right) \end{aligned}$

- 证明：强对偶条件下，满足KKT条件的解，肯定是原问题和对偶问题的最优解。

记$x^*,u^*,v^*$满足KKT条件，那么有：

$\begin{aligned} g\left(u^{*}, v^{*}\right) &=f\left(x^{*}\right)+\sum_{i=1}^{m} u_{i}^{*} h_{i}\left(x^{*}\right)+\sum_{j=1}^{r} v_{j}^{*} \ell_{j}\left(x^{*}\right) \\ &=f\left(x^{*}\right) \end{aligned}$



**总结：对于一个强对偶问题，如果$x^*,u^*,v^*$分别为原问题和对偶问题的最优解，那么$x^*,u^*,v^*$肯定满足KKT条件。**