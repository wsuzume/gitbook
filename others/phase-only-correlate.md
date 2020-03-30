---
description: 2020/3/30公開
---

# 位相限定相関法

## はじめに

位相限定相関法（POC:Phase-Only Correlation）は高速かつ高精度にテンプレートマッチングを行う手法である。大抵は画像の横ズレ・縦ズレを検出するために用いられる。さらにLog-Polar変換をかけた画像に対して適用することで回転ズレ・スケールの違いを検出する回転不変位相限定相関法（RIPOC:Rotation Invariant Phase-Only Correlation）が導かれる。

## 位相限定相関法

テンプレートマッチングはテンプレート画像が与えられた画像のどこに埋め込まれているかを探す問題のことである。

位相限定相関法はその名の通り、信号の位相の情報に限定して相関をとる手法で、フーリエ変換の性質をうまく利用することで「ある位置ズレを与えたときに2つの画像がどの程度一致しているか」の評価を$$O(1)$$で行うことを可能にしている。計算量のほとんどは画像をフーリエ変換・逆フーリエ変換する部分に使われる。

### 画像の離散フーリエ変換

$$\mathbb{R}$$を実数全体の集合、$$\mathbb{C}$$を複素数全体の集合とする。また$$\mathbb{M} = \{ 0, 1, 2, \cdots, M - 1 \}$$、$$,\mathbb{N}= \{ 0, 1, 2, \cdots, N - 1 \}$$とおく。

サイズ$$M \times N$$の画像は位置$$x,y$$に対して画素値$$f (x,y)$$が定まる信号とみなすことができる（より数学的な表記が好みの人のために書いておくと$$f \colon \mathbb{M} \times \mathbb{N} \to \mathbb{R} \colon (x,y) \mapsto f(x,y)$$である）。

この信号を離散フーリエ変換（DFT:discrete Fourier transform）した信号を$$F(u,v)$$とおく（こちらは$$F \colon \mathbb{M} \times \mathbb{N} \to \mathbb{C} \colon (u, v) \mapsto F(u,v)$$となる）。すなわち

$$
F(u,v) = \frac{1}{\sqrt{MN}} \sum _ {x = 0} ^ {M - 1}\sum _ {y = 0} ^ {N - 1} f(x, y) \exp \left( - 2 \pi i \left( \frac{ux}{M} + \frac{vy}{N} \right) \right) \tag{1}
$$

である。余計な記号が多いので

$$
j = - \frac{2 \pi i}{M}, k= - \frac{2 \pi i}{N} \tag{2}
$$

を用いて整えつつ、離散フーリエ変換の作用素$$\mathcal{F}$$を導入しておくと

$$
F(u,v) = (\mathcal{F} f)(u,v)= \frac{1}{\sqrt{MN}} \sum _ {x \in \mathbb{M}} \sum _ {y \in \mathbb{N}} f(x, y) \exp \left( jux + kvy \right) \tag{3}
$$

である（作用素を導入しておくと$$F = \mathcal{F}f$$と書ける）。

逆離散フーリエ変換（IDFT:inverse discrete Fourier transform）は偏角が逆向きの変換で

$$
f(x,y) = (\mathcal{F} ^ {-1} F)(x,y) =  \frac{1}{\sqrt{MN}} \sum _ {u \in \mathbb{M}} \sum _ {v \in \mathbb{N}} F(u, v) \exp \left( - (jux + kvy) \right) \tag{4}
$$

で定義できる（同様に$$f = \mathcal{F} ^ {-1}F$$である）。

### 位相限定画像

位相限定相関法では位相限定画像の内積を扱う。DFTした後の信号$$F(u, v)$$は複素数信号なので、振幅$$A(u,v)$$と位相$$\exp (i \phi(u,v))$$の情報を持っており、それらの積の形に分解できる。すなわち

$$
F(u,v) = A(u,v) \exp (i \phi(u,v)) \tag{5}
$$

である。位相限定相関法においては、この画像の位相成分$$\exp (i \phi(u,v))$$を**位相限定画像**（phase-only image）と呼ぶ。

位相限定画像$$P(u,v)$$を求めるには、DFTした画像$$F(u,v)$$を、それ自身の振幅$$A(u, v) = | F(u,v) | $$で割ればよい。すなわち直感的には$$P (u,v) = \exp(i\phi(u,v))$$であり、

$$
P(u,v) = \frac{F(u,v)}{| F(u,v) |} \tag{6}
$$

である。ただし、ある$$(u,v)$$において$$| F(u,v) | = 0$$のとき$$(6)$$式の左辺は定義できない。より正確には$$(5)$$式を満たしさえすればよいので振幅が 0 の周波数$$(u,v)$$に対応する位相$$P(u,v)$$は任意である。実際の計算では分母に微小な正数$$\varepsilon$$を足すことで 0 割りによるエラーを防ぎつつ

$$
P(u,v) = \frac{F(u,v)}{| F(u,v) | + \varepsilon} = \frac{0}{0 + \varepsilon} = 0 \tag{7}
$$

としておく。

位相限定画像は、直感的には画像の形状に関する情報を保持している。実際に位相限定画像を逆フーリエ変換で空間領域の関数$$p = \mathcal{F} ^ {-1} P$$に戻してからその実部を表示すると、元の画像が浮かび上がる。一応丁寧に書いておくと、

$$
p(x,y) = \frac{1}{\sqrt{MN}} \sum _ {x \in \mathbb{M}} \sum _ {y \in \mathbb{N}} P(u, v) \exp \left( - (jux + kvy) \right)  \tag{8}
$$

である。

一般に、画像は低周波成分の振幅が大きく、高周波成分の振幅が小さい。そして高周波成分には画像の輪郭の情報が含まれているから、周波数領域での画像$$F(u,v)$$をその振幅で割った位相限定画像への変換は元の画像の輪郭を強調する変換であるとも解釈できる。

### 位相限定相関法

位相限定相関法は理論的には空間領域における位相限定画像を用いたテンプレートマッチングである。与えられたサイズ$$M ^ \prime \times N ^ \prime$$の画像$$f(x ^ \prime,y ^ \prime)$$の中から、サイズ$$M  \times N  \,\,(M \leq M ^ \prime, N \leq N ^ \prime)$$のテンプレート画像$$g(x, y)$$が一致する場所を探す。

テンプレートが完全に一致する点$$(\Delta x, \Delta y)$$では画像どうしの内積が最大になる。すなわちテンプレートマッチングの問題は

$$
\underset{(\Delta x, \Delta y)}{\operatorname{arg}\operatorname{max}} \sum _ {x \in \mathbb{M}} \sum _ {y \in \mathbb{N}} f(x + \Delta x, y + \Delta y) g(x, y) \tag{9}
$$

と書ける。位相限定相関法では代わりに位相限定画像どうしの内積が最大になる点を探す。つまり与えられた画像、テンプレート画像のそれぞれの位相限定画像を$$p(x ^ \prime, y ^ \prime), q(x,y)$$とおけば

$$
\underset{(\Delta x, \Delta y)}{\operatorname{arg}\operatorname{max}} \sum _ {x \in \mathbb{M}} \sum _ {y \in \mathbb{N}} p(x + \Delta x, y + \Delta y) q(x, y) \tag{10}
$$

である。位相限定画像は元の画像の輪郭の情報が強調されているから、画像の輪郭がぴったり合う点を探せという問題に置き換わったとも解釈できる。

ところで$$(9)$$式や$$(10)$$式の

$$
\sum _ {x \in \mathbb{M}} \sum _ {y \in \mathbb{N}} f(x + \Delta x, y + \Delta y) g(x, y) \tag{11}
$$

の部分は、畳み込み積分によく似ている。実際これは2つの信号の間の**相互相関関数**（cross-correlation function）であり、片方の信号を反転して畳み込み積分をかけたものに一致する。信号$$f$$と$$g$$の相互相関関数は

$$
(f \star g)(s, t) = \sum _ {x \in \mathbb{M}} \sum _ {y \in \mathbb{N}} f(x + s, y + t) g(x, y) \tag{12}
$$

で定義され、$$s= \Delta x, t = \Delta y$$とおけば$$(11)$$式に一致する。さて、相互相関関数には畳み込み積分とほぼ同様の性質が成り立ち、

$$
\mathcal{F} (f \star g)(u,v) = (\mathcal{F} f)(u,v) (\bar{\mathcal{F}} g)(u,v) = F(u,v)\overline{G(u,v)} \tag{13}
$$

である。両辺を逆フーリエ変換すれば

$$
(f \star g)(s, t) = \left( \mathcal{F} ^ {-1} (F (u,v) \overline{G(u,v)}) \right)(s,t) \tag{14}
$$

であり、再び$$s= \Delta x, t = \Delta y$$とおいて、位相限定画像での議論に立ち戻れば、

$$
(p \star q)(\Delta x, \Delta y) = \left( \mathcal{F} ^ {-1} (P (u,v) \overline{Q(u,v)}) \right)(\Delta x, \Delta y) \tag{15}
$$

となって、テンプレート画像を$$(\Delta x, \Delta y)$$だけずらしたときの相互相関関数が求まることになる。あとは相互相関が最大になる$$(\Delta x, \Delta y)$$を見つければよい。

### 窓かけ

テンプレートマッチングでは画像の輪郭を合わせることが重要になるから、位相限定画像のうちでも重要なのは高周波成分である。したがってハイパスフィルタをかけてから相互相関をとることで精度の向上を狙うことがある。

## 回転不変位相限定相関法

回転不変位相限定相関法（RIPOC）は、位相限定相関法（POC）を用いて回転ズレとスケールの違いを検出する手法である。位相限定相関法は縦ズレと横ズレを検出できる手法なので、事前に Log-Polar 変換によって回転ズレを縦ズレに、スケールの違いを横ズレに変換してから POC を適用すれば回転ズレとスケールの違いを検出できることになる。

### Log-Polar 変換

Log-Polar 変換は以下の式で定義される座標変換である。

$$
\begin{cases}
\rho = \log \sqrt{x ^ 2+ y ^ 2} \\
\theta = \arctan(y / x)
\end{cases}
$$

Log-Polar 変換の逆変換は以下の式で定義できる。

$$
\begin{cases}
x = e ^ \rho \cos \theta \\
y = e ^ \rho \sin \theta
\end{cases}
$$

解説に合わせて、画像としてプロットするときは$$\rho$$を横軸、$$\theta$$を縦軸としておこう。

元の画像の縦横がともに$$a$$倍に引き伸ばされたとき、すなわち$$x' = \frac{1}{a} x, y' = \frac{1}{a} y$$という変換を行ったとき、

$$
\begin{aligned}
\rho ' &= \log \sqrt{(x') ^ 2 + (y ') ^ 2} \\
&= \log \sqrt{ (1/a) ^ 2 (x ^ 2+ y ^ 2)} \\
&=\log \sqrt{x ^ 2+ y ^ 2} -  \log a ^ 2 \\
&= \rho - \log a ^ 2
\end{aligned}
$$

である。つまりもとの画像を$$a$$倍に拡大すると、Log-Polar 変換後の画像は左側に$$\log a ^ 2$$だけシフトする。

元の画像を反時計回りに$$\theta _ 0$$だけ回転させる座標変換は

$$
\begin{cases}
x' = x \cos \theta _ 0 - y \sin \theta _ 0 \\
y' = x \sin \theta _ 0 + y \cos \theta _ 0
\end{cases}
$$

と表せる。このとき

$$
\rho ' = \log \sqrt{(x') ^ 2 + (y') ^ 2} = \log \sqrt{x^ 2 + y ^ 2} = \rho
$$

で変化はないが、

$$
\begin{aligned}
\theta ' &= \arctan(y' / x') \\
&= \arctan \left( \frac{x \sin \theta _ 0 + y \cos \theta _ 0}{x \cos \theta _ 0 - y \sin \theta _ 0}  \right) \\
&= \arctan \left( \frac{\tan \theta _ 0 + \frac{y}{x}}{1 - \frac{y}{x} \tan \theta _ 0}  \right) \\
&= \arctan(y/x) + \arctan(\tan \theta _ 0) \\
&= \theta + \theta _ 0
\end{aligned}
$$

となる。したがって Log-Polar 変換後の画像は上に$$\theta _ 0$$だけシフトする。

あとは POC によって得られた

$$
\begin{cases}
\Delta x = - \log a ^ 2 \\
\Delta y = \theta _ 0
\end{cases}
$$

の関係から

$$
\begin{cases}
a = \exp ( - \frac{1}{2} \Delta x) \\
\theta _ 0 = \Delta y
\end{cases}
$$

が求まる。

## 参考文献

* [https://ja.wikipedia.org/wiki/%E9%9B%A2%E6%95%A3%E3%83%95%E3%83%BC%E3%83%AA%E3%82%A8%E5%A4%89%E6%8F%9B](https://ja.wikipedia.org/wiki/%E9%9B%A2%E6%95%A3%E3%83%95%E3%83%BC%E3%83%AA%E3%82%A8%E5%A4%89%E6%8F%9B)
* [https://ja.wikipedia.org/wiki/%E7%95%B3%E3%81%BF%E8%BE%BC%E3%81%BF](https://ja.wikipedia.org/wiki/%E7%95%B3%E3%81%BF%E8%BE%BC%E3%81%BF)
* [http://www.mk.ecei.tohoku.ac.jp/papers/data/F00290013.pdf](http://www.mk.ecei.tohoku.ac.jp/papers/data/F00290013.pdf)
* [http://slpr.sakura.ne.jp/qp/fourier-transform-convolution/](http://slpr.sakura.ne.jp/qp/fourier-transform-convolution/)



