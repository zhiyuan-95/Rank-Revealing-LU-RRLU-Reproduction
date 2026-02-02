# Rank-Revealing LU Decomposition (RRLU)
This repository contains a Python implementation of the Rank-Revealing LU (RRLU) decomposition algorithm. Unlike standard LU decomposition, RRLU is designed to reliably reveal the numerical rank of a matrix and provide a stable basis for the range and null space, even in the presence of ill-conditioning.

### 🚀 Overview
The implementation follows the approach of transforming a matrix $A$ into the form: $$P_r A P_c = LU$$ where: $P_r$ and $P_c$ are permutation matrices for rows and columns. $L$ is a unit lower triangular matrix. $U$ is an upper triangular (or trapezoidal) matrix.The core of this algorithm is the ability to swap columns to "expose" the rank and then retriangularize the resulting factors efficiently without recomputing the entire decomposition from scratch.

### ✨ Features
**Column Pivoting**: Initial decomposition using standard column pivoting (LU_cp).

**Efficient Retriangularization**: Implements specialized updates (retriangularization_2) that restore the triangular structure of $L$ and $U$ after column permutations in $O(n^2)$ time.

**Rank Detection**: Iteratively moves columns to ensure the diagonal elements of $U$ accurately reflect the importance of each dimension.

**Verification**: Includes validation scripts to ensure $P_r A P_c - LU \approx 0$.

### 🛠️ Implementation Details
The project is contained within a Jupyter Notebook (RRLU.ipynb) and utilizes:

- NumPy for matrix operations and linear algebra.

- SciPy for initial LU benchmarking.

### Key Functions
- LU_cp(A): Performs LU decomposition with column pivoting.
- retriangularization_2(i, L, U): The engine of the algorithm. It handles the "Upper Hessenberg" form created by column swaps and uses row/column rotations to return the system to triangular form.
- col_swap(A, i, k): A helper function to swap the $i$-th column to the $k$-th position while shifting intervening columns.

### 📝 Mathematical Context
The retriangularization process ensures that if a column swap breaks the triangular structure, we apply a sequence of elementary transformations $E$ such that: 
$$L_{new} = L \cdot E^{-1}, \quad U_{new} = E \cdot U$$. 
This maintains the validity of the decomposition while updating the rank information.
### reference
[On the existence and computation of.pdf](https://github.com/user-attachments/files/25025141/On.the.existence.and.computation.of.pdf)

