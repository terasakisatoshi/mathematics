# 線形モデル、線形回帰のお話

PRML（ぷるぷるむるむる）の線形回帰モデルのお話をします。
エビデンスのお話は他の記事に譲る予定です。

# 記号の導入
## ベクトルと内積

$$K$$ を 1 以上の整数, $$\boldsymbol{x},\boldsymbol{w}$$ を $$K+1$$ 次元ベクトル空間の要素とする.

$$\boldsymbol{x} =
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

$$\boldsymbol{x} =
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

のように記述できるモデル（枠組み）で議論をする. このモデルを線形モデルと呼び, このモデルによる推定を線形回帰と呼ぶ.

# 基底関数

入力変数 $$\boldsymbol{x}\in \mathbb{R}^{K+1}$$ として関数として一次独立な関数 $$\phi_0,\phi_1,\dots,\phi_K$$
