# Lecture 8-近似梯度法

-  函数分解

次梯度法虽然说很generic，但是收敛性很慢，所以有人提出了近似梯度法，主要思路是把目标函数进行分解，分解成一个可微的$g(x)$和另外一个不必是可微的$h(x)$，即$f(x)=g(x)+h(x)$，其中$dom(g)=\mathbb{R}^n$。说明一下，这里我们考虑的都是凸函数，即$f(x),g(x),h(x)$都是凸的。

我们先考虑一个很简单的问题，即函数$f(x)$可微。好，可微课太好了，我们直接用梯度下降$x^{+}=x-t \cdot \nabla f(x)$，如果你要是嫌弃梯度下降下降得还是不够快，牛顿方法可以来加速，即

$x^{+}=\underset{z}{\arg \min } \underbrace{f(x)+\nabla f(x)^{T}(z-x)+\frac{1}{2 t}\|z-x\|_{2}^{2}}_{\tilde{f}_{t}(z)}$，这就是$f(x)$在$x$附近的二阶泰勒展开了，这玩意儿是可以直接用解析解求出来的。

可现在问题没这么理想，我们的$f(x)$是不可微的，咋办呢？我们刚才说可以把$f(x)$分解成一个可微的$g(x)$和另外一个不必是可微的$h(x)$，即$f(x)=g(x)+h(x)$，那我们干脆就二阶近似$g(x)$这部分，而$h(x)$不管它，是多少就是多少，迭代的时候我们原封不动地加上$h(x)$的取值就完事儿了。即$x^{+}=\underset{z}{\arg \min } \tilde{g}_{t}(z)+h(z)$

我们稍微做一点运算，如下：

$\begin{aligned} x^{+} &=\underset{z}{\arg \min } \tilde{g}_{t}(z)+h(z) \\ &=\underset{z}{\arg \min } g(x)+\nabla g(x)^{T}(z-x)+\frac{1}{2 t}\|z-x\|_{2}^{2}+h(z) \\ &=\underset{z}{\arg \min } \frac{1}{2 t}\|z-(x-t \nabla g(x))\|_{2}^{2}+h(z)   ,\text{   公式(1)} \end{aligned}$

倒数第二个式子和倒数第一个式子是等价的，不信的话，求出它们的一阶导数为0的点，真的是一样的。BTW，公式中的$1/t$就是$\nabla^2g(x)$。

仔细看看公式(1)，我们会发现第1项有点类似梯度下降法，但是也不完全一样，前面还有个关于$z$的项；第2项就取当前迭代最优处的$h(z)$即可。

现在，我们定义一个名叫proximal mapping的东西，如下，公式中的$1/t$还是Hessian矩阵：

$\operatorname{prox}_{t}(x)=\underset{z}{\arg \min } \frac{1}{2 t}\|z-x\|_{2}^{2}+h(z)$

于是，我们的近似梯度算法就可以描述为：

$x^{+}=\operatorname{prox}_{t_{}}\left(x-t \nabla g\left(x\right)\right)$

为了和下降法中的书写形式类似，我们不妨把近似梯度法写成$x^+=x-tG_t(x)$的形式，于是我们很容易得到$G_{t}(x)=\frac{x-\operatorname{prox}_{t}(x-t \nabla g(x))}{t}$

- 近似梯度法的作用

虽然看起来变复杂了（其实也没有很复杂），但是关键在于，$prox_t(\cdot)$不依赖于$g$是什么东西，而只依赖于$h$，在很多情况下，$h$又是可以有解析解的。虽然$g$可以很复杂很复杂，但是它是可微的，所以我们在每一次迭代的过程中只要用它的梯度就OK了。

- ISTA

再回顾一下lasso中的情况，$f(\beta)=\underbrace{\frac{1}{2}\|y-X \beta\|_{2}^{2}}_{g(\beta)}+\underbrace{\lambda\|\beta\|_{1}}_{h(\beta)}$，其中$y \in \mathbb{R}^{n \times p}, X \in \mathbb{R}^{n}$。

OK，现在根据近似梯度法中的规则，我们有$\operatorname{prox}_{t}(\beta)=\underset{z \in \mathbb{R}^{n}}{\arg \min } \frac{1}{2 t}\|\beta-z\|_{2}^{2}+\lambda\|z\|_{1}$，这玩意儿有解析解，也就是soft-thresholding operator，即$S_{\lambda t}(\beta)$,其中，$\left[S_{\lambda t}(\beta)\right]_{i}=\left\{\begin{array}{ll}\beta_{i}-\lambda & \text { if } \quad \beta_{i}>\lambda \\ 0 & \text { if } \quad \lambda \leq \beta_{i} \leq \lambda \quad i=1, \ldots n \\ \beta_{i}+\lambda & \text { if } \quad \beta_{i}<-\lambda\end{array}\right.$

而我们又很容易可以知道$\nabla g(\beta)=-X^{T}(y-X \beta)$，所以，近似梯度法的每一次迭代公式为：

$\beta^{+}=S_{\lambda t}\left(\beta+t X^{T}(y-X \beta)\right)$

这个问题通常被称为ISTA(iterative soft-thresholding algorithm),下图展示了ISTA和次梯度法的收敛对比。



![image-20201026163000121](/Users/liuzhian/Library/Application Support/typora-user-images/image-20201026163000121.png)

- 近似梯度法的加速

略