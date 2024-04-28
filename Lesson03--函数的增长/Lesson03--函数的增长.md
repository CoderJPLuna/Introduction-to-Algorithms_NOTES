# 3. 函数的增长

## 3.1 渐进记号

**渐进紧确界(asymptotically tight bound)**

$$
\Theta (g(n))= \{ f(n)| \exist c_1>0,c_2>0,n_0>0, \forall n \geqslant n_0,0 \leqslant c_1g(n) \leqslant f(n) \leqslant c_2g(n) \}
$$

我们称 $g(n)$ 是 $f(n)$ 的一个渐进紧确界.

**渐进上界**

$$
\Omicron (g(n))= \{ f(n)| \exist c>0,n_0>0, \forall n\geqslant n_0,0 \leqslant f(n) \leqslant cg(n) \}
$$

当描述一个算法的运行时间为 $\Omicron (g(n))$ 时,通常指的时其在 **最坏情况下** 的运行时间的 **最紧上界** .

**渐进下界**

$$
\Omega (g(n))= \{ f(n)| \exist c>0,n_0>0, \forall n\geqslant n_0,0 \leqslant cg(n) \leqslant f(n) \}
$$

**定理**

$$
f(n)= \Theta (g(n)) \Leftrightarrow f(n)= \Omicron (g(n)) \wedge f(n)= \Omega (g(n))
$$

**非渐进紧确界**

$$
\omicron (g(n))= \{ f(n)| \forall c>0, \exist n_0>0, \forall n\geqslant n_0,0 \leqslant f(n)<cg(n) \} \Leftrightarrow \lim_{n \to \infty} \frac{f(n)}{g(n)}=0
$$

$$
\omega (g(n))= \{ f(n)| \forall c>0, \exist n_0>0, \forall n\geqslant n_0,0 \leqslant cg(n)<f(n) \} \Leftrightarrow \lim_{n \to \infty} \frac{f(n)}{g(n)}= \infty
$$

**渐进记号的性质**
* 传递性
  $f(n)= \Theta (g(n)) \wedge g(n)= \Theta (h(n)) \Rightarrow f(n)= \Theta (h(n))$
  $f(n)= \Omicron (g(n)) \wedge g(n)= \Omicron (h(n)) \Rightarrow f(n)= \Omicron (h(n))$
  $f(n)= \Omega (g(n)) \wedge g(n)= \Omega (h(n)) \Rightarrow f(n)= \Omega (h(n))$
  $f(n)= \omicron (g(n)) \wedge g(n)= \omicron (h(n)) \Rightarrow f(n)= \omicron (h(n))$
  $f(n)= \omega (g(n)) \wedge g(n)= \omega (h(n)) \Rightarrow f(n)= \omega (h(n))$
* 自反性
  $f(n)= \Theta (f(n))$
  $f(n)= \Omicron (f(n))$
  $f(n)= \Omega (f(n))$
* 对称性
  $f(n)= \Theta (g(n)) \Leftrightarrow g(n)= \Theta (f(n))$
* 转置对称性
  $f(n)= \Omicron (g(n)) \Leftrightarrow g(n)= \Omega (f(n))$
  $f(n)= \omicron (g(n)) \Leftrightarrow g(n)= \omega (f(n))$
* 三分性
  $\forall a \in R,b \in R,a<b \vee a=b \vee a>b$
  实数两两可比,函数不行.
  
## 3.2 标准记号与常用函数

**单调性**

**向下取整与向上取整**

**模运算**

**多项式**

**指数**

**对数**

**阶乘**

**多重函数**

**多重对数函数**

**斐波那契数**