# Variational Method

## Rayleigh-Ritz method

波動関数$\psi$，Hamiltonian$H$として

$$
    H \psi = E \psi
$$

の固有状態を求めたい．簡単のため，有限次元の場合を考える．
まず，$\psi$をエネルギー固有状態$\{\psi_i\}$で展開する．ここで$\{i=1,2,\dots\}$はエネルギー固有状態のラベルである．このとき，Hamiltonian の期待値は

$$
    \begin{array}{rl}
        \left< H \right> &=& \sum_{ij}{c_i^* \psi_i^* H c_j \psi_j} \\
        &=& \sum_{i}{|c_i|^2 E_i} \\
        &\geq& E_0 \sum_{i}{|c_i|^2} \\
        &=& E_0\left<\psi|\psi\right>
    \end{array}
$$

ここで$E_0$は基底エネルギーである，よって

$$
E_0 \leq \frac{\left<\psi|H|\psi\right>}{\left<\psi|\psi\right>}
$$

を得る．

ここで，$\left|\psi\right>$をパラメータ${\bm{\alpha}}=\left(\alpha_0, \alpha_1, \dots, \alpha_n \right)^\mathrm{T}$で特徴づけられる試行関数$\left|\phi(\bm{\alpha})\right>=\left|\phi(\alpha_0, \alpha_1, \dots, \alpha_n)\right>$を用いて近似して，

$$
\frac{\left<\phi(\bm{\alpha})|H|\phi(\bm{\alpha})\right>}{\left<\phi(\bm{\alpha})|\phi(\bm{\alpha})\right>}
$$

を最小化するような$\bm{\alpha}$を求める．厳密な基底状態$\left|\psi_0\right>$は$(1)$の等号が成り立つ．良い試行関数を選べば選ぶほど$(1)$の右辺は小さくなり，厳密な基底エネルギーに近づく．ここで用いられるパラメータ$\bm{\alpha}$を変分パラメータという．

### 例題

一次元調和振動子

$$
H=-\frac{\hbar^2}{2m} \frac{\partial^2}{\partial x^2} + \frac{K}{2} x^2
$$

において変分法用いて基底エネルギーの近似解を求めよ．ここで $K$は定数である．
ただし，試行関数を$\phi=-Ce^{-\alpha x^2}$($C$は定数，$\alpha$は変分パラメータ)を用いよ．
