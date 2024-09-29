---
tags:
  - Math
  - Linear_Algebra
---
## Basic Definition
- For $A \in F^{n \times l}$ and $B \in F^{l \times m}$,
$$
(AB)_{ij} = \sum \limits_{k=1}^{l} A_{ik}B_{kj}
$$

## Equivalence to Matrix Multiplication
### Matrix Multiplication of Block Matrices
- Even if each element of a matrix is not a scalar (1-dim element), as long as multiplication is defined, matrix multiplication can be extended.
$$
A = \begin{pmatrix} A_{11} & A_{12} & \cdots & A_{1l} \\ A_{21} & A_{22} & \cdots & A_{2l} \\ \vdots & \vdots & \ddots & \vdots \\ A_{m1} & A_{m2} & \cdots & A_{ml} \end{pmatrix}, \quad B = \begin{pmatrix} B_{11} & B_{12} & \cdots & B_{1n} \\ B_{21} & B_{22} & \cdots & B_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ B_{l1} & B_{l2} & \cdots & B_{ln} \end{pmatrix}
$$
$$
A \times B = \begin{pmatrix} \sum_{k=1}^{l} A_{1k}B_{k1} & \sum_{k=1}^{l} A_{1k}B_{k2} & \cdots & \sum_{k=1}^{l} A_{1k}B_{kn} \\ \sum_{k=1}^{l} A_{2k}B_{k1} & \sum_{k=1}^{l} A_{2k}B_{k2} & \cdots & \sum_{k=1}^{l} A_{2k}B_{kn} \\ \vdots & \vdots & \ddots & \vdots \\ \sum_{k=1}^{l} A_{mk}B_{k1} & \sum_{k=1}^{l} A_{mk}B_{k2} & \cdots & \sum_{k=1}^{l} A_{mk}B_{kn} \end{pmatrix}
$$

## Matrix Multiplication as a Vector Stack
- For $A \in F^{n \times l}$ and $B = [\mathbf{b}_1, \mathbf{b}_2, \dots, \mathbf{b}_m]$ where $\mathbf{b}_i \in F^l = F^{l \times 1}$,
$$
AB = [A \mathbf{b}_1 \mid A \mathbf{b}_2 \mid \dots \mid A \mathbf{b}_m]
$$
- Let $A = \begin{pmatrix} \mathbf{a}_1 \\ \mathbf{a}_2 \\ \vdots \\ \mathbf{a}_n \end{pmatrix}$ where $\mathbf{a}_i \in F^l = F^{1 \times l}$, and $B = [\mathbf{b}_1, \mathbf{b}_2, \dots, \mathbf{b}_m]$ where $\mathbf{b}_i \in F^l = F^{l \times 1}$, 
  => $\mathbf{a}_i$ is a row vector, and $\mathbf{b}_j$ is a column vector:
$$
AB = \begin{pmatrix} \mathbf{a}_1 \mathbf{b}_1 & \mathbf{a}_1 \mathbf{b}_2 & \cdots & \mathbf{a}_1 \mathbf{b}_m \\ \mathbf{a}_2 \mathbf{b}_1 & \mathbf{a}_2 \mathbf{b}_2 & \cdots & \mathbf{a}_2 \mathbf{b}_m \\ \vdots & \vdots & \ddots & \vdots \\ \mathbf{a}_n \mathbf{b}_1 & \mathbf{a}_n \mathbf{b}_2 & \cdots & \mathbf{a}_n \mathbf{b}_m \end{pmatrix}
$$

- For $A = [\mathbf{a}_1, \mathbf{a}_2, \dots, \mathbf{a}_l]$ where $\mathbf{a}_i \in F^n = F^{n \times 1}$, and $B = \begin{pmatrix} \mathbf{b}_1 \\ \mathbf{b}_2 \\ \vdots \\ \mathbf{b}_l \end{pmatrix}$ where $\mathbf{b}_i \in F^m = F^{1 \times m}$,
$$
AB = \sum\limits^l_{k=1} \mathbf{a}_k \mathbf{b}_k
$$
