
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:2E1065,50:5B21B6,100:7C3AED&height=220&section=header&text=HypaCADD%20QNN%20Implementation&fontSize=38&fontColor=ffffff&animation=fadeIn&fontAlignY=38"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python"/>
  <img src="https://img.shields.io/badge/Qiskit-0.45-purple?style=for-the-badge&logo=ibm"/>
  <img src="https://img.shields.io/badge/Quantum%20ML-QNN-indigo?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Domain-Drug%20Discovery-green?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Architecture-Farhi--Neven-red?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge"/>
</p>

---

# Table of Contents

- [HypaCADD QNN Implementation](#hypacadd-qnn-implementation)
- [Project Overview](#project-overview)
- [Quantum Neural Network Architecture](#quantum-neural-network-architecture)
- [Features Used](#features-used)
- [Dataset](#dataset)
- [Training Configuration](#training-configuration)
- [Results](#results)
- [Key Findings](#key-findings)
- [Repository Structure](#repository-structure)
- [Technologies Used](#technologies-used)
- [Reference Paper](#reference-paper)
- [Course Information](#course-information)
- [Future Improvements](#future-improvements)
- [License](#license)

---

# HypaCADD QNN Implementation

A Quantum Neural Network (QNN) implementation based on the **Farhi–Neven architecture** for predicting the impact of genetic mutations on protein–drug binding interactions.

This project was developed as the final project for the **Quantum Information Processing** course at the **University of Tehran** and is inspired by the paper:

> *Insights from incorporating quantum computing into drug design workflows*  
> Published in *Bioinformatics (2023)*

The implementation reproduces and analyzes the Quantum Machine Learning (QML) component of the **HypaCADD** hybrid classical–quantum drug discovery workflow using **Qiskit**.

---

# Project Overview

The original HypaCADD framework combines:

- Classical molecular docking
- Molecular dynamics simulations
- Feature extraction pipelines
- Quantum Neural Networks (QNNs)

to identify drug candidates resilient against genetic mutations.

This repository specifically focuses on the **QNN-based mutation impact prediction module**, where a variational quantum circuit is trained to classify whether a mutation disrupts protein–drug binding.

---

# Quantum Neural Network Architecture

The implemented model follows the **Farhi–Neven QNN** architecture:

- **4 Input Qubits**
  - One qubit per feature
- **1 Readout Qubit**
- **3 Variational Layers**
  - `RZX → RXX → RZX`
- **12 Trainable Parameters**

Input features are encoded using RX rotations after Min-Max normalization.

The final prediction is obtained from the expectation value of the readout qubit measurement.

---

# Features Used

To remain compatible with 5-qubit IBM quantum systems, the model uses four ligand-independent features:

| Feature | Description |
|---|---|
| `bind_site` | Whether the mutation occurs in the binding site |
| `distance` | Distance between mutation and ligand |
| `polarity_change_index` | Amino acid polarity change |
| `volume_change_index` | Amino acid volume change |

---

# Dataset

The project uses the **GenoDock** dataset introduced in the HypaCADD paper.

Dataset statistics:

| Split | Samples |
|---|---|
| Training | 5142 |
| Validation | 5139 |

Class distribution is highly imbalanced:

- **Non-disruptive:** 93.5%
- **Disruptive:** 6.5%

---

# Training Configuration

Two optimizers were evaluated:

| Optimizer | Result |
|---|---|
| COBYLA | Failed to converge effectively |
| SPSA | Achieved strong convergence and performance |

Final SPSA configuration:

```python
Optimizer: SPSA
Iterations: 200
Learning Rate: 0.05
Perturbation: 0.05
```
---

# Results
Final Performance (SPSA)

| Metric              | Value  |
| ------------------- | ------ |
| Training Accuracy   | 91.52% |
| Validation Accuracy | 91.61% |
| Initial Loss        | 0.51   |
| Final Loss          | 0.11   |

---
# Key Findings
* SPSA significantly outperformed COBYLA for QNN optimization.
* The QNN successfully learned meaningful biomedical classification patterns.
* Hybrid classical–quantum workflows are practical for near-term quantum machine learning applications.
* The implementation demonstrates the feasibility of applying QNNs to real-world drug discovery tasks.
---
# Repository Structure
```bash
├── Quantum_final_project.ipynb
├── Final_Project_Report.pdf
├── btac789.pdf
└── README.md
```
---
# Technologies Used
* Python 3.12
* Qiskit
* Qiskit Machine Learning
* NumPy
* Pandas
* Scikit-learn
---
# Reference Paper

* Bayo Lau et al.
Insights from incorporating quantum computing into drug design workflows
Bioinformatics, 2023.

# Course Information

* Course: Quantum Information Processing
* University: University of Tehran
* Student: Behzad Jannati

# Future Improvements
* Training on real IBM Quantum hardware
* Weighted loss functions for imbalanced datasets
* Larger variational quantum circuits
* Hybrid classical–quantum ensemble models
* Benchmarking against classical deep learning approaches
---
# License

* This project is for academic and research purposes.

<div align="center"> <sub>Built with ❤️ using Qiskit and Jupyter Notebooks</sub> </div> 
