Optimal Matrix Chain Ordering Problem
=====================================

Python implementation of the “Matrix-Chain-Order” algorithm from
Thomas H. Cormen et al. “Introduction to Algorithms Third Edition”,
which uses Dynamic Programming to determine the optimal
parenthesization for Matrix-chain multiplication.

Matrix Chain Multiplication
---------------------------

“We state the *matrix-chain multiplication problem* as follows: given
a chain "A_1, A_2, ..., A_n" of "n" matrices, where for "i = 1, 2,
..., n", matrix "A_i" has dimension "p_(i-1) * p_i", fully
parenthesize the product "A_1, A_2, ..., A_n" in a way that minimizes
the number of scalar multiplications.”

Cormen et al. show the algorithm for this at the bottom of page 375,
which returns two tables. The “S” table may be further input to the
“Print-Optimal-Parens” algorithm at the bottom of page 377 to display
the  optimal ordering.

Both algorithms are implemented here. They may be invoked from the
commandline to show (i,j) entries in the S matrix, and to display the
optimal parentheses for the multiplication.


Example Usage
-------------

```bash
 $ python MatrixChainOrdering.py --chain 2,20,4,6
 ((A_1A_2)A_3)

 $ python MatrixChainOrdering.py --chain 2,20,4,6 --verbose
 (i,j) = (1,1): 0
 (i,j) = (2,2): 0
 (i,j) = (3,3): 0
 (i,j) = (1,2): 160
 (i,j) = (2,3): 480
 (i,j) = (1,3): 208
```

---

MatrixChainOrdering.matrix_chain_order(*p*)
-------------------------------------------

Given a list of integers corresponding to the
dimensions of each pair of matrices forming a chain.

Parameters:
  **p** (*list*) – A list of integers corresponding to the dimensions in
  the chain of matrices.

Returns:
  **M, S** (*dict, dict*) – Dictionaries corresponding to minimum costs of each chain and the optimal values of `k`.

```python
>>> M, S = matrix_chain_order([2, 20, 4, 6])
>>> print(M)
{(1, 1): 0, (2, 2): 0, (3, 3): 0, (1, 2): 160, (2, 3): 480, (1, 3): 208}
>>> print(S)
{(1, 2): 1, (2, 3): 2, (1, 3): 2}
```

MatrixChainOrdering.print_optimal_parens(*s*, *i*, *j*)
-------------------------------------------------------

Print the optimal parentheses according to the S-matrix computed by
the matrix_chain_order function.

Parameters:
  * **s** (*dict*) – A dictionary of tuples corresponding to the
    minimum k values from each step of "matrix_chain_order".

  * **i** (*int*) – Starting index.

  * **j** (*int*) – End index.

Example (continued from previous function):

```python
>>> M, S = matrix_chain_order([2, 20, 4, 6])
>>> print_optimal_parens(S, 1, 3)
((A_1A_2)A_3)
```

General form:

```python
>>> chain = [2, 20, 4, 6]
>>> M, S = matrix_chain_order(chain)
>>> print_optimal_parens(S, 1, len(S) - 1)
((A_1A_2)A_3)
```
