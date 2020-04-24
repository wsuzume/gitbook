# 2.2.4. ベイズ線形回帰モデル

前回の確率モデルで事前分布と事後分布をうまく設計すれば、重みについてのベイズ推定を行うことができる。

$$
\begin{aligned}
p(w | y, x) &= \frac{p(y|x,w)p(w)}{p(y,x)} \\
&\propto p(y|x,w)p(w)
\end{aligned}
$$

$$
p(w) = \mathcal{N} (w | \mu, \Sigma) = \frac{1}{\sqrt{(2 \pi ) ^ N | \Sigma |}} \exp \left( - \frac{1}{2}(w - \mu) ^ \mathrm{T} \Sigma ^ {-1} (w - \mu) \right)
$$

$$
p(y | x, w) = \prod _ {i = 1} ^ N \mathcal{N} (y | w ^ \mathrm{T} \phi(x), \lambda ^ {-1})
$$

$$
\begin{aligned}
p(w | y, x) & \propto p(y | x,w)p(w) \\
&= 
\end{aligned}
$$

