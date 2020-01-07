# 4.3. ニュートン法

## アルゴリズム

1. 初期値$$x ^ 0 \in \mathbb{R} ^ n$$を定める（定め方は任意である）

2. 収束するまで次の更新式を用いて更新を繰り返す

$$
\begin{aligned}
x ^ {k+1} &= x ^ k + \Delta x ^ k \\
&= x ^ k - H _ {x ^ k} ^ {-1} \operatorname{grad} f ( x ^ k )
\end{aligned}
$$

## 原理

最急降下法のときと同様に

$$
\operatorname{grad} f (x) = 0 \tag{4.3.1}
$$

を満たすような点$$x$$を見つける。ただしニュートン法では以下の関数の2次近似を用いる。

$$
f _ {\rm II} (x)  
= f(\overline{x}) + \left< \operatorname{grad} f(\overline{x}), \Delta x \right> + \left< \operatorname{Hess} f(\overline{x}) \Delta x, \Delta x \right> \tag{4.3.2}
$$

2次近似した関数の極値を与える点$$x$$を見つけるには

$$
\nabla f _ {\rm II} (x) = 0
$$

となる場所を見つければよい。\(4.3.2\) 式の右辺では$$\overline{x}$$は定数であり$$\Delta x$$が$$x$$の関数であることに注意する。具体的には \(1.2.2\) 式の書き換えを用いているので $$\Delta x = x - x ^ k$$である。このことを考慮しつつ \(4.3.2\) 式の両辺を$$x$$で微分すると

$$
\nabla f _ {\rm II} (x) = \operatorname{grad} f (\overline{x}) + \operatorname{Hess} f (\overline{x}) \Delta x
$$

となるから、$$\nabla f _ {\rm II}(x) = 0$$となるとき

$$
- H _ {x ^ k} \Delta x = \operatorname{grad} f (\overline{x}) \tag{4.3.3}
$$

である。ただし Hessian operator は Hesse 行列による表記に直した。Hesse 行列が正則ならば連立方程式 \(4.3.3\) を満たす解は、両辺に左から$$- H _{x ^ k} ^ {-1}$$をかけることで

$$
\Delta x = - H _ {x ^ k} ^ {-1} \operatorname{grad} f (\overline{x}) \tag{4.3.4}
$$

と唯一通りに定まる。なお、\(4.3.4\) 式による更新が最適解へ向かうためには Hesse 行列が常に正則であることに加えて正定値でなければならない。

## 収束性

ニュートン法は2次収束のアルゴリズムであり、極値の近傍では比較的少ない回数のイテレーションで極値へ収束する。一方で実験的には極値から離れた点では最急降下法などの手法に比べて収束性が悪いことが知られており、最適解の近くまでは最急降下法や共役勾配法によって近づき、最適解の近くでニュートン法に切り替えるといった手法がよく用いられる。

