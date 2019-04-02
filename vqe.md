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
  - こっちで解説: [QPE]()
  - 実用のためには"millions or billions quantum gates"が必要
  - quantum gate を作用させる間 coherence を維持しなければならない
    - これが非常に難しい

## Method

-

## Conclusion

## Discussion
