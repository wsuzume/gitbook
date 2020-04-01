# 2.2.4. ベイズ線形回帰モデル

前回の確率モデルで事前分布と事後分布をうまく設計すれば、重みについてのベイズ推定を行うことができる。

$$
\begin{aligned}
p(w | \mathcal{D} _ y, \mathcal{D} _ x) &= \frac{p(w)p(\mathcal{D_y | \mathcal{D} _ x, w})}{p(\mathcal{D _  y | \mathcal{D} _ x})} \\
&\propto p(w)p(\mathcal{D_y | \mathcal{D} _ x, w})
\end{aligned}
$$



