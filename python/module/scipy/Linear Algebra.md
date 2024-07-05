> data_struct of numpy and scipy is basically universal
> Matrix is 2d array
# Libear Equation
$$
\begin{equation*}
	\begin{cases}
		3 x_{1} + 2 x_{2}  = 8 \\
		- 3 x_{1} + 5 x_{2} = -1
	\end{cases}
\end{equation*}
\Longrightarrow
\begin{equation*}
	\begin{cases}
		x_1 = 2 \\
		x_2 = 1
	\end{cases}
\end{equation*}
$$
```python
import numpy as np
import pandas.io.clipboard as cp
from scipy import linalg

## scipy
A =  np.array([[3,2], [-3,5]]) # create array A with [[3,2], [-3,5]]
b = np.array([[8, -1]]).T  # create array with array [[8, -1]] | transpose it | save to b
						# b = np.array([[8, -1]]).T can be replaced with b = np.array([8, -1])

linalg.solve(A,b)   # solve linear_eq corresponding to array A, b

## sympy
A = Matrix([[3,2], [-3,5]])
b = Matrix([8, -1])
A.solve(b, 'LU')	# solve linear_eq corresponding to Matrix A, col_vec b

```

$A=\left[\begin{matrix}3 & 2\\-3 & 5\end{matrix}\right]\\\text{Matrix rank矩阵阶数, condition number条件数 = ?}$
```python
from sympy import *
import numpy as np
import pandas.io.clipboard as cp
from scipy import linalg
"""
using numpy
"""
np.array([[3,2], [-3,5]])   # create array A [[3,2], [-3,5]]
np.linalg.matrix_rank(A)    # return rank of matrix A
np.linalg.cond(A)   # return condition_number of matrix A
"""
using sympy
"""
A = Matrix([[3,2],[-3,5]])    # create Matrix A  [[3,2],[-3,5]]
A.rank()    # return Matrix A's rank
A.condition_number().evalf(10)    # return Matrix A's condition number
```

$A=\left[\begin{matrix}3 & 2\\-3 & 5\end{matrix}\right]=PLU\\P,L,U = ??? \\\text{whether A  = P@L@U ?}$
```python
import numpy as np
import pandas.io.clipboard as cp
from scipy import linalg

## scipy
A = np.array([[3, 2], [-3, 5]])  # create array A with [[3, 2], [-3, 5]]
P, L, U = linalg.lu(A)  # linear_solve A's P,L,U | save to P, L, U
np.allclose(A, P@L@U) ;    #return True if A = P@L@U

## sympy
A = Matrix([[3, 2],[-3, 5]])
L, U, _ = A.LUdecomposition()   # evaluate A's U_matrix, L_matrix, save to L, U

"""
P is a transposed matrix
U is a upper triangular matrix
L is a lower triangular matrix
@ is matrix *
"""
```
# eigenvalue 特征值
## concepts
- eigenvalue problem : $\lambda$ and $\vec{x}$ of matrix A whether satisfy the following expr
	- [x, $\lambda$] = conditional [vector, scalar]
$$
A x = \lambda x\text{\quad or \quad}\left(A - I \lambda\right)x = 0
$$
- if A is singular matrix, then
$$
	det(A - \lambda I) = 0
$$
- when No.n order matrix A has n different eigenval, its diagonal matrix D
	- X = eigenvec_matrix
$$
D = X^{-1}AX
$$
- $A^{n} = XD^{n}X^{-1}$
	- D : digonal matrix对角矩阵
- $D = Q^{-1}AQ$
	- Q : Orthogonal matrix正交矩阵，$Q^{-1} = Q^T$
## python
### For $A=\left[\begin{matrix}2 & 3\\1 & 4\end{matrix}\right]$, evalueate eigenval, eigenvect, diagonal matrix,
```python
from sympy import *
import numpy as np
import pandas.io.clipboard as cp
from scipy import linalg

A = np.array([[2,3], [1,4]])  # create matrix A [[2,3], [1,4]]

## eigenval, eigenvect
w, x = linalg.eig(A)    # return eigenval_array and eigenvec_array for matrix A | save to w,x

Matrix(w)    # w >> symMatrix
Matrix(x)    # x >> symMatrix

## evaluate diagonal matrix using scipy
linalg.inv(x) @ A @ x # evaluate diagonal_matrix using A's eigenvec_array x | >> symMatrix

## evaluate diagonal matrix using sympy
Matrix(A)
X, D = A.diagnalize()   # evaluate A's eigenvect_array and diagonal_matrix | save to X, D

"""
eigenval, eigenvec = eigenvalue, eigenvector
"""
```
### For $A = \left[\begin{matrix}1 & 0\\0 & 1\end{matrix}\right]\\ \text{evaluate B = the 0.5th power of matrix A}\\ \text{judge wthether } A = B^2$
```python
from sympy import *
import numpy as np
import pandas.io.clipboard as cp
from scipy import linalg

A = np.array([[1,0],[0,1]]) # create array A [[1,0],[0,1]]
B = linalg.fractional_matrix_power(A, 0.5)  # evaluate the 0.5th power of matrix A | save to B
np.allclose(A, B@B) # return True if A = B@B 
```
### For A = $\left[\begin{matrix}4 & 2 & -3\\2 & 5 & -2\\-3 & -2 & 4\end{matrix}\right]$, verify whether A equals $Q^TAQ$
```python
A = np.array([[4, 2, -3], [2, 5, -2], [-3, -2, 4]])    # create matrix A [[4, 2, -3], [2, 5, -2], [-3, -2, 4]]
w, Q = linalg.eig(A)    # return the eigenval_array and eigenvec_array for matrix A | save to w, Q

np.allclose(np.diag(w), Q.T @ A @ Q)   # return the diagonal_matrix of matrix w | return True if { } = transposed_matrix of Q @ A @ Q 
# { 0 } : return value of the first cmd ; { } = return value of the previous cmd
```