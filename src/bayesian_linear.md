# ベイズ推定の立場から見た線形モデル


# ベイズ的に取り扱う線形モデル

ここでは重みパラメータの事前分布を導入することでベイズ的に線形モデルを取り扱うことにする。

## 記号の整備

PRML(プリプリプルンプルン)の記号に合わせるために以下で用いる記号の確認を行う.

基底関数, すなわち, $$\phi_0, \phi_1,\dots,\phi_K$$ を函数として一次独立な函数の組とする. べき乗でも良いし、中心が互いに異なるガウス函数でも良い.
これらに対して, $$\phi(x)$$ を $$M:=(K+1)$$ 次元のベクトル

$$
\boldsymbol{\phi}(x)
=
\begin{bmatrix}
\phi_0(x)\\
\phi_1(x)\\
\vdots
\\
\phi_K(x)
\end{bmatrix}
\in \mathbb{R}^M
$$

とおく. このとき, $$\phi_0$$ はバイアスを表すので定数関数としても良いし, すでにデータが平均が0として正規化されておりバイアス項がないとしても良い（はず）.また, 入力 $$x$$ は１次元と限定する必要はなくなる.ここではひとまず $$x\in\mathbb{R}^d$$ としておく.

観測データは次で与えられるとする:

$$
\mathcal{D}_N=\{(x_n,y_n)\mid x\in\mathbb{R}^d,y_n\in\mathbb{R},n=1,2,\dots,N\}
$$

これに対する計画行列は $$N$$ 行 $$M$$ 列の行列

$$
\Phi
=
\begin{bmatrix}
\boldsymbol{\phi}(x_1)^\top \\
\boldsymbol{\phi}(x_2)^\top \\
\vdots \\
\boldsymbol{\phi}(x_N)^\top
\end{bmatrix}
$$

となる.

データと観測する際に, 目標変数 $$y$$ にはノイズがかかっており真の値とのズレは平均が0で分散が(データの撮り方によらず) $$\beta^{-1}$$ である正規分布に従うとする.

この時, 尤度は

$$
\begin{align}
p(\boldsymbol{y}|\Phi, \boldsymbol{w},\beta)
&=
\prod_{n=1}^N \mathcal{N}(y_n-\langle \boldsymbol{w},\boldsymbol{\phi}(x_n)\rangle,0,\beta^{-1})\\
&=
\prod_{n=1}^M\left(\frac{\beta}{2\pi}\right)^{1/2}\exp\left(-\frac{\beta}{2}(y_n-\mu_n)^2\right)\\
&=
\left(\frac{\beta}{2\pi}\right)^{N/2}
\exp
\left(
    -\frac{\beta}{2}\sum_{n=1}^N (y_n-\mu_n)^2
\right) \\
&=
\left(\frac{\beta}{2\pi}\right)^{N/2}
\exp
\left(
    (\boldsymbol{y}-\boldsymbol{\mu})^\top
    \mathrm{diag}(\beta)
    (\boldsymbol{y}-\boldsymbol{\mu})
\right) \\
&=
\frac{1}{(2\pi)^{N/2}}
\frac{1}{(\det \Sigma)^{1/2}}
\exp
\left(
    (\boldsymbol{y}-\boldsymbol{\mu})^\top
    \Sigma^{-1}
    (\boldsymbol{y}-\boldsymbol{\mu})
\right) \\
&=
\mathcal{N}(\boldsymbol{y}|\Phi\boldsymbol{w},\Sigma).
\end{align}
$$

ここで $$\mu_n = \langle \boldsymbol{w},{\boldsymbol{\phi}(x)}\rangle$$, $$\boldsymbol{\mu}=\begin{bmatrix}\mu_n\end{bmatrix}$$ および $$\Sigma = \beta^{-1}I_N$$ である.
