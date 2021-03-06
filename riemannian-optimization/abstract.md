# Riemannian最適化（概要）

Riemannian 最適化（Riemannian Optimization）は Riemann 多様体上での連続最適化を指す。Riemannian 最適化は通常は計算量が大きく、理論上は可能でも応用が難しい手法であったが、P. A. Absil, R. Mahony, R. Sepulchre らによる書籍『Optimization Algorithms on Matrix Manifold』にて軽量化された直線探索法が提案された。

直線探索法は目的関数の降下方向を定め、その探索直線に沿った極値へと更新を繰り返していく手法で、最急降下法、ニュートン法、およびそこから派生した方法の総称である。通常の直線探索法はユークリッド空間の全体を探索領域とするが、Riemannian 最適化では探索領域を Riemann 多様体上に制限することができる。たとえば直交行列全体からなる Stiefel 多様体上での探索が可能となるので直交性を厳密に保証したまま探索するといったことができる。

Riemannian 最適化を厳密に理解するには高度な数学的知識（数学科の学部4年生程度）を必要とすること、また比較的新しい技術であるため入門書がほぼ存在しないことが敷居を高めている。

一方で Riemannian 最適化をおおまかに理解して実装するだけであれば、それほど難しくはない。Absil らの手法はユークリッド空間上での直線探索にいくつかの修正を加えただけであり、その修正がどうして行われていてどんな意味があるのかはかなり直感的に理解できる（それで本当に収束性が保証されると証明したのが Absil らの功績である）。

そこで本書では、

1. 簡単な例を実装しながらユークリッド空間上での直線探索と異なる点を列挙する
2. Riemann 多様体上での線形探索に用いられる概念について詳しく説明する

という2段階の手順で解説を行う。

1段階目には

* とりあえず試してみたい読者がすぐに実装できるようにする
* 先に実装を終えていることで読者が自信を持って高度な話題に進めるようにする
* 高度な話題の最中で目標を見失ったときに概略図に立ち戻れるようにする

という意味がある。

2段階目は

* 専門書や論文で Riemannian 最適化を学びたい人のために踏み込んだ知識を提供する

という場にしたい。そこから先は本書を執筆している2020年現在でも最先端の領域になるのでご自身で切り開いていただきたい。

