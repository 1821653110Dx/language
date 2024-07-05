```python
import numpy as np

## remove duplicated elements
x = np.array([[1, 6, 2], [6, 1, 3], [1, 5, 2]])  # create an array with [[1, 6, 2], [6, 1, 3], [1, 5, 2]] | save to x
print(np.unique(x)) # get array of x, create a list with unique elements of x | echo

y = np.array([1, 6, 5])
print(np.intersect1d(x,y))  # get a list with elements both in x and y | echo
print(np.union1d(x, y)) # get a list with unique elements of elements of x and y  | echo
print(np.setdiff1d(x, y))   # get a list with elements that in x instead of y | echo
print(np.setxor1d(x, y))    # get a list with elements that only in x instead of in both x and y | echo
```