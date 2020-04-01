---
description: 2020/4/2公開
---

# 2.2.2. 線形回帰モデルと正則化

## 導入

前回は$$y=ax$$という非常に簡単なモデルを扱ったが、では切片を追加して

$$
y = ax + b \tag{2.2.2.1}
$$

としたらどうなるだろうか。また、もっと入力を増やして

$$
y = w _ 0 + w _ 1 x _ 1 + w _ 2 x _ 2 + \cdots + w _ n x _ n \tag{2.2.2.2}
$$

としたらどうだろう。つまり出力$$y$$を決めうるファクターとしての入力が$$x = (x _ 1, x _ 2, \ldots, x _ n)$$のように複数ある状況を想定している。

今回は線形回帰モデルを扱うことにしよう。

## モデリング

実は入力を増やすだけであればやることはほとんど変わらない。$$(2.2.2.2)$$式は$$(2.2.2.1)$$式の拡張になっているから、$$(2.2.2.2)$$式についてだけ議論すればよく、前回と同様にガウス分布に従う誤差$$\varepsilon$$を導入して

$$
y = w _ 0 + w _ 1 x _ 1 + w _ 2 x _ 2 + \cdots + w _ n x _ n + \varepsilon \tag{2.2.2.3}
$$

とすればよい。出力$$y$$を$$(2.2.2.3)$$式で表現するモデルを**線形回帰モデル**（linear regression model）という。やることは前回『2.2.1. 線形回帰の基礎』とほとんど同じでやることがなさすぎるので、ついでに$$(2.2.2.3)$$式を今後使いやすい形に整えておこう。

まず$$(2.2.2.3)$$式で切片$$w _ 0$$の項には$$x$$が現れないのでアンバランスである。そこで

$$
\phi _ i (x) = \begin{cases}
1 & {\rm if} \,\, i = 0 \\
x _ i & {\rm otherwise}
\end{cases} \tag{2.2.2.4}
$$

とおく。今後は煩雑化を防ぐために$$\phi _ i ^ {(j)} = \phi _ i (x ^ {(j)} )$$という書き換えを断りなく用いることがある。このとき$$(2.2.2.3)$$式は

$$
\begin{aligned}
y &= w _ 0 \phi _ 0 (x) + w _ 1 \phi _ 1 (x) + w _ 2 \phi _ 2 (x) + \cdots + w _ n \phi _ n (x) + \varepsilon \\
&= \sum _ {i=0} ^ n w _ i \phi _ i (x) + \varepsilon \\
&= w ^ \mathrm{T} \phi(x)  + \varepsilon
\end{aligned} \tag{2.2.2.5}
$$

と書ける。上式の$$w ^ \mathrm{T} \phi(x)$$は**行列**（matrix）による表記である。つまり

$$
y = (
w _ 0 \,\,\, w _ 1 \,\,\, w_ 2 \, \cdots \, w _ n ) \left(
\begin{matrix}
\phi _ 0 (x) \\
\phi _ 1 (x) \\
\phi _ 2 (x) \\
\vdots \\
\phi _ n (x)
\end{matrix}
\right) + \varepsilon \tag{2.2.2.6}
$$

である。前回の内容と並べて

$$
\begin{aligned}
y &= ax + \varepsilon \\
y &= w ^ \mathrm{T} \phi(x) + \varepsilon
\end{aligned} \tag{2.2.2.7}
$$

と書けば、とても構造が似通った問題だとわかる。前回と同様にノイズを

$$
\varepsilon \sim \mathcal{N} (\varepsilon | 0, \sigma ^ 2) \tag{2.2.2.8}
$$

とおけば、

$$
p(y | x, w) = \mathcal{N}(y | w ^ \mathrm{T} \phi(x), \sigma ^ 2) \tag{2.2.2.9}
$$

となるので、尤度関数は

$$
\mathcal{L}(w|\mathcal{D}) = \prod _ {i=1} ^ N \frac{1}{\sqrt{2 \pi \sigma ^ 2}} \exp \left(- \frac{(y ^ {(i)} - w ^ \mathrm{T} \phi (x ^ {(i)})) ^ 2}{2 \sigma ^ 2} \right) \tag{2.2.2.10}
$$

である。最尤推定の文脈で解くべき最適化問題は

$$
\underset{w \in \mathbb{R} ^ {n+1}}{\operatorname{arg} \operatorname{max}} \,\, \mathcal{L} (w | \mathcal{D})
$$

となる。

### 最適化問題の解法

今回の尤度関数は多変数関数である。一応、丁寧に書いておけば

$$
\mathcal{L}(w | \mathcal{D}) = \mathcal{L}(w _ 0, w _ 1, w _ 2 , \ldots, w _ n | \mathcal{D}) \tag{2.2.2.11}
$$

である。求めるべき変数は増えたがせいぜい2次関数を多変数に拡張したものにすぎないので、方針は前回と変わらず微分して 0 になる点を探すことになる。まずはさくさくと対数尤度関数を用いた最適化問題に変形してしまおう。途中計算は前回とまったく同様なのでごっそり省くが、

$$
\begin{aligned}
\underset{w \in \mathbb{R} ^ {n+1}}{\operatorname{arg} \operatorname{max}} \,\, \ln \mathcal{L}(w | \mathcal {D}) &= \underset{w \in \mathbb{R} ^ {n+1}}{\operatorname{arg} \operatorname{max}} \,\, \left\{ -\sum _ {i=1} ^ N (y ^ {(i)}- w ^ \mathrm{T} \phi(x^{(i)})) ^ 2 \right\} \\
&=\underset{w \in \mathbb{R} ^ {n+1}}{\operatorname{arg} \operatorname{min}} \,\, \left\{ \sum _ {i=1} ^ N (y ^ {(i)} - w ^ \mathrm{T} \phi(x^{(i)})) ^ 2 \right\}
\end{aligned} \tag{2.2.2.12}
$$

である。上式は行列を用いてもっと綺麗に書き直せる。つまり$$N$$次元ベクトル$$a = (a _ 1, a _ 2, \ldots, a_N) ^ \mathrm{T}$$について一般に

$$
\| a \| ^ 2 =  a ^ \mathrm{T} a = \sum _ {i = 1}  ^ N a _ i ^ 2 \tag{2.2.2.13}
$$

が成り立つことを用いればよい。いま

$$
y ^ {(i)} - w ^ \mathrm{T} \phi(x ^ {(i)}) \tag{2.2.2.14}
$$

の部分は、

$$
y ^ {(i)} - \phi(x ^ {(i)}) ^ \mathrm{T}  w \tag{2.2.2.15}
$$

と書いても同じことであるから、各データ点について式を列挙すれば

$$
\left(
\begin{matrix}
y ^ {(1)} - \phi (x ^ {(1)}) ^ \mathrm{T}  w \\
y ^ {(2)} - \phi (x ^ {(2)}) ^ \mathrm{T}  w \\
\vdots \\
y ^ {(N)} - \phi (x ^ {(N)}) ^ \mathrm{T}  w
\end{matrix}
\right) \tag{2.2.2.16}
$$

であり、$$\phi _ i ^ {(j)} = \phi _ i (x ^ {(j)} )$$の略記と

$$
y = \left(
\begin{matrix}
y ^ {(1)} \\
y ^ {(2)} \\
\vdots \\
y ^ {(N)}
\end{matrix}
\right), \quad \Phi ^ \mathrm{T} = \left(
\begin{matrix}
\phi _ 0 ^ {(1)} & \phi _ 1 ^ {(1)} & \cdots & \phi _ n ^ {(1)} \\
\phi _ 0 ^ {(2)} & \phi _ 1 ^ {(2)} & \cdots & \phi _ n ^ {(2)} \\
\vdots \\
\phi _ 0 ^ {(N)} & \phi _ 1 ^ {(N)} & \cdots & \phi _ n ^ {(N)} \\
\end{matrix}
\right), \quad w = \left(
\begin{matrix}
w ^ {(0)} \\
w ^ {(1)} \\
\vdots \\
w ^ {(n)}
\end{matrix}
\right) \tag{2.2.2.17}
$$

を用いれば、

$$
\left(
\begin{matrix}
y ^ {(1)} - \phi (x ^ {(1)}) ^ \mathrm{T}  w \\
y ^ {(2)} - \phi (x ^ {(2)}) ^ \mathrm{T}  w \\
\vdots \\
y ^ {(N)} - \phi (x ^ {(N)}) ^ \mathrm{T}  w
\end{matrix}
\right) = y - \Phi ^ \mathrm{T} w \tag{2.2.2.18}
$$

と書ける。したがって$$(2.2.2.12)$$式は

$$
\underset{w \in \mathbb{R} ^ {n+1}}{\operatorname{arg} \operatorname{max}} \,\, \ln \mathcal{L}(w | \mathcal {D}) =\underset{w \in \mathbb{R} ^ {n+1}}{\operatorname{arg} \operatorname{min}} \,\, \| y - \Phi ^ \mathrm{T} w\| ^ 2 \tag{2.2.2.19}
$$

と非常にシンプルな式で記述できる。

ではこの問題を解いていこう。あらためて目的関数を

$$
f(w) = \| y - \Phi ^ \mathrm{T} w\| ^ 2 \tag{2.2.2.20}
$$

とおく。多変数関数なので偏微分（勾配ベクトル）が 0 ベクトルになる場所が最小値である。勾配ベクトル$$\nabla f(w)$$は

$$
\nabla f(w) = - 2 \Phi(y - \Phi ^ \mathrm{T} w) \tag{2.2.2.21}
$$

であるから、これが 0 ベクトルに等しいとき、

$$
\Phi \Phi ^ \mathrm{T} w = \Phi y \tag{2.2.2.22}
$$

となる。上式を線形回帰の**正規方程式**（normal equation）という。正規方程式は$$\Phi \Phi ^ \mathrm{T} $$が正則なとき、ただそのときに限り唯一の解

$$
w = (\Phi \Phi ^ \mathrm{T}) ^ {-1} \Phi y \tag{2.2.2.23}
$$

を持つ。これで$$\Phi \Phi ^ \mathrm{T} $$が正則なときは重みベクトルが求まった。

## 正則化

さて、次は当然の疑問として「$$\Phi \Phi ^ \mathrm{T} $$が正則でないとき重みベクトルはどう求めればよいのか」と考えるだろう。結論から言えば、正則でないならば無理やり正則にしてしまえばよい。目的関数$$g(w)$$に狭義単調増加関数$$\Psi$$を付け加えた関数

$$
f(w) = g(w) + \Psi( \|w \|) \tag{2.2.2.24}
$$

を新たな目的関数とする操作を**正則化**（regularization）といい、このとき$$\Psi(\|w\|)$$を**正則化項**（regularization term）という。いきなりややこしくなったので少しずつよく使われる形にしていこう。

### ノルム

まず知っておいてほしいのが、**ノルム**（norm）の概念だ。聞き慣れない言葉かもしれないが、ラテン語のノルマ（norma：定規のこと）が英語になったもので「長さを測るもの」をイメージしてもらえればよく、ノルムはその名の通りベクトルの長さを測る数学の道具である。

私たちが日常生活で使っている「距離」の概念は、実は$$L^2$$-ノルムに対応している。ベクトル$$a = (a _1, a _ 2, \ldots, a _ n ) ^ \mathrm{T}$$の$$L^2$$-ノルムは$$\| a \| _ 2$$と表記し、

$$
\| a \| _ 2 = \sqrt{ a _ 1 ^ 2 + a _ 2 ^ 2 + \cdots + a _ n ^ 2} \tag{2.2.2.25}
$$

で定義される。一般に、$$L ^ p$$-ノルムは$$|\cdot |$$を絶対値の記号として

$$
\| a \| _ p = (|a _ 1| ^ p + |a _ 2 | ^ p + \cdots + |a _ n |^ p) ^ {1/p} \tag{2.2.2.26}
$$

で定義される。ここでは説明しないが、ノルムはノルムで定義があって、ノルムの性質を満たす関数ならばなんでもノルムと呼んでよく、$$L ^ p$$-ノルム自体は無数に存在するノルムのうちでも特殊なものである。たとえば$$L ^ 1$$-ノルムと$$L ^ 2$$-ノルムを足した

$$
\| a \| = \|a\| _ 1+ \| a \| _ 2 \tag{2.2.2.27}
$$

もノルムの性質を満たすので、これを新たなノルムとしてもよい。

$$(2.2.2.20)$$式では目的関数を$$f(w) = \| y - \Phi ^ \mathrm{T} w \| ^ 2$$と書いたが、これはより正確さを期するならば

$$
f(w) = \| y - \Phi ^ \mathrm{T} w \| _ 2^ 2 \tag{2.2.2.28}
$$

と書くほうがよい。よっていま$$(2.2.2.24)$$式では

$$
g(w) = \| y - \Phi ^ \mathrm{T} w \| _ 2^ 2 \tag{2.2.2.29}
$$

としよう。$$(2.2.2.24)$$式内にある$$\|w\|$$のノルムは任意である。よく使うのはやはり$$L ^ 2$$-ノルムで、狭義単調増加関数に$$\Psi(x) = \lambda x ^ 2 \,\, (\lambda > 0)$$を用いれば

$$
f(w)= \| y - \Phi ^ \mathrm{T} w \| _ 2^ 2 + \lambda \| w \| _ 2 ^ 2 \tag{2.2.2.30}
$$

となる。これは正則化項に$$L ^ 2$$-ノルムを用いているので$$L^2$$-正則化と呼んだりする。

### L2正則化問題の解法

問題が複雑になったように見えるが、$$w$$に関する2次形式（行列とベクトルでいうところの2次関数）であることは変わっていないので、先ほどと同様に微分して 0 でよい。

$$
\nabla f(w) = - 2 \Phi(y - \Phi ^ \mathrm{T} w) + 2 \lambda w \tag{2.2.2.31}
$$

であるから、

$$
- 2 \Phi(y - \Phi ^ \mathrm{T} w) + 2 \lambda w = 0 \\
\therefore (\Phi \Phi ^ \mathrm{T} + \lambda I) w = \Phi y \tag{2.2.2.32}
$$

となる。ここで$$I$$は単位行列であり$$(\Phi \Phi ^ \mathrm{T} + \lambda I)$$は必ず正則な行列になる（$$\Phi \Phi ^ \mathrm{T}$$は半正定値対称行列であり、$$I$$は正定値対称行列だから、それらの線形結合は正定値対称行列になる）から、逆行列が存在して、

$$
w = (\Phi \Phi ^ \mathrm{T} + \lambda I) ^ {-1} \Phi y \tag{2.2.2.33}
$$

となる。

### 他の正則化

正則化項には任意のノルム$$\| \cdot \|$$と任意の狭義単調増加関数$$\Psi$$を用いてよいので選択肢の幅はかなり広いのだが、機械学習の分野で使われる正則化項はだいたい次の3種類である。もっと複雑な正則化項（グラフ正則化など）もあるので、論文を読むときはどんな目的関数にどんな正則化項がくっついているか確かめると面白い。

#### L1正則化

ベクトルの個々の要素の絶対値の和を正則化項にとる。

$$
\Psi (\| w\|) = \lambda \| w \| _ 1 \tag{2.2.2.34}
$$

$$L^1$$-正則化による線形回帰は**LASSO**（least absolute shrinkage and selection operator）と呼ばれ、解がスパースになる（重みベクトル$$w$$の要素で 0 が選択されやすくなる）ことが知られている。目的関数が滑らかでなくなるので「微分して 0 になる」が使えない典型的な問題である。

{% page-ref page="../../data-science/sparse-modeling/lasso/" %}

#### L2正則化

先ほど紹介した通りである。

#### エラスティックネット

エラスティックネット（elastic net）による正則化は$$L ^ 1$$-正則化と$$L^2$$-正則化の折衷案である。

$$
\Psi (\| w\|) = \alpha \| w \| _ 1 + \beta \| w \| _ 2 ^ 2 \tag{2.2.2.35}
$$

$$L ^ 1$$-正則化は解がスパースになる反面、関数の形状があまりよくないので学習アルゴリズムが収束しづらくなる。一方で$$L ^ 2$$-正則化は学習アルゴリズムの収束性がよい反面、解にスパース性は望めない。そこでエラスティックネットはこれらの正則化項を足し合わせることで、学習アルゴリズムを収束しやすくしつつスパースな解を得ることを期待する。

深層学習ではパラメータが非常に多いため、とっとと収束してもらいたいが、解がスパースでないとネットワークが無駄な枝を残して圧縮したりできないので、エラスティックネットを使うことがよくある。勾配法などで解く。

