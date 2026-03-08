# Entanglement Swapping Across Architectures

Minimal cross-architecture entanglement-swapping benchmark spanning pure Python, QuTiP, Qiskit, IonQ-native, Quantinuum-native, and Strawberry Fields CV.

## Overview

This repository implements a compact, reproducible benchmark for **entanglement swapping**, one of the core primitives in quantum networking and distributed quantum information processing.

The project asks a simple but important question:

> How does the same entanglement-swapping task look across different software stacks, abstraction layers, and quantum paradigms?

To answer that, this repo holds the problem fixed at the smallest meaningful level:
- two entangled resource pairs
- intermediate measurement on the middle subsystems
- remote entanglement generation on the end subsystems
- one shared comparison framework

The result is a minimal benchmark that highlights **syntax, abstraction, and architecture translation** more than algorithmic complexity.

## Why entanglement swapping matters

Entanglement swapping is a foundational building block for quantum technology. It enables two systems that have never interacted directly to become entangled through intermediate measurement and classical conditioning. This primitive underlies key ideas in:

- quantum repeaters
- long-distance quantum communication
- modular quantum networking
- distributed quantum sensing
- multi-node quantum architectures

Because it sits at the intersection of **state preparation, measurement, communication, and orchestration**, entanglement swapping is a useful test case for comparing how different quantum software ecosystems express the same operational task.

## What is included

This repository contains local-simulation implementations of the same core problem across multiple stacks:

### Technical brief
- brief_technical.pdf

### Discrete-variable (DV) implementations
- pure Python linear algebra: swap_qutip.ipynb
- QuTiP: swap_qutip.ipynb
- Qiskit: swap_qiskit.ipynb
- IonQ-native syntax: swap_ionq.ipynb
- Quantinuum-native compilation flow: swap_quantinuum.ipynb

### Continuous-variable (CV) implementation
- Strawberry Fields with homodyne-based swapping logic: swap_cv_sf.ipynb

### Plotting tool
- Plotting tool:swap_plot.ipynb

## Benchmark design

### DV benchmark
For the discrete-variable implementations, the protocol and metrics are held fixed:

- prepare two Bell pairs
- perform Bell-state projection on the middle qubits
- evaluate the resulting swapped state on the end qubits

All DV versions compute the same three metrics:

- **Bell-state fidelity**
- **success probability**
- **entanglement yield = success probability × Bell fidelity**

These DV results should agree exactly in the ideal noiseless case up to numerical precision.

### CV benchmark
The continuous-variable version implements the same protocol **in spirit**, but not with forced one-to-one metrics.

Instead, the Strawberry Fields implementation uses:
- two entangled Gaussian resources
- intermediate interference
- homodyne measurement on the middle modes
- reduced-state evaluation on the end modes

The CV version reports:
- **success probability**
- **native entanglement metric** (log-negativity)
- **generalized entanglement yield**

This keeps the comparison honest and consistent:

- **DV metrics are identical**
- **CV metrics are generalized but operationally aligned**

## Figure

The main output is a two-panel comparison figure:

- **left panel:** DV exact-metric comparison across five stacks
- **right panel:** CV native metric reported separately in the same operational spirit

This structure preserves exact DV comparability while keeping the CV treatment architecture-native.

## Repository intent

This project is designed as a **minimal cross-stack benchmark** rather than a hardware-performance benchmark.

It is intended to demonstrate:
- translation of one protocol across abstraction layers
- architecture-aware benchmarking 
- local reproducibility
- clear separation between identical and generalized metrics
- compact, auditable benchmarking code

## Local-only philosophy

All implementations are designed for **local simulation**.

This repository does **not** require:
- cloud authentication
- remote hardware access
- provider credentials
- job queues

That keeps the artifact fast to run, easy to inspect, and straightforward to reproduce.

## Key takeaway

This repository shows that a single quantum networking primitive can be expressed consistently across:

- explicit linear algebra
- physics-oriented simulation
- circuit SDKs
- native vendor gate models
- continuous-variable photonic simulation

while preserving:
- exact DV comparability
- honest and consistent CV generalization
- a unified customer-facing interpretation layer

## Planned extensions

Potential next steps include:
- noise-aware DV variants
- architecture-specific compilation summaries
- gate-count / depth comparison tables
- feedforward-corrected swapping branches
- broader network-level scaling studies

## License

See the `LICENSE` file in this repository.

## Author

Boris Kiefer
