```python
import numpy as np

"""
square
"""
x = np.arange(6) # create a sequence : [0,6) d1 | save to x
print(x)
print(np.square(x)) # square each elements of x | printf it + '\n'

"""
sqrt
"""
x = np.arange(6)
print(x)
print(np.sqrt(x))	# sqrt each element of x | echo it

"""
mod
"""
x = np.array([1.5, 1.6, 1.7, 1.8])    # create an array with [1.5, 1.6, 1.7, 1.8] | overwrite to x
y, z = np.modf(x)    # cp integer and decimal parts of x | save to y, z
print(x)    # print "{ x }\n"
print(y)    # print "{ y }\n"

"""
maximum, minimum
"""
x = np.array([[1,4], [6,7]])
y = np.array([[2,3], [5,8]])
print(np.maximum(x, y)) # create an array with max element of each coincident position between x and y | printf "{ it }\n"
print(np.minimum(x, y)) # create an array with min element of each coincident position between x and y | printf "{ it }\n"

"""
where
"""
cond = np.array([True, False, True, False])
x = np.where(cond, -2, 2) # cp array of cond, for each elements, replaced with -2 if = True. otherwise replaced with 2 | overwite to x
print(x)

cond = np.array([1, 2 ,3, 4]) 
x = np.where(cond > 2, -2, 2)   # cp array of cond, for each elements, replaced with -2 if > 2. otherwise 2 | overwite to x
print(x)

y1 = np.array([-1, -2, -3, -4])
y2 = np.array([1, 2, 3, 4])
x = np.where(cond > 2, y1, y2)  # cp array of cond, replaced with y1[coincident position] if > 2, otherwise y2[] | overwirte to x
print(x)

y1 = np.array([-1, -2, -3, -4, -5, -6])
y2 = np.array([1, 2, 3, 4, 5, 6])
y3 = np.zeros(6)    # create an (6,1) zeros array | save to y3
cond = np.array([1, 2, 3, 4, 5, 6])
x = np.where(cond > 5, y3, np.where(cond > 2, y1, y2))# cp array of cond, replaced with y1[conincident position] if > 2, otherwise y2 | cp array of cond, replaced with y3[conincident posistion] if > 5, otherwise { return0 }[] | overwite to x
print(x)

```