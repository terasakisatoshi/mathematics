# エビデンス函数の評価

ベイス的なアプローチで線形モデルは $$\alpha, \beta$$ というパラメータに依存している.これは学習前に事前に設定されるハイパーパラメータである.適切なハイパーパラメータの選択方法について議論する. $$\alpha,\beta$$ 共に確率変数とみなし, あらかじめ観測したデータに関する尤度を考える.

$$
p(y|\alpha,\beta)
=
\int p(\boldsymbol{y}|\boldsymbol{w},\alpha,\beta)p(\boldsymbol{w}|\alpha,\beta)d\boldsymbol{w}.
$$

これをエビデンス函数という.我々はこれを最大化するようなハイパーパラメータを選択するとこにする. ターゲットとする尤度は次のように線形モデル出かける場合に従う分布と事前分布の積を積分し形に分解できる:

$$
\begin{align}
p(\boldsymbol{y}|\alpha,\beta)
&=
\int p(\boldsymbol{y}|\boldsymbol{w},\alpha,\beta)p(\boldsymbol{w}|\alpha,\beta)d\boldsymbol{w}\\
&=
\int p(\boldsymbol{y}|\boldsymbol{w},\beta)p(\boldsymbol{w}|\alpha)d\boldsymbol{w}
\\
&=
\int\prod_{n=1}^N\mathcal{N}(y_n|\langle \boldsymbol{w},\boldsymbol{\phi}(x_n)\rangle,\beta^{-1})\mathcal{N}(\boldsymbol{w}|0,\alpha^{-1}I_M)d\boldsymbol{w} \\
&=
\left(
\frac{\beta}{2\pi}
\right)^{N/2}
\left(
\frac{\alpha}{2\pi}
\right)^{M/2}
 \int \exp(-E(\boldsymbol{w}))d\boldsymbol{w}.
\end{align}
$$

ここで $$M$$ はパラメータの数, $$N$$ は学習データの数であり,

$$
E(\boldsymbol{w})=-\frac{\beta}{2}||\boldsymbol{y}-\Phi\boldsymbol{w}||{}_2^2 + \frac{\alpha}{2}||\boldsymbol{w}||{}_2^2
$$

と置いている. $$E(\boldsymbol{w})$$ を $$\boldsymbol{m}_N=\beta S_N\Phi^{\top}\boldsymbol{y}$$ を用いて

$$
E(\boldsymbol{w})=E(\boldsymbol{m}_N)+\frac{1}{2}(\boldsymbol{w}-\boldsymbol{m}_N)^{\top}S_N^{-1}(\boldsymbol{w}_N-\boldsymbol{m}_N)
$$

のように分解する(計算略).以下、これを認め,

$$
A:=S_N^{-1}=\alpha I+\beta\Phi^{\top}\Phi
$$

とおくと

$$
\begin{align}
\int \exp(-E(\boldsymbol{w}))d\boldsymbol{w}
&=
\exp(-E(\boldsymbol{m}_N))\int \exp\left(-\frac{1}{2}(\boldsymbol{w}-\boldsymbol{m}_N)^{\top}A(\boldsymbol{w}-\boldsymbol{m}_N)\right)d\boldsymbol{w}\\
&=
\exp(-E(\boldsymbol{m}_N))(2\pi)^{M/2}(\det A)^{-1/2}
\end{align}
$$

と計算できる. 従って, エビデンス函数の対数をとると

$$
\log p(\boldsymbol{y}|\alpha,\beta)=\frac{M}{2}\log\alpha+\frac{N}{2}\log\beta -E(\boldsymbol{m}_N)-\frac{1}{2}\log \det A +\mathrm{const}
$$

となる.これを最大化することを考えたい.

## $$\alpha$$ に関して最大化

我々は $$\alpha$$ の微分を求めてきたい. 行列 $$A$$ の行列式の微分を計算するために、$$A$$ の固有値を計算することを考える. 天下りであるが

$$
(\beta\Phi^{\top}\Phi)u=\lambda u
$$

という固有方程式を解くことにする.対称行列なので対角化できる.重複も込めて $$\lambda_1,\dots,\lambda_M$$ が得られたとする. この時 $$A$$ の固有値は $$\alpha+\lambda$$ の形に書けることに注意すると

$$
\frac{\partial}{\partial\alpha}\log \det A
=
\frac{d}{d\alpha}\log\left(\prod_{i=1}^M(\alpha+\lambda_i)\right)=\sum_{i=1}^M \frac{1}{\lambda_i+\alpha}
$$

従って,
$$
\frac{\partial}{\partial\alpha}\log p(\boldsymbol{y}|\alpha,\beta)=\frac{M}{2\alpha}-\frac{1}{2}\langle\boldsymbol{m}_N,\boldsymbol{m}_N\rangle-\frac{1}{2}\sum_{i=1}^M \frac{1}{\lambda_i+\alpha}
$$

この値が 0 になることを要請すると

$$
\alpha
\langle\boldsymbol{m}_N,\boldsymbol{m}_N\rangle
=M-\alpha\sum_{i=1}^M\frac{1}{\lambda_i+\alpha}
$$

という $$\alpha$$ に関する方程式が出来上がる.
ここで, 右辺を $$\gamma$$ とおくと,

$$\gamma=
M-\alpha\sum_{i=1}^M\frac{1}{\lambda_i+\alpha}
=\sum_{i=1}^M\left(1-\frac{\alpha}{\lambda_i+\alpha}\right)
=
\sum_{i=1}^M\frac{\lambda_i}{\lambda_i+\alpha}
$$

と変形できる. まとめると

$$
\alpha=\frac{\gamma}{\langle\boldsymbol{m}_N,\boldsymbol{m}_N\rangle}
$$

となる. ただし, 右辺も $$\alpha$$ に依存しているので　陽に求まる形をしていない.そこで数値計算的に求めることにする.

## $$\alpha$$の逐次計算

まず $$\alpha$$ の初期値を決める.$$\gamma$$ を
$$
\gamma=\sum_{i=1}^M\frac{\lambda_i}{\lambda_i+\alpha}
$$

で定義する. この時固有値は $$\alpha$$ に依存せず定まるので $$\alpha$$の更新のためにわざわざ再計算する必要はないことに注意しておく.一方で $$m_N$$ は $$\alpha$$ に依存するので

$$\boldsymbol{m}_N
=
\beta S_N\Phi^{\top}\boldsymbol{y}
=
\beta(\alpha I+\beta\Phi^{\top}\Phi)\Phi^{\top}\boldsymbol{y}
$$

で定める式で定義する.

そして新しい $$\alpha_{\mathrm{new}}$$ を

$$
\alpha_{\mathrm{new}}=\frac{\gamma}{\langle\boldsymbol{m}_N,\boldsymbol{m}_N\rangle}
$$

で定義する.これで $$\alpha$$ を更新して収束先を決定する.

## $$\beta$$ の決定

上記アルゴリズムで $$\alpha$$ を決めたとする.エビデンス函数を $$\beta$$ で微分する.

まず次が成り立つことに注意する(当たり前のようでなかなか気づきにくい):

$$
\frac{d\lambda_i}{d\beta}=\frac{\lambda_i}{\beta}.
$$

実際, $$\lambda_i$$ の定義(行列の固有ベクトルであること)
から $$\lambda_i=c_i\beta$$ のように書ける.従って,

$$
\frac{d\lambda_i}{d\beta}=c_i=\frac{\lambda_i}{\beta}.
$$

これを用いると

$$
\frac{\partial}{\partial\beta}\log\det A =\frac{\partial}{\partial\beta}\sum_{i=1}^M\log(\lambda_i+\alpha)=\frac{1}{\beta}\sum_{i=1}^M \frac{\lambda_i}{\lambda_i+\alpha}=\frac{\gamma}{\beta}
$$

これからエビデンス函数の $$\beta$$ による微分が0になることを要請すると $$\beta$$ についての方程式

$$
\frac{1}{\beta}=\frac{1}{N-\gamma}\sum_{n=1}^N(y_n-\boldsymbol{m}_N^\top\boldsymbol{\phi}(x_n))^2
$$

を得る.

この方程式の右辺は $$\gamma$$ を含むため $$\beta$$ に依存する ( $$\lambda_i$$ と $$\beta$$ の関係に注意).

従って数値計算的に $$\beta$$ を求める必要がある.

以上のプロセス(チーズ)を得ることによってエビデンス函数を最大にするハイパーパラメータを決定できる.

# Implementation

[This article is helpful](https://qiita.com/amber_kshz/items/35bf3ef761e4d3b248b3)
