# Quantum-Enhanced Memetic Tabu Search for LABS

## Overview
This repository implements a **Memetic Tabu Search (MTS)** solver for the **Low Autocorrelation Binary Sequence (LABS)** problem.  
The solution follows a **hybrid quantum–classical optimization philosophy**, where the quantum component is used as a **sampler for high-quality initial solutions**, and the classical component performs the main optimization.

The current codebase focuses on a **robust classical baseline**, which is designed to be easily extended with **quantum-generated seeds** (e.g., DCQO / variational sampling) as required by the NVIDIA iQuHACK 2026 challenge.

---

## LABS Problem
Given a binary sequence of length `N`:

This is a highly non-convex, NP-hard optimization problem with applications in radar and telecommunications.

---

## Algorithmic Structure

### 1. Cost Function
- `labs_cost(bitstring)`
- Converts `{0,1}` bitstrings to `{−1,+1}` spins
- Computes full LABS autocorrelation energy

---

### 2. Local Optimization: Tabu Search
- `tabu_local_search(...)`
- Explores 1-bit-flip neighbors
- Uses a tabu list to avoid cycling
- Performs aggressive local descent

This component is responsible for **most of the optimization power**.

---

### 3. Memetic Framework
- Population-based optimization
- Each individual is locally improved using Tabu Search
- Best solutions are preserved via **elitism**
- New candidates are generated via **mutation**

This combines:
- Global exploration (population)
- Local exploitation (tabu search)

---

Initial Population (bitstrings)
↓
Tabu Local Search (per individual)
↓
Select Elite Solutions
↓
Mutation-Based Refill
↓
Repeat for multiple generations
↓
Return Best Sequence Found

## Code Flow (High-Level)

