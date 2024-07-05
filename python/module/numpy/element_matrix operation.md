# element operation
```python
import numpy as np

a = np.array([1,2,3,4]) # create an array with [1, 2, 3, 4] | save to a
b = np.arange(4)    # create a sequence: [0,4), 1 | save to b

print(a,b)
print(a-b)  # element operation : array a - array b | print
print(a*b)  # element operation : array a * array b | print
print(a**b)
print(2 * np.sin(a))
print(a > 2)    # judge whether > 2 for each element of a
print(np.exp(a))
```

# matrix operation
```python
import numpy as np
"""
dot
"""
a = np.array([[1,2],[3,4]])  # create an array with [[1,2],[3,4]] | save to a
b = np.arange(6).reshape((2,3))  # create a sequence: [0,6), 1 | reshape into (2,3) array | save to b
print(a,'\n',b)
print(a.dot(b)) # print "{ dot product标量积 of array a, array b }\n"

"""
invert
"""
x = np.array([[1, 2], [3, 4]])
y = np.linalg.inv(x)	# get invert matrix of array x | save to y
print(x.dot(y))
print(np.linalg.det(x))	# get the determinant行列式的值 of array x | echo
```