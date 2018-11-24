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

# 基底関数

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

他にも互いに異なる $$\mu_k$$ に対して定まるガウス分布と同じ形をするガウス基底関数

$$
\phi_k(x)=\exp\left(-\frac{(x-\mu_k)}{2s^2} \right)
$$

や logistic sigmoid 関数 $$\sigma$$ を用いた sigmoid 関数
$$
\phi_k(x) = \sigma\left(\frac{x-\mu_k}{s}\right), \quad \sigma(a) = \frac{1}{1+\exp(-a)}
$$

などもある（らしい）.
