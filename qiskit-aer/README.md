Qiskit-Aer
===========

Qiskit Aer is high-performance quantum computing simulators with realistic noise models. It provides interfaces to run quantum circuits with or without noise using multiple different simulation methods. Qiskit Aer supports leveraging MPI and running on GPUs to improve the performance of simulation.

# Installation Instructions

Follow the [Getting Started Guide](https://qiskit.org/ecosystem/aer/getting_started.html) from the official IBM Qiskit-Aer documentation.

You may use a package manager such as `python pip` or `conda`. However *bonus* points will be awarded for building Qiskit-Aer from source.

## Installing Qiskit-Aer from Source

`Qiskit-Aer` has a core dependency of `Qiskit`, which is [IBM SDK and Toolkit](https://www.ibm.com/quantum/qiskit) for programming and running experiments on quantum computers.

### Create and Activate a New Virtual Environment

Separate your python projects and ensure that they exist in their own, clean enviromnets:

```bash
python3 -m venv QiskitAer
  source QiskitDevenv/bin/activate
  ```
### Install a Rust Compiler

You're going to need a [Rust Compiler](https://forge.rust-lang.org/infra/other-installation-methods.html) installed on your system, in order to compile Qiskit:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Install Qiskit
