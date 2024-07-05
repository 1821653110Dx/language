```python
import matplotlib.pyplot as plt
import numpy as np

'def argument x'
x = np.linspace(-1,1,50) ;   # create an array with 50 number uniformly distrubuted均匀分布 in [-1,1] | save to x

'def func y1, y2'
y1 = 2*x + 1
y2 = x**2

'generate 2Dplots in figure1 : y1(x)'
fig1 = plt.figure(num=1)	# create figure1 | save to fig1
plt.plot(x, y1, color='red', linewidth=10, linestyle='--')  # generate y1(x), [color, linewidth, linestyle] = [red, 10, --]

'generate 2Dplots in figure2 : y2(x)'
fig2 = plt.figure(num=2)	# create figure2 | save to fig2
plt.plot(x, y2) # generate y2(x)

'generate 2Dplots in figure2: y1(x), y2(x)'
fig3 = plt.figure(num=3) # create figure3 | save to fig3
plt.plot(x, y1) # generate y1(x)
plt.plot(x, y2)

'show figures'
plt.show()  
```
