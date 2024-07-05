```python
import numpy as np

# basic
x = np.array([[1,2], [2,3], [1,2]]) # create an array with [[1,2], [2,3], [1,2]] | save to x
print(x.mean()) # get avg of array x | echo
print(x.mean(axis = 1)) # get avg of each row of array x | echo
print(x.mean(axis = 0)) # get avg of each col of array x | echo
print(x.sum())  # get sum of array x | echo
print(x.sum(axis = 1))  # get sum of each row of array x | echo
print(x.max())  # get the max of array x | echo
print(x.max(axis = 1))  # get the max of each row of array x | echo
print(x.argmin())   # get index of max element of array x | echo
print(x.argmin())   # get index of min element of array x | echo
print(x.cumsum())   # get cumulative sum累积和 of array x | echo
print(x.cumprod())  # get cumlulative prod of array x | echo 
print(x.std())  # get standard devidation标准差 of array x | echo
print(x.var())  # get variance方差 of array x | echo

y = np.array([1, 2, 3, 4])
print(np.ptp(y))    # print max - min for 1d y


# count by boolean list
x = np.array([[True, False], [True, False]])
print(x.sum())  # get True counts of x | echo
print(x.sum(axis = 1))   # get True counts of each row in x| echo
print(x.any(axis = 0))  # get boolean list of x, if True in col, boolean value = True. Otherwise False | echo
print(x.all(axis = 1))	# get boolean list of x, if False not in col, boolean value = True, Otherwise False | echo

# sort
x = np.array([[1, 6, 2], [6, 1, 3], [1, 5, 2]])
x.sort(axis = 1)    # sort evey row in a-oder
print(x)

# 分位数
print(np.quantile(x, [0.25, 0.5, 0.75])) # newline print the [0.25, 0.5, 0.75] quantiles of array x  # 0.25 quantile = 0.25分位数
print(np.percentile(x, [25, 50, 75])) # newline print the number [25, 50, 75] percentiles of array x # the number 25 percentile 20% 分位数
```