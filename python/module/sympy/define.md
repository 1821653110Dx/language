# vars
```python
import sympy

x = symbols('x',  real = True, integer=True, positive=True)

# def vars: sym(x_{1..5}){positive, real}
vars = symbols('x_1:5')

# def var : a_1
a_1 = symbols("a_1")

# def x, y in (0,5)
x, y = symbols('x y', domain=(0, 5))
```

# func
```python
## def f(x)
# def func
f = symbols('f', cls=Function)
# def arguments
x = symbols('x', real = True, integer=True, positive=True)
# create f(x)
func = f(x)
```
# special const
E 纳皮尔常数e
I 虚数单位
lamda $\lambda$
# unicode
$\delta$ = \u2206