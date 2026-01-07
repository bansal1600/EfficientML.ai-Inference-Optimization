# Pruning and Sparsity in Neural Networks
EfficientML.ai – Lecture Notes

---

## Overview

As modern AI models continue to grow in size, they demand increasing amounts of computation, memory, and energy. This makes deployment on resource-constrained devices such as mobile phones, embedded systems, and microcontrollers difficult. **Pruning and sparsity** are key techniques in model compression that address this challenge by removing redundant parameters while preserving model accuracy.

This document summarizes the EfficientML.ai lecture on pruning, expanding on the motivation, methods, and practical trade-offs.

---

## Motivation

Large neural networks are often **over-parameterized**, meaning many weights contribute little to the final prediction.

Benefits of pruning:
- Reduced model size
- Lower inference latency
- Lower memory bandwidth usage
- Reduced power consumption
- Easier deployment on edge devices

### MLPerf Insight

The MLPerf benchmark shows that **optimized models** can achieve **10×–100× faster inference** on the same hardware compared to unoptimized ones. These gains come from:
- Pruning
- Quantization
- Compiler and kernel optimizations

---

## What Is Neural Network Pruning?

Neural network pruning is the process of converting a **dense network** into a **sparse network** by removing:
- Individual weights (synapses)
- Neurons
- Filters or channels
- Entire structural components

### Biological Analogy

Pruning mirrors how the human brain improves efficiency by eliminating unused synaptic connections during development.

---

## Dense vs Sparse Networks
Dense Layer:
[[ W W W W ]
[ W W W W ]
[ W W W W ]]

Sparse Layer (after pruning):
[[ W 0 W 0 ]
[ 0 W 0 W ]
[ W 0 0 W ]]


Sparse networks perform the same computation with fewer active parameters.

---

## Iterative Pruning Workflow

Pruning is most effective when applied iteratively:

1. Train the dense model to convergence  
2. Prune a fraction of parameters  
3. Retrain the remaining network  
4. Repeat until the target compression is achieved

Train → Prune → Retrain → Prune → Retrain


### Key Observation

- Models like **AlexNet** achieve up to **10× parameter reduction**
- Accuracy often remains unchanged or improves
- Reduced overfitting is a common benefit

This behavior is closely related to the **Lottery Ticket Hypothesis**.

---

## Pruning Granularity

### 1. Unstructured (Fine-Grained) Pruning

- Removes individual weights
- Produces irregular sparsity

**Pros**
- High compression
- Minimal accuracy loss

**Cons**
- Difficult to accelerate on GPUs/CPUs
- Requires specialized sparse kernels

---

### 2. Structured Pruning (Industry Standard)

Removes entire structures:
- Channels
- Filters
- Neurons
- Attention heads

**Pros**
- Hardware-friendly
- Direct speedups using standard libraries
- Widely adopted in production

**Cons**
- Less flexible than unstructured pruning

---

## Structured Pruning Examples

### Channel Pruning (CNNs)
  Before:
[ C1 | C2 | C3 | C4 ]

After:
[ C1 | C3 ]


Removes full feature maps, reducing FLOPs and memory access.

---

## Pruning Criteria (How to Decide What to Remove)

### 1. Magnitude-Based Pruning

- Remove weights with small absolute values
- Based on the assumption that small weights contribute less

**Why it works**
- Simple
- No second-order computation
- Strong empirical results

Used for:
- Weight pruning
- Filter pruning (via L1/L2 norms)
- Channel pruning

---

### 2. BatchNorm Scaling Factors

Batch normalization introduces learnable scale parameters (γ).

- Channels with small γ values have low importance
- These channels can be safely pruned

Often combined with sparsity-inducing regularization.

---

### 3. Second-Order Pruning

- Uses Hessian or Fisher Information Matrix
- Measures sensitivity of loss to parameter removal

**Trade-off**
- Strong theory
- Very high computational cost
- Rarely used at scale

---

### 4. Activation-Based Pruning

- Prunes neurons or channels that:
  - Rarely activate
  - Produce mostly zero outputs

Common in ReLU-based networks.

---

### 5. Regression-Based (Layer-Wise) Pruning

- Minimizes reconstruction error per layer
- Avoids full end-to-end fine-tuning

Especially useful for:
- Large Language Models (LLMs)
- Very large transformer models

---

## Pruning in Transformers and LLMs

Common targets:
- Attention heads
- Feed-forward network dimensions
- Hidden channels

Why layer-wise pruning matters:
- Fine-tuning LLMs is expensive
- Layer-wise methods reduce compute cost

---

## Trade-Off Summary

| Aspect | Unstructured | Structured |
|------|-------------|------------|
| Compression Ratio | High | Medium |
| Accuracy Retention | High | High |
| Hardware Speedup | Low | High |
| Production Use | Low | Very High |

---

## Key Takeaways

- Pruning is a **core efficiency technique** for deep learning
- Simple magnitude-based methods are often sufficient
- Structured pruning enables real-world speedups
- Iterative pruning is critical for best results
- Sparsity can improve generalization, not just efficiency

---

## References

- EfficientML.ai Course  
- Han et al., *Learning both Weights and Connections for Efficient Neural Networks*  
- Lottery Ticket Hypothesis  
- MLPerf Benchmarks  

---





