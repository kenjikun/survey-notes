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

- Classical Processing Unit(CPU) と Quantum Processing Unit(QPU)を組み合わせることで指数高速化が可能
- 変分法で固有状態を求める．[変分法](variational_method.md)
- QPU 上で Hamiltonian の期待値の計算を行い，CPU 上で最適化問題を解く．

### Algorithm1(QPU)

- QPU 上での量子期待値計算

  - 任意の Hamiltonian を
    $$
    H = \sum_{i\alpha}{h_\alpha^i \sigma_\alpha^i} + \sum_{ij\alpha\beta}h_{\alpha\beta}^{ij}\sigma_\alpha^i\sigma_\beta^j + \dots \tag{1}
    $$
    と展開する．ここで$h$は実数，roman indices は演算子が作用する部分空間を指定，greek indices は Pauli operator を指定．
  - Hamiltonian の期待値は，期待値の線形性より
    $$
    \left<H\right> = \sum_{i\alpha}{h_\alpha^i \left<\sigma_\alpha^i\right>} + \sum_{ij\alpha\beta}{h_{\alpha\beta}^{ij}\left<\sigma_\alpha^i\sigma_\beta^j\right> + \dots}
    $$
  - Hamiltonian に現れる項の数がシステムのサイズに対して多項式であれば，Hamiltonian の期待値を取るのに必要な計算回数はシステムのサイズに対して多項式
  - このような展開は可能なのか？

    - 第二量子化した Hamiltonian の生成消滅演算子を Jordan-Wigner 変換により量子ゲート演算子(Pauli 演算子)にマッピングする

      - ここでは，量子化学計算を考える．Born Oppenheimer 近似を行い，[第二量子化](https://github.com/kenjikun/survey-notes/blob/master/second_quantization.md)した Hamiltonian は

      $$
      H = \sum_{pq}{h_{pq}\hat{a}_{p}^{\dagger}\hat{a}_{q}}+\sum_{pqrs}{h_{pqrs}\hat{a}_{p}^{\dagger}\hat{a}_{q}^{\dagger}\hat{a}_{r}\hat{a}_{s}}
      $$

      となる．$h_{pq}, h_{pqrs}$は定数となる．この Hamiltonian はどの準位にいくつ粒子があるか？で状態を記述している(数表示)．実際の量子化学系では軌道の数は無限大であるため，Hamiltonian の次元数は無限大になる．ただし，興味のある軌道はせいぜい数軌道〜数十軌道程度なのでそこで軌道を打ち切り，有限自由度系として扱う．([第二量子化](https://github.com/kenjikun/survey-notes/blob/master/second_quantization.md)を参照)

      - [Jordan Wigner transformation](https://github.com/kenjikun/survey-notes/blob/master/jordan_wigner_transformation.md)

      $$
      \begin{array}{rl}
        \hat{a}_j &\rightarrow& I^{\bigotimes j-1}\bigotimes \sigma_+ \bigotimes \sigma_z^{\bigotimes N-j} \\
        \hat{a}_j^\dag &\rightarrow& I^{\bigotimes j-1}\bigotimes \sigma_- \bigotimes \sigma_z^{\bigotimes N-j} \tag{1}
      \end{array}
      $$

      により，$N$準位の Fermion 系を$N$個のスピン$1/2$系で記述することができる．これを用いると$(1)$が得られる．

### Algorithm2(CPU)

- パラメータを変化させてエネルギーが最小になるように仕向ける．ここに関しては classical な最適化手法を使えばいい．
  - この論文では Nelder-Mead method を用いている．導関数が不要
  - 単純な最急降下法だと導関数が必要
- 波動関数が多項式の数のパラメータで特徴づけられれば，多項式次元の空間を探索すればいいので，そういったタイプの試行関数を利用する．
- この論文では"unitary coupled cluster ansatz"[1]を用いている．これの詳細よくわからない...量子化学計算界隈ではよく使われる？
  $$
  \left|\Psi\right> = e^{T-T^{\dag}} \left| \Phi \right>_{\mathrm{ref}}
  $$
  - $\left|\Phi\right>_{\mathrm{ref}}$は Hartree Fock の時の ground state を用いる．
    - Hartree Fock で近似すると ground state は古典でも効率よく求められるそこに電子相関を考慮した分が乗るようにしていると考えられる．
  - unitary coupled cluster ansatz は古典で効率よく計算できる方法は知られていない．

## Discussion

- ゲート数は少なくてすむ
- コヒーレンスを維持するのは Hamiltonian の期待値計算の間だけ
- ansatz は興味のある system の知識に基づいて選ぶ必要がある
  - 量子化学計算等ではそういった ansatz はあるみたい(unitary coupled cluster ansatz)だが，他の問題をマップした場合にどうなるか
  - ある程度厳密解なり近似解がすでに効率よく求められるモデルから出発して多体効果をパラメータ化して取り入れるのが正攻法な気がする．

[1]: https://doi.org/10.1002/qua.21198
