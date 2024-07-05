```python
import numpy as np
a = np.random.randint(0,10,100)	# create 100 randint in [0,10] | save to a
print(a)

b = np.random.rand(40)	# create 40 randfloat in [0,1) | save to b
print(b)

c = np.random.randn(10)	# create 10 randfloat following standard normal distribution标准正态分布 | save to c
print(c)

d = np.random.normal(0,1,100)	# create 100 randfloat whose [mean均值, std deviation标准差] = [0,1] | save to d
print(d)

e = np.random.ranf(20)	# create 20 randfloat in [0,1] | save to e
print(e)

f = np.random.uniform(-1,1,100)	# create 100 randfloat in [-1,1] | save to f
print(f)
```

```python
import matplotlib.pyplot as plt
import numpy as np

"generate figrue1: histogram直方图 "
fig, ax = plt.subplots(constrained_layout = True)   # create a figure and axel, save to [fig, ax]
ax.hist(np.random.randn(1000), bins=20) # generate 1000 randfloat following the std normal distribution | plot its distribution in 20 equan-width intervals等宽区间

ax.set_xlabel("bin")    # set xlabel for current figure = 'bin'
ax.set_ylabel("frequency")  # sey ylabel for current figure = 'frequency'

"show all figures"
plt.show()
```