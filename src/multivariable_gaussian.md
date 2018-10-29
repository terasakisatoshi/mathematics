
# 多次元正規分布

確率変数 $y_1,\dots,y_n$ が互いに独立に標準正規分布に従うとする.これらの変数における同時確率密度関数を考える.
確率変数が互いに独立ということから,$$y_1,\dots,y_n$$ の同時確率密度関数 $g(y_1,\dots,y_n)$ は

$$
\begin{align}
g(y_1,\dots,y_n) & = \prod_{j=1}^n
                     \frac{1}{\sqrt{2\pi}}\exp\left(-\frac{y_j^2}{2}\right) \\
                 & = \left(\frac{1}{\sqrt{2\pi}}\right)^n
                     \exp\left(-\frac{1}{2}\sum_{j=1}^n y_j^2\right) \\
                 & = \left(\frac{1}{\sqrt{2\pi}}\right)^n
                     \exp\left(-\frac{1}{2} \boldsymbol{y}^{\top}\boldsymbol{y}\right). \\

\end{align}
$$

ここで

$$
\boldsymbol{y} = \begin{bmatrix} y_1\\y_2\\\vdots\\y_n\\\end{bmatrix}
$$

であって $\boldsymbol{y}^{\top}$ は転置を表している.

今, $T= [t_{ij}]_{i,j=1}^n$ を正則な $n$ 次正方行列とする.

$$
\boldsymbol{x} = T\boldsymbol{y} + \boldsymbol{\mu}
$$

のようにアフィン変換した確率変数に対応する確率密度関数 $f=f(\boldsymbol{x})$ を求める. 上記変換のヤコビアンは

$$
\left[\frac{\partial{x_i}}{\partial y_j}\right]_{i,j=1}^n = \left[t_{ij}\right]_{i,j=1}^n = T
$$


である. よって,多変数の積分の変数変換を考えることで

$$
\begin{align}
\int_{\mathbb{R}} g(\boldsymbol{y})\, dy_1dy_2\cdots dy_n & = \int_{\mathbb{R}}
                                                              g(T^{-1}(\boldsymbol{x}-\boldsymbol{\mu}))
                                                              \left|\det T\right|^{-1}\, dx_1dx_2\cdots dx_n \\
                                             & = \frac{1}{(2\pi)^{n/2}\det T}
                                                 \exp\left(-\frac{1}{2}
                                                           (T^{-1}(\boldsymbol{x}-\boldsymbol{\mu}))^{\top}
                                                           (T^{-1}(\boldsymbol{x}-\boldsymbol{\mu})\right) \\
                                             & = \frac{1}{(2\pi)^{n/2} \sqrt{\det\Sigma}}
                                                 \exp\left(
                                                     -\frac{1}{2}
                                                     (\boldsymbol{x}-\boldsymbol{\mu})^{\top}
                                                      \Sigma^{-1}
                                                     (\boldsymbol{x}-\boldsymbol{\mu})
                                                 \right).
\end{align}
$$

ここで

$$\Sigma = TT^{\top}$$

と置いている.

$$
f(\boldsymbol{x}) =
\frac{1}{(2\pi)^{n/2} \sqrt{\det\Sigma}}
\exp\left(
        -\frac{1}{2}
        (\boldsymbol{x}-\boldsymbol{\mu})^{\top}
         \Sigma^{-1}
        (\boldsymbol{x}-\boldsymbol{\mu})
    \right)
$$

が求めたい関数の形になっている.

# 分散共分散行列(共分散行列)

上では
$$
\Sigma = TT^{\top}
$$
と与えられていたが, これは次で与える分散共分散行列 (または単に共分散行列) と一致する. すなわち:

$$
\Sigma = \mathbb{E} \left[(\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}])(\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}])^{\top}\right].
$$

ここで

$$\mathbb{E}[\boldsymbol{x}]$$

は要素ごとに期待値をとるオペレータ, つまり

$$
\mathbb{E}[\boldsymbol{x}] = \begin{bmatrix}
                                 \mathbb{E}[x_1] \\ \mathbb{E}[x_2] \\ \vdots \\ \mathbb{E}[x_n]
                             \end{bmatrix}
$$

と定める. また,

$$
\boldsymbol{z}=\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}]
$$

とおいたとき,

$$
\begin{align}
(\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}])(\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}])^{\top} &=
\boldsymbol{z} \boldsymbol{z}^{\top} \\
 &=
\begin{bmatrix} z_1\\z_2\\ \vdots \\z_n \end{bmatrix} [z_1, z_2, \dots, z_n] \\
&=
\begin{bmatrix}
z_1^2   & z_1 z_2 & \dots  & z_1 z_n \\
z_2 z_1 & z_2^2   & \dots  & z_2 z_n \\
z_3 z_1 & z_3 z_2 & \ddots & z_3 z_n \\
\vdots  & \vdots  &        & \vdots  \\
z_n z_1 & z_n z_2 & \dots  & z_n^2
\end{bmatrix} \\
&=\left[z_{i}z_{j}\right]_{i,j=1}^n
\end{align}
$$

であることに注意して

$$
\mathbb{E}[(\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}])(\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}])^{\top}]
$$

は行列の要素ごとに期待値をとるオペレータ, つまり

$$
\mathbb{E}[(\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}])(\boldsymbol{x}-\mathbb{E}[\boldsymbol{x}])^{\top}]=\mathbb{E}[\boldsymbol{z}\boldsymbol{z}^{\top}] := \left[\mathbb{E}[z_iz_j]\right]_{i,j=1}^n
$$

で定義する. さて,

$$
\boldsymbol{x}=T\boldsymbol{y}+\boldsymbol{\mu}$$

という変換則だったことを思い出すと

$$
\begin{align}
\mathbb{E}[\boldsymbol{x}] & =\left[\mathbb{E}\left[\sum_{j=1}^n t_{ij}y_j + \mu_i \right]\right]_{i=1}^n
                           = \left[\sum_{j=1}^n t_{ij}\mathbb{E}\left[y_j\right] + \mu_i \right]_{i=1}^n, \\

\mathbb{E}\left[{(\boldsymbol{x}-\boldsymbol{\mu})(\boldsymbol{x}-\boldsymbol{\mu})^{\top}}\right]
&=
\left[\mathbb{E}[z_i z_j]\right]_{i,j=1}^n
=
\left[\mathbb{E}\left[\sum_{k,l=1}^n t_{ik}y_kt_{jl}y_l\right]\right]_{i,j=1}^n.
\end{align}
$$

がわかる. ここで, $y_i$ および $y_j$ が互いに独立な正規分布であったことから

$$
\begin{align}
\mathbb{E}[y_iy_j]&=\mathbb{E}[y_i]\mathbb{E}[y_j] = 0 \quad \mathrm{if} \quad i\neq j\\
\mathbb{E}[y_i^2] & = V[y_i] = 1
\end{align}
$$


などに注意すると

$$
\left[\mathbb{E}\left[\sum_{k,l=1}^n t_{ik}y_kt_{jl}y_l\right]\right]_{i,j=1}^n
=
\left[\sum_{k,l=1}^n t_{ik}t_{jl} \delta_{k,l} \right]_{i,j=1}^n
=
\left[ \sum_{k=1}^n t_{ij} t_{jk} \right]_{i,j=1}^n = T T^{\top}.
$$

よって, 示したいことが示された.
