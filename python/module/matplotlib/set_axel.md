```python
import matplotlib.pyplot as plt
import numpy as np

'def arg x'
x = np.linspace(-3,3,50)   # create an array with 50 numbers unifomly distributed in [-3,3] | save to x

'def func y1(x), y2(x)'
y1 = 2*x +1
y2 = x**2

'generate 2Dplots in figure1: y1(x), y2(x)'
fig1 = plt.figure(num=1)	# create figure1 | save to fig1
plt.plot(x,y1,color="red", linewidth=1.0, linestyle='--')    # generate y1(x), [color, linewidth, linestyle] = [red, 1.0, --]
plt.plot(x,y2)   # generate y2(x)


'''
set axis for figure1, 2D
'''
'set display range'
plt.xlim((-1, 2))
plt.ylim((-2, 3))

'set layout'
ax = plt.gca()  # save current axis to ax

## rm right,top spines of ax
ax.spines['right'].set_color('none') 
ax.spines['top'].set_color('none')

## set position of xaxis, yaxis
ax.xaxis.set_ticks_position('bottom')   # set x-axis of ax as botom spine
ax.yaxis.set_ticks_position('left') # set y-axis of ax as left spine
ax.spines['bottom'].set_position(('data', 0))  # mv bottom spine of ax to line y=0
ax.spines['left'].set_position(('data', 0))  # mv left spine of ax to line x=0

'set axislabels'
plt.xlabel('I am X')
plt.ylabel('I am y')

'set tickslabels刻度标签'
ticks1 = np.linspace(-1,2,5)    # set ticks1 = array with 5 numbers uniformly distributed in [-1,2]
plt.xticks(ticks1)  # set the ticklabels of x-axis as ticks1

plt.yticks([-2, -1.8, -1, 1.22, 3], ['really bad', 'bad', 'normal', 'good', 'really good'])    # dispaly ['really bad', 'bad', 'normal', 'good', 'really good'] at [-2, -1.8, -1, 1.22, 3] of y-axis


'show figures '
plt.show()
```