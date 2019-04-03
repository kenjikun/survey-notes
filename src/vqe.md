# Variational Quantum Eigen Solver

original paper: [https://arxiv.org/pdf/1304.3061.pdf](https://arxiv.org/pdf/1304.3061.pdf)

## Abstract

- 指数関数的に状態空間が増える量子力学の固有値問題
- 量子位相推定は効率的に固有状態の探索を行えるが，コヒーレンスを維持しなければならない
  - ノイズの多い系ではコヒーレンス維持が非常に困難
- 仮設(ansatz)と古典計算機による最適化を併せれば，コヒーレンス維持の問題を回避可能

## Background

- 量子化学計算では Schrodinger 方程式を解けば(固有状態を求めれば)，原子や分子の性質がわかる．その物質の化学がわかる．
  - まともにやると高次元過ぎて無理
  - 例えば，L 個の電子軌道があって，n 個電子がある場合 [引用元](https://www.slideshare.net/NakataMaho/ss-117321322)
    - 波動関数の空間の次元は${}_L\mathrm{C}_n$
    - Hamiltonian の大きさは${}_L\mathrm{C}_n\times{}_L\mathrm{C}_n$
    - $L=20, n=10$
      - ${}_L\mathrm{C}_n \approx 1.8 \times 10^5, {}_L\mathrm{C}_n\times{}_L\mathrm{C}_n\approx3.4 \times 10^{10}$
    - Benzene$\left(\mathrm{C}_6\mathrm{H}_6\right)$でさえ$L=72, n=42$
  - メモリに乗らない
- 近似方法はいろいろあるが，できる限り厳密解に近いものがほしい
- 量子化学計算以外でも大規模な固有値問題はある．
  - 検索とか，創薬とか
- 量子計算で大規模固有値問題をやるときは量子位相推定という方法がある．
  - こっちで解説: [QPE](https://github.com/kenjikun/survey-notes/blob/master/qpe.md)
  - 実用のためには"millions or billions quantum gates"が必要
  - quantum gate を作用させる間 coherence を維持しなければならない
    - これが非常に難しい

## Method

### Algorithm1(QPU)

- Classical Processing Unit(CPU) と Quantum Processing Unit(QPU)を組み合わせることで指数高速化が可能
- 変分法で固有状態を求める．[変分法](https://github.com/kenjikun/survey-notes/blob/master/variational_method.md)
- QPU 上で Hamiltonian の期待値の計算を行い，CPU 上で最適化問題を解く．
- QPU 上での量子期待値計算
  - 任意の Hamiltonian を
    $$
    H = \sum_{i\alpha}{h_\alpha^i \sigma_\alpha^i} + \sum_{ij\alpha\beta}{h_{\alpha\beta}^{ij}\sigma_\alpha^i\sigma_\beta^j + \dots}
    $$
    と展開する．ここで$h$は実数，roman indices は演算子が作用する部分空間を指定，greek indices は Pauli operator を指定．
  - Hamiltonian の期待値は，期待値の線形性より
    $$
    \left<H\right> = \sum_{i\alpha}{h_\alpha^i \left<\sigma_\alpha^i\right>} + \sum_{ij\alpha\beta}{h_{\alpha\beta}^{ij}\left<\sigma_\alpha^i\sigma_\beta^j\right> + \dots}
    $$
  - Hamiltonian に現れる項の数がシステムのサイズに対して多項式であれば，Hamiltonian の期待値を取るのに必要な計算回数はシステムのサイズに対して多項式
  - このような展開は可能なのか？
    - 第二量子化した Hamiltonian の生成消滅演算子を Jordan-Wigner 変換により量子ゲート演算子にマッピングする
      - [第二量子化](https://github.com/kenjikun/survey-notes/blob/master/second_quantization.md)した Hamiltonian
      $$
      H = \sum_{pq}{h_{pq}\hat{a}_{p}^{\dagger}\hat{a}_{q}}+\sum_{pqrs}{h_{pqrs}\hat{a}_{p}^{\dagger}\hat{a}_{q}^{\dagger}\hat{a}_{r}\hat{a}_{s}}+\dots
      $$
      $h$は相互作用係数，$\dots$以降は 3 体以上の相互作用項
      - [Jordan Wigner transformation](https://github.com/kenjikun/survey-notes/blob/master/jordan_wigner_transformation.md)

### Algorithm2(CPU)

- QPU を使って Hamiltonian の期待値を求めるために，基底状態の波動関数をよく近似する必要がある → [Rayleigh-Ritz](https://github.com/kenjikun/survey-notes/blob/master/variational_method.md)
- 波動関数が多項式の数のパラメータで特徴づけられれば，多項式次元の空間を探索すればいい

## Discussion

- ゲート数は少なくてすむ
- ansatz は興味のある system の知識に基づいて選ぶ必要がある
  - 量子化学計算等ではそういった ansatz はあるみたいだが，他の問題をマップした場合にどうなるか
