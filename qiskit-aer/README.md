Qiskit-Aer
===========

Qiskit Aer is high-performance quantum computing simulators with realistic noise models. It provides interfaces to run quantum circuits with or without noise using multiple different simulation methods. Qiskit Aer supports leveraging MPI and running on GPUs to improve the performance of simulation.

# Installation Instructions

Follow the [Getting Started Guide](https://qiskit.org/ecosystem/aer/getting_started.html) from the official IBM Qiskit-Aer documentation.

You may use a package manager such as `python pip` or `conda`. However *bonus* points will be awarded for building [Qiskit-Aer from source](https://github.com/Qiskit/qiskit-aer/blob/main/CONTRIBUTING.md#install-from-source).

## Installing Qiskit-Aer from Source

`Qiskit-Aer` has a core dependency of `Qiskit`, which is [IBM SDK and Toolkit](https://www.ibm.com/quantum/qiskit) for programming and running experiments on quantum computers.

### Create and Activate a New Virtual Environment

Separate your python projects and ensure that they exist in their own, clean enviromnets:

```bash
$ python3 -m venv QiskitAer
  source QiskitDevenv/bin/activate
  ```
### Install a Rust Compiler

You're going to need a [Rust Compiler](https://forge.rust-lang.org/infra/other-installation-methods.html) installed on your system, in order to compile Qiskit:
```bash
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Build and Install Install Qiskit

```bash
$ git clone https://github.com/Qiskit/qiskit.git
$ cd qiskit
$ pip install -r requirements-dev.txt
$ pip install .
```

### Build and Install Qiskit-Aer

Within the same python virtual but under a different folder, follow the same instructions as you did for building and installing `Qikit`.

```bash
$ git clone https://github.com/Qiskit/qiskit-aer
```

Depending on your system, you may need to additionally add `PyBind11`, this can be added to the `requirements-dev.txt` file.

# Benchmark: Quantum Volume Experiment (Single Node) *[4%]*

*Quantum Volume (QV)** is a single-number metric that can be measured using a concrete protocol on near-term quantum computers of modest size. The QV method quantifies the largest random circuit of equal width and depth that the computer successfully implements. Quantum computing systems with high-fidelity operations, high connectivity, large calibrated gate sets, and circuit rewriting toolchains are expected to have higher quantum volumes. Simply put, Quantum Volume is a single number meant to encapsulate the performance of today’s quantum computers, like a classical computer’s transistor count.

For this benchmark, you'll be writing your own Python code, to conduct the (Quantum Volume Experiment)(https://qiskit.org/ecosystem/experiments/dev/manuals/verification/quantum_volume.html). Save the following in a Python script `qv_experiment.py`:

```python
from qiskit import *
from qiskit.circuit.library import *
from qiskit_aer import *
import time
import numpy as np
def quant_vol(qubits=15, depth=10):
  sim = AerSimulator(method='statevector', device='CPU')
  circuit = QuantumVolume(qubits, depth, seed=0)
  circuit.measure_all()
  circuit = transpile(circuit, sim)

  start = time.time()
  result = sim.run(circuit, shots=1, seed_simulator=12345).result()
  time_val = time.time() - start
  # Optionally return and print result for debugging
  # Bonus marks available for reading the simulation time directly from `result`
  return time_val
```

To run the QV experiment, you'll need to parameterize the following variables, in order to generate the QV circuits and run them on a backend and on an ideal simulator:
* `qubits`: number or list of physical qubits to be simulated for the experiment,
* `depth`: meaning the number of discrete time steps during which the circuit can run gates before the qubits decohere.

Append the following to your `qv_experiment.py` script:

```python
# number of qubits, for your system see how much higher that 30 your can go...
num_qubits = np.arrange(10, 30)
# QV Depth
qv_depth = 10
# Array for storing the output results
result_array = [[], []]

# iterate over qv depth and number of qubits
for i in num_qubits:
  result_array[i] = quant_vol(qubits=i, depth=qv_depth)
  # for debugging purposes you can optionally print the output
  print(i, result_array[i])

```
## Submission

Repeat the experiment with `20` and then `30` qubits. Submit you build script, you compilation output,

# Graph: Number of Qubits vs Simulation time to Solution *[2%]*

Plot a graph of your quantum volume experiment, with the following changes to your `qv_experiment.py`:
```python
import matplotlib.pyplot as plt
plt.xlabel('Number of qubits')
plt.ylabel('Time (sec)')
plt.plot(num_qubits, results_array)
plt.title('Quantum Volume Experiment with depth=' + str(qv_depth))
plt.savefig('qv_experiment.png')
```

# Benchmark: Quantum Volume Experiment (Multiple Nodes) *[4%]*

In order to run the benchmark across your cluster, you will need to configure **Qiskit-Aer** with **MPI** support. Parallelizing the simulation can extend the available memory allowing you to run the experiment with a larger number of quibits. Recompile your binary with *MPI* support:
```bash
$ $ python ./setup.py bdist_wheel -- -DAER_MPI=True
```

Repeat the experiment and determine the maximum number of qubits that you can simulate on your cluster.
