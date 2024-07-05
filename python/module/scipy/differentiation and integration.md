# differentitaion
## $f'(x) \approx \dfrac{f{\left(x + \delta x \right)} - f{\left(x - \delta x \right)}}{2 \delta x},dx = 10^{-6} ,f'(x=1) = ?$
```python
from scipy.misc import derivative

## def f(x) = x**3 + x**2
def f(x) :    # def func f : arg = x, dvalue = null
    return x**3 + x**2

derivative(f, 1.0, dx=1e-6) # eval f'(x=1.0) with dx = 10**-6
```

## eval gradients of each number in a 1d array
```python
import numpy as np
import matplotlib.pyplot as plt

" def array x y dy dx "
x, dx = np.linspace(-3, 3, 201, retstep=True)   # create an array with 201 number uniformlt distrubuted in [-3, 3], save [array, step] to [x, dx]   # step = step between 2 points
y = x**3    # save array x**3 to y
dydx = np.gradient(y, dx)   # eval the gradient(also called derivative) of each number in array y with respect to关于 step = dx  | save the array to dydx

"generate figure1 : (x, y), (x, dydx)"
fig, ax = plt.subplots(constrained_layout = True)   # create a figure and axel, save to [fig, ax]

ax.plot(x, y, label=r'$f(x)=x^3$')  # generate plot(x, y), label = "f(x)=x^3"
ax.plot(x, dydx, '--', label=r"$f'(x)=3x^2$")   # generate plot(x, dxdy), linestyle = '--', label = "f'(x)=3x^2"

ax.grid()   # generate grid in the current figure
ax.legend() 

"show all figures"
plt.show()
```

## eval X_gradients, Y_gradients of each number in a 2d_array
> X_gradient : partial derivative偏导数 along the X-axis
```python
import numpy as np
import matplotlib.pyplot as plt

" def array: X, Y, dX, dY"
coords, ds = np.linspace(-2, 2, 21, retstep=True)   # create an array with 21 numbers uniformly distrubuting in [-2. 2], save [array, step] to [coords, ds]
X, Y = np.meshgrid(coords, coords)  # generate a meshgrid([x of base_points, y of side_points] = [X, Y]), save (x, y) of each point to [X, Y]
Z = X*np.exp(-X**2 - Y**2)
dY,dX = np.gradient(Z, ds)  # eval [X_gradient, Y_gradient] of each number in array z with respect of step=ds, save to [dX, dY]

"generate figure1: "
fig, ax = plt.subplots(constrained_layout=True) # create a figure and axel, save to [fig, ax]

ax.quiver(X, Y, dX, dY) # plot vectors( components = [dX, dY] ) at each points of a grid( (x,y) = (X, Y) ) # dX = the component of the vector along x_axis

"show all figures"
plt.show()
```
# integration
## 1 arg
### $\int\limits_{-1}^{1} e^{- x}\, dx$
- simps method
```python
import numpy as np
from scipy import integrate

x = np.linspace(-1, 1, 17)  # create an array with 17 numbers uniformly distributing in [-1, 1] | save to x
y = np.exp(-x)
integrate.simps(y, x)
```
- romb method
```python
import numpy as np
from scipy import integrate

x, dx = np.linspace(-1, 1, 1+4*2, retstep=True)   # create an arrary with 1+4*2 numbers uniformly distributing in [-1, 1], save [array, step] to [x, dx]  // 3rd arg must be odd number
y = np.exp(-x)
integrate.romb(y, dx=dx)
```
### $\int\limits_{0}^{\infty} \left(x^{12} - x^{5}\right) e^{- x^{2}}\, dx$
```python
import numpy as np
from scipy import integrate

def f(x) :  # def func f : arg = x, dvalue = none
    return np.exp(-x**2)*(x**12 - x**5)
integrate.quad(f, 0, np.inf)	# return integration value and error
```
### $\int\limits_{1}^{0} \left(a x^{2} + b x\right)\, dx$
```python
import numpy as np
from scipy import integrate

def f(x, a, b) :  # def func f : arg = [x, a, b], dvalue = none
    return a*x**2 + b*x

integrate.quad(f, 0, 1, args=(1, 2))    # 3 args, so add "agrs=(1,2)"	# # return integration value and error
```
### $\int\limits_{0}^{1}\int\limits_{x - 1}^{1 - x} \left(- x^{2} - y^{2} + 4\right)\, dx\, dy$
```python
import numpy as np
from scipy import integrate

def f(x,y) :    # def func f : arg = [x, y], dvalue = none
    return 4-x**2-y**2

integrate.dblquad(f, 0, 1, lambda x:x-1, lambda x:1-x)
```
### $\int\limits_{-1}^{1}\int\limits_{-1}^{1}\int\limits_{-1}^{1} \left(x + y + z\right)^{2}\, dx\, dy\, dz$
```python
import numpy as np
from scipy import integrate

def f(x,y,z) :  # def func f : arg = [x, y, z], dvalue = none
    return (x+y+z)**2

integrate.tplquad(f, -1, 1, lambda x:-1, lambda x:1, lambda x,y:-1, lambda x,y:1)
```