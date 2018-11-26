# MAP 推定

ここでは, $$p(\theta)$$ を $$\theta$$ の事前分布, $$\mathcal{D}_N=\{\boldsymbol{x}_n\, |\, n=1,2,\dots,N\}$$ をデータの集合とする. この $$\mathcal{D}_N$$ を観測した条件下での $$\theta$$ の事後分布は $$p(\theta|\mathcal{D}_N)$$ となる.

$$
\hat{\theta}_{\mathrm{MAP}} = \underset{\theta}{\mathrm{argmax}}\, p(\theta | \mathcal{D}_N)
$$

を推定する方法を最大事後確率推定という.

ベイズ(Bayes)の定理より

$$
\hat{\theta}_{\mathrm{MAP}} = \underset{\theta}{\mathrm{argmax}}\, p(\theta | \mathcal{D}_N) = \underset{\theta}{\mathrm{argmax}}\, \frac{p(D|\theta)p(\theta)}{p(\mathcal{D})}
=\underset{\theta}{\mathrm{argmax}}\, p(\mathcal{D}|\theta)p(\theta)
$$

対数函数は単調増加なので

$$
\begin{align}
\theta_{\mathrm{MAP}}
&=
\underset{\theta}{\mathrm{argmax}}\, p(\theta|\mathcal{D}_N) \\
&=
\underset{\theta}{\mathrm{argmax}}\,
p(\mathcal{D}_N|\theta)p(\theta) \\
&=
\underset{\theta}{\mathrm{argmax}}\,
(\log p(\mathcal{D}_N|\theta)+\log p(\theta)) \\
&=
\underset{\theta}{\mathrm{argmax}}\,
\left(\sum_{n=1}^N \log p(x_n|\theta)+\log p(\theta)\right)
\end{align}
$$

# コイン投げの例

コインをトスして表がでたとき1を,裏が出たときに0をとる確率変数を $$x$$ と置く. この時コインの裏表が $$\theta$$ によってコントロールされているとし, $$p(x=1|\theta)=\theta,\ p(x=0|\theta)=1-\theta$$ だとする. この確率変数はベルヌーイ分布に従い、それは次の確率密度関数を持つ:

$$
\mathrm{Bern}(x;\theta)=\theta^x(1-\theta)^{1-x}
$$

ここで, $$N$$ 回コインを投げた結果を記録したデータ

$$
\mathcal{D}_N=\{x_n;n=1,2,\dots,N,\ x_n\in \{0,1\}\}
$$

に関する尤度は次のように書ける:

$$
L(\theta)=\prod_{n=1}^N\mathrm{Bern}(x_n;\theta)=\prod_{n=1}^N \theta^{x_n}(1-\theta)^{1-x_n}.
$$

さて, この尤度を最大にする $$\theta$$ を推定しよう(最尤推定法).

尤度の対数

$$
\log L = \sum_{n=1}^N \left(x_n\log\theta+(1-x_n)\log(1-\theta)\right)
$$

を微分して極値をとる $$\theta$$ をとると

$$
\begin{align}
\frac{d}{d\theta}\log L
&=
\sum_{n=1}^N
\left(
    \frac{x_n}{\theta}-\frac{1-x_n}{1-\theta}
\right)\\
&=
\frac{\sum_{n=1}^N x_n - N\theta}{\theta(1-\theta)}
\end{align}
$$
これから
$$
\theta=\frac{1}{N}\sum_{n=1}^N x_n
$$
となる. これは, 表が出た割合そのものである.

さて, $$\theta$$ には次のようなベータ分布に従っていたとしよう. いわゆる事前分布として

$$
\mathrm{Beta}(\theta;a,b)=\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}\theta^{a-1}(1-\theta)^{b-1}
$$

と与えられていたとする. MAP推定では

$$
\begin{align}
\log p(\mathcal{D}_N|\theta)+\log p(\theta)
&=
\sum_{n=1}^N \left(x_n\log\theta+(1-x_n)\log(1-\theta)\right)+(a-1)\log\theta +(b-1)\log(1-\theta)+\mathrm{const}
\end{align}
$$

となる. 最尤推定と同様にこの関数を $$\theta$$ で微分してその値が0とする条件を課すと

$$
\theta=\frac{\sum_{n=1}^N x_n + a-1}{N+(a+b-2)}
$$

が得られる.これはコインを $$(a+b-2)$$ 回トスして $$(a-1)$$ 回だけ表が出たという状態からさらに $$N$$ 回投げて $$\sum_{n-1}^N x_n$$ 回表が出たとして得られる最尤推定の結果と一致する.



# 線形回帰での例

線形回帰の例では $$\theta$$ として重みベクトル $$\boldsymbol{w}$$ が対応する.

仮に $$\boldsymbol{w}$$ の事前分布 $$p(\boldsymbol{w})$$ として

$$
\mathcal{N}(0, \sigma^2_{0}I_{M}) = \frac{1}{(2\pi\sigma_0^{2})^{M/2}} \exp\left(-\frac{1}{2\sigma_0^2}\boldsymbol{w}^{\top}\boldsymbol{w}\right)
$$

が与えられていたとしよう. ここで $$M$$ はパラメータの数である.

線形回帰モデルで議論した対数尤度の計算に

$$
-\frac{1}{\sigma^2} \sum_{n=1}^N (y_n-\langle\boldsymbol{w},\boldsymbol{x}\rangle)^2
$$

があったことを思い出すと

$$
\begin{align}
\hat{\boldsymbol{w}}
&=
\underset{\theta}{\mathrm{argmax}}\,
\left(\sum_{n=1}^N \log p(y_n|\theta)+\log p(\theta)\right)\\
&=
\underset{\boldsymbol{w}}{\mathrm{argmax}}\,
\left(\frac{1}{\sigma^2}\sum_{n=1}^N (y_n-\langle \boldsymbol{w},\boldsymbol{x}\rangle)^2+\frac{1}{\sigma_0^2}
\langle
\boldsymbol{w},\boldsymbol{w}
\rangle
\right)
\end{align}
$$

これは $$L^2$$ 正則化をつけた最小値問題を解くことに対応している.

他にも $$L^1$$ をつける lasso の場合は事前分布としてラプラス分布

$$
p(\boldsymbol{w})=\left(\frac{1}{2\eta}\right)^K \exp\left(-\frac{||\boldsymbol{w}||}{\eta}\right)
$$

が対応する. 実際, この対数をとると

$$
\log p(\boldsymbol{w})= -\frac{||\boldsymbol{w}||}{\eta}+\mathrm{const}
$$

という形をしているからである.
