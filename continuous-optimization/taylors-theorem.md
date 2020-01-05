---
description: 2020/1/6公開
---

# 2. Taylorの定理と誤差の評価

前の節では説明の簡略化のために Taylor 展開を有限個の項で打ち切ることで関数近似を導出したが、Taylor 展開を用いるには

* $$f(x)$$が無限階微分可能である
* Taylor 級数が収束する
* Taylor 級数がもとの関数$$f(x)$$に一致する

といった比較的厳しい条件を満たす必要があり、また近似した関数のもとの関数からの誤差を評価するのが難しくなる。

実際に理論的に解析するには、より緩い条件で成り立つ Taylor の定理を用いる。Taylor の定理は、整数$$n \,\,(n \geq 1)$$をとったとき、$$n$$階微分可能な関数$$f \colon \mathbb{R} \to \mathbb{R}$$に対して、次の性質

$$
\begin{aligned}
f(x) = f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x + \frac{1}{2} \frac{d ^ 2 f (\overline{x})}{dx ^ 2} \Delta x ^ 2 + \cdots + \frac{1}{n!} \frac{d ^ n f (\overline{x})}{dx ^ n} \Delta x ^ n + h _ n (\Delta x) \Delta x ^ n \\
\left( \lim _ {\Delta x \to 0} h _ n (\Delta x) = 0 \right)
\end{aligned} \tag{2.1}
$$

を満たす関数$$h _ n\colon \mathbb{R} \to \mathbb{R}$$が存在するという主張である。

\(2.1\) 式から$$h _ n (\Delta x) \Delta x ^ n$$の項を取り除くと前節で定義した \(1.1.2\) 式による関数の$$n$$次近似と一致している。すなわち

$$
f(x) - f _ n (x) = h _ n (\Delta x) \Delta x ^ n
$$

が成り立つので、$$h _ n (\Delta x) \Delta x ^ n$$は近似誤差を表しているとみなせる。この近似誤差はランダウの記号を用いれば

$$
h _ n (\Delta x) \Delta x ^ n = o \left( |\Delta x | ^n \right) \tag{2.2}
$$

と書けるから、関数の1次近似と2次近似について

$$
\begin{aligned}
f (x) &= f _ {\rm I} (x) + o \left( |\Delta x | \right) \\
f (x) &= f _ {\rm II} (x) + o \left( |\Delta x | ^ 2 \right)
\end{aligned} \tag{2.3}
$$

が成り立つ。

関数$$f \colon \mathbb{R} ^ n \to \mathbb{R} \colon x \mapsto f(x)$$についても同様に、ユークリッドノルム$$\| \cdot \| \colon \mathbb{R} ^ n \to \mathbb{R}$$を用いて

$$
\begin{aligned}
f (x) &= f _ n (x) + h _ n (\Delta x) \|\Delta x \| ^ n \quad \left( \lim _ {\| \Delta x \| \to 0} h _ n (\Delta x) = 0 \right)
\end{aligned} \tag{2.4}
$$

が成り立つ。近似誤差は

$$
h _ n (\Delta x) \| \Delta x \| ^ n = o \left( \| \Delta x \| ^ n \right)
$$

と評価できて、$$n = 1, 2$$の場合について

$$
\begin{aligned}
f (x) &= f _ {\rm I} (x) + o \left( \|\Delta x \| \right) \\
f (x) &= f _ {\rm II} (x) + o \left( \|\Delta x \| ^ 2 \right)
\end{aligned} \tag{2.5}
$$

である。

