```python
import numpy as np

x = np.array([1, 2.6, 3], dtype = np.int64)    # create an array with [1,2.6,3], dtype = int64 | save to x
print(x)
print(x.dtype)

y = np.array([1, 2, 3], dtype = np.float64)    # create an array with [1,2,3], dtype = float64 | save to y
print(y)
print(y.dtype)

x = np.array([1, 2,6, 3], dtype = np.float64)  # create an array with [1, 2.6, 3], dtype = float64 | overwrite to x
y = x.astype(np.int32) # overwite y with array of x, set dtype = int 32
print(x)
print(y)

z = y.astype(np.float64)   # cp array of y to z, set dtype = float64
print(z)

x = np.array(['1', '2', '3'], dtype = np.string_)# create an array with ['1', '2', '3'], dtype = string | overwrite to x
x = y.astype(np.int32)  # overwirte y with array of x, set dtype = int32
print(x)
print(y)

x = np.array([1., 2.6, 3.], dtype = np.float32)    # create an array with [1., 2.6, 3.], dtype = float32 | overwite to x
y = np.arange(3, dtype=np.int32)   # create a sequence: [0,3), 1, dtype = int32 | overwrite to y
print(y)
print(y.astype(x.dtype))    # get array of y, set dtype = x.dtype | print
```