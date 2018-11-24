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
