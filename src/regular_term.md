# 正則化項の効果のお話

学習データーに適合しすぎると訓練データ以外の未知のデータに対する予測性能（これを汎化性能という）が劣化する過学習の現象が見られる.例えば, 多項式近似の例では, データ数に対して（相対的に）過剰な次数を用意したモデルを導入すると生じやすくなる. これは近似に用いる多項式の係数、すなわち重みベクトルの絶対値、が大きくなる項の存在によって生ずる.

そこで, 最小化する対象 $$E(\boldsymbol{w})$$ に重みベクトルの大きさに制約を与える項 $$R(\boldsymbol{w})$$（正則化項）を付与することがある. 例えば二乗誤差函数の最小化の代わりに

$$
\hat{\boldsymbol{w}}
=
\underset{\boldsymbol{w}}{\mathrm{argmin}}\,
\left(\sum_{n=1}^N (y_n-\langle \boldsymbol{w},\boldsymbol{x}\rangle)^2  + \lambda ||\boldsymbol{w}||{}_p^q \right)
$$

を行う方法がある.

たとえば, $$p=q=2$$ の場合

$$
\frac{\partial}
{\partial \boldsymbol{w}}
\left(
    \left\langle \boldsymbol{y}-X\boldsymbol{w},
    \boldsymbol{y}-X\boldsymbol{w}
    \right\rangle
    +\lambda
    \left\langle
    \boldsymbol{w},
    \boldsymbol{w}
    \right\rangle
\right)
=
2X^\top (\boldsymbol{y}-X\boldsymbol{w})+2\lambda \boldsymbol{w}
$$

この値が0になることを要請することで
$$
\hat{\boldsymbol{w}} = (\lambda I + X^\top X)^{-1}X^\top\boldsymbol{y}
$$

を得る. $$\boldsymbol{w}$$ の空間において同心円上に等高線を引いたとする元々のロス函数の等高線と接する位置で極値をとるようになる.これは重みの $$L^2$$ ノルムの値を固定した条件下での極値問題を逐次解いていくことになるからである. 正確には KKT 条件による極値問題になる.




[See](https://gist.github.com/terasakisatoshi/91d09fef11068b4447dec2998438818b)

<script src="https://gist.github.com/terasakisatoshi/1efa34e74be83ee73c7ca5c9cc381c3a.js"></script>
