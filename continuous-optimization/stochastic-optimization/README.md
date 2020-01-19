# 5. 確率的最適化

連続最適化の文脈での直線探索法では

$$
\underset{x \in \mathcal{S}}{\operatorname{arg} \operatorname{min}} \, f(x)
$$

という最適化問題を考えたが、確率的最適化では

$$
\underset{x \in \mathcal{S}}{\operatorname{arg} \operatorname{min}} \, \frac{1}{\# \Lambda}\sum _ { \ell \in \Lambda} f ^{(\ell)} (x)
$$

と記述できる問題を考える。ただし$$\# \Lambda$$は集合$$\Lambda$$の要素数である。上の式の表記は難しく見えるが、$$\Lambda$$は観測したデータの番号だと思えば、パラメータを$$x$$に固定したときの各データ点ごとの誤差$$f ^ {(\ell)}(x)$$の平均

$$
F(x) = \frac{1}{\# \Lambda}\sum _ { \ell \in \Lambda} f ^{(\ell)} (x)
$$

を最小化する問題だとみなせるので幾分解釈しやすいだろう。たとえば5つのデータが観測されたときは$$\Lambda = \{1,2,3,4,5 \}$$として

$$
\frac{1}{\# \Lambda}\sum _ { \ell \in \Lambda} f ^{(\ell)} (x) = \frac{f ^ {(1)}(x) + f ^ {(2)}(x) + f ^ {(3)}(x) + f ^ {(4)}(x) + f ^ {(5)}(x)}{5}
$$

である。

最小二乗法による線形回帰を確率最適化の文脈に書き直してみよう。

