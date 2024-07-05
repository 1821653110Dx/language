```python
import numpy as np

"""
manual reshape
"""
x = np.arange(0,6)	# create a sequence : [0,5], 1 | save to x
print(x)
print(x.reshape((2,3)))	# get array of x, reshape into (2, 3) array | echo
print(x.reshape((2,3)).reshape((3,2)))	# get array of x, reshape into (2, 3) array | reshape into (3, 2) array | echo

y = np.array([[1, 1, 3], [1, 1, 1]])	# create an array with [[1, 1, 3], [1, 1, 1]] | save to y
x = x.reshape(y.shape)	# get array of x, reshape into shape of y | overwite to x
print(x)
"""
auto reshape
"""
arr = np.arange(15)
print(arr.reshape(5, -1))	# get array of arr, reshape into (5, auto calc) array | echo

"""
flatten
"""
print(x.flatten())	# cp array of x, reshape into 1D array | echo
print(x.ravel())	# reshape array x into 1D array | echo
x.ravel()[0] = -1	# reshape array x into 1D array | set its [0] = -1
print(x)

```