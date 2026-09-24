# QET Core Selection - Problem Statement 1: Statevector Simulator

## Task

Implement a **statevector simulator** for an $n$-qubit quantum system using **NumPy only** (plus the Python standard library; no Qiskit or other quantum libraries).

Fill in the class template in [`statevector_simulator.py`](./statevector_simulator.py). Your simulator must support:

- **Single qubit gates:** X, H, Z
- **Two qubit gates:** CNOT, CZ
- **Bipartite entanglement entropy:** the von-Neumann entanglement entropy across the half bipartition of the system.
- **2 Qubit Grover Search**

### Grover's Search (Main Loop)

In addition to the class, implement the `grover_2qubit` function and the `if __name__ == "__main__":` block in [`statevector_simulator.py`](./statevector_simulator.py) so that running

```bash
uv run statevector_simulator.py
```

executes a **2-qubit Grover search** for a marked state. The oracle and the diffusion operator must be built only from the gates in your `StatevectorSimulator` class. Exactly one Grover iteration is optimal for $n = 2$, and the final statevector should have probability $\approx 1$ on the marked state.

## Rules

- Only **NumPy** is allowed (no Qiskit, PennyLane, etc.).
- Your simulator must work for **arbitrary $n$**.
- The statevector must remain normalized after every gate.

## Setting Up

### Repository

1. Clone this repository:

   ```bash
   git clone <repo-url>
   ```

2. Create a **private** repository of your own named `QET_{RollNo}_PROBLEM_{1/2}` depending on which problem statement you picked. For example, `QET_EP24BTECH11026_PROBLEM_1`.
   - [Creating a new repository (GitHub Docs)](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository)
   - [Setting repository visibility to private (GitHub Docs)](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility)

3. Share access to your private repository with one of the heads:
   - [Inviting collaborators to a personal repository (GitHub Docs)](https://docs.github.com/en/account-and-profile/how-tos/setting-up-and-managing-your-personal-account-on-github/managing-access-to-your-personal-repositories/inviting-collaborators-to-a-personal-repository)

### Commit Guidelines

- Commit early and often; your commit history is part of the evaluation.
- Write clear, descriptive commit messages (what changed and why).
- [How to write a good commit message](https://cbea.ms/git-commit/)
- [GitHub Git cheatsheet](https://training.github.com/downloads/github-git-cheat-sheet/)

### Environment

We require you to use **uv** for environment and dependency management. This repository already contains a `uv.lock`, so setup is:

1. Install uv: [uv installation](https://docs.astral.sh/uv/getting-started/installation/)
2. Create the environment and install dependencies:

   ```bash
   uv sync
   ```

3. Activate the virtual environment:

   ```bash
   source .venv/bin/activate
   ```

- [NumPy quickstart tutorial](https://numpy.org/doc/stable/user/quickstart.html)

## Learning Resources

### Quantum Computing Basics

- IBM Quantum lectures:
  - [Lecture 1](https://www.youtube.com/watch?v=3-c4xJa7Flk&list=PLOFEBzvs-VvqKKMXX4vbi4EB1uaErFMSO&index=3)
  - [Lecture 2](https://www.youtube.com/watch?v=DfZZS8Spe7U&list=PLOFEBzvs-VvqKKMXX4vbi4EB1uaErFMSO&index=4)
  - [Lecture 3](https://www.youtube.com/watch?v=30U2DTfIrOU&list=PLOFEBzvs-VvqKKMXX4vbi4EB1uaErFMSO&index=5)

### Entanglement Entropy

Split the $n$ qubits into part $A$ (the first $s = n/2$ qubits) and part $B$ (the rest). The statevector coefficients form a matrix $a$ of size $2^s \times 2^{n-s}$. Its singular value decomposition

$$a = U \Lambda V^\dagger, \quad \Lambda = \mathrm{diag}\{\lambda_1, \lambda_2, \ldots\}$$

gives the Schmidt decomposition of the state. The reduced density matrix of part $B$ is then diagonal in the Schmidt basis with eigenvalues $\lambda_\alpha^2$, and the entanglement entropy is

$$S(\hat{\rho}_B) = -\sum_\alpha \lambda_\alpha^2 \log\left(\lambda_\alpha^2\right)$$

Terms with $\lambda_\alpha = 0$ contribute 0.

- [Nielsen & Chuang, Ch. 2.5 (Schmidt decomposition) and Ch. 11 (entropy)](https://www.cambridge.org/highereducation/books/quantum-computation-and-quantum-information/01E10196D0A682A6AEFFEA52D53BE9AE)
- [Entanglement entropy (Wikipedia)](https://en.wikipedia.org/wiki/Entropy_of_entanglement)

## Submission

Push your completed solution to your private `QET_{RollNo}_PROBLEM_{1/2}` repository and make sure the head you were assigned has collaborator access before the deadline.
