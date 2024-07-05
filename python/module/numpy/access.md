# normal
```python
import numpy as np
x = np.array([[1,2], [3,4], [5,6]])   # create an array with [[1,2], [3,4], [5,6]] | save to x
print(x[0]) # printf "{ row0 of x }\n"
print(x[0][1])  # printf "{ (row0, col1) of x}\n"

x = np.array([ [[1, 2], [3, 4]] , [[5, 6], [7, 8]] ])  # create an array  with [ [[1, 2], [3, 4]] , [[5, 6], [7, 8]]] | save to x
print(x[0]) # printf "{ lay0 of x }\n"

y = x[0].copy() # copy x[0] to y
z = x[0]    # save addr of x[0] to z
print(y)

y[0, 0] = 0 # set y[0, 0] = 0
z[0, 0] = -1    # set array[0, 0] z points to = -1
print(y)
print(z)
print(x[0])

x = np.array([1, 2, 3, 4, 5])   # create an array with [1, 2, 3, 4, 5] | overwirte to x
print(x[1:3])
print(x[:3])
print(x[0:4:2])

x = np.array([[1,2],[3,4],[5,6]])
print(x[:2])    # x[:2] = row in [0, 2-1]
print(x[:2, :1])    # x[:2, :1] = row in [0, 2-1], col in [0:1-1]

x[:2, :1] = 0
print(x)

x[:2, :1] = [[8], [6]]
print(x)
```
# by boolean
```python
import numpy as np
x = np.array([3, 2, 3, 1, 3, 0])  # create an array with [3, 2, 3, 1, 3, 0] | save to x
y = np.array([True, False, True, False, True, False])
print(x[y]) # printf "{ x's elements corresponding to position of True of y }\n"
print(x[y == False])    # printf "{ x's elements coresponding to position of False of y'}\n"

print(x >= 3)   # printf "{ array with x's elements' boolean value about >=3 }\n"
print(x[~( x >= 3 )])   # printf "{ elements that of x and not >= 3}\n"
print((x == 2) | (x == 1)) # get an array with x's elements' boolean value about { = 2 or = 1 } | printf "{}\n"
print(x[(x == 2) | (x == 1)]) # printf "{ elements that in x and ( = 2 or = 1) }\n"
x[(x == 2) | (x == 1)] = 0 # set elements that in x and ( =2 or =1) to 0
print(x)
```

# by list
```python
import numpy as np

x = np.array([1, 2, 3, 4, 5, 6]) # create an array with [1, 2, 3, 4, 5, 6] | save to x
print(x[[1, 2, 3]])   # printf "{ index(0, 1, 2) of x }\n"
print(x[[-1, -2, -3]]) # printf "{ index(-1, -2, -3) of x }\n"

x = np.array([[1,2],[3,4],[5,6]])
print(x[[0,1]]) # printf "{ row(0, 1) of x }\n"
print(x[[0, 1], [0, 1]]) # printf "{ (0,0) and (1,1) in x }\n"
print(x[[0,1]][:,[0,1]]) # printf "{ row(0, 1) and col(0,1) in x }\n"
print(x[np.ix_([0, 1],[0, 1])]) # printf "{ row(0, 1) and col(0,1) in x }\n"

x[[0,1], [0,1]] = [0,0]
print(x)
```