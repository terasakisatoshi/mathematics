# バイアス・バリアンス分解

観測データの集合 $$\mathcal{D}_N=\{(\boldsymbol{x}_n,y_n)\, |\, n=1,2,\dots,N\}$$ から学習されたモデルにおいて, 新しいデータ $$\boldsymbol{x}$$ に対して $$y$$ の予測する予測値
$$y(\boldsymbol{x})$$ の真の値 $$y_t$$ のズレを損失という. ここではズレの指標として二乗誤差 $$\mathcal{L}(y(\boldsymbol{x}))=(y(\boldsymbol{x})-y_t)^2$$ について考える. これは $$y$$ についての汎関数になっている. $$p(\boldsymbol{x},y_t)$$ を $$\boldsymbol{x}$$ と $$y_t$$ の同時分布とおく. 損失函数の期待値は次で与えられる.

$$
\mathbb{E}[\mathcal{L}(y)]=\iint (y(\boldsymbol{x})-y_t)^2p(\boldsymbol{x},y)\, dy_td\boldsymbol{x}
$$

定義により様々な $$\boldsymbol{x}$$ を観測した際の $$y(\boldsymbol{x})$$ と $$y_t$$ のズレの平均を表している.

このズレを最小にする $$y=y(\boldsymbol{x})$$ は次のように書ける:

$$
\underset{y}{\mathrm{argmax}}\, \mathbb{E}[\mathcal{L}(y)] = \mathbb{E}[y_t|\boldsymbol{x}] = \int y_t p(y_t|\boldsymbol{x})dy_t
$$

証明

いま, $$y: \boldsymbol{x} \mapsto y(\boldsymbol{x})$$ が $$E[\mathcal{L}(y)]$$ を最小にするものとする. この $$y$$ に良い条件を持つ (e.g. 十分滑らかな) テスト函数 $$\eta$$ をわずかに付与, すなわち十分に小さい $$\varepsilon$$ を用いて $$y+\varepsilon\eta$$, なるものを考える. このとき

$$
\lim_{\varepsilon\to 0} \frac{\mathbb{E}[\mathcal{L}(y+\varepsilon\eta)]-\mathbb{E}[\mathcal{L}(y)]}{\varepsilon} = 0
$$

を要請する (平たくいうと汎関数 $$\mathbb{E}[\mathcal{L}(\cdot)]$$ の極値).

![imageisimage](images/variational_method.png)
