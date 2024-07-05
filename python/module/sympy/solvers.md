# linear quations
linear equations have only real solutions
## 1 var
$2x-4=0$
```python
from sympy import *
## def vars
x = symbols('x')

## def exprs
expr = 2*x - 4

## solution(return a list, not a value)
pprint(solve(expr, x))
```
## 2vars
$$\begin{align*}2x-y-3 &= 0 \\ 3x+y-7 &= 0\end{align*}$$
```python
from sympy import *
## def vars
x,y = symbols('x y')

## expr
eq = Matrix(([2,-1,3], [3,1,7]))

## solution(return a finitesite, not original py_type)
pprint(linsolve(eq, [x,y]))
## solution(return a tuple)
pprint(linsolve(eq, [x,y]).args[0])
```
## 3 vars
$$
\begin{align*}
    x+y+z-2 &= 0 \\
    2x - y + z + 1 &= 0\\
    x + 2y + 2z - 3 &= 0
\end{align*}
$$
```python
from sympy import *
## def vars
x,y,z = symbols('x y z')

## expr
eq = Matrix(([1,1,1,2],[2,-1,1,-1],[1,2,2,3]))

## solution(return a finitesite, not original py_type)
pprint(linsolve(eq, [x,y,z]))
## solution(return a tuple)
pprint(linsolve(eq, [x,y,z]).args[0])
```

# non linear equation
nonlinsolve can return real/complex solution
-c = $-\infty$
## in simple form
$x^2 - x = 0, x=?$
```python
from sympy import *

# def vars
x = symbols('x')

## expr
eq = x**2 - x

## Real solution(return a list, not a value)
pprint(solve(eq,x,domain=S.Reals))
## Complex solution
pprint(solve(eq,x))
## img of 1st solution of Complex solution
pprint(img(solve(eq,x)[0]))
```
$$
\begin{align*}
    x^2 + y^3 - 2 &= 0 \\
    x^3 + y^3 &= 0
\end{align*}
$$
```python
from sympy import *

## def vars
x,y = symbols('x y')

## expr
eq = [x**2 + y**3 - 2 , x**3 + y**3]

## solution(return a finiteset)
pprint(nonlinsolve(eq, [x,y]))
## solution(return a tuple)
pprint(nonlinsolve(eq, [x,y]).args)
```
## in form of LambertW(such as functions with $e^{x}$)
$$
x^{2} - y^{2} e^{- x}
$$
- get x(y)(return a list with dict)
	- solve(expr0,x,dict=True)
- y(x)
	- solve(expr0,y,dict=True)
- solution of x, y
	- - solve(expr0,[x,y],dict=True)

## when equations have trigonometric functions
$$
\begin{equation*}
		\begin{cases}
			\sin{\left(x + y \right)} = 0 \\
			\cos{\left(x - y \right)} = 0
		\end{cases}
		\Longrightarrow \left[ \left\{ x : - \frac{3 \pi}{4}, \  y : \frac{3 \pi}{4}\right\}, \  \left\{ x : - \frac{\pi}{4}, \  y : \frac{\pi}{4}\right\}, \  \left\{ x : \frac{\pi}{4}, \  y : \frac{3 \pi}{4}\right\}, \  \left\{ x : \frac{3 \pi}{4}, \  y : \frac{\pi}{4}\right\}\right] \\
\end{equation*}
$$
	solve([expr0,expr1],[y,x],dict=True)
# differential equation
$$
f(x) - 2 f'(x) + f''(x) = sin(x)
$$
```python
from sympy import *

## def arguments, func
x = symbols('x')
f = symbols('f', cls=Function)

## expr
expr  = Eq(f(x) - 2*f(x).diff(x) + f(x).diff(x, x), sin(x))

## solution(return a equalty)
pprint(dsolve(expr, f(x)))
## solution(return the value of f(x))
pprint(dsolve(expr, f(x)).args[1])
```

# inequation
$$x^2 -3 > 0, x=?$$
```python
from sympy import *

x = symbols('x')

b = x**2 - 3 > 0

c = solve(b, x, domain=S.Reals)

pprint(c)
```
$$|x-2|<5, x=?$$
```python
from sympy import *

x = symbols('x')

b = Abs(x-2) <5

c = solve(b, x, domain=S.Reals)

pprint(c)
```
$$x > x^2,x + x^2 < 5\\x=?$$
```python
from sympy import *

x, y = symbols('x y')

a = x > x**2
b = x + x**2 < 5

c = solve((a,b),x, domain=S.Reals)

pprint(c)
```