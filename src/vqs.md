# Theory of Variational Quantum Simulator

original paper: [http://arxiv.org/abs/1812.08767](http://arxiv.org/abs/1812.08767)

## Abstract

- 変分法のまとめ

  - Dirac and Frenkel Variational principle
  - McLachlan's variational principle
  - time-dependent variational principle
    - 3 つの(Dirac and Frenkel, McLachlan, time-dependent)の変分原理が等価であることを見ていく
  - 純粋状態の unitary な時間発展だけでなく，混合状態の general な(散逸を含む)時間発展を導入する．

    - > We show how the results can be reduced to the pure state case with a correction term that takes accounts of global phase alignment
    - ^純粋状態に還元できるらしい，期待

## Background

- Hilbert space は広大なので古典コンピュータでは simulate できない．そこで，物理的な性質を考慮しつつ小さい subset を探索するのが変分法
- それにしても classical method(variational classical simulation)では多体系の entangle state が効率的に表現できないので解けない問題がいっぱいある．
- universal quantum computer だと simulate できる．ただ，universal なものは実装が難しい → VQS なら NISQ でもできるよ！
- 既存手法の問題点
  - 複数の variational principle があるのでどれを使うかによってパラメータの従う方程式が異なる
  - さらには今までは閉じた系の純粋状態しか扱ってこなかった
    - 現実の system は環境と相互作用がある開いた系
- **この論文では variational principle の equivalence と difference を議論して，VQS を混合状態の general な確率過程に拡張する**

## Real dynamics: three variational principles

time dependent Schrodinger's equation

$$
\frac{\partial\left|\psi\left(t\right)\right>}{\partial t} = -iH\left|\psi\left(t\right)\right>
$$

の時間発展を simulate するために試行関数$\left|\phi\left(\bm{\theta}\left(t\right))\right)\right>$を用いることを考える．ここで parameter は実であるとする．これは実数のパラメータで任意の試行関数を unitary gate と使って用意することができるからである．

時刻$t$における試行関数が$\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>$と表されるとする．この時，$t+\delta t$における試行関数をどう求めればいいか？単純に考えると (時間に依存しない Hamiltonian の場合)Schrodinger 方程式から，

$$
\left|\phi\left(\bm{\theta}\left(t+\delta t\right)\right)\right> = \left(1-i\delta tH\right)\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>
$$

が得られる．ただ，これは試行関数では表現できない．

> may be impossible to be represented by the trial state with any parameters

^の理由がよくわかっていない．
とりあえず，$\left|\phi\left(\bm{\theta}\left(t+\delta t\right)\right)\right>$を試行関数多様体に射影したい．
ここで variational principles を紹介
簡単にまとめると

1. The Dirac and Frenkel variational principle は試行関数に対する Schrodinger 方程式を試行関数の接ベクトル空間へ射影すると得られる．ただしこれはパラメータが複素数になり得るので unitary gate で扱いづらい
2. Mclachlan's variational principle は**試行関数の時間微分**と**試行関数に$-iH$を作用させたもの**の距離を最小化させるようにパラメータを動かすことを考える．そうすると，Dirac and Frenkel と同じような方程式系が得られるが，この場合にはパラメータが実になるので unitary gate で扱いやすい．
3. time-dependent variational principle は Schrodinger 方程式を与える Lagrangian の状態$\left|\psi\left(t\right)\right>$試行関数$\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>$によって置き換えて Euler-Lagrangian 方程式を求めると，パラメータが満たすべき方程式が得られる．この場合もパラメータが実になる．

### 1. The Dirac and Frenkel variational principle

試行関数を Schrodinger 方程式に代入すると

$$
\sum_{j}\frac{\partial \left|\phi\left(\bm{\theta}\left(t\right)\right)\right>}{\partial \theta_j}\dot{\theta}_j = -iH\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>
$$

左辺は試行関数多様体の接ベクトル空間に属する．試行関数を接ベクトル空間に射影することを考える．そのためには射影子として

$$
P = \sum_{i}\frac{\partial \left|\phi\left(\bm{\theta}\left(t\right)\right)\right>}{\partial \theta_i} \frac{\partial \left<\phi\left(\bm{\theta}\left(t\right)\right)\right|}{\partial \theta_i}
$$

を両辺に左から作用させて

$$
\sum_{i}\frac{\partial \left|\phi\left(\bm{\theta}\left(t\right)\right)\right>}{\partial \theta_i} \frac{\partial \left<\phi\left(\bm{\theta}\left(t\right)\right)\right|}{\partial \theta_i}\sum_{j} \frac{\partial \left|\phi\left(\bm{\theta}\left(t\right)\right)\right>}{\partial \theta_j} \dot{\theta}_j= -i \sum_{i}\frac{\partial \left|\phi\left(\bm{\theta}\left(t\right)\right)\right>}{\partial \theta_i} \frac{\partial \left<\phi\left(\bm{\theta}\left(t\right)\right)\right|}{\partial \theta_i}H\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>
$$

両辺の$\frac{\partial\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>}{\partial \theta_i}$ の係数を比較すると

$$
\frac{\partial \left<\phi\left(\bm{\theta}\left(t\right)\right)\right|}{\partial \theta_i}\sum_{j} \frac{\partial \left|\phi\left(\bm{\theta}\left(t\right)\right)\right>}{\partial \theta_j}\dot{\theta}_j = -i \frac{\partial \left<\phi\left(\bm{\theta}\left(t\right)\right)\right|}{\partial \theta_i}H\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>
$$

行列要素として

$$
\begin{array}{rl}
A_{ij} &=& \sum_{j}\frac{\partial \left<\phi\left(\bm{\theta}\left(t\right)\right)\right|}{\partial \theta_i} \frac{\partial \left|\phi\left(\bm{\theta}\left(t\right)\right)\right>}{\partial \theta_j} \\
C_i &=& \frac{\partial \left<\phi\left(\bm{\theta}\left(t\right)\right)\right|}{\partial \theta_i}H\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>
\end{array}
$$

と定義すると

$$
\sum_{j} A_{ij}\dot{\theta}_j = -i C_i
$$

となる．

一般に$A_{ij}, C_i$は複素数になる．実はこれが厄介で，Quantum simulation ではパラメータが実数でないと仮設から逸脱してしまう(そもそも試行関数を設定する際に，パラメータは実であると仮定していた．パラメータが実でないと unitary gate の用意が大変？)．なので，Dirac and Frenkel variational principle は今回の場合使いづらい．

### 2. McLachlan's variational principle

試行関数の時間微分と，試行関数に Hamiltonian を作用させたもの(Schrodinger 方程式の右辺)の距離を最小化することを考える．

$$
\delta ||\left(\partial / \partial t\right) + iH \left|\phi\left(\bm{\theta}\left(t\right)\right)\right>|| = 0
$$

変形していくと(計算は省略する)

$$
\sum_{j}A_{ij}^R\dot{\theta}_j = C_i^I
$$

と，Dirac and Frenkel の場合と似た方程式系が得られる．ただし，ここで$A_{ij}^R, C_i^I$はそれぞれ，Dirac and Frenkel で得られた$A_{ij}, C_i$の実部と虚部である．
これでパラメータを実数で扱えるので嬉しい！が，気をつけておくことがあって，それは global 位相によっては物理は不変であるが，変分法においては global 位相が役割を持ってしまうことである．つまり，時間微分を取る際に，global 位相が時間変化すると，$\left|\psi\left(t\right)\right>$と$\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>$の時間微分が異なる．そのため(計算は省略するが)$A^R,C^I$に加えて，$\left<H^2\right> = \left<\phi\left(\bm{\theta}(t)\right)\right|H^2\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>$も測定すると，variational principle が首尾よく行えているか検証できる．

### 3. time-dependent variational principle

Lagrangian

$$
L = \left<\psi\left(t\right)\right|\left(\partial/\partial t + iH\right)\left|\psi\left(t\right)\right>
$$

は^の Schrodinger 方程式を与える．ここで$\left|\psi\left(t\right)\right>$を試行関数$\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>$で置き換えると

$$
L = \left<\phi\left(\bm{\theta}\left(t\right)\right)\right|\left(\partial/\partial t + iH\right)\left|\phi\left(\bm{\theta}\left(t\right)\right)\right>
$$

この Lagrangian に対して Euler Lagrange 方程式を求めると

$$
\sum_{j}A_{ij}^I \dot{\theta}_j = -C_i^R
$$

ただし，ここで$A_{ij}^I, C_i^R$はそれぞれ，Dirac and Frenkel で得られた$A_{ij}, C_i$の虚部と実部である．
