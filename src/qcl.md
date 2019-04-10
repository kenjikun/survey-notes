# Quantum Circuit Learning

original paper: [https://arxiv.org/abs/1803.00745](https://arxiv.org/abs/1803.00745)

## Background

- HHL によって行列の演算が Quantum でできるようになった．しかし，これは QPE の用に深い量子回路が必要になる．
- この論文では VQE のような Quantum-Classical の hybrid framework で機械学習をやる．

## Algorithm

1. input data $\left\{\bm{x}_i\right\}$をエンコードした量子状態$\left|\psi_\mathrm{in}\left(\bm{x}_i\right)\right>$を unitary gate $U\left(\bm{x}_i\right)$を初期状態$\left|0\right>$に適用してつくる．
2. output state $\left|\psi_\mathrm{out}\left(\bm{x}_i;\bm{\theta}\right)\right>$をパラメータ$\bm{\theta}$で特徴づけられた unitary gate $U\left(\theta\right)$を$\left|\psi_\mathrm{in}\left(\bm{x}_i\right)\right>$に適用してつくる．
3. output state から output data $y\left(\bm{x}_i;\theta\right)=F\left(\left\{\left<B_j\left(\bm{x}_i,\theta\right)\right\}\right>\right)$の期待値計算を$\left|\psi_\mathrm{out}\left(\bm{x}_i;\theta\right)\right>$を使って行う．ここで，$\left\{B_j\right\}$は Peauli 演算子からなる
4. $\theta$を動かして cost function$L\left(f\left(\bm{x}_i\right), y\left(\bm{x}_i;\theta\right)\right)$を最小化する．ここで$f\left(\bm{x}_i\right)$は教師ラベル

- VQE では Nelder-Mead 法を使っているが，一般にパラメータ空間が大きい場合には勾配を用いる最適化手法のほうが良い．
-

## Numerical Simulation
