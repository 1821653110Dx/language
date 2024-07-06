# what's the 插值

已知未知函数的n个数据点，求出该函数的近似函数（插值）

# 多项式Polynominal

## create a Polynomidnal : 2 - 3x + x^2 = \left(x - 2\right) \left(x - 1\right)

```python
from numpy.polynomial import Polynomial as P
"创建一个多项式 based on the 系数 of [x0，x1，x2] = [2, -3, 1]"
p = P([2, -3, 1]) # create a polynomial based on the coefficient of [x0, x1, x2] = [2, -3, 1] | save to p

"创建一个多项式 from roots [1, 2]"
p = P.fromroots([1, 2]) # create a polynomial from roots [1, 2]
```

## eval the roots of polynomial p

```py
"eval the roots of polynomial p"
p.roots()
```

## eval polynomial p(x=[0, 1, 1.5])

```py
"eval polynomial p(x = [0, 1, 1.5])"
p(np.array([0, 1, 1.5])) # eval polynomial p(x = [0, 1, 1.5])
```

## division 除法

- ##### 多项式 除 标量: (x - 1)(x - 2) / 2
    
- ```py
    p / 2
    ```
    
- ##### 多项式 除 多项式: (x - 2)(x -1) // (x - 1)
    
- ```py
    p2 = P.fromroots([1])   # create a polynomial from roots [1] | save to p2
    p // p2
    ```
    

## 微分differential

微分与求导的关系:求导 =求出某点切线的斜率=

\dfrac{\text{微分}dy}{dx}

```py
p.deriv()   # eval the differential of polynomial p
```

## 积分intergrate

```py
p.integ()
```

## create a chebyshev polynomial base切比雪夫基底多项式:2.5 T_{0}{\left(x \right)} - 3 T_{1}{\left(x \right)} + 0.5 T_{2}{\left(x \right)}

```py
from numpy.polynomial import Chebyshev as T
ch = T([2.5, -3. , .5])# create a chebyshev polynomial base based on the coefficient of [T0, T1, T2] = [2.5, -3. , .5]
```

# 多项式插值polynomial interpolation

已知未知函数的n个数据点，求出该函数的n-1次近似函数（插值函数）

n个数据点对应n-1次插值多项式

## 求出(x,y)的3次插值函数, x = [1,2,4,5], y = [1,-1,4,5]

```py
from numpy.polynomial import Polynomial as P

"def (x,y) set"
x = np.array([1,2,4,5])  # create array x [1,2,4,5]
y = np.array([1,-1,4,5])    # create array y [1,-1,4,5]

"定义多项式插值的次数 def the degree of polynomial interpolation"
deg = len(x) - 1

"求出关于(x,y)集的3次插值函数"
p = P.fit(x, y, deg)    # eval the interpolation_func p of (x,y), deg = deg
```

## 求出之前求得的插值函数各项的系数

```py
P.convert().coef    # eval the coefficient of interpolation_func P
```

## 绘制插值点集和其对应的插值函数

```py
import matplotlib.pyplot as plt
import numpy as np
from numpy.polynomial import Polynomial as P

"def (x,y), (x2, p(x2))"
## create array x, y
x = np.array([1, 2, 4, 5])  # create array x [1, 2, 4, 5]
y = np.array([1, -1, 4, 5])  # create array y [1, -1, 4, 5]

## create x2, p(x2)
x2 = np.linspace(x.min(), x.max(), 100) # create an array with 100 numbers uniformly distributing in [x.min(), x.max()] | save to x2
deg = len(x) - 1
p = P.fit(x, y, deg)    # eval the polynomial_interpolation_func p for (x,y), deg = deg

"generate figure1"
fig, ax = plt.subplots(constrained_layout=True)    # create a figure and axel | save to fig, ax

ax.plot(x, y, 'o', label="data points") # plot (x, y), color = orange, label = "data points"
ax.plot(x2, p(x2), "b", label="interpolation")  # plot (x2, p(x2)), color = blue, label = "interpolation"

## set labels of axis_{x, y} = [x, y]
ax.set_xlabel("x")
ax.set_ylabel("y")

ax.legend() # generate legend

"show figures"
fig.show()
```

## 龙格现象

插值函数相对于原函数发生了震荡

```py
import matplotlib.pyplot as plt
import numpy as np
from numpy.polynomial import Polynomial as P

"def (x1, runge(x1)), (x2, runge(x2)), (x2, p(x2))"
x1 = np.linspace(-1, 1, 9)    # create an array with 9 numbers uniformly distributing in [-1, 1] | save to x1
x2 = np.linspace(-1, 1, 300)    # create an array with 300 numbers uniformly distributing in [-1, 1] | save to x1

def runge(x) :
    return 1 / (25 * x**2 + 1)
p = P.fit(x1, runge(x1), 9)    # eval the polynomial_interpolation_func p for (x1, runge(x1)), deg = 9

"generate figure 1"
fig, ax = plt.subplots(constrained_layout=True)    # create a figure and axel | save to fig, ax

ax.plot(x1, runge(x1), 'o', label="data points")    # plot(x1, runge(x1)), color = forestgreen, label="data points"
ax.plot(x2, runge(x2), 'k--', label="original function")#     plot(x2, runge(x2)), color = dark, line_style=--, lable="original function"
ax.plot(x2, p(x2), 'b', label="9th order interpolation_function")

## set labels of axis_{x, y} = [x, y]
ax.set_xlabel("x")
ax.set_ylabel("y")

ax.legend() # generate legend

"show figures"
fig.show()
```

# 样条插值 spline interpolation

已知原函数的n个数据点，这些数据点构成n-1个区间，通过拼接这些区间的k次(由函数或用户决定)多项式插值函数来求得原函数的近似函数(插值函数）

## 3th order interpolation func of f(x) = \dfrac{1}{25x^2 + 1}

```python
import matplotlib.pyplot as plt
import numpy as np
from scipy import interpolate


"def (x1, runge(x1)), (x2, runge(x2)), (x2, y2)"
x1 = np.linspace(-1, 1, 9)    # create an array with 9 numbers uniformly distribuing in [-1,1] | saveto x1
x2 = np.linspace(-1, 1, 300)    # create an array with 300 numbers uniformly distributing in [-1, 1] | save to x2

def runge(x) : # def func runge : arg = x, dvalue = null
    return 1 / (25 * x**2 + 1)
spl = interpolate.InterpolatedUnivariateSpline(x1, runge(x1))    # create a spline_inerpolation_func( spl(x) ) for (x1, runge(x1)), deg = 3
y2 = spl(x2)    # eval array y2 using spl(x2)

"generate figure1"
fig, ax = plt.subplots(constrained_layout=True)    # create a figure and axel | save to fig, ax
ax.plot(x1,runge(x1),'o', label="data points")    # plot (x1, runge(x1)), color = forestgreen, label="data points"
ax.plot(x2, runge(x2), 'k--',  label="oranginal function")    # plot (x2, runge(x2)), color = dark, line_type = --, label="oranginal function"
ax.plot(x2, y2, 'b', label="3rd order spline")    # plot (x2, y2), color=blue, label="3rd order spline"

## set labels of axel_{x,y} = [x, y]
ax.set_xlabel('x')
ax.set_ylabel('y')

ax.legend()    # generate legend

"show figures"
fig.show()
```