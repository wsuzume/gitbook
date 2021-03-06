# 球面幾何（楕円幾何）

## 球面幾何（楕円幾何）

球面幾何（spherical geometry）は楕円幾何（elliptic geometry）の特殊な場合であり、楕円幾何は曲率が正の非ユークリッド幾何である。たとえば地球の地表は2次元の球面で近似することができ、ある方向に「まっすぐ」進むといつかは元の場所に戻ってくる「閉じた」空間である。

これは数学的にはより高次元の空間にも拡張できる。相対論が適用できるような規模では我々の宇宙空間も「閉じて」いるかもしれず、宇宙の果てに向かって「まっすぐ」進んで行ったらいつかはもと地球があった場所に戻ってくるかもしれない。

宇宙の果てはどうなっているか知りようがないのだが、もっと身近で簡単に次元が膨れ上がるのが「データ」である。100種類のカラムを持つデータは100次元のユークリッド空間上の点として表現されていることになるが、適切な写像を定義することで非ユークリッド空間上に「写す」ことができる。もっとも簡単には、単に各ベクトルをそのノルムで割ってノルムを 1 にする正規化の操作を行うと、データは99次元の球面上に写されたことになる。

球面幾何はコンピュータと非常に相性がよい幾何のひとつだと私は考えている。コンピュータは有限の範囲、有限の精度でしか数値を表現できないので、ノルムが定数で各座標も大きな値を取れない球面幾何はオーバーフローの心配がないのである。

適切な座標変換を与えれば楕円幾何は常に球面幾何に翻訳できるので、ここでは取り扱いが簡単な球面幾何についてのみ考察する。

## 球面

$$n$$次元球面$$S^n$$は$$n+1$$次元のユークリッド空間$$\mathbb{R} ^ {n+1}$$で原点からの距離が 1 の点をすべて集めた部分空間として定義される。つまり

$$
S ^ n = \{ x \mid \|x\| = 1,\, x \in \mathbb{R} ^ {n + 1} \}
$$

である。$$n=1$$のときは「円」、$$n=2$$のときは「球面」として我々が認識しているもので、通常は$$n \geq3$$の$$n$$次元球面を想像することはできず、それらは十把一絡げに「超球面」と呼ばれる。

厳密には、球面$$S^n$$はユークリッド空間$$\mathbb{R} ^ {n+1}$$に埋め込まれたときのみ球面となる。たとえば$$S^1$$は我々が認識する「円」であり、これを我々が生活している3次元ユークリッド空間$$\mathbb{R} ^ {3}$$に埋め込んでもそれはやはり円に過ぎず球面とはみなされない。逆に$$S ^ 2$$は我々が認識する「球面」であり、これを2次元のユークリッド空間$$\mathbb{R} ^ 2$$である平面に「描き込む」ことはできない。2次元ユークリッド空間$$\mathbb{R} ^ 2$$における球面は円$$S ^ 1$$である。

## 球面上の座標

球面上の任意の点$$x$$は、零ベクトルではないあるユークリッド空間上のベクトル$$v$$を用いて

$$
x = \frac{v}{\| v \|}
$$

と表せる。ただし$$\| \cdot \|$$はベクトルのノルム（ユークリッドノルム）である。通常は$$\| v \| = 1$$のもので代表するが、ノルムは任意でもよい。この表現を用いる場合、$$n$$次元球面上の点を表現するのに$$n+1$$次元のベクトルを用いることになる。

極座標を用いるとノルムの情報を保存する必要がないので$$n$$ 個の角度を保存することで必要十分な情報を扱えるが、高次元の場合になると数値計算上の利点はほぼない上に、$$n \gg 1$$の状況では大してメモリ効率がよくなるわけでもない。したがって本書では極座標は取り扱わない。

## 球面のユークリッド空間への射影

様々な方式の世界地図が存在すること（メルカトル図法や正距方位図法）から想像できることだが、球面を、同じ次元のユークリッド空間へ翻訳しようとすると何かしらの歪みが生じる。

本書では球面上の点を同じ次元のユークリッド空間への射影ではなく、次元が 1 だけ大きいユークリッド空間への埋め込みによって表現するため、歪みを考慮する必要はないが、一応情報を整理する目的で概要だけ触れておく。もしかしたら結果を可視化する目的で球面を射影したい人がいるかもしれない。

参考：[https://www.researchgate.net/publication/330888153\_Elliptic\_geometry](https://www.researchgate.net/publication/330888153_Elliptic_geometry)

### 円筒射影（cylindrical projection）

メルカトル図法や正距円筒図法などが該当する。

### 方位角射影（azimuthal projection）

正距方位図法が該当する。

## 球面上の2点間の距離

「飛行機は世界地図の上をまっすぐには飛ばない」という事実を中学校や高校で習って覚えている人もいることだろう。球面上の2点間の距離（球面上を移動したときの最短ルート）は大円（その2点と原点を通る平面で球面を切断して断面にできる円）に沿った短い方の弧の長さである。2点$$x,y$$がそれぞれユークリッド空間上の位置ベクトル$$u,v$$によって表現されているなら、ベクトル$$u,v$$の偏角であると言い換えてもよい。つまり弧の長さは rad で測られる。rad は無次元量であることに注意する。

数式で書いておこう。球面上の2点$$x,y \in S ^ n$$がユークリッド空間上の位置ベクトル$$u, v \in \mathbb{R} ^ {n+1}$$で表現されるとき、すなわち

$$
x = \frac{u}{\| u \|}, \, y = \frac{v}{\| v \|}
$$

であるとき、球面上の2点$$x,y$$間の球面上での距離$$d(x,y)$$は

$$
d(x,y) = \arccos \left( \frac{  u \cdot v }{ \| u \| \| v \|} \right), \quad \quad 0 \leq d (x,y) \leq \pi
$$

である。ただし$$u \cdot v$$は$$u$$と$$v$$のユークリッド空間上における内積であり、同様に$$\| \cdot \|$$もベクトルのユークリッドノルムを表している。

## 球面上の3点が作る三角形の面積

球面上でモンテカルロ法を使いたい場合などに必要になるかもしれない。

## 球面上の確率分布

当然のことながら、球面上ではユークリッド空間上で定義される確率分布、たとえば多変量ガウス分布などを用いることはできない（多変量ガウス分布からサンプルされた点が球面上に位置する確率は 0 である）。

一般にユークリッド空間に埋め込まれた低次元多様体上の分布を定義することは困難だが、球面の場合は例外的に扱いやすく、デルタ分布と一様分布だけでなく、指数型分布族も定義されている。

### デルタ分布

どんな多様体上でもまず定義できるであろう分布の代表格。ある一点にのみ集中した分布。

### 一様分布

性質のよい多様体上なら大体定義できるであろう分布の代表格。

### Langevin分布（von Mises-Fisher分布）

球面上で定義される指数型分布族のひとつである。Langevin分布（ランジュバン分布と読む）は球面上のガウス分布みたいなもので、中心と分散のパラメータを持つ。



Langevin分布は von Mises-Fisher分布（フォンミーゼス・フィッシャー分布）とも呼ばれる。特に$$n=2$$のとき von Mises分布（フォンミーゼス分布）と呼ばれる。



## 球面の接ベクトル空間

球面上で定義された関数の勾配を考えるには接ベクトル空間の概念が必要になってくる。ユークリッド空間では気にする必要がなかったが、勾配には「勾配に沿って少しだけ動いても空間からはみ出さない」という性質がある（微分幾何、リーマン多様体などの範囲）。

具体的には円の接線を考えてもらえればよい。円のある接点からそこでの接線に沿ってほんの少しだけ動いても、円からははみ出さないように見える。接線以外の方向へ移動すれば、どれだけ慎重にほんのちょっと動いたとしても円からはみ出してしまうだろう。

この接線の概念を$$n$$次元球面に一般化したのが**接ベクトル空間**（tangent vector space）である。接ベクトル空間は単に接空間（tangent space）ともいう。

球面の接ベクトル空間はとても簡単で、

$$
T _ x S ^ n = \{ \xi \mid x ^ \mathrm{T} \xi = 0 , \xi \in \mathbb{R} ^ {n+1} \}
$$

である。要するに、点$$x$$に直交するベクトル$$\xi$$であればなんでもよい。

## レトラクション



