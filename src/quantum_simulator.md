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

## pyQuil

- shell を 2 つ立ち上げて qvm と quilc を走らせておく
  `qvm -S`
  `quilc -S`

- 簡単なプログラム

```python
from pyquil import Program, get_qc
from pyquil.gates import *
```

初期状態と測定

```python
# 1qbitのqvm立ち上げ
qc = get_qc('1q-qvm')
# Programインスタンス立ち上げ時には|0>が入っている．
p = Program()
# declareで結果を格納するメモリを確保する．roはreadoutの略
# 下の例では1bitの領域を確保している．
ro = p.declare('ro', 'BIT', 1)
# MEASUREによってro[0]にqubit 0の測定結果を格納
# 今は1qbitのsystemにおいて|0>方向で測定している．systemが大きくなったときにはindexの付け方に注意．
p += MEASURE(0, ro[0])

executable = qc.compile(p)
result = qc.run(executable)
print(result)
```

    [[0]]

Hadamard

```python
p = Program()
ro = p.declare('ro', 'BIT', 1)
# Hadamardを|0>に作用させる
p += H(0)
p += MEASURE(0, ro[0])
# Hadamardを作用させたことによって測定結果は確率的になるので1000回分やってみる
p.wrap_in_numshots_loop(1000)

executable = qc.compile(p)
result = qc.run(executable)
print(result.flatten().mean())
```

    0.507

Parametric なゲート

```python
import numpy as np
qubit = 0

p = Program()
ro = p.declare("ro", "BIT", 1)
theta_ref = p.declare("theta", "REAL")
p += RX(np.pi / 2, qubit)
p += RZ(theta_ref, qubit)
p += RX(-np.pi / 2, qubit)
p += MEASURE(qubit, ro[0])

executable = qc.compile(p)

parametric_measurements = []
for theta in np.linspace(0, 2 * np.pi, 200):
    # ここでパラメータを指定できる
    bitstrings = qc.run(executable, {'theta': [theta]})
    parametric_measurements.append(bitstrings[0][0])
print(parametric_measurements)
```

    [0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 1, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 0, 1, 0, 1, 0, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
