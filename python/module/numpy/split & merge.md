```python
import numpy as np
"""
merge
"""
x = np.array([[1,2,3],[4,5,6]])	# create an array with [[1,2,3],[4,5,6]] | save to x
y = np.array([[7,8,9],[10,11,12]])
print(np.concatenate([x, y], axis = 0))	# merge cp of array y to the bottom of cp of array x | echo
print(np.vstack((x,y)))	# merge cp of array y to the bottom of cp of array x | echo
print(np.concatenate([x,y], axis= 1))	# merge cp of array y to the right of cp of array x | echo
print(np.hstack((x,y)))	# merge cp of array y to the right of cp of array x | echo

"""
split
"""
print(np.split(x,2,axis = 0))	# horizontally split cp of array x into 2 arrays | echo
print(np.split(x,3,axis = 1))	# vertically split cp of array x into 3 arrays | echo
```