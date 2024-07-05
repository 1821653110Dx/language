```python
import matplotlib.pyplot as plt
import numpy as np

'def arg x'
x = np.linspace(-3,3, 50)   # generate 50 number uniformly distributed in [-3, 3] | save to x

'def func y1, y2'
y1 = 2*x + 1
y2 = x**2

'generate 2Dplots in figure1: y1(x), y2(x)'
fig1 = plt.figure(num=1)	# create figure1 | save to fig1
plt.plot(x, y1, label='up') # generate y1(x), label = 'up'
plt.plot(x, y2, label='down')   # generate y2(x), label = 'down'

'generate labels of each plots'
plt.legend()

'show figures'
plt.show()
```