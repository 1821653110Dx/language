```python
import numpy as np
k = np.arange(9)    # create a sequence: [0,9), 1 | save to k
m = k.reshape((3,3))   # get sequence of k, reshape into an (row3, col3) array | save to m  # row*col = 9
print(k)
print(m)

print(m.T)  # print transposed matrix corresponding to m

print(m.dot(m.T))   # print dot product of m, m.T

k = np.arange(8).reshape(2,2,2) # create a sequence : F0 T7 d(differemce)1 | reshape into (lay2, row2, col2) | overwite to k    # row*col*lay = 8
print(k)
print(k[1][0][1])   # print element at (lay1, row0, col1)

m = k.transpose(1,0,2)  # get array of k, mv data of axis0 to axis1, mv data of axis1 to axis0 | overwite to m
print(m)
print(m[0][1][0])

m = k.swapaxes(0,1) # get array of k, swap axis0 with axis1 | overwite to m     # axis 0..2 = xyz
print(m)
print(m[0][1][0])
```