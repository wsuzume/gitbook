# 4.4.1. 原始的な共役勾配法

## アルゴリズム

1. 初期値$$x ^ 0 \in \mathbb{R} ^ n$$を定める（定め方は任意である）

2. 探索方向$$m ^ k$$を

$$
m ^ k = \operatorname{grad} f (x ^ k) + \beta ^ k r ^ k
$$

　により定める。ただし

$$
\beta ^ k = \begin{cases}
\quad \quad \quad \,\, 0& \quad {\rm if} \,\, k =0 \\
- \frac{\left< r ^ k, H _ {x ^ k} \operatorname{grad}f(x ^ k) \right> }{\left< r ^ k, H _ {x ^ k} r ^ k \right>} &\quad otherwise
\end{cases}
$$

$$
r ^ k = m ^ {k - 1}
$$

　である（$$r ^ 0$$は未定義だが係数の$$\beta ^ 0$$が 0 なので$$m ^ 0 = \operatorname{grad} f (x ^ 0)$$となる）。

3. ステップサイズ$$\alpha ^ k > 0$$を定める。$$\alpha ^ k$$は通常の直線探索で決定してもよいが、

$$
\alpha ^ k = - \frac{\left< m ^ k,  \operatorname{grad} f (x ^ k) \right>}{\left< m ^ k, H _ {x ^ k} m ^ k \right>}
$$

　を用いてもよい。

4. 次の更新式を用いて現在の点を更新する

$$
\begin{aligned}
x ^ {k+1} &= x ^ k + \alpha ^ k m ^ k \\
&= x ^ k + \alpha ^ k \left( \operatorname{grad} f ( x ^ k ) + \beta ^ k r ^ k \right)
\end{aligned}
$$

5. 収束していなければ手順 2 へ戻る

## 原理

ニュートン法と同様に、2次近似した関数

$$
f _ {\rm II} (x)  
= f(\overline{x}) + \left< \operatorname{grad} f(\overline{x}), \Delta x \right> + \left< \operatorname{Hess} f(\overline{x}) \Delta x, \Delta x \right> \tag{4.4.1}
$$

を$$x$$で微分して

$$
\nabla f _ {\rm II} (x) = \operatorname{grad} f (\overline{x}) + \operatorname{Hess} f (\overline{x}) \Delta x \tag{4.4.2}
$$

を得る。2次近似した関数の極値は$$\nabla f _ {\rm II}(x) = 0$$を満たすので

$$
\operatorname{grad} f (x ^ k) + H _ {x ^ k} \Delta x = 0 \tag{4.4.3}
$$

となる。ここで$$\operatorname{grad} f (x ^ k) \perp r ^ k$$を満たす$$r ^ k$$を選んだとして、\(4.4.3\) 式の両辺で$$r ^ k$$との内積をとると、左辺は

$$
\begin{aligned}
\left< r ^ k, \operatorname{grad} f (x ^ k) + H _ {x ^ k} \Delta x \right> &= \left< r ^ k, \operatorname{grad} f (x ^ k) \right> + \left< r ^ k, H _ {x ^ k} \Delta x \right> \\
&= 0 + \left< r ^ k, H _ {x ^ k} \Delta x \right> \\
&= \left< r ^ k, H _ {x ^ k} \Delta x \right>
\end{aligned}
$$

であるから、

$$
\left< r ^ k, H _ {x ^ k} \Delta x \right> = 0 \tag{4.4.4}
$$

となることがわかる。そこで

$$
m ^ k = \operatorname{grad} f(x ^ k) + \beta ^ k r ^ k \tag{4.4.5}
$$

の方向に更新することを考える。

まず$$\beta ^ k$$を導出する。ステップサイズを$$\alpha ^ k$$とすると

$$
\Delta x = \alpha ^ k m ^ k \tag{4.4.6}
$$

とおける。これを \(4.4.4\) 式に代入すると

$$
\begin{aligned}
&\left< r ^ k, H _ {x ^ k} (\alpha ^ k m ^k) \right> = \alpha ^ k \left< r ^ k, H _ {x ^ k} m ^ k \right> = 0 \\
&\therefore \left< r ^ k, H _ {x ^ k} m ^ k \right> = 0
\end{aligned}
$$

となるので

$$
\begin{aligned}
\left< r ^ k, H _ {x ^ k} m ^ k \right> &= \left< r ^ k, H _ {x ^ k}  \left(\operatorname{grad} f (x ^ k) + \beta ^ k r ^ k \right) \right> \\
&= \left< r ^ k, H _ {x ^ k} \operatorname{grad} f (x ^ k) \right> + \beta ^ k \left< r ^ k, H _ {x ^ k} r ^ k \right> = 0
\end{aligned}
$$

より

$$
\beta ^ k = - \frac{\left< r ^ k, H _ {x ^ k} \operatorname{grad} f (x ^ k) \right>}{\left< r ^ k, H _ {x ^ k} r ^ k \right>} \tag{4.4.7}
$$

と求まる。

次に共役勾配方向$$r ^ k$$を求める。$$r ^ k$$は$$\operatorname{grad} f (x ^ k)$$と直交してさえいればよいので選び方には自由度があるが、ここでは古典的な

$$
r ^ k = m ^ {k - 1} \tag{4.4.8}
$$

を用いる。

厳密直線探索を用いると$$\operatorname{grad} f (x ^ k) \perp r ^ k$$となることを示しておく。いま点$$x ^ k$$を始点として$$m ^ k$$方向への直線探索を考えると、媒介変数$$t$$による関数

$$
F(t) = f (x ^ k + t m ^ k) \tag{4.4.10}
$$

の極値を与える$$t$$を求めることになる。この関数の点$$x ^ {k + 1} = x ^ k + t m ^ k$$における方向微分を考えると

$$
\frac{d F(t)}{dt} = \left< \nabla f (x ^ {k+1}), \frac{d m ^ {k}}{dt}\right> \tag{4.4.9}
$$

である（方向微分を \(4.4.10\) 式の右辺の形に分解するには微分の連鎖律を用いる）。$$F(t)$$が極値をとるときの$$t$$を$$t ^ \ast$$とおくと

$$
\left. \frac{d F(t)}{dt} \right| _ {t = t ^ \ast} = 0 \tag{4.4.11}
$$

であるから、$$x ^ {k+1} = x ^ k + t ^ \ast m ^ k$$を選べば、\(4.4.10\), \(4.4.11\) 式より

$$
\left< \nabla f (x ^ {k+1}), \frac{d m ^ {k}}{dt}\right> = 0 \tag{4.4.12}
$$

となる。また、直線探索なので$$\frac{d m ^ k}{dt} \parallel m ^ k$$だから、\(4.4.12\) 式と定数$$c \neq 0$$を用いて

$$
\left< \nabla f (x ^ {k+1}), \frac{d m ^ {k+1}}{dt}\right> = \left< \nabla f (x ^ {k+1}), c m ^ k \right> = c \left< \nabla f (x ^ {k+1}), m ^ k \right> = 0\tag{4.4.13}
$$

となることがわかる。ゆえに

$$
\begin{aligned}
\left< \nabla f (x ^ {k+1}), m ^ k \right> = 0  \\
\Rightarrow \nabla f (x ^ {k+1}) \perp m ^ k
\end{aligned} \tag{4.4.14}
$$

となる。したがって$$r ^ {k + 1} = m ^ k$$とおけば$$\nabla f (x ^ {k+1}) \perp r ^ {k+1}$$となることがわかるので共役勾配方向$$r ^ k$$が得られたことになる。

残る未知数はステップサイズ$$\alpha ^ k$$であるが、\(4.4.8\) 式、すなわち$$r ^ k = m ^ {k-1}$$の正当性を保証しているのは厳密直線探索を行っていることであるから、\(4.4.10\), \(4.4.11\) 式のあたりの議論から$$\alpha ^ k = t ^ \ast$$とすればよいことがわかる。

$$t ^ \ast$$を厳密に求めるのは難しいので、これをどう求めるかもアルゴリズムの構成の自由度となる。もっとも簡単な方法は目的関数を2次近似した極値へ到達する$$\alpha ^ k$$を求める方法で、 \(4.4.3\) 式に \(4.4.6\) 式を代入して

$$
\begin{aligned}
&\operatorname{grad} f (x ^ k) + H _ {x ^ k} (\alpha ^ k m ^ k) = 0 \\
&\therefore  \alpha ^ k \cdot H _ {x ^ k} m ^ k = - \operatorname{grad} f (x ^ k)
\end{aligned}
$$

となることから、両辺で$$m ^ k$$との内積をとって

$$
\begin{aligned}
&\alpha ^ k \left< m ^ k, H _ {x ^ k} m ^ k \right> = - \left< m ^ k,  \operatorname{grad} f (x ^ k) \right> \\
&\therefore \alpha ^ k = - \frac{\left< m ^ k,  \operatorname{grad} f (x ^ k) \right>}{\left< m ^ k, H _ {x ^ k} m ^ k \right>}
\end{aligned} \tag{4.4.15}
$$

が求まる。

## 収束性

共役勾配法は1次収束のアルゴリズムである。

## 特徴

共役勾配法の収束性は最急降下法と同じ1次収束であるが、経験的に最急降下法よりも早く収束することが知られている。

原始的な共役勾配法でも Hesse 行列の逆行列の計算は回避できるが、Hesse 行列自体はまだ$$\beta ^ k$$を求める際の更新式に現れている。現代では Hesse 行列自体の計算も回避するようなバリエーションが提案されており、それが次に解説するような PRP 法や HS 法である。

