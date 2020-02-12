# Table of contents

* [数学プログラミング置き場](README.md)
* [数学記号記法一覧](notation.md)

## 機械学習・データサイエンス <a id="mml"></a>

* [1. 機械学習・データサイエンス（概要）](mml/abstract.md)
* [2. 機械学習](mml/machine-learning/README.md)
  * [2.1. 機械学習をこれから始める人へ](mml/machine-learning/wokorekarameruhe.md)
  * [2.2. 回帰問題](mml/machine-learning/hui-gui-wen-ti/README.md)
    * [2.2.1. 線形回帰](mml/machine-learning/hui-gui-wen-ti/xian-xing-hui-gui.md)
    * [2.2.2. 重線形回帰と正則化](mml/machine-learning/regression/222-to.md)
    * [2.2.3. 線形基底関数モデル](mml/machine-learning/hui-gui-wen-ti/moderu.md)
    * [2.2.4. カーネル回帰](mml/machine-learning/hui-gui-wen-ti/kneru-2.md)
    * [2.2.5. ガウス過程回帰](mml/machine-learning/hui-gui-wen-ti/gausu.md)
  * [分類問題](mml/machine-learning/fen-lei-wen-ti/README.md)
    * [線形判別分析](mml/machine-learning/fen-lei-wen-ti/xian-xing-pan-bie-fen-xi.md)
    * [SVM](mml/machine-learning/fen-lei-wen-ti/svm.md)
    * [カーネルSVM](mml/machine-learning/fen-lei-wen-ti/knerusvm.md)
  * [強化学習](mml/machine-learning/jiang-hua-xue-xi.md)
  * [ニューラルネットワーク](mml/machine-learning/nyrarunettowku/README.md)
    * [画像処理](mml/machine-learning/nyrarunettowku/hua-xiang-chu-li.md)
    * [自然言語処理](mml/machine-learning/nyrarunettowku/zi-ran-yan-yu-chu-li.md)
* [データサイエンス](mml/data-science/README.md)
  * [主成分分析](mml/data-science/zhu-cheng-fen-fen-xi.md)
  * [白色化](mml/data-science/bai-se-hua.md)
  * [低ランク行列近似](mml/data-science/ranku.md)
  * [行列補完](mml/data-science/hang-lie-bu-wan.md)
* [ベイズ推論](mml/beizu.md)
  * [確率](mml/beizu/que-lv.md)
  * [確率分布](mml/beizu/que-lv-fen-bu.md)
  * [ちょっとだけ振り返って](mml/beizu/chottodakeritte.md)
* [大学数学概要](mml/mathematics-for-university-students/README.md)
  * [線形代数学](mml/mathematics-for-university-students/linear-algebra.md)
  * [解析学](mml/mathematics-for-university-students/analytics.md)
  * [確率論](mml/mathematics-for-university-students/probability-theory.md)
  * [統計学](mml/mathematics-for-university-students/statistics.md)
  * [情報理論](mml/mathematics-for-university-students/information-thory.md)

## 連続最適化 <a id="continuous-optimization"></a>

* [1. Taylor展開と関数近似](continuous-optimization/taylor-series.md)
* [2. Taylorの定理と誤差の評価](continuous-optimization/taylors-theorem.md)
* [3. 最適化問題](continuous-optimization/optimization-problem.md)
* [4. 直線探索法](continuous-optimization/line-search-method/README.md)
  * [4.1. 最急降下法](continuous-optimization/line-search-method/gradient-descent.md)
  * [4.2. Armijo条件・Wolfe条件](continuous-optimization/line-search-method/armijo-wolfe-condition.md)
  * [4.3. ニュートン法](continuous-optimization/line-search-method/newtons-method.md)
  * [4.4. 共役勾配法](continuous-optimization/line-search-method/conjugate-gradient-method/README.md)
    * [4.4.1. 原始的な共役勾配法](continuous-optimization/line-search-method/conjugate-gradient-method/na.md)
    * [4.4.2. PRP法](continuous-optimization/line-search-method/conjugate-gradient-method/prp-fa.md)
    * [4.4.3. HS法](continuous-optimization/line-search-method/conjugate-gradient-method/hs-fa.md)
  * [4.5. 準ニュートン法](continuous-optimization/line-search-method/quasi-newton-method/README.md)
    * [4.5.1. DFP法](continuous-optimization/line-search-method/quasi-newton-method/dfp-method.md)
    * [4.5.2. BFGS法](continuous-optimization/line-search-method/quasi-newton-method/bfgs-method.md)
    * [4.5.3. L-BFGS法](continuous-optimization/line-search-method/quasi-newton-method/lbfgs-method.md)
    * [4.5.4. Bryoden family of methods](continuous-optimization/line-search-method/quasi-newton-method/4.5.4.-bryoden-family-of-methods.md)
    * [4.5.5. Broyden法](continuous-optimization/line-search-method/quasi-newton-method/broyden-class-method.md)
* [5. 確率的最適化](continuous-optimization/stochastic-optimization/README.md)
  * [5.1. 確率的勾配降下法（SGD）](continuous-optimization/stochastic-optimization/sgd.md)
  * [5.2. 確率的準ニュートン法（SQN）](continuous-optimization/stochastic-optimization/sqn.md)

## カーネル法 <a id="kernel-method"></a>

* [カーネル法（概要）](kernel-method/abstract.md)

## Riemannian最適化 <a id="riemannian-optimization"></a>

* [Riemann多様体って？](riemannian-optimization/riemanntte.md)
* [Riemannian最適化（概要）](riemannian-optimization/abstract.md)
* [概説](riemannian-optimization/overview.md)
* [詳説](riemannian-optimization/detail/README.md)
  * [解析学](riemannian-optimization/detail/analytics.md)
  * [線形代数学（反変性・共変性・不変量）](riemannian-optimization/detail/linear-algebra.md)
  * [テンソル解析](riemannian-optimization/detail/tensor-analysis.md)
  * [リーマン積分と微分形式](riemannian-optimization/detail/differential-form.md)
  * [位相空間論](riemannian-optimization/detail/topology.md)
  * [多様体論（解析幾何学）](riemannian-optimization/detail/duo-yang-ti-lun-jie-xi-ji-he-xue.md)
  * [Riemann多様体](riemannian-optimization/detail/riemannian-manifold.md)

## プログラミングサイドブック <a id="programming-side-book"></a>

* [はじめに](programming-side-book/attitude.md)
* [Step 0. 勉強の仕方](programming-side-book/study-hard/README.md)
  * [いつ始める？どれくらい勉強する？](programming-side-book/study-hard/when-how-much.md)
  * [どうやって勉強する？](programming-side-book/study-hard/how.md)
  * [どこから手をつけたらいい？](programming-side-book/study-hard/where.md)
* [Step 1. インターネットで調べる](programming-side-book/using-internet.md)
* [Step 2. コンピュータの仕組みを学ぶ](programming-side-book/step-2-konpytanomiwobu.md)
* [Step 3. 開発環境を整える](programming-side-book/step-3-woeru.md)
* [Step 4. プログラミング言語を学ぶ](programming-side-book/step-4-puroguraminguwobu.md)
* [Step 5. 次のステップへ進むには](programming-side-book/step-5-nosuteppuhemuniha.md)
* [Step 6. 情報科学を学ぶ](programming-side-book/step-6-wobu.md)

## プログラミング <a id="programming"></a>

* [プログラミング（概要）](programming/system-abstract.md)
* [システムの構成](programming/system-architecture.md)
* [サーバーのセットアップ](programming/setup-server/README.md)
  * [OSセットアップ](programming/setup-server/setup-os/README.md)
    * [ユーザの作成](programming/setup-server/setup-os/create-user.md)
    * [SSHの設定](programming/setup-server/setup-os/ssh-setting.md)
    * [ファイアウォールの設定](programming/setup-server/setup-os/firewall-setting.md)
  * [ドメインの取得と設定（Google domain）](programming/setup-server/domain.md)
* [Dockerによる仮想化](programming/virtualize-with-docker.md)
* [サーバーサイド（golang/gin）](programming/server-side.md)
* [リバースプロキシの設置（nginx）](programming/reverse-proxy.md)
* [SSL/TLS（Let's Encrypt）](programming/ssl-tls-setting.md)
* [フロントエンド（Elm）](programming/front-end.md)
* [Authentication（Firebase）](programming/authentication-firebase.md)
* [DB（MySQL）](programming/db-mysql.md)
* [KVS（Redis）](programming/kvs-redis.md)

## 書籍メモ <a id="book-memo"></a>

* [書籍メモ（概要）](book-memo/abstract.md)

## 論文メモ <a id="article-memo"></a>

* [論文メモ（概要）](article-memo/abstract.md)
* [線形代数](article-memo/linear-algebra/README.md)
  * [The Matrix Cookbook](article-memo/linear-algebra/the-matrix-cookbook.md)
  * [ON THE EARLY HISTORY OF THE SINGULAR VALUE DECOMPOSITION](article-memo/linear-algebra/on-the-early-history-of-the-singular-value-decomposition.md)
  * [The tensor rank decomposition](article-memo/linear-algebra/the-tensor-rank-decomposition.md)
* [行列分解](article-memo/matrix-factorization/README.md)
  * [Probabilistic Matrix Factorization](article-memo/matrix-factorization/probabilistic-matrix-factorization.md)
  * [Probabilistic Matrix Factorization with Non-random Missing Data](article-memo/matrix-factorization/probabilistic-matrix-factorization-with-non-random-missing-data.md)
  * [Graph Regularized Non-negative Matrix Factorization for Data Representation](article-memo/matrix-factorization/graph-regularized-non-negative-matrix-factorization-for-data-representation.md)
  * [Alternating least squares for personalized ranking](article-memo/matrix-factorization/alternating-least-squares-for-personalized-ranking.md)
* [連続最適化](article-memo/continuous-optimization/README.md)
  * [Quasi-Newton Methods: Superlinear Convergence Without Line Searches for Self-Concordant Functions](article-memo/continuous-optimization/quasi-newton-methods-superlinear-convergence-without-line-searches-for-self-concordant-functions.md)
* [確率・統計](article-memo/probability-and-statistics/README.md)
  * [Statistical inference of Langevin  distributionfor directional data](article-memo/probability-and-statistics/statistical-inference-of-langevin-distributionfor-directional-data.md)
  * [Bayesian Inference over the Stiefel Manifold via the Givens Representation](article-memo/probability-and-statistics/bayesian-inference-over-the-stiefelmanifold-via-the-givens-representation.md)
* [Riemannian最適化](article-memo/riemannian-optimization/README.md)
  * [A Broyden Class of Quasi-Newton Methods for Riemannian Optimization](article-memo/riemannian-optimization/a-broyden-class-of-quasi-newton-methods-for-riemannian-optimization.md)
  * [Riemannian stochastic quasi-Newton algorithm with variance reduction and its convergence analysis](article-memo/riemannian-optimization/riemannian-stochastic-quasi-newton-algorithm-with-variance-reduction-and-its-convergence-analysis.md)
  * [Primal-Dual Optimization Algorithms over Riemannian Manifolds: an Iteration Complexity Analysis](article-memo/riemannian-optimization/primal-dual-optimization-algorithms-over-riemannian-manifolds-an-iteration-complexity-analysis.md)
  * [Extending FISTA to Riemannian Optimization for Sparse PCA](article-memo/riemannian-optimization/extending-fista-to-riemannian-optimization-for-sparse-pca.md)
* [RCD空間](article-memo/rcd-kong-jian/README.md)
  * [On the geometry of metric measure spaces. I](article-memo/rcd-kong-jian/on-the-geometry-of-metric-measure-spaces.-i.md)
  * [On the geometry of metric measure spaces. II](article-memo/rcd-kong-jian/on-the-geometry-of-metric-measure-spaces.-ii.md)
  * [Cohomology and other analyticalaspects of RCD spaces](article-memo/rcd-kong-jian/cohomology-and-other-analyticalaspects-of-rcd-spaces.md)
  * [Untitled](article-memo/rcd-kong-jian/untitled-1.md)

## 数学勉強ノート <a id="note"></a>

* [集合](note/sets.md)
* [ファジィ集合](note/fuzzy-sets.md)
* [ルベーグ積分](note/lebesgue.md)

## 数値解析 <a id="numerical-analysis"></a>

* [常微分方程式](numerical-analysis/ode.md)
* [偏微分方程式](numerical-analysis/pde.md)
* [固有値分解/特異値分解](numerical-analysis/evd-and-svd.md)

