# Jordan Wigner Transformation

参考: https://whyitsso.net/physics/quantum_mechanics/Jordan_Wigner.html
n 個の fermion 粒子系を n 個の 1/2 スピン系にマッピングすることを考える．
i でラベル付けられる準位に粒子を一個生成/消滅するのは生成消滅演算子を用いて

$$
a_i^\dag\left|0\right>=\left|1_i\right> \\
a_i\left|1\right>=\left|0_i\right>
$$

と表せる．
一方，i 番目のスピンの昇降演算子は

$$
s_{i,+}\left|\downarrow_i\right> = \left|\uparrow_i\right>\\
s_{i,-}\left|\uparrow_i\right> = \left|\downarrow_i\right>
$$

単純には$\left|\downarrow_i\right>$と$\left|0_i\right>$を，$\left|\uparrow_i\right>$と$\left|1_i\right>$を対応させれば良さそうに思えるが，多粒子系では生成消滅演算子とスピン昇降演算子の反交換関係が一部異なる．実際，

$$
[s_{i,-}, s_{j,+}]_+ = 2s_{i,-}s_{j,+}
$$

$$
[a_i,a_j^{\dag}]_+ = 0
$$

となっている．これは昇降演算子は交換するのに対し，生成消滅演算子は反交換するためである．ではどうするか？まずは生成消滅演算子が多粒子系の状態にどのように作用するかを確認する．$n$準位系で$i$番目の準位が空であり，ほかが$f_i = \{0,1\}$である状態

$$
\left|1_1,1_2,\dots,1_{i-1},0_i,1_{i+1}\dots1_n\right> = \left(a_n^\dag\right)^{f_{n-1}} \left(a_{n-1}^\dag\right)^{f_{n-1}}\dots \left(a_{i+1}^\dag\right)^{f_{i+1}} \left(a_{i-1}^{\dag}\right)^{f_{i-1}}\dots \left(a_1^{\dag}\right)^{f_1}\left|0\right>
$$

に対して$a_i^\dag$を作用させると

$$
\begin{array}{rl}
a_i^\dag\left|f_1,f_2,\dots,f_{i-1},0_i,f_{i+1}\dots1_n\right> &=& a_i^\dag \left(a_n^\dag\right)^{f_{n-1}} \left(a_{n-1}^\dag\right)^{f_{n-1}}\dots \left(a_{i+1}^\dag\right)^{f_{i+1}} \left(a_{i-1}^{\dag}\right)^{f_{i-1}}\dots \left(a_1^{\dag}\right)^{f_1}\left|0\right> \\
&=& (-1)^{f_n+f_{n-1}+\dots+f_{i+1}}\left(a_n^\dag\right)^{f_{n-1}} \left(a_{n-1}^\dag\right)^{f_{n-1}}\dots \left(a_{i+1}^\dag\right)^{f_{i+1}} \left(a_{i-1}^{\dag}\right)^{f_{i-1}}\dots \left(a_1^{\dag}\right)^{f_1}\left|0\right>\\
&=& (-1)^{f_n+f_{n-1}+\dots+f_{i+1}}\left|f_1,f_2,\dots,f_{i+1}, 1, f_{i-1}, \dots, f_n\right>
\end{array}
$$

と$(-1)^{f_n+f_{n-1}+\dots+f_{i+1}}$が出てくる．一方でスピン昇降演算子に関しては，$\sigma_i=\left\{ \right\}$ $\left|0\right>$をスピンがすべて下向きの状態として

$$
\begin{array}{rl}
    s_{i,+}\left|\sigma_1, \sigma_2, \dots \sigma_{i-1}, \downarrow_i, \sigma_{i+1}, \dots, \sigma_n \right> &=& s_{i,+} \left(s_{1,+}\right)^{\sigma_1} \left(s_{2,+}\right)^{\sigma_2}\dots \left(s_{i-1,+}\right)^{\sigma_{i-1}} \left(s_{i+1,+}\right)^{\sigma_{i+1}}\dots\left(s_{n,+}\right)^{\sigma_{n}}\left|0\right> \\
    &=&  \left(s_{1,+}\right)^{\sigma_1} \left(s_{2,+}\right)^{\sigma_2}\dots \left(s_{i-1,+}\right)^{\sigma_{i-1}} s_{i,+} \left(s_{i+1,+}\right)^{\sigma_{i+1}}\dots\left(s_{n,+}\right)^{\sigma_{n}}\left|0\right> \\
    &=& \left|\sigma_1, \sigma_2, \dots \sigma_{i-1}, \uparrow_i, \sigma_{i+1}, \dots, \sigma_n \right>
\end{array}
$$

と符号は反転しない．スピン状態から符号を取り出す演算子としては$\sigma_{i,z}\left|\sigma_i\right>=\sigma_i\left|\sigma_i\right>$がある．そのため$a_i^\dag=(-1)^{n-(i+1)+1}{\sigma_{n,z}\sigma_{n-1,z}\dots\sigma_{i+1,z}}s_{i,+}$という変換を考えるとうまくいきそうだとわかる．
この変換を Jordan Wigner 変換という．改めて書くと

$$
\begin{array}{ll}
a_i^\dag&=&(-1)^{n-i}{\sigma_{n,z}\sigma_{n-1,z}\dots\sigma_{i+1,z}}s_{i,+}\\
a_i&=&(-1)^{n-i}{\sigma_{n,z}\sigma_{n-1,z}\dots\sigma_{i+1,z}}s_{i,-}\\
\end{array}
$$

計算は省略するが，これらが fermion の反交換関係を満たしていることは容易に確認できる．
逆変換も考えることができる．$s_{i,z}$は$s_{i,z}=s_+s_--1/2=a_i^\dag a_i-1/2$と簡単に導ける．
$s_x$は

$$
\frac{c_i^\dag+c_i}{2} = (-1)^{n-i}{\sigma_{z,n}\sigma_{z,n-1}\dots\sigma_{z,i+1}}s_{i,x}
$$

と

$$
\sigma_{i,z}=2s_{i,z}=2a_i^\dag a_i-1
$$

となることを使うと

$$
\begin{array}{rl}
    s_{i,x}&=&(-1)^{n-i}(2a_n^\dag a_n-1)(2a_{n-1}^\dag a_{n-1}-1)\dots(2a_1^\dag a_1-1)\frac{c_i^\dag+c_i}{2}\\
    &=& (1-2a_n^\dag a_n)(1-2a_{n-1}^\dag a_{n-1})\dots(1-2a_1^\dag a_1)\frac{c_i^\dag+c_i}{2}
\end{array}
$$

となることがわかる．同様にして$s_{i,y}$は

$$
s_{i,y} = (1-2a_n^\dag a_n)(1-2a_{n-1}^\dag a_{n-1})\dots(1-2a_1^\dag a_1)\frac{c_i^\dag-c_i}{2i}
$$

逆変換をまとめると

$$
\begin{array}{rl}
    s_{i,x}&=&(1-2a_n^\dag a_n)(1-2a_{n-1}^\dag a_{n-1})\dots(1-2a_1^\dag a_1)\frac{c_i^\dag+c_i}{2}\\
    s_{i,y}&=&(1-2a_n^\dag a_n)(1-2a_{n-1}^\dag a_{n-1})\dots(1-2a_1^\dag a_1)\frac{c_i^\dag-c_i}{2i}\\
    s_{i,z}&=&a_i^\dag a_i-\frac{1}{2}
\end{array}
$$

となる．
