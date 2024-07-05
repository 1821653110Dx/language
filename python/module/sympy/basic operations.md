# Substitution
$$\cos x + 1 \Longrightarrow  \cos y + 1$$
```python
expr = cos(x) + 1
expr.subs(x, y)
```

$$x = 0, \cos x + 1 = ?$$
```python
expr = cos(x) + 1
expr.subs(x, 0)
```

$$ x^y \Longrightarrow x^{x^{x^x}} $$
```python
expr = x**y
expr = expr.subs(y,x**y)
expr = expr.subs(y,x**x)
```

$$
\sin 2x + \cos 2x \Longrightarrow 2 \sin x \cos x + \cos 2x
$$
```python
expr = sin(2*x) = cos(2*x)
expr = expr.subs(sin(2*x), 2*sin(x)*cos(x))
```

$$
[x,y,z] = [2,4,0] ; x^3 + 4xy -z = ?
$$
```python
expr = x**3 + 4*x*y - z
expr.subs([(x,2), (y,4), (z,0)])
```

$$
expr = y^4 - 4x^3 + 4y^2 - 2x + 3, \text{replace all instances of x with an even power(偶次幂) with y that has the same even power}
$$
```python
expr = x**4 - 4*x**3 + 4*x**2 - 2*x + 3
expr.subs((x**i, y**i) for i in range(5) if i%2 == 0)
```

# extract num, denom
```python
num, denom = ratsimp(expr).as_numer_denom()
```

# extract the left/right part of a eq
```python
eq.lhs
eq.rhs
```

# converting str to sympy expr
```python
str_expr = input()
expr = sympify(str_expr)
expr.subs(x,2)
```

# evalf
## evaluate a numerical expr into a floating point number
```python
expr = sqrt(5)
expr.evalf()
```

## compute first 100 digits of $\pi$
```python
pi.evalf(100)
```

## $x = 2.4, \text{the floating point value of} \cos 2x = ?$ 
```python
expr = cos(2*x)
expr.evalf(subs = {x: 2.4})	# this method not suitable for a expression with multi-args
```

# lambdify
```python
import numpy as np
a = np.arange(10)   # create a sequence : [0,9], d 1 | save to a
f = lambdify(x, sin(x), "numpy")    # create func f(x) = numpy.sin(x)
print(f(x = a))
```


