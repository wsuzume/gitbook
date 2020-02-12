# 2.2.1. 線形回帰

## 導入

ここではまず簡単な例として1次元の線形回帰について解説する。扱う問題自体は中学校で習うような簡単なものだが、モデリングや数式の表記は手加減せずに論文で使われているレベルのものを用いるので、機械学習の難しい数式に慣れることに集中できるだろう。

流れとしては直線$$y=ax$$による回帰を生成モデルによって捉え直し、最尤推定を行うことで最小二乗法を導出する。今後の議論の基礎になるので、ぜひ時間をかけて取り組んでみてほしい。

## 問題

中学校でオームの法則を習ったことを覚えているだろうか。物体の電気抵抗$$R$$と物体にかける電圧$$V$$、流れる電流$$I$$の間には

$$
V=RI \tag{2.2.1.1}
$$

の関係が成り立つ。この法則を利用すれば物体の電気抵抗を測定でき、物体に所望の電圧をかけたり、電流を流したりできるようになる。

より一般化して$$(2.2.1.1)$$式を直線の方程式で書き直せば

$$
y=ax \tag{2.2.1.2}
$$

となる。電圧、電気抵抗、電流をそれぞれ$$y,a,x$$で置いただけである。機械学習の文化では$$x$$を入力\(input\)、$$y$$を出力\(output\)またはラベル\(label\)という。また$$a$$は重み\(weight\)と呼ばれ、本来なら$$w$$で表記することが多い。

$$(2.2.1.2)$$式のような関係性を持つことがわかっている、またはそのような関係性を持ちそうだと思われる現象は、重み$$a$$さえ求めれば入力から出力を予測できる。いまの状況ではどれくらいの電流を流したときにどれくらいの電圧がかかっているかが推測できる。

中学校や高校の範囲では、適当に1点$$(x,y)$$を測定してそれを代表とし、

$$
a = \frac{y}{x}
$$

とすれば求まるということになっていた。しかし電気抵抗を実際に何回か測定してみると、どの点を代表とするかによって求まる$$a$$の値は若干変わり、毎回同じ値になるとは限らない。これは物体の電気抵抗が温度に依存することや電気回路の接触などに起因するが、何が原因かはよくわからないことがほとんどだろう。

こういった「よくわからない観測値の揺らぎ」の扱いを得意とするのが**確率論**である。中学高校の範囲でならいくつかの観測点について求めた$$a$$を平均する、大学の学部教養レベルであれば最小二乗法を用いて$$a$$を求める、といった方法がある。

どちらも十分に実用的な方法であり、実際それで片付いてしまうことも多いが、いまは機械学習への導入に適した形で問題を解き直そう。

## モデリング

出力$$y$$と入力$$x$$の間には以下の関係があると仮定する。

$$
y = a x + \varepsilon \tag{2.2.1.3}
$$

この式は「$$y$$は基本的に$$ax$$で求まるが、よくわからない誤差$$\varepsilon$$を含む」という意味であり、理論値からのズレを$$\varepsilon$$という補正項に吸収させたことになる。ここで$$\varepsilon$$は平均$$0$$、分散$$\sigma ^ 2$$のガウス分布に従うものとする。

$$
\varepsilon \sim \mathcal{N} (\varepsilon | 0, \sigma ^ 2) \tag{2.2.1.4}
$$

この段階は**モデリング**\(modeling\)といって、**現象に対して人間が勝手に仮定を置くことであり、誤差が本当にガウス分布に従うかどうかはわからない**。しかし人間は現象に何かしら仮定を置かなければ対象を数学的に扱うことはできないし、また仮定の置き方に自由度があることで、人間やコンピュータが計算しやすい形の数式が導出されることもある。仮定がどれだけ正しそうかは、得られた結果を見てから考えればよく、もし満足いかない結果なら満足いくまで仮定を変更すればよい。

**ガウス分布**\(Gaussian distribution\)または**正規分布**\(normal distribution\)は以下の式で定義される連続確率分布である。

$$
\mathcal{N} (x | \mu, \sigma ^ 2) = \frac{1}{\sqrt{2 \pi \sigma ^ 2}} \exp \left(- \frac{(x - \mu) ^ 2}{2 \sigma ^ 2} \right) \tag{2.2.1.5}
$$

出力$$y$$は$$ax$$に$$\varepsilon$$を足したものなので、平均$$ax$$、分散$$\sigma ^ 2$$のガウス分布にしたがうものとみなせるから、その確率分布は

$$
p(y | x, a) = \mathcal{N} (y | ax, \sigma ^ 2) \tag{2.2.1.6}
$$

と表せる。最初なので一応丁寧に書いておくと、

$$
p(y | x , a) = \frac{1}{\sqrt{2 \pi \sigma ^ 2}} \exp \left(- \frac{(y - ax) ^ 2}{2 \sigma ^ 2} \right) \tag{2.2.1.7}
$$

である。パラメータ$$\sigma ^ 2$$は今後の計算にはあまり関わってこないので、議論の簡略化のため既知の定数とした。ちなみに、今回のように出力$$y$$がある確率分布から生成されるモデルを**生成モデル**（generative model）という。

観測した$$n$$個のデータ点の集合を

$$
\mathcal{D} = \left\{ (x ^ {(1)}, y ^ {(1)}), (x ^ {(2)}, y ^ {(2)}), \ldots, (x ^ {(n)}, y ^ {(n)}) \right \} \tag{2.2.1.8}
$$

とおく。$$\mathcal{D} ^ {(i)} = (x ^ {(i)}, y ^ {(i)})$$は$$i$$番目に観測されたデータ点を表し、入力の集合、出力の集合はそれぞれ

$$
\begin{aligned}
\mathcal{D} _ x = \left\{ x ^ {(1)}, x ^ {(2)},  \ldots, x ^ {(n)}\right \} \\
\mathcal{D} _ y = \left\{ y ^ {(1)}, y ^ {(2)},  \ldots, y ^ {(n)}\right \} \tag{2.2.1.9}
\end{aligned}
$$

で表す。

これらのデータ点が独立に観測されたと仮定すると、すべてのデータ点が観測される同時確率分布は

$$
\begin{aligned}
&p(\mathcal{D} _ y | \mathcal{D} _ x , a) \\
=\,&p(y ^ {(1)}, y ^ {(2)}, \ldots, y ^ {(n)} | x ^ {(1)}, x ^ {(2)}, \ldots, x ^ {(n)}, a) \\
=\,& p(y ^ {(1)} | x ^ {(1)}, a) \times p(y ^ {(2)} | x ^ {(2)}, a) \times  \cdots \times p(y ^ {(n)} | x ^ {(n)}, a) \\
=\,& \prod _ {i=1} ^ n p(y ^ {(i)} | x ^ {(i)}, a) 
\end{aligned} \tag{2.2.1.10}
$$

である。$$p(\mathcal{D} _y | \mathcal{D} _ x, a)$$は慣習的に$$p(\mathcal{D})$$という不親切な略記をすることが多いが、今回は丁寧に書いておく。

$$p(\mathcal{D} _y | \mathcal{D} _ x, a)$$はニュアンス的には「入力の集合$$\mathcal{D} _ x$$と重み$$a$$を与えたときの出力の集合$$\mathcal{D} _ y$$の観測されやすさ」を表す指標である。また入力$$\mathcal{D} _ x$$は実験後に動かすことはできないから、重み$$a$$を変数とみなして$$p(\mathcal{D} _y | \mathcal{D} _ x, a)$$を最大化すれば「いま手元にあるデータ$$\mathcal{D} _ y$$を生成しそうな、もっとも尤もらしい重み$$a$$」を求められることになる。

つまり最適化問題

$$
\underset{a \in \mathbb{R}}{\operatorname{arg} \operatorname{max}} \,\,p (\mathcal{D} _ y | \mathcal{D} _ x, a) \tag{2.2.1.11}
$$

を解くことで重み$$a$$を求めよう、というのが機械学習的なアプローチになる。

$$(2.2.1.11)$$式の形で重み$$a$$を推定する手法を**最尤推定**\(さいゆうすいてい：maximum likelihood estimation\)という。ちなみに「尤もらしい」は「もっともらしい」と読む。

$$(2.2.1.11)$$式のような最適化問題の表記は論文や書籍でよく用いられるので覚えておくとよい。**最大化問題**（maximization problem）に使われる$$\operatorname{arg} \operatorname{max}$$は argument of the maximum の略で日本語に訳すと「関数の最大値を与える引数」の意味だ。$$\operatorname{arg} \operatorname{max}$$の下についている$$a \in \mathbb{R}$$は「実数全体の範囲で」の意味であり、$$(2.2.1.11)$$式は「関数$$p(\mathcal{D} _  y | \mathcal{D} _ x, a$$\)の値を最大化する$$a$$を実数全体の範囲で求めよ」という意味になる。この問題の最適解$$a ^ \ast$$は

$$
a ^ \ast = \underset{a \in \mathbb{R}}{\operatorname{arg} \operatorname{max}} \,\,p (\mathcal{D} _ y | \mathcal{D} _ x, a) \tag{2.2.1.12}
$$

のように表記される（$$a ^ \ast$$は$$a _ {\rm opt.}$$などの表記も好まれる）。厳密には最大値を与える$$a$$はひとつとは限らず右辺は集合を表しているものと解釈されるため、左辺が実数であるという意図と矛盾するので、上式のような表記は本来であれば好ましくないのだが、論文や書籍ではよく用いられる。

同様に**最小化問題**（minimization problem）では$$\operatorname{arg} \operatorname{min}$$を用い、これは argument of the minimum の略である。

## 最適化問題を解く

**最適化問題**（optimization problem）が解けるかどうかは異なるし、またその解き方にもバリエーションがあるものだが、$$(2.2.1.11)$$式は対数尤度関数の最大化というよく使われる方法で解ける。

**尤度関数**（likelihood function）はパラメータを変数とみなした関数のことで、今回のケースでは

$$
\mathcal{L}(a | \mathcal{D}) = p (\mathcal{D} _ y | \mathcal{D} _ x, a) \tag{2.2.1.13}
$$

のことである。尤度関数は厳密には確率分布ではないので左辺の表記は条件付き確率分布の表記とややこしいのだが「$$a$$を変数、$$\mathcal{D}$$を定数とみなす」の意味だと思ってもらえればよい。もういっそ単に$$\mathcal{L}(a)$$と書いたほうが誤解しにくいので今回はそうしよう。

対数尤度関数とは尤度関数の対数をとったもの、すなわち

$$
\ln \mathcal{L}(a) \tag{2.2.1.14}
$$

のことである。対数変換は単調変換であるから、対数変換した関数の最大化問題ともとの関数の最大化問題の最適解は一致する。したがって

$$
\underset{a \in \mathbb{R}}{\operatorname{arg} \operatorname{max}} \,\, \ln \mathcal{L}(a) = \underset{a \in \mathbb{R}}{\operatorname{arg} \operatorname{max}} \,\,p (\mathcal{D} _ y | \mathcal{D} _ x, a) \tag{2.2.1.15}
$$

であり、解きやすい左辺のほうを右辺の代わりに解いてもよいことになる。

$$(2.2.1.15)$$式の左辺の$$\ln \mathcal{L}(a)$$を変形していこう。対数を取ると掛け算が足し算になり、さらに$$\exp$$も外れるという部分がミソだ。式変形に使った式番号も書いておくので、少し大変だが追ってみてほしい。

$$
\begin{aligned}
\ln \mathcal{L}(a) &= \ln p(\mathcal{D} _ y | \mathcal{D} _ x, a) \\
&= \ln \prod _ {i=1} ^ n p(y ^ {(i)} | x ^ {(i)}, a) \quad \leftarrow (2.2.1.10) \\
&= \sum _ {i = 1} ^ n \ln p(y ^ {(i)} | x ^ {(i)}, a) \\
&=  \sum _ {i = 1} ^ n \ln \left\{ \frac{1}{\sqrt{2 \pi \sigma ^ 2}} \exp \left(- \frac{(y ^ {(i)}- ax^{(i)}) ^ 2}{2 \sigma ^ 2} \right)  \right\} \quad \leftarrow (2.2.1.7) \\
&= \sum _ {i = 1} ^ n \left[ \ln \left\{ \frac{1}{\sqrt{2 \pi \sigma ^ 2}} \right\} +\ln \left\{ \exp \left(- \frac{(y ^ {(i)}- ax^{(i)}) ^ 2}{2 \sigma ^ 2} \right)  \right\} \right] \\
&= \sum _ {i=1} ^ n  \left(- \frac{(y ^ {(i)}- ax^{(i)}) ^ 2}{2 \sigma ^ 2} \right) + \sum _ {i = 1} ^ n \ln \left\{ \frac{1}{\sqrt{2 \pi \sigma ^ 2}} \right\} \\
&= - \frac{1}{2 \sigma ^ 2} \sum _ {i=1} ^ n (y ^ {(i)}- ax^{(i)}) ^ 2 + n \cdot \ln \left\{ \frac{1}{\sqrt{2 \pi \sigma ^ 2}} \right\}
\end{aligned}
$$

したがって

$$
\ln \mathcal{L}(a) = - \frac{1}{2 \sigma ^ 2} \sum _ {i=1} ^ n (y ^ {(i)}- ax^{(i)}) ^ 2 + n \cdot \ln \left\{ \frac{1}{\sqrt{2 \pi \sigma ^ 2}} \right\} \tag{2.2.1.16}
$$

が求まった。$$a$$に関する最大化問題なので、第1項に関する正数倍、および$$a$$に関係ない第2項は問題の解に影響しないから、

$$
\begin{aligned}
\underset{a \in \mathbb{R}}{\operatorname{arg} \operatorname{max}} \,\, \ln \mathcal{L}(a) &= \underset{a \in \mathbb{R}}{\operatorname{arg} \operatorname{max}} \,\, \left\{ -\sum _ {i=1} ^ n (y ^ {(i)}- ax^{(i)}) ^ 2 \right\} \\
&=\underset{a \in \mathbb{R}}{\operatorname{arg} \operatorname{min}} \,\, \left\{ \sum _ {i=1} ^ n (y ^ {(i)}- ax^{(i)}) ^ 2 \right\}
\end{aligned} \tag{2.2.1.17}
$$

である。$$(2.2.1.17)$$式は**最小二乗法**（least squares method）の式そのものである。

あとは$$a$$に関して整理して

$$
\sum _ {i=1} ^ n (y ^ {(i)}- ax^{(i)}) ^ 2 = \left( \sum _ {i=1} ^ n \left(x ^ {(i)}\right) ^ 2 \right) a ^ 2 - 2 \left( \sum _ {i=1} ^ n x ^ {(i)} y ^ {(i)}\right) a + \left(y ^ {(i)}\right) ^ 2
$$

であり、また二次関数の最小値を取る点は微分して$$0$$になる点だから、

$$
\frac{d}{da} \sum _ {i=1} ^ n (y ^ {(i)}- ax^{(i)}) ^ 2 = 2\left( \sum _ {i=1} ^ n \left(x ^ {(i)}\right) ^ 2 \right) a - 2 \left( \sum _ {i=1} ^ n x ^ {(i)} y ^ {(i)}\right) = 0
$$

より、

$$
a = \frac{ \sum _ {i=1} ^ n x ^ {(i)} y ^ {(i)}}{\sum _ {i=1} ^ n \left(x ^ {(i)}\right) ^ 2} \tag{2.2.1.18}
$$

が解となる。データ点をひとつだけ用いるとき、すなわち$$n=1$$のとき

$$
a = \frac{x ^ {(1)} y ^ {(1)}}{\left(x ^ {(1)}\right) ^ 2} = \frac{y ^ {(1)}}{x ^ {(1)}}
$$

であり、この結果は$$(2.2.1.18)$$式が代表点をひとつ決めて$$a$$を求める方法の一般化になっていることを示している。

これで私たちは最小二乗法の裏にあるモデルとその数理を理解したことになる。これから登場する回帰モデルはほとんど今回の議論の拡張に過ぎないので、ここまでの話を理解できたのであればあとはぐっと楽になるであろう。

