---
description: 2020/1/4公開
---

# 3. 最適化問題

\*\*\*\*$$\mathcal{S}$$を空でない任意の集合とする。$$\mathcal{S}$$上の**目的関数**（objective function）と呼ばれる関数$$f \colon \mathcal{S} \to \mathbb{R} \colon x \mapsto f(x)$$を最小化（または最大化）する点$$x ^ \ast$$を求める問題を$$\mathcal{S}$$上の**最適化問題**（optimization problem）という。この問題の解$$x ^ \ast$$は問題の**最適解**（optimal solution）という。

特に関数$$f$$が$$\mathcal{S}$$上の連続関数であるとき、その最適化問題は**連続最適化問題**（continuous optimization problem）と呼ばれる。

関数$$f$$の最小値（minimum value）、最大値（maximum value）はそれぞれ

$$
\underset{ x \in \mathcal{S} }{\operatorname{min}} \, f(x) \, , \,\, \underset{ x \in \mathcal{S} }{\operatorname{max}} \, f(x)
$$

と表記される。

最適解$$x ^ \ast$$は一般にひとつとは限らない。そこで関数$$f$$の最小値を与える最適解の集合を

$$
\underset{x \in \mathcal{S}}{\operatorname{arg} \operatorname{min}} \, f(x)
$$

と表記する。最適解の集合は空集合になることもあるし、最適解が無数に存在することもある。$$\operatorname{arg}\operatorname{min}$$は「argument of minimum（最小値を与える引数）」の略である。この最適解の集合を求める問題を$$\mathcal{S}$$上の**最小化問題**（minimization problem）という。同様に、関数$$f$$の最大値を与える最適解の集合を

$$
\underset{x \in \mathcal{S}}{\operatorname{arg} \operatorname{max}} \, f(x)
$$

と表記する。$$\operatorname{arg}\operatorname{max}$$は「argument of minimum（最大値を与える引数）」の略である。この集合を求める問題を$$\mathcal{S}$$上の**最大化問題**（maximization problem）という。

関数$$f$$の符号を反転すれば最小化問題と最大化問題は入れ替えることができるので、最適化問題ではどちらか一方を考えれば十分であり、大抵は最小化問題として扱うことが多い。

最適化問題には**制約条件**（constraint、束縛条件ということもある）を課す場合がある。たとえば正定値対称行列$$A$$の最大の固有値に対応する固有ベクトルを求めるには、レイリー商

$$
f(x) = x ^ \mathrm{T} A x
$$

の最大化問題を考えることになる。しかしこの目的関数は$$x$$のノルムを大きくしていけばいくらでも大きな値をとるので、その最適解は$$\| x \| = +\infty$$となるような点$$x$$の集合という無意味な解になる。実際、固有ベクトルにはノルムの自由度が存在して、重要なのはその方向だけなので、$$\| x \| = 1$$の範囲で解を探せば十分である。この最大化問題は

$$
\underset{x \in \mathbb{R} ^ n}{\operatorname{arg} \operatorname{max}} \, x ^ \mathrm{T} A x\quad \operatorname{s.t.} \|x\| = 1
$$

と書く。「$$\operatorname{s.t.}$$」は「such that（〜を満たすような）」または「subject to（〜の条件下で）」の略である。どちらと読むかはその人の好みでよい。

制約条件のついた最適化問題を**制約付き最適化問題**（constrained optimization problem）という。$$g(x) = c$$の形で書かれる制約条件を**等式制約**（equality constraint）といい、$$h(x) \leq c$$の形で書かれる制約条件を**不等式制約**（inequality constraint）という。$$h(x) < c$$の形で不等式制約を設けると目的関数の最大値や最小値の存在を保証するのが難しくなるので、この形は連続最適化の文脈ではほとんど見かけない。

等式制約と不等式制約は同時に課してもよいし、また同時にいくつ課してもよい。したがって制約付き最適化問題は一般に

$$
\underset{x \in \mathbb{R} ^ n}{\operatorname{arg} \operatorname{max}} \, f(x) \quad \operatorname{s.t.} \underset{i}{{\sf E}} \left\{ g _ i (x) = c _ i \right\}, \underset{j}{{\sf E}} \left\{ h _ j (x) \leq d _ j \right\}
$$

という形で表される。ただし$${\sf E}$$は「列挙」を意味する記号で

$$
\underset{i}{{\sf E}} \left\{ g _ i (x) = c _ i \right\} \equiv g _ 1(x) = c _ 1, g _ 2(x) = c _ 2, \ldots, g _ n(x) = c _ n
$$

と定義する。詳しくは

{% page-ref page="../notation.md" %}

を参照のこと。

制約付き最適化問題に対して、制約条件のない最適化問題は**制約なし最適化問題**（unconstrained optimization problem）という。

