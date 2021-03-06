---
description: 2020/1/6公開
---

# 4.1. 最急降下法

## アルゴリズム

1. 初期値$$x _ {(0)} \in \mathbb{R} ^ n$$を定める（定め方は任意である）

2. 探索方向$$m _ {(k)}$$を点$$x _ {(k)}$$における勾配によって$$m _ {(k)} = - \operatorname{grad} f (x _ {(k)})$$と定める

3. ステップサイズ$$t _ {(k)} > 0$$を定める（定め方は任意である）

4. 次の更新式を用いて現在の点を更新する

$$
\begin{aligned}
x _ {(k+1)} &= x _ {(k)} + t _ {(k)} m _ {(k)} \\
&= x _ {(k)} - t _ {(k)} \operatorname{grad} f ( x _ {(k)} )
\end{aligned}
$$

5. 収束していなければ手順 2 へ戻る

収束したかどうかの判定には小さい正の定数$$\varepsilon$$などを用いて

$$
\| \operatorname{grad} f(x) \| < \varepsilon
$$

とする。大抵は$$10 ^ {-16} < \varepsilon < 10 ^ {-8}$$くらいの範囲に設定する。

## 原理

**最急降下法**（steepest descent）はもっとも単純で基本的な直線探索法だが、目的関数の勾配（gradient）さえ計算できれば適用できるので汎用性が高い。

目的関数$$f \colon \mathbb{R} ^ n \to \mathbb{R}$$が定義域の全体で微分可能ならばその極値を与える点$$x$$では

$$
\operatorname{grad} f (x) = 0 \tag{4.1.1}
$$

が成り立つ。最小値は極値であるから、最適化問題

$$
\underset{x \in \mathbb{R} ^ n}{\operatorname{arg} \operatorname{min}} \,\, f(x)
$$

を解くには目的関数を単調減少させながら \(4.1.1\) 式を満たすまで更新を繰り返せば少なくとも最適解の候補には到達する（一般に$$f(x)$$が性質のよい関数でない限り真の最適解に到達するのはどんなアルゴリズムでも非常に難しいため極値で妥協する）。

現在の点$$x _ {(k)} \in \mathbb{R} ^ n$$は既知であるとして、更新方向$$m _ {(k)} \in \mathbb{R} ^ n$$として妥当な方向を探す。ステップサイズはあとから定めるから$$m _ {(k)}$$は方向の情報だけが重要であり、$$\| m _ {(k)} \| = 1$$としてよい。目的関数$$f \colon \mathbb{R} ^ n \to \mathbb{R}$$の点$$x _ {(k)}$$の周りで Taylor の定理（1次近似）を適用する、すなわち \(2.6\) 式で$$\Delta x = t m _ {(k)} \,\,(t > 0)$$とおくと、

$$
\begin{aligned}
f(x _ {(k)} + t m _ {(k)}) &= f(x _ {(k)}) + \left< \operatorname{grad} f(x _ {(k)}), t m _ {(k)} \right> + o \left( \| t m _ {(k)} \| \right) \\
&= f(x _ {(k)}) + t \left< \operatorname{grad} f(x _ {(k)}),  m _ {(k)} \right> + o \left( t \| m _ {(k)} \| \right) \\
&= f(x _ {(k)}) + t \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> + o \left( t \right) 
\end{aligned} \tag{4.1.2}
$$

である。したがって、更新後の目的関数の値と更新前のそれとの差$$\Delta f$$は

$$
\begin{aligned}
\Delta f &= f(x _ {(k)} + t m _ {(k)}) - f(x _ {(k)}) \\
&= t \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> + o \left( t \right) \\
&= t \left( \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> + \frac{o \left( t \right)}{t} \right)
\end{aligned} \tag{4.1.3}
$$

である。ここで$$o(t)$$の素性は \(4.1.2\) 式から \(2.5\) 式まで辿れるから、

$$
o(t) = o (\| t m _ {(k)} \|) = h _ 1 (t m _ {(k)}) \| t m _ {(k)} \| = t \cdot h _ 1 (t m _ {(k)})
$$

であるとわかる。したがって Taylor の定理から

$$
\begin{aligned}
\lim _ {t \to 0} \frac{o(t)}{t} &= \lim _ {t \to 0} \frac{o(t)}{t} \\
&= \lim _ {t \to 0} \frac{t \cdot h _ 1(t m _ {(k)})}{t} \\
&= \lim _ {t \to 0} h _ 1 (t m _ {(k)}) \\
&= 0
\end{aligned}
$$

が求まる。点$$x _ {(k)}$$が極値や停留点でなければ$$\operatorname{grad} f(x _ {(k)}) \neq 0$$であるから、$$m _ {(k)}$$を$$\operatorname{grad} f(x _ {(k)})$$と直交しないように取れば$$\left| \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> \right| > 0$$であるから、$$t$$を 0 に近づける途中で、ある$$t$$が存在して

$$
\left| \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> \right| > \left| \frac{o \left( t \right)}{t} \right| \tag{4.1.4}
$$

となる。ゆえに$$t$$が十分小さいとき \(4.1.3\) の符号は

$$
\operatorname{sign}(\Delta f) = \operatorname{sign} \left( \left< \operatorname{grad} f(x _ {(k)}), tm _ {(k)} \right> \right)
$$

によって定まることがわかるので、$$t > 0$$であることを思い出せば

$$
\left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> < 0
$$

となるように$$m _ {(k)}$$を選べば目的関数が単調減少するように$$t$$を選ぶことが可能になる。

以上の議論はこれから紹介するうちでニュートン法を除くすべての直線探索法に共通した議論であり、直線探索法のバリエーションはこの$$m _ {(k)}$$の選び方を変えたものに過ぎない。

探索方向$$m _ {(k)}$$は$$\operatorname{grad} f(x _ {(k)})$$を用いた式で定義されることが多いので、これらの手法を総称して**勾配法**（gradient descent）ともいう。

### 最急降下法

最急降下法は$$m _ {(k)} = - \operatorname{grad} f(x _ {(k)})$$とする手法で、

$$
\begin{aligned}
\left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> &= \left< \operatorname{grad} f(x _ {(k)}), -  \operatorname{grad} f(x _ {(k)})\right> \\
&= - \left< \operatorname{grad} f(x _ {(k)}),  \operatorname{grad} f(x _ {(k)})\right> \\
&= - \| \operatorname{grad} f(x _ {(k)}) \| ^ 2 < 0
\end{aligned}
$$

より、点$$x _ {(k)}$$の近傍で十分小さい$$t$$を選べば目的関数は単調減少する。

「最急降下（steepest descent）」の名は$$\left| \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> \right|$$がもっとも大きくなる探索方向$$m _ {(k)}$$を用いていることに由来する。実際に、Cauchy-Schwarz の不等式と$$\| m _ {(k)} \| = 1$$より

$$
\left| \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> \right| \leq \| \operatorname{grad} f(x _ {(k)}) \| \cdot \| m _ {(k)} \| = \| \operatorname{grad} f(x _ {(k)}) \|
$$

となる。不等式の等号成立は

$$
m _ {(k)} = \pm \frac{\operatorname{grad} f(x _ {(k)})}{ \| \operatorname{grad} f(x _ {(k)}) \| }
$$

のときであり、ただそのときに限る。したがって$$t \to 0$$の極限、すなわち点$$x _ {(k)}$$の周りのごく狭い範囲では$$m _ {(k)} = - \operatorname{grad} f(x _ {(k)})$$が目的関数をもっとも減少させる方向である。

### ニュートン法

ニュートン法は関数の2次近似から導出されるので、誤解を防ぐためここでは説明しない。

{% page-ref page="newtons-method.md" %}

### 共役勾配法

共役とは簡単に言えば「直交している」という意味である。つまり勾配に直交するベクトル$$r _ {(k)}$$を$$m _ {(k)}$$に加えて$$m _ {(k)} + r _ {(k)}$$を探索方向とするのが共役勾配法である。

\(4.1.4\) 式の時点で$$m _ {(k)}$$は$$\operatorname{grad}f(x _ {(k)})$$と直交しないものを選んだが、そうして選んだ$$m _ {(k)}$$に$$\operatorname{grad} f (x _ {(k)})$$と直交するベクトル$$r _ {(k)}$$を加えても

$$
\begin{aligned}
\left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} + r _ {(k)} \right> &= \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> + \left< \operatorname{grad} f(x _ {(k)}), r _ {(k)} \right> \\
&= \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> + 0 \\
&= \left< \operatorname{grad} f(x _ {(k)}), m _ {(k)}\right>
\end{aligned}
$$

となるので目的関数が単調減少するような$$t$$が選べるという議論は変わらない。

{% page-ref page="conjugate-gradient-method/" %}

### 準ニュートン法

準ニュートン法は$$B _ {(k)}$$を正定値行列として$$m _ {(k)}$$に

$$
m _ {(k)} = - B _ {(k)} \operatorname{grad} f(x _ {(k)})
$$

を選ぶ方法である。このときやはり

$$
\begin{aligned}
\left< \operatorname{grad} f(x _ {(k)}), m _ {(k)} \right> &= \left< \operatorname{grad} f(x _ {(k)}), -  B _ {(k)}\operatorname{grad} f(x _ {(k)})\right> \\
&= - \left< \operatorname{grad} f(x _ {(k)}),  B _ {(k)} \operatorname{grad} f(x _ {(k)})\right>  < 0
\end{aligned}
$$

が成り立つので$$m _ {(k)}$$は依然として降下方向である。

{% page-ref page="quasi-newton-method/" %}

## 収束性

最急降下法は1次収束のアルゴリズムである。

## 特徴

最急降下法は1次収束のアルゴリズムで、本書で紹介する中ではもっとも収束性が悪い部類に入るが、実装がもっとも簡単であり、イテレーションごとの計算量も勾配を計算するだけなので比較的小さい。

勾配法でうまくいくかどうかを検証するためにまずとりあえず最急降下法を実装してみるのは手段としてはありである。収束性は悪いが回しておけば徐々に最適解には近づいていくので、一晩回しておいて最適解の候補を得ておけば他の手法を試すときにも安心感がある。

## 参考文献

1. [http://www.dais.is.tohoku.ac.jp/~shioura/teaching/mp08/mp08-10.pdf](http://www.dais.is.tohoku.ac.jp/~shioura/teaching/mp08/mp08-10.pdf)
2. [http://www2.kaiyodai.ac.jp/~yoshi-s/Lectures/Optimization/2011/lecture\_1.pdf](http://www2.kaiyodai.ac.jp/~yoshi-s/Lectures/Optimization/2011/lecture_1.pdf)

