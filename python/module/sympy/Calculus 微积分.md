# derivatives$\tiny 微分（求导）$
## create unevaluated derivatives
$$
\frac{\partial^{7}}{\partial z^{4}\partial y^{2}\partial x} e^{x y z} \\
$$
	Derivative(expr, x, y, 2, z, 4)
	
##  evaluate$\tiny 求解$ derivatives
$$
\begin{align*}
	& \frac{d}{d x} \cos{\left(x \right)} \Longrightarrow - \sin{\left(x \right)} \\
	& \frac{d}{d x} e^{x^{2}} \Longrightarrow 2 x e^{x^{2}} \\
\end{align*}
$$
	diff(expr, x)
		or
	expr = Derivative(expr0, x)
	expr.doit()
$$
\frac{d^3}{d x^3} x^{4} \Longrightarrow 24 x
$$
	diff(expr, x, x, x)
		or
	diff(expr, x, 3)
		or
	expr = Derivative(expr0, x, 3)
	expr.doit()
$$
 \frac{\partial^{7}}{\partial z^{4}\partial y^{2}\partial x} e^{x y z} \Longrightarrow x^{3} y^{2} \left(x^{3} y^{3} z^{3} + 14 x^{2} y^{2} z^{2} + 52 x y z + 48\right) e^{x y z} \\
$$
	diff(expr, x, y, y, z, z, z, z)
		or
	diff(expr, x, y, 2, z, 4)
		or
	...


# integrals$\tiny 积分$
## create unevaluated integrals
$$
\int x^{x}\, dx \\
$$
	Integral(expr0,x)
## evaluate integrals
$$
\int \cos{\left(x \right)}\, dx \Longrightarrow \sin{\left(x \right)} \\
$$
	integrate(expr,x)
		or
	expr = Integral(expr0, x)
	expr.doit()

$$
\int_{0}^{\infty} e^{- x}\, dx \Longrightarrow 1 \\
$$
	integrate(expr, (x, 0, oo))
		or
	...

$$
\int_{-\infty}^{\infty}\int_{-\infty}^{\infty} e^{- x^{2} - y^{2}}\, dx\, dy \Longrightarrow \pi \\
$$
	integrate(expr0, (x, -oo, oo), (y, -oo, oo))
		or
	...

# Limits
## create unevaluated counterpart$\tiny 对应的式子$
$$
	\lim_{x \to x0} f{\left(x \right)} \\
$$
	Limit(expr, x, x0, '+-')

## evaluate
$$
\begin{align*}
	& \lim_{x \to 0}\left(\frac{\sin{\left(x \right)}}{x}\right) \Longrightarrow 1 \\
\end{align*}
$$
	limit(expr0, x, 0, '+-')
		or
	expr = Limit(expr0, x, 0, '+-')
	expr.doit()
	
$$
\begin{align*}
& \lim_{x \to 0^+} \frac{1}{x} \Longrightarrow \infty \\
\end{align*}
$$
	limit(expr, x, 0,'+')

$$
\begin{align*}
& \lim_{x \to 0^-} \frac{1}{x} \Longrightarrow -\infty \\
\end{align*}
$$
	limit(expr, x, 0,'-')
	
# series expansion$\tiny 级数展开$
Through series expansion, complex functions can be approximated to be the sum of polynomials, which are much easier to compute
$$
\begin{align*}
& \text{the 4th order expansion of }e^{\sin{\left(x \right)}} \Longrightarrow 1 + x + \frac{x^{2}}{2} + O\left(x^{4}\right) \\
& \qquad O\left(x^{4}\right) \text{ is a remained term$\tiny \text{余项}$ including the reamined terms with exponents $ \ge $ 4, value of which $ \approx $ 0}
\end{align*}
$$
	expr.series(x, 0, 4)
	
$$
\begin{align*}
& \text{the Taylor series expansion of } e^{x - 6} \text{ at x = 6} \Longrightarrow -5 + \frac{\left(x - 6\right)^{2}}{2} + \frac{\left(x - 6\right)^{3}}{6} + \frac{\left(x - 6\right)^{4}}{24} + \frac{\left(x - 6\right)^{5}}{120} + x + O\left(\left(x - 6\right)^{6}; x\rightarrow 6\right) \\
& \qquad O\left(\left(x - 6\right)^{6}; x\rightarrow 6\right) \text{is a remained term including the remained terms with exponents} \ge 6
\end{align*}
$$
	expr.series(x, x0=6)
	
# laplace
	LaplaceTransform(*args)
	
	sympy.laplace_transform(f, t, s, noconds=True)
> its quicker version :
> def L(f):
> $\quad$return sympy.laplace_transform(f, t, s, noconds=True)
	
# inverse laplace
	InverseLaplaceTransform(*args)
	
	inverse_laplace_transform(F, s, t)
> its quicker version :
> def invL(F):
> $\quad$ return sympy.inverse_laplace_transform(F, s, t)

