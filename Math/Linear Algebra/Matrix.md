## Matrix
- Genral Notation
$$
A = \begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
$$
- Matrix in Vector Space on $F$
$$
A \in F^{m \times n}
$$
- Element-wise
$$
(A)_{ij} = a_{ij}
$$
## Various Matrix
### Row & Column Martix
- [[Vector]]를 Matrix의 관점에서 이해
- **Row Matrix (Row Vector, $\mathbf v$)**
$$
\mathbf v = (v_1, v_2, \dots , v_m)
$$
- **Column Matrix (Column Vector, $\mathbf v$)**
$$
\mathbf v = \begin{pmatrix}v_1 \\v_2 \\ \vdots \\ v_n     \end{pmatrix} = \;<v_1;v_2;\dots;v_n>\; = (v_1, v_2, \dots, v_n)^T
$$
### Square Matrix
$$
A \text{ is square } := A \in F^{n \times n}
$$
### Diagonal Matrix ($D$)
- square matrix that confilm:
$$
(D)_{ij} = \begin{cases}
d_{i} & i = j \\
0 & i \neq j
\end{cases}
$$
- Notation
$$
D = diag(d_i) = diag(d_1, d_2, \dots, d_n)
$$
#### Properties
- diagonal matrix is [[Matrix#Symmetric Matrix|symmetric]]
- **Scaling**: for $A \in F^{n\times m}$, diagonal matrix $D=diag(d_i)$
$$
(AD)_{ij} = (A)_{ij} \times d_j
$$
$$
(DA)_{ij} = (A)_{ij} \times d_i
$$
### Identity Matrix ($I$)
$$
I = I_n = diag(\mathbf 1^n)
$$
### Symmetric Matrix
- A matrix that is the same as its transpose
$$
A \text{ is symmetric } \Longleftrightarrow A^T = A
$$
#### Properties
- Symmetric matrix is [[Matrix#Square Matrix|square]]
- For any matrix $A$, $AA^T$ and $A^TA$ are symmetric
- For any matrix $A$ and diagonal matrix $D$, $ADA^T$ and $A^TDA$ are symmetric
-
## Operations of Matrix
### Sum / Difference
- $A,B \in F^{n\times m}$
$$
(A \;\pm \;B)_{ij} = A_{ij}\; \pm \; B_{ij}
$$
### Mult ![[Matrix Multiplication#Basic Definition]]### Transpose ![[Matrix Transpose#Transpose Matrix]]