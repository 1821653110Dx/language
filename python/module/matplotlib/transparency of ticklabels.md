```python
import matplotlib.pyplot as plt
import numpy as np

'def arg : x'
x = np.linspace(-3, 3, 50)  # create an array with 50 numbers uniformly distributed in [-3, 3] | save to x

'def func : y'
y = 0.1*x

'generage 2Dplots in figure1: y(x)'
fig1 =plt.figure(num=1) # create figure1 | save to fig1
plt.plot(x, y, color='red', lw = 10, zorder=1)    # generate y(x), [color, linewidth, zorder] = [red, 10, 1]    # zorder = layer of y(x) in current figure

'''
set axis for figure1, 2D
'''
'set display range'
plt.ylim(-2, 2)

'set layout'
ax = plt.gca()  # save current axis of ax
## rm right, top spine of ax
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')

## set position of xaxis, yaxis
ax.xaxis.set_ticks_position('bottom')   # set xaxis of ax as bottom spline
ax.yaxis.set_ticks_position('left') # set yaxis of as as left spine
ax.spines['bottom'].set_position(('data', 0))   # mv bottom spine of ax to line y=0
ax.spines['left'].set_position(('data', 0)) # mv left spine of ax to line x=0


'set ticklabels'
## set zorder = 2, fontsize = 12, background box = {'facecolor':'white', 'edgecolor':'none', 'alpha':0.7} for [xticklabels, yticklabels]
for label in ax.get_xticklabels() + ax.get_yticklabels() :
    label.set_zorder(2) # set layer=2 for label
    label.set_fontsize(12)  # set fontsize = 12 for label
    label.set_bbox(dict(facecolor='white', edgecolor='none', alpha=0.7))  # set background box = {'facecolor':'white', 'edgecolor':'none', 'alpha':0.7} for label # facecolor = fill-color

'show figures'
plt.show()

```