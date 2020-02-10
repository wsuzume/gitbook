# 4.5.2. BFGS法

## アルゴリズム

$$B _ {(k+1)}$$​を以下の BFGS 公式によって更新する

$$
B _ {(k+1)} = B _ {(k)} - \frac{B _ {(k)} s _ {(k)} s_ {(k)} ^ \mathrm{T} B _ {(k)}}{\left<s _ {(k)}, B _ {(k)} s _ {(k)} \right>} + \frac{y _ {(k)} y _ {(k)} ^ \mathrm{T}}{\left<s _ {(k)}, y _ {(k)} \right>}
$$

あるいはその逆行列$$H _ {(k+1)} = B _ {(k+1)} ^ {-1}$$を次の式で更新することもできる（上の式を Sherman-Morrison の公式で反転したものであり、DFP 法の式とよく似ているので間違えないように注意する）

$$
H _ {(k+1)} = \left( I - \frac{s _ {(k)} y _ {(k)} ^ \mathrm{T}}{\left<s _ {(k)}, y _ {(k)} \right>} \right) H _ {(k)} \left( I - \frac{s _ {(k)} y _ {(k)} ^ \mathrm{T}}{\left<s _ {(k)}, y _ {(k)} \right>} \right) ^ \mathrm{T} + \frac{s _ {(k)} s _ {(k)} ^ \mathrm{T}}{\left<s _ {(k)}, y _ {(k)} \right>}
$$

## 原理

あとで。

