# 4.3. ニュートン法

## アルゴリズム

1. 初期値$$x ^ 0 \in \mathbb{R} ^ n$$を定める（定め方は任意である）

2. 次の更新式を用いて更新を繰り返す

$$
\begin{aligned}
x ^ {k+1} &= x ^ k + \Delta x ^ k \\
&= x ^ k - H _ {x ^ k} ^ {-1} \operatorname{grad} f ( x ^ k )
\end{aligned}
$$

## 原理

最急降下法のときと同様に

$$
\| \operatorname{grad} f (x) \| = 0 \tag{4.3.1}
$$

を満たすような点$$x$$を見つける。ただしニュートン法では以下の関数の2次近似を用いる。

$$
f _ {\rm II} (x)  
= f(\overline{x}) + \left< \operatorname{grad} f(\overline{x}), \Delta x \right> + \left< \operatorname{Hess} f(\overline{x}) \Delta x, \Delta x \right> \tag{4.3.2}
$$

2次近似した関数の極値は

