# Quantum simulator

- rigetti pyQuil
- Microsoft Q#
- qunaSys qulacs
  の 3 つを試してみる．

## インストール

- pyQuil
  - https://pyquil.readthedocs.io/en/latest/start.html
  - puQUil 以外にも qvm(virtual machine), quilc(complier)のインストールが必要
- Q#
  - https://docs.microsoft.com/en-us/quantum/install-guide/?view=qsharp-preview
  - Q#のインストールの前に .NET Core SDK(2.1 or later)が必要
- qulacs
  - https://github.com/qulacs/qulacs
  - pip install の際に gcc で compile している．mac だと gcc コマンドが clang を呼ぶようになっているのでエイリアスを変更しておく必要がある．

## multi qubit の並べ方

pyQuil は以下を参考にしている．
[SOMEONE SHOUTS, $\left|01000\right>$! WHO IS EXCITED?](https://arxiv.org/abs/1711.02086)

## pyQuil

- shell を 2 つ立ち上げて qvm と quilc を走らせておく
  `qvm -S`
  `quilc -S`
- デバッグ用に波動関数シミュレータが利用可能
  - $H \left|0\right>$に対して$0.707106812\left|0\right> +  0.707106812\left|1\right>$を出力できる．
- [grove](https://github.com/rigetti/grove)を使うといくつかの Quantum algorithms が利用可能

- 簡単な実装例 [pyquil.ipynb](https://github.com/kenjikun/survey-notes/blob/master/src/pyquil.ipynb)
