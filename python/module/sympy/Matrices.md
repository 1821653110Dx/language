# create
$$
\left[\begin{matrix}1 & -1\\3 & 4\\0 & 2\end{matrix}\right]
\left[\begin{matrix}1\\2\\3\end{matrix}\right]
$$
	Matrix([[1, -1], [3, 4], [0, 2]])
	Matrix([1, 2, 3])

$$
\left[\begin{matrix}1 & 0 & 0\\0 & 1 & 0\\0 & 0 & 1\end{matrix}\right]
$$
	eye(3)

$$
\left[\begin{matrix}0 & 0 & 0\\0 & 0 & 0\end{matrix}\right]
$$
	zeros(2,3)

$$
\left[\begin{matrix}1 & 1 & 1\\1 & 1 & 1\end{matrix}\right]
$$
	ones(3,2)

$$
\left[\begin{matrix}-1 & 0 & 0 & 0\\0 & 1 & 1 & 0\\0 & 1 & 1 & 0\\0 & 0 & 0 & 5\\0 & 0 & 0 & 7\\0 & 0 & 0 & 5\end{matrix}\right]
$$
	diag(-1, ones(2,2), Matrix([5,7,5]))

# Basic Operations
## shape
	shape(M)
## accessing Rows and Columns
	M.row(0)
	M.col(-1)
## delteing and inserting rows and columns
	M.col_del(0)
	M.row_del(0)
	M.row_insert(1, Matrix([[0, 4]]))
	M.col_insert(0, Matrix([-1, -2]))

# Methods
## Basic
$$
\left[\begin{matrix}1 & 3\\-2 & 3\end{matrix}\right]
+
\left[\begin{matrix}0 & 3\\0 & 7\end{matrix}\right]
=
\left[\begin{matrix}1 & 6\\-2 & 10\end{matrix}\right] 
$$
	M + N

$$
\left[\begin{matrix}1 & 3\\-2 & 3\end{matrix}\right]
\cdot
\left[\begin{matrix}0 & 3\\0 & 7\end{matrix}\right]
=
\left[\begin{matrix}0 & 24\\0 & 15\end{matrix}\right]
$$
	M*N

$$
3
\cdot
\left[\begin{matrix}0 & 3\\0 & 7\end{matrix}\right]
=
\left[\begin{matrix}0 & 9\\0 & 21\end{matrix}\right]
$$
	3*M

$$
\left(\left[\begin{matrix}1 & 3\\-2 & 3\end{matrix}\right]\right)^2
=
\left[\begin{matrix}-5 & 12\\-8 & 3\end{matrix}\right]
$$
	M**2

$$
\left(\left[\begin{matrix}1 & 3\\-2 & 3\end{matrix}\right]\right)^{-1}
=
\left[\begin{matrix}\frac{1}{3} & - \frac{1}{3}\\\frac{2}{9} & \frac{1}{9}\end{matrix}\right]
$$
M**-1

$$
\left[\begin{matrix}1 & 2 & 3\\4 & 5 & 6\end{matrix}\right]_{.T}=
\left[\begin{matrix}1 & 4\\2 & 5\\3 & 6\end{matrix}\right]
$$
M.T

## advanced
- compute the determinant of a matrix
$$
\left[\begin{matrix}1 & 0 & 1\\2 & -1 & 3\\4 & 3 & 2\end{matrix}\right] \Longrightarrow -1
$$
	M.det()
- put a matrix into reduced row echelon$\tiny 梯队$ form
$$
\left[\begin{matrix}1 & 0 & 1 & 3\\2 & 3 & 4 & 7\\-1 & -3 & -3 & -4\end{matrix}\right] \Longrightarrow \left( \left[\begin{matrix}1 & 0 & 1 & 3\\0 & 1 & \frac{2}{3} & \frac{1}{3}\\0 & 0 & 0 & 0\end{matrix}\right], \  \left( 0, \  1\right)\right)
$$
	M.rref()
- eigenvalues$\tiny 特征值$
$$\left[\begin{matrix}3 & -2 & 4 & -2\\5 & 3 & -3 & -2\\5 & -2 & 2 & -2\\5 & 2 & -3 & 3\end{matrix}\right] \Longrightarrow \left\{ -2 : 1, \  3 : 1, \  5 : 2\right\}$$
	M.eigenvals()
- eigenvalues and eigenvactors
$$
\left[\begin{matrix}3 & -2 & 4 & -2\\5 & 3 & -3 & -2\\5 & -2 & 2 & -2\\5 & -2 & -3 & 3\end{matrix}\right] \Longrightarrow \left[ \left( -2, \  1, \  \left[ \left[\begin{matrix}0\\1\\1\\1\end{matrix}\right]\right]\right), \  \left( 3, \  1, \  \left[ \left[\begin{matrix}1\\1\\1\\1\end{matrix}\right]\right]\right), \  \left( 5, \  2, \  \left[ \left[\begin{matrix}1\\1\\1\\0\end{matrix}\right], \  \left[\begin{matrix}0\\-1\\0\\1\end{matrix}\right]\right]\right)\right]
$$
	M.eigenvects()
- diagonalization$\tiny 对角化$
$$
M = \left[\begin{matrix}3 & -2 & 4 & -2\\5 & 3 & -3 & -2\\5 & -2 & 2 & -2\\5 & -2 & -3 & 3\end{matrix}\right] \Longrightarrow P =  \left[\begin{matrix}0 & 1 & 1 & 0\\1 & 1 & 1 & -1\\1 & 1 & 1 & 0\\1 & 1 & 0 & 1\end{matrix}\right] , D = \left[\begin{matrix}-2 & 0 & 0 & 0\\0 & 3 & 0 & 0\\0 & 0 & 5 & 0\\0 & 0 & 0 & 5\end{matrix}\right] \\
M = PDP^{-1}
$$
	P,D = M.diagonalize()