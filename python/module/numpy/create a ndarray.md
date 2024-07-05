```python
import numpy as np

"""
1D array
"""
data = [1,2,3,4,5,6]
x = np.array(data)  # create an array with list data | save to x
print(x)
print(x.dtype) # print type of data of array x

"""
2D array
"""
data = [[1,2],[3,4],[5,6]]
x = np.array(data)  # create an array with list data | overwrite to x
print(x)
print(x.dtype)

"""
zeros, ones array
"""
print('create arries with zero/ones/empty according to shape')
x = np.zeros(6)     # create an (6,1) zero array | overwrite to x
print(x)
x = np.zeros((2,3))   # create an (2,3) zero array | overwrite to x
print(x)
x = np.ones((2,3))    # create an (2,3) one array | overwrite to x
print(x)
x = np.ones((3,3))    # create an (3,3) one array | overwrite to x
print(x)

"""
identity matrix
"""
x = np.eye(3)	# create an (3,3) identity matrix | overwite to x
print(x)

"""
series
"""
print(np.arange(6))    # create a sequence: [0,6), divison = 1  | print it
print(np.arange(0,6,2))    # create a sequence: [0,6), divison = 2  | print it

```