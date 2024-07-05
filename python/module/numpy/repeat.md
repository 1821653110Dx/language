```python
import numpy as np

x = np.array([[1,2], [3,4]])	# create an array with [[1,2], [3,4]] | save to x
print(x.repeat(2))	# repeat cp of x by elements 2 times | echo
print(x.repeat(2, axis = 0))	# repeat cp of x by row 2 times | echo
print(x.repeat(2, axis = 1))	# repeat cp of x by col 2 times | echo

x = np.array([1,2])
print(np.tile(x, 2))	# create a matrix with 2X1 [1,2] | echo	# 2X1 [1,2] = 2 [1,2] horizontallt, 1 [1,2] horizontally = [1,2,1,2]
print(np.tile(x, (2,2)))	# create a matrix with 2X2 [1,2] | echo
```