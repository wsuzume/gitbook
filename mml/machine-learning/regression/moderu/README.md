# 2.2.3. 線形基底関数モデル

今まで扱ってきた線形回帰や重線形回帰は直線や平面に合わせることしかできず、現実世界の非線形なモデルを扱うには表現力が乏しすぎる。

ニューラルネットについて知りたい人は今回を読んだあとで

{% page-ref page="../neural-network.md" %}

まで飛ばしてよい。

## 線形基底関数モデル

実は前回の線形回帰モデルから変更点はひとつしかない。前回は「切片の項がアンバランスだから」という理由で$$\phi(x)$$という関数を定義したが、実は線形基底関数モデルを見越してのことである。今回はこの$$\phi(x)$$を任意の写像とするだけであり、解法や正則化の議論はまったく変わらない。

説明おしまい。

と締めくくってはあまりにも不親切なので、具体例としてガウス基底関数を紹介したあと、確率モデルの観点から正則化を導出する。

線形回帰モデルで扱っていた関数$$\phi \colon \mathbb{R} ^ n \to \mathbb{R} ^ {n+1}$$は

$$
\begin{aligned}
\phi (x) &= (\phi _ 0 (x), \phi_1(x), \cdots , \phi _n(x)) ^ \mathrm{T} \\
&\phi _ i (x) = \begin{cases}
1 & {\rm if} \,\, i = 0 \\
x _ i & {\rm otherwise}
\end{cases}
\end{aligned} \tag{2.2.3.1}
$$

であった。線形基底関数モデルでは任意の写像$$\phi \colon \mathcal{X} \to \mathbb{R} ^ n$$を用いてよい。すなわち個々の写像は$$\phi _ i \colon \mathcal{X} \to \mathbb{R}$$で

$$
\phi (x) = (\phi _ 1 (x), \phi_2(x), \cdots , \phi _n(x)) ^ \mathrm{T} \tag{2.2.3.2}
$$

である。この$$\phi$$を**基底関数**（basis function）または**特徴量写像**（feature map）という。

$$\phi _ i$$の添字が 0 から始まったり 1 から始まったりしているが、切片の項にあたる定数写像$$\phi _ 0 (x) = 1$$はモデルに付け加えたり外したりがよくあるので、添字 0 を割り当てておくと楽である。つまり線形基底関数モデルでも

$$
\phi (x) = (\phi _ 0 (x), \phi _ 1 (x), \phi_2(x), \cdots , \phi _n(x)) ^ \mathrm{T} \tag{2.2.3.3}
$$

と書けば切片の項があるものとし、

$$
y = \sum _ {i = 0} ^ n w ^ \mathrm{T} \phi _ i (x) +\varepsilon \tag{2.2.3.4}
$$

と書けば切片ありのモデル、

$$
y = \sum _ {i = 1} ^ n w ^ \mathrm{T} \phi _ i (x) +\varepsilon \tag{2.2.3.5}
$$

と書けば切片なしのモデルであると約束しておくと数式を書き直す手間が省けてよい。

また特徴量写像$$\phi$$の定義域$$\mathcal{X}$$は任意の集合である。つまり必ずしも数値データである必要はなく、画像、文字列、グラフといったより一般の対象を入力に取ることができる（ここでは紹介しないがカーネル法の書籍などに具体例が載っているだろう）。

### ガウス基底関数

入力が実数値であるときに用いることができ、特徴量写像には次の$$\phi \colon \mathbb{R} \to \mathbb{R} ^ {n}$$を用いる（$$n$$は使用者が適当に決めてよい）。

$$
\phi _ j (x) = \exp \left(- \frac{(x - \mu _ j )^2}{2 s ^ 2} \right) \quad (\mu _ j \in \mathbb{R}, \,j \in \{0, 1,2, \ldots, n \}) \tag{2.2.3.7}
$$

個々の$$\mu _j $$にどんな値を割振るかも使用者が適当に決める。

他によく使うものについては

{% page-ref page="basis-functions.md" %}

にいくつか書いておいたので、必要ならそちらを参照してほしい。

## 確率モデルと正則化

線形基底関数モデルの正則化は確率モデルからも導くことができ、重みベクトルに事前分布を設定してMAP推定を行うことと等価である。

線形基底関数モデルについて、出力$$y$$、入力$$x$$、重み$$w$$の同時確率分布を以下のように設計する（今回はこう仮定する、という意味であって仮定が異なれば結果は異なる）。

$$
p(y, x, w) = p(y|x,w)p(x)p(w) \tag{2.2.3.8}
$$

したがって、入力$$x$$が与えられたときの出力$$y$$と重み$$w$$の**同時確率分布**（joint probability distribution）は

$$
p(y, w | x) = \frac{p(y,x,w)}{p(x)} = p(y|x,w)p(w)  \tag{2.2.3.9}
$$

である。また、$$w$$が観測されたあとでの各サンプリングは条件付き独立であるとすれば、$$N$$個のデータを持つデータセットの確率分布は

$$
p(Y, w | X) = p(w) \prod _ {i=1} ^ N p(y ^ {(i)} | x ^{(i)}, w)
$$

である。あとは上式の確率分布に対して、出力$$y$$を観測したあとで重み$$w$$を変数として確率密度を最大化する。つまり

{% page-ref page="../../../../math-for-ml/probability-theory.md" %}

で定義した確率密度の表記を用いれば、

$$
\rho_w(y,w|x) = \rho _ w(y|x,w) \rho _ w(w) \tag{2.2.3.10}
$$

を最大化する問題

$$
\underset{w}{\operatorname{arg} \operatorname{max}} \,\, \rho _ w (y,w|x) \tag{2.2.3.11}
$$

を解くことになる。$$(2.2.3.10)$$式の右辺を慣習的に「事後確率」とか「事後分布」と呼ぶが、実際には確率密度（または確率質量）であって、一般には確率でも確率分布でもないことに注意する。

$$
\rho _ w (y, w |x) = \rho _ w(w) \prod _ {i=1} ^ N \rho _ w (y ^ {(i)} | x ^ {(i)}, w)
$$

モデルは

$$
p(w) = \mathcal{N}(w | 0,  \lambda I _ n) = \frac{1}{\sqrt{(2 \pi) ^ n \lambda ^ n}} \exp \left(- \frac{\lambda}{2} w ^ \mathrm{T} w \right)
$$

$$
p(y | x,w) = \mathcal{N}(y | w ^ \mathrm{T} \phi(x), \lambda ^ {-1}) = \frac{1}{\sqrt{2\pi \sigma ^ 2}} \exp \left( - \frac{(y - w ^ \mathrm{T} \phi(x)) ^ 2}{2 \sigma ^ 2} \right)
$$

とすると、

$$
\ln p(w) \prod _ {i=1} ^ N p(y ^{(i)}|x ^ {(i)}, w) = \lambda w ^ \mathrm{T} w + \sum _ {i=1} ^ N (y - w ^ \mathrm{T} \phi(x)) ^ 2
$$

が求まる。



