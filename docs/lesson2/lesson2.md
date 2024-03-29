# 2.矩阵消元
## 2.1 课程内容：矩阵消元、回代、矩阵乘法
上一讲我们对于线性方程组可以使用矩阵 $Ax=b$ 来表示，这一讲求解该等式，对于矩阵，使用矩阵消元法，即初等变换。

首先我们要有一个概念，对于线性系统来说，有三种等价的变化，即这三种变换不会改变线性系统的解
+ 交换方程的顺序（Interchange any two equations in the system）
+ 整个方程等号的左右两边同时乘以一个非零整数（Multiply any equation by a nonzero scalar）
+ 将一个方程的常数倍加到另一个方程之上（Add a constant multiple of any equation to another）

以下列方程组为例，我们先使用矩阵消元法，然后回代方程即可求得所要的解：
$$
\begin{cases}
x+2y+z=2  \\
3x+8y+z=12 \\
4y+z=2 \\
\end{cases}
$$

对于系数矩阵 $A$ 和解向量$\vec b$ ,构建增广矩阵
$$
(A,b)=
\begin{pmatrix}
1&2&1&2 \\
3&8&1&12 \\
0&4&1&2 \\
\end{pmatrix}
$$

<br />

下面对增广矩阵$(A,b)$进行消元：
$$
\begin{array}{l}
\begin{pmatrix}
\begin{array}{ccc|c}
1 & 2 &  1 &  2  \\
3 & 8 &  1 &  12  \\
0 & 4 &  1 &  2  \\
\end{array}
\end{pmatrix}
\xrightarrow[\text{加到第二行}]{\text{第一行乘以-3}}
\begin{pmatrix}
\begin{array}{ccc|c}
1 & 2 &  1 &  2  \\
0 & 2 & -2 &  6  \\
0 & 4 &  1 &  2  \\
\end{array}
\end{pmatrix}
\xrightarrow[\text{加到第三行}]{\text{第二行乘以-2}}
\begin{pmatrix}
\begin{array}{ccc|c}
{\color{red}{1}} & 2 &  1 &  2  \\
0 & {\color{red}{2}} & -2 &  6  \\
0 & 0 &  {\color{red}{5}} & -10  \\
\end{array}
\end{pmatrix}
\end{array}
$$

其中，方框中的 1，2，5 称为主元(pivot)，注意，主元不能为 0 。
下面通过回代求得线性方程组的解。

首先由增广矩阵的第三行可知，z=−2z=−2，将 z=−2 代入第二行可得 y=1，再将 z=−2,y=1 代入第一行可得 x=2

__那么如何用矩阵来表示上述消元过程呢？__

由上一讲的内容可知，对于 $AB$ 可以从行和列的角度去理解该乘法，消元法相当于是行变换，因此我们在系数矩阵 $A$ 左乘相应的变换矩阵，即可表示出对于 $A$ 的消元过程。

首先我们将系数矩阵 $A$ 消元之后得到的上三角矩阵称为 U（upper triangular），即
$$
U=\begin{bmatrix}
1 & 2 & 1   \\
0 & 2 & -2  \\
0 & 0 & 5   \\
\end{bmatrix}
$$

将矩阵 $A$ 第一次消元之后得到的矩阵称为$A_{1}$,即
$$
A_{1}=\begin{bmatrix}
1 & 2 & 1   \\
0 & 2 & -2  \\
0 & 4 & 1   \\
\end{bmatrix}
$$

那么消元过程就可以表示为
$$
E_{21}A=E_{21}\cdot\begin{bmatrix}
1 & 2 & 1 \\
3 & 8 & 1 \\
0 & 4 & 1 \\ 
\end{bmatrix}
=A_{1}=\begin{bmatrix}
1 & 2 & 1   \\
0 & 2 & -2  \\
0 & 4 & 1   \\
\end{bmatrix}
$$
$$
E_{32}A_{1}=E_{32}\cdot\begin{bmatrix}
1 & 2 & 1   \\
0 & 2 & -2  \\
0 & 4 & 1   \\
\end{bmatrix}
=U=\begin{bmatrix}
1 & 2 & 1   \\
0 & 2 & -2  \\
0 & 0 & 5   \\
\end{bmatrix}
$$

消元矩阵$E_{21}$左乘 $A$ 表示$E_{21}$的每一行即为 $A$ 的每一行的线性组合的系数，由消元过程可知第一步消元是 $A$ 的第一行的−3 倍加到第二行，而第一行和第三行不变，因此 $E_{21}$ 的第一行和第三行分别为 (1,0,0) 和 (0,0,1) ，第二行即为 (-3,1,0) ，即

$$
E_{21}=\begin{bmatrix}
1 & 0 & 0 \\
-3 & 1 & 0 \\
0 & 0 & 1 \\ 
\end{bmatrix}
$$

消元矩阵 $E_{32}$ 左乘 $A_{1}$ 表示 $E_{32}$ 的每一行即为 $A$ 的每一行的线性组合的系数，由消元过程可知第二步消元是 $A_{1}$ 的第二行的 −2 倍加到第三行，而第一行和第二行不变，因此 $E_{32}$ 的第一行和第二行分别为 (1,0,0) 和 (0,1,0) ，第三行即为 (0,-2,1) ，即
$$
E_{32}=\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & -2 & 1 \\ 
\end{bmatrix}
$$

而由矩阵乘法我们知道我们可以将这两步合并成一步，即可得
$$
E_{32}E_{21}A=U
$$
这就是矩阵消元的乘法表示。 

## 2.2 矩阵消元习题课

这是1999年秋季的[测验题](http://open.163.com/movie/2016/4/O/J/MBKJ0DQ52_MBKJ0M8OJ.html)，利用矩阵消元法求解下列线性方程组：
$$
\begin{cases}
x - y -z + u = 0      \\
2x - 0y +2z + 0u = 8  \\
0x - y -2z + 0u = -8  \\
3x - 3y -2z + 4u = 7  \\
\end{cases}
$$
首先得到增广矩阵 $(A,b)$
$$
\begin{pmatrix}
\begin{array}{cccc|c}
1 & -1  & -1  & 1  & 0   \\
2 &  0  &  2  & 0  & 8  \\
0 & -1  & -2  & 0  & -8   \\
3 & -3  & -2  & 4  & 7   \\
\end{array}
\end{pmatrix}
$$
为了得到第一行的主元，第二行需要加上第一行的 -2 倍，第四行减去第一行的 3 倍，即得到
$$
\begin{pmatrix}
\begin{array}{cccc|c}
1 & -1  & -1  & 1   & 0   \\
0 &  2  &  4  & -2  & 8  \\
0 & -1  & -2  & 0   & -8   \\
0 &  0  &  1  & 1   & 7   \\
\end{array}
\end{pmatrix}
$$
此时第二行主元也已经OK，对第三行进行消元，即第三行加第二行的 0.5 倍即可，即得到
$$
\begin{pmatrix}
\begin{array}{cccc|c}
1 & -1  & -1  & 1   & 0   \\
0 &  2  &  4  & -2  & 8  \\
0 &  0  &  0  & -1  & -4   \\
0 &  0  &  1  & 1   & 7   \\
\end{array}
\end{pmatrix}
$$
由于此时第三行主元为0，因此交换第三行和第四行，即得到
$$
\begin{pmatrix}
\begin{array}{cccc|c}
1 & -1  & -1  & 1   & 0   \\
0 &  2  &  4  & -2  & 8  \\
0 &  0  &  1  & 1   & 7   \\
0 &  0  &  0  & -1  & -4   \\
\end{array}
\end{pmatrix}
$$
可表示为线性方程组
$$
\begin{cases}
x - y -z + u = 0      \\
2y + 4z  -2u = 8  \\
z + u = 7  \\
-u = -4  \\
\end{cases}
$$
由下往上求解即可得
$$
\begin{array}{c}
x = 1  \\
y = 2  \\
z = 3  \\
u = 4  \\
\end{array}
$$