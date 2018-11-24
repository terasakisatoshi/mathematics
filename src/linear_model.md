# 線形モデル、線形回帰のお話

PRML（ぷるぷるむるむる）の線形回帰モデルのお話をします。
エビデンスのお話は他の記事に譲る予定です。

# 記号の導入
## ベクトルと内積

$$K$$ を 1 以上の整数, $$\boldsymbol{x},\boldsymbol{w}$$ を $$K+1$$ 次元ベクトル空間の要素とする.

$$
\boldsymbol{x} =
\begin{bmatrix}
x_0 \\
x_1 \\
\vdots \\
x_K
\end{bmatrix}
\in \mathbb{R}^{K+1}
,\quad
\boldsymbol{w} =
\begin{bmatrix}
w_0 \\
w_1 \\
\vdots \\
w_K
\end{bmatrix}
\in \mathbb{R}^{K+1}.
$$

このとき, $$\boldsymbol{x}$$ と $$\boldsymbol{w}$$ に対して $$\langle\boldsymbol{x},\boldsymbol{w}\rangle$$ を標準的な内積と定義する:

$$
\begin{align}
\langle\boldsymbol{x},\boldsymbol{w}\rangle
&:=
w_0x_0 + w_1x_1 + \dots + w_Kx_K \\
&=
\sum_{k=0}^{K} w_kx_k.
\end{align}
$$

内積は $$\langle\boldsymbol{x},\boldsymbol{w}\rangle = \boldsymbol{x}^{\top} \boldsymbol{y}$$ と記述できる. ここで $$\boldsymbol{x}^{\top}$$ は $$\boldsymbol{x}$$ の転置を表す:

$$
\boldsymbol{x}^{\top} =
\begin{bmatrix}
x_0, x_1,\dots, x_{K}
\end{bmatrix}.
$$



## やりたいこと

下記のように $$K+1$$ 次元空間の要素と実数の組 (データ)
の集合が与えられたとする.

$$
\mathcal{D}_N = \{(\boldsymbol{x}_n,y_n)\, | \, \boldsymbol{x}_n \in \mathbb{R}^{K+1}, y_n \in\mathbb{R}, n \in \{1,2,\dots,N\} \}
$$

このとき, $$(\boldsymbol{x},y) \in \mathcal{D}_N$$ に対して $$\boldsymbol{x}$$ を入力変数, $$t$$ を目標変数と呼ぶことにする.

ただし, 入力変数 $$\boldsymbol{x}$$ は

$$
\boldsymbol{x} =
\begin{bmatrix}
x_0 \\
x_1 \\
\vdots \\
x_K
\end{bmatrix}
\in \mathbb{R}^{K+1},\quad x_0 = 1
$$

という形をしているとする.

各々の要素が $$f(\boldsymbol{x_n})=y_n$$ という関係で与えられているとする. 我々が興味を持つのはこの関係を $$\mathcal{D}_N$$ に属さない入力変数に相当する $$\boldsymbol{x}$$ が与えられたとき, 対応する目標変数の値 $$y$$ がどのようになるかを予測し、データ全体の構造 (母集団) を推定することである. ここでは我々は $$f$$ の形が重みベクトル $$\boldsymbol{w}$$ を用いて

$$
\begin{align}
y
=
f(\boldsymbol{x})
&=
\langle \boldsymbol{w},\boldsymbol{x} \rangle \\
&= w_0 + w_1x_1+\dots+w_Kx_K
\end{align}
$$

のように記述できるモデル（枠組み）で議論をする. このモデルを線形モデルと呼び, このモデルによる推定を線形回帰と呼ぶ.これは　$$\boldsymbol{x}$$ 側の値を固定した時に $$f$$ は $$\boldsymbol{w}$$ に関して線形だからである.

# 基底関数を用いた線形モデル

入力変数 $$\boldsymbol{x}\in \mathbb{R}^{K+1}$$ は関数として一次独立な関数 $$\phi_0,\phi_1,\dots,\phi_K$$ が与えられたとき,

$$
\boldsymbol{x} =
\begin{bmatrix}
\phi_0(x) \\
\phi_1(x) \\
\vdots \\
\phi_K(x)
\end{bmatrix}
\in \mathbb{R}^{K+1},\quad x\in \mathbb{R}
$$

という形をしていても良い. ただし, $$\phi_0$$ は $$\phi_0(x)=1$$ となる定数関数とする. この場合の線形モデルは

$$
\begin{align}
y
=
f(\boldsymbol{x})
&=
\langle \boldsymbol{w},\boldsymbol{x} \rangle \\
&= w_0 + w_1\phi_1(x)+\dots+w_K\phi_K(x)
\end{align}
$$

となる. 例えば, $$\phi_k(x)=x^k\ (k=0,1,2,\dots, K)$$ のように $$x$$ の $k$ をだす関数だとすると, これらは関数として一次独立であり

$$
\begin{align}
y
=
f(\boldsymbol{x})
&=
\langle \boldsymbol{w},\boldsymbol{x} \rangle \\
&= w_0 + w_1x+ w_2x^2+\dots+w_Kx^K
\end{align}
$$

となる. この場合, 線形回帰モデルは $$f$$ を $$w_0, w_1,\dots, w_K$$ を係数とする $$x$$ の多項式にで近似する問題になる.

このように多項式近似の問題を線形モデルの回帰問題として扱うことができる.

他にも互いに異なる $$\mu_k$$ に対して定まるガウス分布と同じ形をするガウス基底関数

$$
\phi_k(x)=\exp\left(-\frac{(x-\mu_k)}{2s^2} \right)
$$

や logistic sigmoid 関数 $$\sigma$$ を用いた sigmoid 関数
$$
\phi_k(x) = \sigma\left(\frac{x-\mu_k}{s}\right), \quad \sigma(a) = \frac{1}{1+\exp(-a)}
$$

などもある（らしい）.

# 尤度最大化による重みパラメータの推定

ここでは, $$N$$ のデータからなるデータ集合

$$
\mathcal{D}_N = \{(\boldsymbol{x}_n,y_n)\, | \, \boldsymbol{x}_n \in \mathbb{R}^{K+1}, y_n \in\mathbb{R}, n \in \{1,2,\dots,N\} \}
$$

から線形モデルのパラメータである重みベクトル $$\boldsymbol{w}$$ を推定していく. データ $$(\boldsymbol{x},y)$$ には $$y=f(x)=\langle \boldsymbol{w},\boldsymbol{x}\rangle$$ という関係を持っているとした現実問題として観測データに当たる目標変数にはノイズ・雑音 $$\varepsilon$$ が混ざっていることが多い.

$$
y=\langle \boldsymbol{w},\boldsymbol{x} \rangle + \varepsilon
$$

このとき $$\varepsilon$$ が導入されることで一見複雑に見えてしまう.しかしこれを逆手に取り, データ集合 $$\mathcal{D}_N$$ に対する尤度を計算することで最尤推定法によって重みベクトル $$\boldsymbol{w}$$ をすることができる. ノイズ $$\varepsilon$$ がある種の確率分布にしたがった値をとるものと仮定する.　これは言い換えるとデータの真の観測値（理想的な観測値）と線形モデルの差がその確率分布に従うということになる. 以下, ノイズが (データとは独立に) 平均 $$\mu=0$$, 分散が $$\sigma^2$$ の正規分布 $$\mathcal{N}(\mu,\sigma^2)$$ に従うとしよう.　これを $$\mathcal{N}(\mu,\sigma^2) \sim \varepsilon$$ と書くことにすれば.

$$
y-\langle \boldsymbol{w}, \boldsymbol{x} \rangle \sim \mathcal{N}(\mu,\sigma^2),\quad \mu=0
$$

と見做すことが出来る. 上述の正規分布 $$\mathcal{N}(\mu,\sigma^2)$$ に対応する確率密度関数

$$
p(x;\mu,\sigma) = \frac{1}{\sqrt{2\pi\sigma^2}}
\exp\left(-\frac{1}{2\sigma^2}(x-\mu)^2\right)
$$

を用いて $$\mathcal{D}_N$$ の尤度(likehood) $$L$$ を計算すると

$$
\begin{align}
L
&= \prod_{n=1}^N p(y_n-\langle \boldsymbol{w}, \boldsymbol{x}\rangle; \mu, \sigma^2) \\
&=
\left(\frac{1}{2\pi\sigma^2}\right)^{N/2} \exp\left(-\frac{1}{2\sigma^2}\sum_{n=1}^N (y_n-\langle \boldsymbol{w}, \boldsymbol{x} \rangle)^2\right)
\end{align}
$$

となる. これを $$\boldsymbol{w}$$ の函数 $$L=L(\boldsymbol{w})$$ とみなし尤度を最大にする $$\boldsymbol{\hat{w}}$$ を計算する（最尤推定法）:

$$
\begin{align}
\boldsymbol{\hat{w}}
&=
\underset{\boldsymbol{\hat{w}}}{\mathrm{argmax}}\, L \\
&=
\underset{\boldsymbol{\hat{w}}}{\mathrm{argmax}}\, \log L \\
&=
\underset{\boldsymbol{\hat{w}}}{\mathrm{argmax}}\, \sum_{n=1}^N (y_n - \langle \boldsymbol{w},\boldsymbol{x}_n\rangle)^2
\end{align}
$$

ここで対数函数が単調増加であることを利用して $$L$$ の対数尤度の計算に帰着している:

$$
\log L = -\frac{N}{2}\log (2\pi\sigma^2) - \frac{1}{2\sigma^2} \sum_{n=1}^N (y_n - \langle
\boldsymbol{w},\boldsymbol{x}_n
\rangle)^2.
$$


## ここまででわかったこと

正規分布の雑音を持つと仮定した線形モデルにおいて最尤推定法による線形回帰の計算は下記の損失函数を

$$
E=E(\boldsymbol{w})=\sum_{n=1}^N (y_n - \langle \boldsymbol{x}_n,\boldsymbol{w}\rangle)^2
$$

最小にする $$\boldsymbol{w}=\boldsymbol{\hat{w}}$$ を求めることに帰着される:

$$
\begin{align}
\boldsymbol{\hat{w}}
:&=
\underset{\boldsymbol{w}}{\mathrm{argmax}}\, L \\
&=
\underset{\boldsymbol{w}}{\mathrm{argmin}}\, E. \\
\end{align}
$$

# ここから示していくこと

$$
\begin{align}
\boldsymbol{\hat{w}}
:&=
\underset{\boldsymbol{w}}{\mathrm{argmax}}\, L \\
&=
\underset{\boldsymbol{w}}{\mathrm{argmin}}\, E. \\
&=
(X^\top X)^{-1}X^{\top}\boldsymbol{y}
\end{align}
$$

ここで $$X$$ は次で与えられる $$N$$ 行 $$(K+1)$$ 列の行列である:

$$
\begin{align}
X
&=
\begin{bmatrix}
\boldsymbol{x_1^\top}\\
\boldsymbol{x_2^\top}\\
\vdots
\\
\boldsymbol{x_N^\top}
\end{bmatrix}
\\
&=
\begin{bmatrix}
x_{10} &x_{11}& \cdots &x_{1K}\\
x_{20} &x_{21}& \cdots &x_{2K}\\
\vdots & \vdots &      &\vdots\\
x_{N0} &x_{N1}& \cdots &x_{NK}\\
\end{bmatrix}.
\end{align}
$$
また,
$$
\boldsymbol{x}_n =
\begin{bmatrix}
x_{n0}\\
x_{n1}\\
\vdots \\
x_{nK}\\
\end{bmatrix}, \quad
\boldsymbol{y}=
\begin{bmatrix}
y_1\\
y_2 \\
\vdots \\
y_N
\end{bmatrix}.
$$

## 計算の方針

まず, $$E$$ が内積を用いて次のように変形できることに注意しよう:

$$
\begin{align}
E
&=
\sum_{n=1}^N (y_n-\langle \boldsymbol{w},\boldsymbol{x}\rangle)^2 \\
&=
\langle y - X\boldsymbol{w}, y-X\boldsymbol{w}\rangle \\
&=
\langle \boldsymbol{y},\boldsymbol{y}\rangle -
\langle \boldsymbol{y},X\boldsymbol{w}\rangle -
\langle X\boldsymbol{w},\boldsymbol{y}\rangle +
\langle X\boldsymbol{w},X\boldsymbol{w}\rangle
\end{align} \\
$$

このように変形したのちに $$E=E(\boldsymbol{w})$$ の勾配を計算することになる:

$$
\frac{\partial{E}}{\partial \boldsymbol{w}}:=
\begin{bmatrix}
\frac{\partial{E}}{\partial{w_0}}\\
\frac{\partial{E}}{\partial{w_1}}\\
\vdots \\
\frac{\partial{E}}{\partial{w_K}}\\
\end{bmatrix} \in \mathbb{R}^{K+1}
$$

### Lemma

- ベクトル $$\boldsymbol{w}$$ に依存しない定数ベクトル $$\boldsymbol{a} \in \mathbb{R}^{K+1}$$ に対して

$$
\frac{\partial}{\partial \boldsymbol{w}} \langle \boldsymbol{a},\boldsymbol{w}\rangle
=
\frac{\partial}{\partial \boldsymbol{w}} \langle \boldsymbol{w},\boldsymbol{a}\rangle
=
\boldsymbol{a}.
$$

これは

$$
\frac{\partial}{\partial w_i} \sum_{j} a_j w_j = a_i
$$

ということから明らか.

- 内積の性質:次が成り立つ:

$$
\langle \boldsymbol{a},X\boldsymbol{b} \rangle = \langle X^\top\boldsymbol{a},\boldsymbol{b} \rangle.
$$

これは次のようにして確かめられる:

$$
\begin{align}
\langle \boldsymbol{a}, X\boldsymbol{b} \rangle
&=
\sum_{j}a_j \sum_{k} X_{jk}\boldsymbol{b}_k \\
&=
\sum_{k}\left(\sum_{j} X_{kj}^{\top} a_j\right) b_k \\
&=
\langle X^{\top} \boldsymbol{a},\boldsymbol{b}\rangle
\end{align}
$$

- ベクトル値函数 $$\boldsymbol{f}, \boldsymbol{g}$$ に対して次が成り立つ:
$$\frac{\partial}{\partial\boldsymbol{w}} \langle\boldsymbol{f}(\boldsymbol{w}),\boldsymbol{g}(\boldsymbol{w})\rangle
=
\begin{bmatrix}
\langle \frac{\partial}{\partial w_1} \boldsymbol{f},\boldsymbol{g}\rangle \\
\langle \frac{\partial}{\partial w_2} \boldsymbol{f},\boldsymbol{g}\rangle \\
\vdots \\
\langle \frac{\partial}{\partial w_K} \boldsymbol{f},\boldsymbol{g}\rangle \\
\end{bmatrix}
+
\begin{bmatrix}
\langle \boldsymbol{f},\frac{\partial}{\partial w_1} \boldsymbol{g}\rangle \\
\langle \boldsymbol{f},\frac{\partial}{\partial w_2} \boldsymbol{g}\rangle \\
\vdots \\
\langle \boldsymbol{f},\frac{\partial}{\partial w_K} \boldsymbol{g}\rangle \\
\end{bmatrix}.
$$

- 特に $$\boldsymbol{f}(\boldsymbol{w})=X\boldsymbol{w}$$ の場合,

$$
\frac{\partial}{\partial{w_k}}X\boldsymbol{w}
=
\begin{bmatrix}
\frac{\partial}{\partial w_{kj}} \sum_{j}X_{ij}w_j
\end{bmatrix}_{i}
=
\begin{bmatrix}
X_{ik}
\end{bmatrix}_{i}
$$

および

$$
\left\langle \frac{\partial}{\partial w_k} X\boldsymbol{w},\boldsymbol{g}\right\rangle =
\begin{bmatrix}
X_{0k},X_{1k},X_{2k},\dots,X_{Nk}
\end{bmatrix}
\begin{bmatrix}
g_1 \\
g_2 \\
\vdots \\
g_N
\end{bmatrix}
$$

を利用することで

$$
\frac{\partial}{\partial \boldsymbol{w}}\left\langle X\boldsymbol{w},\boldsymbol{g}\right\rangle = X^\top \boldsymbol{g}
$$

がわかる。

以上の計算から

$$
\begin{align}
\frac{\partial E}{\partial \boldsymbol{w}}
&=
-
\frac{\partial E}{\partial \boldsymbol{w}}
\langle \boldsymbol{y},X\boldsymbol{w}\rangle -
\frac{\partial E}{\partial \boldsymbol{w}}
\langle X\boldsymbol{w},\boldsymbol{y}\rangle +
\frac{\partial E}{\partial \boldsymbol{w}}
\langle X\boldsymbol{w},X\boldsymbol{w}\rangle \\
&=
-2X^{\top}\boldsymbol{y}
+2X^{\top}X\boldsymbol{w}.
\end{align}
$$

この値が 0 であることを要請し $$\boldsymbol{w}$$ について解くと

$$
\boldsymbol{\hat{w}} = (X^{\top}X)^{-1} X^{\top}\boldsymbol{y}
$$

がわかる.

# ノイズの分散の推定


対数尤度

$$
\log L = -\frac{N}{2}\log (2\pi\sigma^2) - \frac{1}{2\sigma^2} \sum_{n=1}^N (y_n - \langle
\boldsymbol{w},\boldsymbol{x}_n
\rangle)^2
$$

を $$\boldsymbol{w}$$ の函数として尤度の最大化を図った. 尤度には二乗誤差の式とは独立にノイズの標準偏差を表す $$\sigma$$ がある $$\lambda = 1/\sigma^2$$ とおくと

$$
\frac{\partial}{\partial\lambda}\log L = \frac{N}{2\lambda} -\frac{1}{2}\sum_{n=1}^N (y_n - \langle\boldsymbol{w},\boldsymbol{x}_n\rangle)^2.
$$

この値が 0 であることを要請して $$\lambda^{-1}$$ について解くと,

$$
\sigma^2 = \lambda^{-1} = \frac{1}{N} \sum_{n=1}^N(y_n-\langle \boldsymbol{w},\boldsymbol{x}_n\rangle)^2
$$
