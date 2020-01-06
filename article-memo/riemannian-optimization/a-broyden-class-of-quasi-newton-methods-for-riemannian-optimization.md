---
description: 2020/1/4公開
---

# A Broyden Class of Quasi-Newton Methods for Riemannian Optimization

## メモ

Riemannian 最適化の準ニュートン法に関する論文。『Optimization Algorithms on Matrix Manifolds』の Absil が共著。主著の Huang は他にも Riemannian 最適化の論文を出しており、界隈のトップ研究者のひとりである。

『Optimization Algorithms on Matrix Manifolds』では最急降下法、ニュートン法、共役勾配法、信頼領域法について言及があったが、準ニュートン法はなかった。この論文によって Riemannian 最適化の準ニュートン法についての収束性が示された。

Broydenクラス、すなわちDFP法とBFGS法を含むクラスの準ニュートン法を isometric vector transport（等長性が追加された vector transport）を導入して構成し、収束性を確かめている。しかし

1. isometric vector transport を具体的に構成するのが非常に難しいこと
2. Riemannian最適化においてBroydenクラスは非現実的な計算量（時間、空間両方）になること

が言及されている。

ただし L-BFGS 法は時間計算量、空間計算量ともにギリギリセーフな範囲である。本来は isometric vector transport を用いるべきであるが、この論文では通常の vector transport を用いて L-BFGS 法を実装し、実験している。L-BFGS 法は共役勾配法と比べてイテレーションごとの計算量が大きいが、より少ない回数のイテレーションで収束するので、全体的な実行時間は L-BFGS 法のほうが小さくなると報告されている。

## 論文

{% embed url="https://www.math.fsu.edu/~aluffi/archive/paper488.pdf" %}



