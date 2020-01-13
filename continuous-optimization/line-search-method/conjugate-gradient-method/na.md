---
description: 2020/1/8公開
---

# 4.4.1. 原始的な共役勾配法

## アルゴリズム

1. 初期値$$x _ {(0)} \in \mathbb{R} ^ n$$を定める（定め方は任意である）

2. 探索方向$$m _ {(k)}$$を

$$
m _ {(k)}= \operatorname{grad} f (x _ {(k)}) + \beta _ {(k)} r _ {(k)}
$$

　により定める。ただし

$$
\beta _ {(k)} = \begin{cases}
\quad \quad \quad \,\, 0& \quad {\rm if} \,\, k =0 \\
- \frac{\left< r _ {(k)}, H _ {x _ {(k)}} \operatorname{grad}f(x _ {(k)}) \right> }{\left< r _ {(k)}, H _ {x _ {(k)}} r _ {(k)} \right>} &\quad otherwise
\end{cases}
$$

$$
r _ {(k)} = m _ {(k-1)}
$$

　である（$$r _ {(0)}$$は未定義だが係数の$$\beta _ {(0)}$$が 0 なので$$m _ {(0)} = \operatorname{grad} f (x _ {(0)})$$となる）。

3. ステップサイズ$$\alpha _ {(k)} > 0$$を定める。$$\alpha _ {(k)}$$は通常の直線探索で決定してもよいが、

$$
\alpha _ {(k)} = - \frac{\left< m _ {(k)},  \operatorname{grad} f (x _ {(k)}) \right>}{\left< m _ {(k)}, H _ {x _ {(k)}} m _ {(k)} \right>}
$$

　を用いてもよい。

4. 次の更新式を用いて現在の点を更新する

$$
\begin{aligned}
x _ {(k+1)} &= x _ {(k)} + \alpha _ {(k)} m _ {(k)} \\
&= x _ {(k)} + \alpha _ {(k)} \left( \operatorname{grad} f ( x _ {(k)} ) + \beta _ {(k)} r _ {(k)} \right)
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
\operatorname{grad} f (x _ {(k)}) + H _ {x _ {(k)}} \Delta x = 0 \tag{4.4.3}
$$

となる。ここで$$\operatorname{grad} f (x _ {(k)}) \perp r _ {(k)}$$を満たす$$r _ {(k)}$$を選んだとして、\(4.4.3\) 式の両辺で$$r _ {(k)}$$との内積をとると、左辺は

$$
\begin{aligned}
\left< r _ {(k)}, \operatorname{grad} f (x _ {(k)}) + H _ {x _ {(k)}} \Delta x \right> &= \left< r _ {(k)}, \operatorname{grad} f (x _ {(k)}) \right> + \left< r _ {(k)}, H _ {x _ {(k)}} \Delta x \right> \\
&= 0 + \left< r _ {(k)}, H _ {x _ {(k)}} \Delta x \right> \\
&= \left< r _ {(k)}, H _ {x _ {(k)}} \Delta x \right>
\end{aligned}
$$

であるから、

$$
\left< r _ {(k)}, H _ {x _ {(k)}} \Delta x \right> = 0 \tag{4.4.4}
$$

となることがわかる。そこで

$$
m _ {(k)} = \operatorname{grad} f(x _ {(k)}) + \beta _ {(k)} r _ {(k)} \tag{4.4.5}
$$

の方向に更新することを考える。

まず$$\beta _ {(k)}$$を導出する。ステップサイズを$$\alpha _ {(k)}$$とすると

$$
\Delta x = \alpha _ {(k)} m _ {(k)} \tag{4.4.6}
$$

とおける。これを \(4.4.4\) 式に代入すると

$$
\begin{aligned}
&\left< r _ {(k)}, H _ {x _ {(k)}} (\alpha _ {(k)} m _ {(k)}) \right> = \alpha _ {(k)} \left< r _ {(k)}, H _ {x _ {(k)}} m _ {(k)} \right> = 0 \\
&\therefore \left< r _ {(k)}, H _ {x _ {(k)}} m _ {(k)} \right> = 0
\end{aligned}
$$

となるので

$$
\begin{aligned}
\left< r _ {(k)}, H _ {x _ {(k)}} m _ {(k)} \right> &= \left< r _ {(k)}, H _ {x _ {(k)}}  \left(\operatorname{grad} f (x _ {(k)}) + \beta _ {(k)} r _ {(k)} \right) \right> \\
&= \left< r _ {(k)}, H _ {x _ {(k)}} \operatorname{grad} f (x _ {(k)}) \right> + \beta _ {(k)} \left< r _ {(k)}, H _ {x _ {(k)}} r _ {(k)} \right> = 0
\end{aligned}
$$

より

$$
\beta _ {(k)} = - \frac{\left< r _ {(k)}, H _ {x _ {(k)}} \operatorname{grad} f (x _ {(k)}) \right>}{\left< r _ {(k)}, H _ {x _ {(k)}} r _ {(k)} \right>} \tag{4.4.7}
$$

と求まる。

次に共役勾配方向$$r _ {(k)}$$を求める。$$r _ {(k)}$$は$$\operatorname{grad} f (x _ {(k)})$$と直交してさえいればよいので選び方には自由度があるが、ここでは古典的な

$$
r _ {(k)} = m _ {(k-1)} \tag{4.4.8}
$$

を用いる。

厳密直線探索を用いると$$\operatorname{grad} f (x _ {(k)}) \perp r _ {(k)}$$となることを示しておく。いま点$$x _ {(k)}$$を始点として$$m _ {(k)}$$方向への直線探索を考えると、媒介変数$$t$$による関数

$$
F(t) = f (x _ {(k)} + t m _ {(k)}) \tag{4.4.10}
$$

の極値を与える$$t$$を求めることになる。この関数の点$$x _ {(k+1)} = x _ {(k)} + t m _ {(k)}$$における方向微分を考えると

$$
\frac{d F(t)}{dt} = \left< \nabla f (x _ {(k+1)}), \frac{d m _ {(k)}}{dt}\right> \tag{4.4.9}
$$

である（方向微分を \(4.4.10\) 式の右辺の形に分解するには微分の連鎖律を用いる）。$$F(t)$$が極値をとるときの$$t$$を$$t ^ \ast$$とおくと

$$
\left. \frac{d F(t)}{dt} \right| _ {t = t ^ \ast} = 0 \tag{4.4.11}
$$

であるから、$$x _ {(k+1)} = x _ {(k)} + t ^ \ast m _ {(k)}$$を選べば、\(4.4.10\), \(4.4.11\) 式より

$$
\left< \nabla f (x _ {(k+1)}), \frac{d m _ {(k)}}{dt}\right> = 0 \tag{4.4.12}
$$

となる。また、直線探索なので$$\frac{d m _ {(k)}}{dt} \parallel m _ {(k)}$$だから、\(4.4.12\) 式と定数$$c \neq 0$$を用いて

$$
\left< \nabla f (x _ {(k+1)}), \frac{d m _ {(k)}}{dt}\right> = \left< \nabla f (x _ {(k+1)}), c m _ {(k)} \right> = c \left< \nabla f (x _ {(k+1)}), m _ {(k)} \right> = 0\tag{4.4.13}
$$

となることがわかる。ゆえに

$$
\begin{aligned}
\left< \nabla f (x _ {(k+1)}), m _ {(k)} \right> = 0  \\
\Rightarrow \nabla f (x _ {(k+1)}) \perp m _ {(k)}
\end{aligned} \tag{4.4.14}
$$

となる。したがって$$r _ {(k+1)} = m _ {(k)}$$とおけば$$\nabla f (x _ {(k+1)}) \perp r _ {(k+1)}$$となることがわかるので共役勾配方向$$r _ {(k)}$$が得られたことになる。

残る未知数はステップサイズ$$\alpha _ {(k)}$$であるが、\(4.4.8\) 式、すなわち$$r _ {(k)} = m _ {(k-1)}$$の正当性を保証しているのは厳密直線探索を行っていることであるから、\(4.4.10\), \(4.4.11\) 式のあたりの議論から$$\alpha _ {(k)} = t ^ \ast$$とすればよいことがわかる。

$$t ^ \ast$$を厳密に求めるのは難しいので、これをどう求めるかもアルゴリズムの構成の自由度となる。もっとも簡単な方法は目的関数を2次近似した極値へ到達する$$\alpha _ {(k)}$$を求める方法で、 \(4.4.3\) 式に \(4.4.6\) 式を代入して

$$
\begin{aligned}
&\operatorname{grad} f (x _ {(k)}) + H _ {x _ {(k)}} (\alpha _ {(k)} m _ {(k)}) = 0 \\
&\therefore \,\, \alpha _ {(k)} \cdot H _ {x _ {(k)}} m _ {(k)} = - \operatorname{grad} f (x _ {(k)})
\end{aligned}
$$

となることから、両辺で$$m _ {(k)}$$との内積をとって

$$
\begin{aligned}
&\alpha _ {(k)} \left< m _ {(k)}, H _ {x _ {(k)}} m _ {(k)} \right> = - \left< m _ {(k)},  \operatorname{grad} f (x _ {(k)}) \right> \\
&\therefore \alpha _ {(k)} = - \frac{\left< m _ {(k)},  \operatorname{grad} f (x _ {(k)}) \right>}{\left< m _ {(k)}, H _ {x _ {(k)}} m _ {(k)} \right>}
\end{aligned} \tag{4.4.15}
$$

が求まる。

## 収束性

共役勾配法は1次収束のアルゴリズムである。

## 特徴

共役勾配法の収束性は最急降下法と同じ1次収束であるが、経験的に最急降下法よりも早く収束することが知られている。

原始的な共役勾配法でも Hesse 行列の逆行列の計算は回避できるが、Hesse 行列自体はまだ$$\beta ^ k$$を求める際の更新式に現れている。現代では Hesse 行列自体の計算も回避するようなバリエーションが提案されており、それが次に解説するような PRP 法や HS 法である。

