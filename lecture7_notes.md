# Lecture 7-次梯度法

-  梯度下降法

$x^{(k)}=x^{(k-1)}-t_{k} \cdot \nabla f\left(x^{(k-1)}\right), k=1,2,3, \ldots$

其中$t_k$通常是被固定成一个较小的量，或通过backtracking line search完成，梯度下降法有两个不是那么好的地方：

1. 需要$f$ 可微；
2. 收敛慢。

- 次梯度法

我们不再要求函数可微，把梯度下降法中的梯度换成次梯度，即：

$x^{(k)}=x^{(k-1)}-t_{k} \cdot g^{(k-1)}, k=1,2,3 \ldots$

其中$g^{(k-1)}\in \partial f(x^{(k-1)})$，即$x^{(k-1)}$处的任意一个次梯度。

注意，次梯度下降法不一定是一个descent method，所以在迭代的过程中，我们需要记录每次迭代后的函数值，最终取个最小，即$f\left(x_{b e s t}^{(k)}\right)=\min _{i=0, \ldots k} f\left(x^{(i)}\right)$

- 次梯度法的步长选取

因为次梯度法不一定是一个descent method，自然也没办法backtracking line search，更不用说exact line search，所以在次梯度法中，步长的选取大概有两种方法：

1. 固定步长，即$t_k=t, k=1,2,3...$
2. 使得每次的步长满足条件$\sum_{k=1}^{\infty} t_{k}^{2}<\infty, \sum_{k=1}^{\infty} t_{k}=\infty$，即 square summable but not summable，一个常用的就是$t_k=1/k$

反正记住一点，这些步长都是在迭代之前都预先设定好的，不是每一步都需要去搜寻的。

- 一个例子

给定 $\left(x_{i}, y_{i}\right) \in \mathbb{R}^{p} \times\{0,1\}$ for $i=1, \ldots n$，考虑logistics regression的问题，即：

$f(\beta)=\sum_{i=1}^{n}\left(-y_{i} x_{i}^{T} \beta+\log \left(1+\exp \left(x_{i}^{T} \beta\right)\right)\right)$

因为log-sum of exponetials是凸函数，所以这个问题肯定是凸优化问题，并且$f$是可微的，所以很简单，可以知道：

$\begin{aligned} \nabla f(\beta) &=\sum_{i=1}^{n}\left(y_{i}-p_{i}(\beta)\right) x_{i}, \text { where } \\ p_{i}(\beta) &=\exp \left(x_{i}^{T} \beta\right) /\left(1+\exp \left(x_{i}^{T} \beta\right)\right), i=1, \ldots, n \end{aligned}$

现在考虑加正则项的情况，即$\min _{\beta \in \mathbb{R}^{p}} f(\beta)+\lambda P(\beta)$，，其中$P(\beta)$是$\beta$的范数，如果取1范数，那上述问题就是lasso，如果取2范数，就是ridge问题。下图是两个问题在使用梯度下降法和次梯度下降法在不同步长选取策略时的收敛情况：

![image-20201025193014227](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201025193014227.png)

- 随机次梯度法（stochastic subgradient method）

考虑这样一个问题，$\min _{x} \sum_{i=1}^{m} f_{i}(x)$

我们知道$\partial \sum_{i=1}^{m} f_{i}(x)=\sum_{i=1}^{m} \partial f_{i}(x)$，因此用次梯度法，我们的迭代是形如以下这样子的，即：

$x^{(k)}=x^{(k-1)}-t_{k} \cdot \sum_{i=1}^{m} g^{(k-1)}, \quad k=1,2,3 \ldots$，其中$g_{i}^{(k-1)} \in \partial f_{i}\left(x^{(k-1)}\right)$，也就是说，把每个函数的次梯度都算一下，然后求和。

但是在随机梯度法中，我们采取的策略是$x^{(k)}=x^{(k-1)}-t_{k} \cdot g_{i_k}^{(k-1)}, \quad k=1,2,3 \ldots$，其中$i_{k} \in\{1, \ldots m\}$，也就是说，随便取其中一个函数的次梯度就OK了。

- 随机梯度下降法（stochastic gradient descent）

我们考虑随机次梯度法的一个特例，即当函数$f$可微时的情况，于是就退化成了随机梯度下降法。既然名字都叫随机梯度下降法，那随机在哪里呢？没错，就是在采样$m$的时候了。如果熟悉深度学习的话，那我们就可以把$m$看成训练集中的样本总数，而$f_i(x),i=1,2,...,m$就是每个样本的loss。

如果我们训练的每个iteration选所有$m$个样本，我们就称为是batch gradient descent；如果每次只取一个样本，那就是stochastic gradient descent；如果每次选取k个样本，那就是mini-batch  gradient descent。形式化描述如下：
$x^{(k+m)}=x^{(k)}-t \sum_{i=1}^{m} \nabla f_{i}\left(x^{(k+i-1)}\right)$ ( SGD）

$x^{(k+1)}=x^{(k)}-t \sum_{t=1}^{m} \nabla f_{i}\left(x^{(k)}\right)$（batch）

可以看到，一个epoch之后，两种方法的loss下降差值为$E=t \sum_{i=1}^{m}\left(\nabla f_{i}^{(k-i+1)}-\nabla f_{i}^{(k)}\right)$，当$\nabla f(x)$随$x$变化不是很大时，我们可以认为SGD等效于batch-GD，即当$\nabla f(x)$满足Lipschitz条件时。

