# Taylor展開と関数近似

Taylor展開可能な関数$$f \colon \mathbb{R} \to \mathbb{R} \colon x \mapsto f(x)$$の、点$$\overline{x}$$の周りのTaylor展開は、$$x = \overline{x} + \Delta x$$の変数変換のもとで

$$
\begin{aligned}
f(x)= f(\overline{x} + \Delta x) &= \sum _ {n=0} ^ {+\infty} \frac{1}{n!} \frac{d ^ n f (\overline{x})}{dx ^ n} \Delta x ^ n \\
&= f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x + \frac{1}{2} \frac{d ^ 2 f (\overline{x})}{dx ^ 2} \Delta x ^ 2 + \cdots
\end{aligned} \tag{1}
$$

で与えられる。$$\overline{x}$$が定数で$$\Delta x$$が新たな変数である。つまり点$$\overline{x}$$から$$\Delta x$$だけ移動した点における点$$x = \overline{x} + \Delta x$$における$$f(x)$$の値が \(1\) 式によって任意の精度で近似できる。

Taylor展開を$$\Delta x ^ n$$の項で打ち切った関数

$$
f _ n (x) = f _ n(\overline{x} + \Delta x) = f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x + \frac{1}{2} \frac{d ^ 2 f (\overline{x})}{dx ^ 2} \Delta x ^ 2 + \cdots + \frac{1}{n!}\frac{d ^ n f (\overline{x})}{dx ^ n} dx ^ n
$$

を$$f(x)$$の$$n$$次近似という。本書で紹介する連続最適化で使われるのは主に1次近似と2次近似であり、それぞれ



$$
\begin{aligned}
f _ {\rm I} (x) &= f _ 1 (\overline{x} + \Delta x) = f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x \tag{2} \\
f _ {\rm II} (x) &= f _ 1 (\overline{x} + \Delta x) = f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x + \frac{1}{2} \frac{d ^ 2 f (\overline{x})}{dx ^ 2} \Delta x ^ 2 
\end{aligned}
$$

である。3次以上の項に着目することは少ない（c.f. self-concordant function）。

同様に、Taylor展開可能な関数$$f \colon \mathbb{R} ^ n \to \mathbb{R} \colon x \mapsto f(x)$$の点$$\overline{x}$$の周りのTaylor展開は、

$$
x = \left(\begin{matrix}
x _ 1 \\
x _ 2 \\
\vdots \\
x _ n
\end{matrix} \right) =  \left(\begin{matrix}
\overline{x} _ 1 + \Delta x _ 1 \\
\overline{x} _ 2 + \Delta x _ 2 \\
\vdots \\
\overline{x} _ n + \Delta x _ n
\end{matrix} \right) = \left(\begin{matrix}
\overline{x} _ 1 \\
\overline{x} _ 2 \\
\vdots \\
\overline{x} _ n
\end{matrix} \right) + \left(\begin{matrix}
\Delta x _ 1 \\
\Delta x _ 2 \\
\vdots \\
\Delta x _ n
\end{matrix} \right) = \overline{x} + \Delta x
$$

の変数変換のもとで、

$$
f(x) = f(\overline{x} + \Delta x) =  f(\overline{x}) + \sum _ {i=1} ^ n \frac{\partial f (\overline{x})}{\partial x _ i} \Delta x _ i + \frac{1}{2} \sum _ {i=1} ^ n \sum _ {j=1} ^ n \frac{\partial ^ 2 f (\overline{x})}{\partial x _ i \partial x _ j} \Delta x _ i \Delta x _ j+ \cdots \tag{2}
$$



