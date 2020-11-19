# Lecture-3 优化问题相关基础

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

**key property**：如果$f$是严格凸的，那么最优解唯一。

