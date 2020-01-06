---
description: 2020/1/4公開
---

# 1. Taylor展開と関数近似

## 1.1. Taylor展開と関数の1次近似、2次近似

Taylor 展開による関数近似は**直線探索法**（line search method）と呼ばれる連続最適化手法を理解する上での基礎になる。

Taylor 展開可能な関数$$f \colon \mathbb{R} \to \mathbb{R} \colon x \mapsto f(x)$$の、点$$\overline{x}$$の周りの Taylor 展開は、$$x = \overline{x} + \Delta x$$の変数変換のもとで

$$
\begin{aligned}
f(x)= f(\overline{x} + \Delta x) &= \sum _ {n=0} ^ {+\infty} \frac{1}{n!} \frac{d ^ n f (\overline{x})}{dx ^ n} \Delta x ^ n \\
&= f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x + \frac{1}{2} \frac{d ^ 2 f (\overline{x})}{dx ^ 2} \Delta x ^ 2 + \cdots
\end{aligned} \tag{1.1.1}
$$

で与えられる。$$\overline{x}$$が定数で$$\Delta x$$が新たな変数である。つまり点$$\overline{x}$$から$$\Delta x$$だけ移動した点における点$$x = \overline{x} + \Delta x$$における$$f(x)$$の値が \(1.1.1\) 式によって任意の精度で近似できる。

Taylor 展開を$$\Delta x ^ n$$の項で打ち切った関数

$$
f _ n (x) = f _ n(\overline{x} + \Delta x) = f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x + \frac{1}{2} \frac{d ^ 2 f (\overline{x})}{dx ^ 2} \Delta x ^ 2 + \cdots + \frac{1}{n!}\frac{d ^ n f (\overline{x})}{dx ^ n} \Delta x ^ n \tag{1.1.2}
$$

を$$f(x)$$の$$n$$次近似という（$$n$$次の Taylor 多項式ともいう）。本書で紹介する連続最適化で使われるのは主に1次近似と2次近似であり、それぞれ

$$
\begin{aligned}
f _ {\rm I} (x) &= f _ 1 (\overline{x} + \Delta x) = f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x  \\
f _ {\rm II} (x) &= f _ 1 (\overline{x} + \Delta x) = f(\overline{x}) + \frac{d f (\overline{x})}{dx} \Delta x + \frac{1}{2} \frac{d ^ 2 f (\overline{x})}{dx ^ 2} \Delta x ^ 2 
\end{aligned} \tag{1.1.3}
$$

である。3次以上の項に着目することは少ない（c.f. self-concordant function）。

同様に、Taylor 展開可能な関数$$f \colon \mathbb{R} ^ n \to \mathbb{R} \colon x \mapsto f(x)$$の点$$\overline{x}$$の周りの Taylor 展開は、

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
f(x) = f(\overline{x} + \Delta x) =  f(\overline{x}) + \sum _ {i=1} ^ n \frac{\partial f (\overline{x})}{\partial x _ i} \Delta x _ i + \frac{1}{2} \sum _ {i=1} ^ n \sum _ {j=1} ^ n \frac{\partial ^ 2 f (\overline{x})}{\partial x _ i \partial x _ j} \Delta x _ i \Delta x _ j+ \cdots \tag{1.1.4}
$$

で与えられる。一般項は表記が面倒な上に、どうせ2次の項までしか使わないので書かなかった。

ここでナブラ演算子$$\nabla$$を列ベクトル

$$
\nabla = \left( \frac{\partial }{\partial x _ 1}, \frac{\partial }{\partial x _ 2}, \cdots , \frac{\partial }{\partial x _ n} \right) ^ \mathrm{T}
$$

として定義すると、

$$
\nabla f = \left( \frac{\partial f}{\partial x _ 1}, \frac{\partial f}{\partial x _ 2}, \cdots , \frac{\partial f}{\partial x _ n} \right) ^ \mathrm{T}
$$

であるから、内積

$$
\left< a , b\right> = a ^ \mathrm{T} b = \sum _ {i = 1} ^ n a _ i b _ i
$$

を用いて、\(1.1.4\) 式の1次の項は

$$
\left< \nabla f(\overline{x}), \Delta x \right> = \sum _ {i=1} ^ n \frac{\partial f (\overline{x})}{\partial x _ i} \Delta x _ i \tag{1.1.5}
$$

と書ける。幾何的な意味づけとしては$$\nabla f (\overline{x})$$は点$$\overline{x}$$における関数$$f(x)$$の勾配だから

$$
\operatorname{grad} f = \nabla f \tag{1.1.6}
$$

である。

2次の項についても同様の行列形式による表記を行いたい。次の

$$
H = (\nabla \nabla ^ \mathrm{T}) f = \left(
\begin{matrix}
\frac{\partial ^ 2 f}{\partial x _ 1 \partial x _ 1} & \frac{\partial ^ 2 f}{\partial x _ 1 \partial x _ 2} & \cdots & \frac{\partial ^ 2 f}{\partial x _ 1 \partial x _ n} \\
\frac{\partial ^ 2 f}{\partial x _ 2 \partial x _ 1} & \frac{\partial ^ 2 f}{\partial x _ 2 \partial x _ 2} & \cdots & \frac{\partial ^ 2 f}{\partial x _ 2 \partial x _ n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial ^ 2 f}{\partial x _ n \partial x _ 1} & \frac{\partial ^ 2 f}{\partial x _ n \partial x _ 2} & \cdots & \frac{\partial ^ 2 f}{\partial x _ n \partial x _ n}
\end{matrix}
\right)
$$

で定義される$$H$$は Hesse 行列と呼ばれる。Hesse 行列を用いれば \(1.1.4\) 式の2次の項は

$$
\left< H _ {\overline{x}} \Delta x, \Delta x \right> = \sum _ {i=1} ^ n \sum _ {j=1} ^ n \frac{\partial ^ 2 f (\overline{x})}{\partial x _ i \partial _ j} \Delta x _ i \Delta x _ j \tag{1.1.7}
$$

と書ける。ただし$$H _ x = (\nabla \nabla ^ \mathrm{T} ) f (x)$$であり、どの点における Hesse 行列なのかを明記している。書物によっては$$H _ x$$を単に$$H$$と書いていたりするので注意する。

Hesse 行列はユークリッド空間上での Hessian 演算子 $$\operatorname{Hess} f (x) \colon \mathbb{R} ^ n \to \mathbb{R} ^ n$$の行列表記であり、ユークリッド空間では

$$
{\rm Hess} f(x) \Delta x = H _ x \Delta x \tag{1.1.8}
$$

である。

\(1.1.4\) 式に \(1.1.5\), \(1.1.6\), \(1.1.7\), \(1.1.8\) 式の結果を用いれば、関数$$f \colon \mathbb{R} ^ n \to \mathbb{R}$$の1次近似と2次近似はそれぞれ

$$
\begin{aligned}
f _ {\rm I} (x) = f _ 1 (\overline{x} + \Delta x) &= f(\overline{x}) + \left< \nabla f(\overline{x}), \Delta x \right> \\
&= f(\overline{x}) + \left< \operatorname{grad} f(\overline{x}), \Delta x \right> \\
f _ {\rm II} (x) = f _ 1 (\overline{x} + \Delta x) &= f(\overline{x}) +  \left< \nabla f(\overline{x}), \Delta x \right> + \left< \Delta x ^ \mathrm{T} H _ {\overline{x}}, \Delta x \right> \\
&= f(\overline{x}) + \left< \operatorname{grad} f(\overline{x}), \Delta x \right> + \left< \operatorname{Hess} f(\overline{x}) \Delta x, \Delta x \right>
\end{aligned} \tag{1.1.9}
$$

と書ける。$$\operatorname{grad}$$や$$\operatorname{Hess}$$を用いた表記は幾何的な意味との対応がついているので、ユークリッド空間以外でも$$\operatorname{grad}, \operatorname{Hess}$$を定義すれば適用できる（本書でも Riemannian 最適化で登場する）。

## 1.2. 連続最適化との関係

現代科学で扱われる大抵の問題は目的関数の最適解が直接的（代数的）には求まらない。代わりに「関数を近似する$$\to$$近似した関数の最適解へ進む」という手順を繰り返して最終的に近似する前のもとの関数の最適解に到達するような手法を構成する（解析的に求める）。

目的関数が複雑な形状をしていても1次近似や2次近似は計算できることが多く、2次近似した関数の最適解は2次関数の頂点を求める問題とほぼ同じなので比較的容易に計算できる。

また連続最適化は、点$$x ^ k$$からある方向$$m ^ k$$に$$\alpha ^ k$$だけ進んだ点$$x ^ {k+1} = x ^ k + \alpha ^ k m ^ k$$が$$k \to +\infty$$の極限で最適解（または極値）に収束するような手法として構成されることが多いので、ある点の近傍での関数の形状を近似する Taylor 展開が連続最適化でよく登場するのである。

点$$x ^ k$$は探索の起点であり固定するから Taylor 展開における$$\overline{x}$$とみなせて、$$\alpha ^ k m ^ k$$は点$$\overline{x}$$からの変化なので$$\Delta x$$に対応する。つまり

$$
\begin{aligned}
\overline{x} = x ^ k, \,\, \Delta x = \alpha ^ k m ^ k \quad (x ^ k, m ^ k \in \mathbb{R} ^ n, \alpha ^ k \in \mathbb{R})
\end{aligned} \tag{1.2.1}
$$

であって

$$
\begin{aligned}
x &= \overline{x} + \Delta x \\
x ^ {k+1} &= x ^ k + \alpha ^ k m ^ k
\end{aligned} \tag{1.2.2}
$$

の2式が対応している。今後は$$x ^ k$$などを用いる方の説明がメインになるが、\(1.2.1\), \(1.2.2\) 式を用いた式の書き換えは断りなしに行うことがあるので注意してほしい。

