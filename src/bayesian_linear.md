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

ここで $$\mu_n = \langle \boldsymbol{w},{\boldsymbol{\phi}(x_n)}\rangle$$, $$\boldsymbol{\mu}=\begin{bmatrix}\mu_n\end{bmatrix}=\Phi\boldsymbol{w}$$ および $$\Sigma = \beta^{-1}I_N$$ である.

## ガウス函数型の事前、事後分布の関係

重みベクトル $$\boldsymbol{w}$$ が次の形の事前分布を持っているとする:

$$
p(\boldsymbol{w})=\mathcal{N}(\boldsymbol{w}|\boldsymbol{m}_0,S_0).
$$

この事前分布から事後分布 $$p(\boldsymbol{w}|\boldsymbol{y})$$ もガウス函数型になり, 具体的には次で与えられる:

$$
p(\boldsymbol{w}|\boldsymbol{y})=\mathcal{N}(\boldsymbol{w}|\boldsymbol{m}_N,S_N).
$$

ここで,

$$
S_N^{-1}
=
S_0^{-1}+\beta \Phi^{\top}\Phi,
\quad
\boldsymbol{m}_N
= S_N^{-1}(S_0^{-1}\boldsymbol{m}_0+\beta\Phi^{\top}\boldsymbol{y}).
$$


これは共役事前分布,条件つきガウス関数型の一般論から導かれる (You can refer your Text book, p90 eq (2.116)):

$$
\begin{align}
p(\boldsymbol{x})
&=
 \mathcal{N}(\boldsymbol{x}|\mu,\Lambda^{-1}) \\
p(\boldsymbol{y}|\boldsymbol{x})
&=
\mathcal{N}(\boldsymbol{y}|A\boldsymbol{x}+b,L^{-1})
\\
\Rightarrow
\\
p(\boldsymbol{y})
&=\boldsymbol{N}(\boldsymbol{y}|A\boldsymbol{\mu}+\boldsymbol{b},L^{-1}+A\Lambda^{-1}A^{\top})\\
p(\boldsymbol{x}|\boldsymbol{y})
&=
\mathcal{N}(\boldsymbol{x}|\Sigma(A^\top L(\boldsymbol{y}-\boldsymbol{b})+\Lambda\boldsymbol{\mu}),\Sigma),\quad \Sigma^{-1}=\Lambda+A^{\top}LA
\end{align}
$$

ここでは、 $$A=\Phi, S_0=\Lambda^{-1}, \boldsymbol{m}_0=\boldsymbol{\mu},\boldsymbol{b}=0,L=\beta I$$ としている.

すでに述べているが, 簡単のために, $$p(\boldsymbol{w})=p(\boldsymbol{w}|\alpha)=\mathcal{N}(\boldsymbol{w},0,\alpha^{-1} I)$$ の場合を考えると,

$$
S_N^{-1}
=
\alpha^{-1}I+\beta \Phi^{\top}\Phi,
\quad
\boldsymbol{m}_N
= S_N^{-1}\beta\Phi^{\top}\boldsymbol{y}.
$$

であって,

$$
\log p(\boldsymbol{w}|\boldsymbol{y})=-\frac{\beta}{2}\sum_{n=1}^N (y_n-\boldsymbol{w}^\top\boldsymbol{\phi}(x_n))^2-\frac{\alpha}{2}\boldsymbol{w}^\top\boldsymbol{w} +\mathrm{const}
$$

要するに正則化項が見える.

# 予測分布

学習前の $$\boldsymbol{w}$$ の事前分布は上記のを踏襲して進める.
新しい入力 $$x$$ に対応する出力 $$y$$ の分布を考える.
これは事前分布に伴う $$\alpha$$ とノイズにともなる $$\beta$$ と学習データにある目的変数がわの値から決まるので $$p(y|\boldsymbol{y},\alpha,\beta)$$ と書ける.データの学習をすることで $$p(\boldsymbol{w})$$ の分布が
$$
p(\boldsymbol{w})=\mathcal{N}(\boldsymbol{w}|\boldsymbol{m}_N,S_N)
$$

に更新されること,

$$
p(y|\boldsymbol{w})=\mathcal{N}(y|\boldsymbol{\phi}(x)\boldsymbol{w},\beta^{-1}I)
$$

であることに注意すると前セクションの一般論を用いると

$$
p(y|\boldsymbol{y},\alpha,\beta)=\mathcal{N}(y|\langle \boldsymbol{\phi}(x),\boldsymbol{m}_N\rangle,\beta^{-1}+\boldsymbol{\phi}(x)^{\top}S_N\boldsymbol{\phi}(x)
$$

新しくデータが増えるたびに分散が小さくなり、最終的には $$\beta^{-1}$$ によって決まるノイズに依存する（らしい）
