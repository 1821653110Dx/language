```python
import matplotlib.pyplot as plt
import numpy as np

"def arg : x"
x = np.arange(0,10,0.1)    # create a sequence : [0,10), d 0.1 | saveto x

"def func : y1(x), y2(x)"
y1 = 0.05*x**2
y2 = -1*y1

"""
generate 2Dplots in figure 1: y1(x), y2(x)
"""
fig1 =plt.figure(num=1) # create figure1 | save to fig1
plt.plot(x,y1,'g-')	# generate y1(x), [color, linestyle] = [g,-]
plt.plot(x,y2,'b--')

"""
set axis for figrue 1, 2D
"""
ax = plt.gca()  # save current axis to ax
ax_cp = ax.twinx()   # save the cp of ax to ax_cp

"set xlabel, ylabel of ax"
ax.set_xlabel("x data") # set xlabel of ax : name = x data
ax.set_ylabel("y1 data", color = "g")   # set ylbale of ax : [name, color] = [y1 data, g]

"set ylabel of ax_cp"
ax_cp.set_ylabel("y2 data", color = "b")    # set ylabel of ax_cp : [name, color] = [y2 data, b]

"show figures"
plt.show()
```
