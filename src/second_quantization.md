# Second Quantization

## Motivation

- 量子力学では**互いに区別できない粒子**が現れる．粒子が互いに区別できないので，多体系の量子論を考えるときには**どの粒子がどこにある**と考えることは意味をなさなくなる．そこで，**どの状態がいくつの粒子に占有されているか**を考えるほうが自然である．
- 多体系では第二量子化しかできない，というわけではなく第二量子化の方が記述が簡単かつスピン等の自由度を自然に導入できる，という利点がある．

## 多体自由粒子系の第一量子化

N 個の**古典**自由粒子系の Hamiltonian は

$$
H = \sum_{j}{\frac{\bm{p}_j^2}{2m}}+V\left(\bm{r}_1,\dots,\bm{r}_N\right)
$$

と表せられる．自由粒子では

$$
V\left(\bm{r}_1,\dots,\bm{r}_N\right) = \sum_{j}{v(\bm{r}_j)}
$$

と書ける．$v(\bm{r})$は potential energy を表す．
第一量子化は$\bm{p}_j \rightarrow -i\hbar\nabla$と置き換えることに対応するので第一量子化された Hamiltonian は

$$
H = \sum_{j}\left\{-\frac{\hbar^2}{2m}\nabla^2+v\left(\bm{r}_j\right)\right\}
$$

定常状態を考える．N 粒子系の固有状態を$\psi(\bm{r}_1,...,\bm{r}_N)$と書くと

$$
H \psi(\bm{r}_1,\dots,\bm{r}_N) = E \psi(\bm{r}_1,\dots,\bm{r}_N)
$$

この方程式は偏微分方程式であり，変数分離によって

$$
\psi_{k_1,k_2,\dots,k_N}(\bm{r}_1,\dots,\bm{r}_N) = \psi_{k_1}(\bm{r}_1)\psi_{k_2}(\bm{r}_2)\dots\psi_{k_N}(\bm{r}_N)
$$

が解となっている．ここで，$\psi_{k_i}(i=1,\dots,N)$は 1 粒子系の波動関数である．
この時，エネルギーは

$$
E_{k_1,k_2,\dots,k_N} = \epsilon_{k_1} + \epsilon_{k_2} + \dots + \epsilon_{k_N}
$$

となる．
$k_i$というラベルは$i$番目の粒子が状態$k_i$をとっており，その時のエネルギーが$\epsilon_{k_i}$である，と読む．そうすると$\{k_i\}$の入れ替えに対してエネルギーが変化しないが，状態は変化するという事がわかる．

## 粒子の入れ替えに関する対称性

N 個の自由粒子系の Hamiltonian は明らかに粒子の入れ替えに対して不変である．すると$i$番目と$j$番目の粒子の入れ替え操作を$P_{ij}(i,j=1,2,\dots,N)$と表して

$$
[H, P_{ij}] = 0
$$

となり，Hamiltonian の固有状態は同時に$P_{ij}$の固有状態であることがわかる．$P_{ij}$の固有値は

$$
\begin{array}{rl}
    P_{ij}\psi(\dots,\bm{r}_i,\dots,\bm{r}_j,\dots) &=& \psi(\dots,\bm{r}_i,\dots,\bm{r}_j,\dots) \\
    &=& p_{ij}\psi(\dots,\bm{r}_j,\dots,\bm{r}_i,\dots)
\end{array}
$$

となる．ここで二度の入れ替えによって状態はもとに戻るので

$$
\begin{array}{rl}
    P_{ij}^2\psi(\dots,\bm{r}_i,\dots,\bm{r}_j,\dots)
    &=& p_{ij}^2\psi(\dots,\bm{r}_j,\dots,\bm{r}_i,\dots)\\
    &=& \psi(\dots,\bm{r}_i,\dots,\bm{r}_j,\dots) \\
\end{array}
$$

ゆえに$p_{ij}^2=1$が得られる．$p_{ij}=1$を Bose 粒子系，$p_{ij}=-1$を Fermi 粒子系と呼ぶ．Fermi 粒子系では粒子の入れ替えに関して状態の符号が反転する．もし，同じ一粒子固有状態に 2 つの粒子が存在すると，粒子の入れ替えに関して符号が反転しない．そのため，Fermi 粒子系においては 2 つの粒子が同じ状態になることはできない．

上で求めた状態はこの対称性，反対称性を満たしていないので，縮退した状態の線形結合によりこれらの対称性を満たす状態を作る．すると

$$
\begin{array}{rl}
    \psi_{\mathrm{Bose}}&=&\psi_{k_1}(\bm{r}_1)\psi_{k_2}(\bm{r}_2)\dots\\
    &+& \psi_{k_2}(\bm{r}_2)\psi_{k_1}(\bm{r}_1)\dots\\
    &=& \sum_{P(\{k_i\})}{\psi_{k_1}(\bm{r}_1)\psi_{k_2}(\bm{r}_2)\dots\psi(\bm{k_N})}
\end{array}
$$

$$
\begin{array}{rl}
    \psi_{\mathrm{Fermi}}&=&\psi_{k_1}(\bm{r}_1)\psi_{k_2}(\bm{r}_2)\dots\\
    &-& \psi_{k_2}(\bm{r}_2)\psi_{k_1}(\bm{r}_1)\dots\\
    &=& \sum_{P(\{k_i\})}{(-1)^P\psi_{k_1}(\bm{r}_1)\psi_{k_2}(\bm{r}_2)\dots\psi(\bm{k_N})}
\end{array}
$$

が得られる．ここで$P({\{k_i\}})$は$\{k_i\}$のすべての可能な置換を表す．この解は$\{k_i\}$の入れ替えに関してエネルギーも状態も変わらない

## 第二量子化

上で得られた(反)対称化された固有状態では$k_1, k_2, \dots, k_N$の順序は意味をなさなくなっている．そこで，

**各粒子が占める一粒子状態を指定することによって状態を定める**
から
**各一粒子状態にある粒子の数を指定することによって状態を定める**
へ移行する．
ここで一粒子状態の重複度を**占有数**と呼ぶ．

一粒子固有状態に$i=1,2,\dots$と名前をつけ直す(一般に状態空間は無限次元となる)．そして，$i$番目の状態を占める粒子の数を$n_i$とする(これが占有数)と，占有数表示での状態$\left|n_1, n_2, \dots\right>$を定義できる．これは Fock 状態と呼ばれる．

こうすると，粒子を一つ付け加える/取り除く演算を考えると都合がよい．それらを$\hat{a}_k^\dag, \hat{a}_k$と表し，状態$k$の生成/消滅演算子と呼ぶ．天下り的ではあるが，生成消滅演算子に関する性質をまず規定する．また，それらを用いて 固有状態や Hamiltonian がどう表せられるかを確認する．

### 生成消滅演算子の性質

**Bose 粒子の場合は交換関係を考え，Fermi 粒子の場合は反交換関係を考えることに注意する．**

- $\hat{a}_k^\dag, \hat{a}_k$の交換関係$[A,B]_-=AB-BA$，反交換関係$[A,B]_+=AB+BA$に対して
  - $[\hat{a}^\dag_k, \hat{a}_{k'}^\dag]_\mp=0$
  - $[\hat{a}_k, \hat{a}_{k'}]_\mp=0$
  - $[\hat{a}_k, \hat{a}_{k'}^\dag]_\mp=\delta_{k,k'}$
- 真空$\left|0\right>$に対して消滅演算は$\hat{a}_k\left|0\right>=0$
- N 粒子状態は$\left|n_1, n_2, \dots\right>=\prod_{k}{\frac{1}{\sqrt{n_k!}}\left(a_k^\dag\right)^{n_k}\left|0\right>}$と表せる．
- Hamiltonian は$\hat{n}_k = \hat{a}_k^\dag\hat{a}_k$を用いて$H=\sum_{k}{\epsilon_k \hat{n}_k}$と表せる．

**生成消滅演算子による表示に移行することを第二量子化という**

### 場の演算子

場の演算子を

$$
\hat{\psi}^\dag(\bm{r}) = \sum_{k}{\phi_k^*(\bm{r}) \hat{a}_k^\dag}
$$

と定義する．このとき，直交性を用いると

$$
    \hat{a}_k^\dag = \int{d\bm{r}\phi_k(\bm{r})}\hat{\psi}^\dag(\bm{r})
$$

と表せるから，Hamiltonian は

$$
\begin{array}{rl}
    H &=& \sum_{k}\epsilon_k\int{d\bm{r} d\bm{r}' \phi_k(\bm{r}) \phi_k^*(\bm{r}') \hat{\psi}^\dag(\bm{r})\hat{\psi}(\bm{r}')}\\
    &=& \int{d\bm{r}\hat{\psi}^\dag(\bm{r})\sum_{k}\phi_k^*(\bm{r})\hat{h}(\bm{r})\phi_k(\bm{r})\hat{\psi}(\bm{r})} \\
    &=& \int{d\bm{r}\hat{\psi}^\dag(\bm{r})\left(-\frac{\hbar^2}{2m}\nabla^2+v(\bm{r})\right)\hat{\psi}(\bm{r})}
\end{array}
$$

となる．ここで一粒子 Hamiltonian $h(\bm{r})=-\frac{\hbar^2}{2m}\nabla^2+v(\bm{r})$が

$$
h(\bm{r})\phi_k(\bm{r}) = \epsilon_k \phi_k(\bm{r})
$$

を満たすことを使った．

これにより，場の演算子を用いて Hamiltonian を表すことができた．場の演算子による Hamiltonian の表示は第一量子化のエネルギーの期待値計算を波動関数の代わりに演算子を用いて表示した形をしている．

## 相互作用がある場合

上記では相互作用がない場合，つまり自由粒子の場合を考えてきた．ここでは相互作用がある Hamiltonian に対して第二量子化を行った場合にどうなるかを見る．

第一量子化での一粒子演算子$F$と二粒子演算子(二体相互作用)$G$は

$$
F = \sum_{i=1}^{N}{f(\bm{r}_i)}
$$

$$
G = \frac{1}{2}\sum_{i\neq j}{g(\bm{r}_i, \bm{r}_j)}
$$

と書ける．

$$
    \hat{F} = \int{d\bm{r}\hat{\psi}^\dag(\bm{r})f(\bm{r})}\hat{\psi}(\bm{r})
$$

の行列要素$\left<\alpha\right|\hat{F}\left|\beta\right>$を計算すると一粒子演算子$F$には$\hat{F}$を対応させればいいことがわかる(計算は省略)

同様に

$$
    \hat{G} = \frac{1}{2}\int{d\bm{r}d\bm{r}'\hat{\psi}^\dag(\bm{r})\hat{\psi}^\dag(\bm{r}')g(\bm{r}, \bm{r}')}\hat{\psi}(\bm{r})\hat{\psi}(\bm{r}')
$$

の行列要素$\left<\alpha\right|\hat{G}\left|\beta\right>$を計算すると一粒子演算子$G$には$\hat{G}$を対応させればいいことがわかる(計算は省略)
