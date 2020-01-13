---
description: 2020/1/13公開
---

# 4.5. 準ニュートン法

## アルゴリズム

1. 初期値$$x _ {(0)} \in \mathbb{R} ^ {n}$$を定める（定め方は任意である）

2. 探索方向$$m _ {(k)}$$を

$$
m _ {(k)} = - B _ {(k)} ^ {-1} \operatorname{grad} f(x _ {(k)})
$$

　または

$$
m _ {(k)} = - H _ {(k)} \operatorname{grad} f(x _ {(k)})
$$

　によって定める（ただし$$B _ {(k)}, H _ {(k)}$$はセカント条件を満たす正定値行列である）

3. 直線探索によってステップサイズ$$\alpha_{(k)}$$を定める

4. 収束するまで以下の式を用いて更新を繰り返す

$$
\begin{aligned}
x _ {(k+1)} = - \alpha _ {(k)} B _ {(k)} ^ {-1} \operatorname{grad} f (x _ {(k)}) \\
B _ {(k+1)} = ({\rm some \, update \, formula})
\end{aligned}
$$

　または

$$
H _ {(k+1)} = ({\rm some \, update \, formula})
$$

　$$B _ {(k)}, H _ {(k)}$$の更新式は DFP 法や BFGS 法の項目を参照のこと。

{% page-ref page="dfp-method.md" %}

{% page-ref page="bfgs-method.md" %}

{% page-ref page="lbfgs-method.md" %}

{% page-ref page="4.5.4.-bryoden-family-of-methods.md" %}

## 準ニュートン法

準ニュートン法（quasi-Newton method）は Hesse 行列を勾配によって近似してニュートン法に近い形で最適化を行う手法である。

準ニュートン法においても実装の仕方によっては近似した Hesse 行列$$B _ {(k)}$$の逆行列を計算せねばならない場合はあるが、その場合でも

1. Hesse 行列が陽な形で計算できない場合
2. Hesse 行列を直接計算するには計算量が大きくなる場合

には有効である。また、BFGS 法などは Hesse 行列の逆行列$$H _ {(k)}$$を直接アップデートできるので逆行列の計算を回避できる。さらに L-BFGS 法では$$H _ {(k)}$$をより小さいサイズのベクトルで近似するので、

* 高速
* 省メモリ
* 高精度

を達成しており、現代で大規模最適化問題を解く際の主流の方法となっている。

## 原理

ニュートン法の原理の説明のときに現れた 、2次近似した関数の極値への移動を表す \(4.3.6\) 式を再び以下に示す。

$$
\Delta x = - H _ {x _ {(k)}} ^ {-1} \operatorname{grad} f (x _ {(k)}) \tag{4.5.1}
$$

準ニュートン法ではこの$$H _ {x _ {(k)}}$$またはその逆行列$$H _ {x _ {(k)}} ^ {-1}$$の計算を回避したい。そこで$$H _ {x _ {(k)}}$$を近似する正定値行列$$B _ {(k)}$$を導入して

$$
m _ {(k)} = - B _ {(k)} ^ {-1} \operatorname{grad} f (x _ {(k)}) \tag{4.5.2}
$$

とする。ニュートン法では更新方向$$m _ {(k)}$$とステップサイズ$$\alpha _ {(k)}$$を合わせた$$\Delta x = \alpha _ {(k)} m _ {(k)}$$が直接求まったが、準ニュートン法では Hesse 行列を近似したため、改めて$$\alpha _ {(k)}$$を直線探索によって求める必要が生じる（Hesse 行列の近似がうまく行っていることを期待して最初は$$\alpha _ {(k)} = 1$$で固定して試してみてもよいが、Hesse 行列は一般に正定値であるとは限らない）。

$$B _ {(k)}$$を正定値行列に限ったのは、更新方向$$m _ {(k)}$$が目的関数の降下方向であることを保証するためである（証明は最急降下法のページに記した）。

{% page-ref page="../gradient-descent.md" %}

$$B _ {(k)}$$の選び方には自由度がある。この$$B _ {(k)}$$の選び方によって、これから紹介する DFP 法や BFGS 法といったバリエーションが生じる。

また、L-BFGS 法では$$B _ {(k)}$$を計算せずその逆行列を直接更新することが可能なので、$$H _ {(k)} = B _ {(k)} ^ {-1}$$とおいて

$$
m _ {(k)} = - H _ {(k)} \operatorname{grad} f (x _ {(k)}) \tag{4.5.3}
$$

とする。$$H _ {(k)} \approx H _ {x _ {(k)}} ^ {-1}$$なので少々紛らわしいが、慣習的にそう置かれることが多いので容赦していただきたい（数学は常に文字不足に悩まされているのだ）。

### セカント条件

正定値行列$$B _ k$$の選び方には自由度があるといったが、準ニュートン法では正定値性に加えて以下の条件を課す。

$$
\begin{aligned}
B _ {(k+1)} s _ {(k)} &= y _ {(k)} \\
H _ {(k+1)} y _ {(k)} &= s _ {(k)}
\end{aligned} \quad {\rm where}
\begin{cases}
s _ {(k)} = x _ {(k+1)} - x _ {(k)} \\ y _ {(k)} = \operatorname{grad} f(x _ {(k+1)}) -  \operatorname{grad} f(x _ {(k)})
\end{cases} \tag{4.5.4}
$$

これを**セカント条件**（secant condition）という。上式の第1式と第2式は$$B _ {(k+1)}$$が正則ならば同値であり、通常はどちらか一方を満たせばよいものとする。

セカント条件は勾配に対する Taylor の定理から導出される。$$\operatorname{grad} f(x)$$について$$x _ {(k+1)}$$の周りで Taylor の定理を適用すると

$$
\operatorname{grad} f (x _ {(k+1)}+\Delta x) = \operatorname{grad}f(x _ {(k+1)}) + \left<\nabla \operatorname{grad}f(x _ {(k+1)}), \Delta x \right> + O(\| \Delta x \| ^ 2) \tag{4.5.5}
$$

である。ここで$$\Delta x = - \left( x _ {(k+1)} - x _ {(k)} \right)$$とおくと、

$$
\operatorname{grad} f (x _ {(k)}) = \operatorname{grad}f(x _ {(k+1)}) - \left<\nabla \operatorname{grad}f(x _ {(k+1)}), x _ {(k+1)} - x _ {(k)} \right> + O(\| x _ {(k+1)} - x _ {(k)} \| ^ 2) \tag{4.5.6}
$$

であり、整理すれば

$$
\left<\nabla \operatorname{grad}f(x _ {(k+1)}), x _ {(k+1)} - x _ {(k)} \right> = \operatorname{grad} f (x _ {(k+1)}) - \operatorname{grad}f(x _ {(k)}) + O(\| x _  {(k+1)} - x _ {(k)} \| ^ 2) \tag{4.5.7}
$$

となる。この式は Hesse 行列$$H _{x _ {(k+1)}} = \nabla \operatorname{grad} f (x _ {(k+1)})$$と \(4.5.4\) 式の$$s_ {(k)}, y _ {(k)}$$を用いれば

$$
H _ {x _ {(k+1)}} s _ {(k)} = y _ {(k)} + O(\| x _  {(k+1)} - x _ {(k)} \| ^ 2) \tag{4.5.7}
$$

と書き直せる。上の式で誤差の項を無視した

$$
B _ {(k+1)} s _ {(k)} = y _ {(k)} \tag{4.5.8}
$$

がセカント条件の第1式である。\(4.5.8\) 式の両辺に左から$$H _ {(k+1)} = B _ {(k+1)} ^ {-1}$$をかければ

$$
H _ {(k+1)} y _ {(k)} = s _ {(k)} \tag{4.5.9}
$$

となってセカント条件の第2式が求まる。

## 収束性

準ニュートン法は超1次収束のアルゴリズムである。

