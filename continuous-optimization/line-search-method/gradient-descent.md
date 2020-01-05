# 4.1. 最急降下法

## 原理

最急降下法はもっとも単純で基本的な直線探索法だが、目的関数の勾配（gradient）さえ計算できれば適用できるので汎用性が高い。

目的関数$$f \colon \mathbb{R} ^ n \to \mathbb{R}$$が定義域の全体で微分可能ならばその極値を与える点$$x$$では

$$
\| \operatorname{grad} f (x) \| = 0 \tag{4.1.1}
$$

が成り立つ。最小値は極値であるから、最適化問題

$$
\underset{x \in \mathbb{R} ^ n}{\operatorname{arg} \operatorname{min}} \,\, f(x)
$$

を解くには目的関数を単調減少させながら \(4.1.1\) 式を満たすまで更新を繰り返せばよい。

