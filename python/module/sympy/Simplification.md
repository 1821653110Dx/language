# automatically arrive at the simplest expr
    simplify()
# rational expr$\tiny \text{有理式}$
## expand
$$
\begin{gather*}
    (x + 1)^2 \Longrightarrow x^{2} + 2 x + 1 \\
    \left(x - 3\right) \left(x + 2\right) \Longrightarrow x^{2} - x - 6 \\
    - x \left(x - 1\right) + \left(x - 2\right) \left(x + 1\right) \Longrightarrow  -2
\end{gather*}
$$
    expand(expr)
## factor$\tiny 因式分解$
$$
    \begin{gather*}
        x^{3} - x^{2} + x - 1 \Longrightarrow \left(x - 1\right) \left(x^{2} + 1\right) \\
        x^{2} z + 4 x y z + 4 y^{2} z \Longrightarrow z \left(x + 2 y\right)^{2}  \\
        \frac{y^{2} - 2 y z + z^{2}}{x - 1} \Longrightarrow \frac{\left(y - z\right)^{2}}{x - 1}
    \end{gather*}
$$
    factor(expr)
## collect  exponents$\tiny 指数$ with the same power$\tiny 幂$
$$
\begin{gather*}
    x^{3} - x^{2} z + 2 x^{2} + x y + x - 3 \Longrightarrow x^{3} + x^{2} \cdot \left(2 - z\right) + x \left(y + 1\right) - 3
\end{gather*}
$$
    collect(expr,  exponoents)
###  give the cofficient${\tiny 系数}$ of $x^n$in expr
    expr.coeff(x, n)

## transform all fractions into a canonical$\tiny 典型的$ fraction, where num and den have no common factors$\tiny 公因式$
$$
\begin{gather*}
    \frac{x^{2} + 2 x + 1}{x^{2} + x} \Longrightarrow \frac{x + 1}{x} \\
    \frac{\frac{3 x}{2} - 2}{x - 4} + \frac{1}{x} \Longrightarrow \frac{3 x^{2} - 2 x - 8}{2 x^{2} - 8 x} \\
    \frac{x y^{2} - 2 x y z + x z^{2} + y^{2} - 2 y z + z^{2}}{x^{2} - 1} \Longrightarrow \frac{y^{2} - 2 y z + z^{2}}{x - 1}
\end{gather*}
$$
    cancel(expr)
## transform all fractions into a non-canonical$\tiny 典型的$ fraction, where num and den have  common factors$\tiny 公因式$$
$$ 
\frac{y}{y + 1} - \frac{y}{\left(x + 1\right) \left(y + 1\right)} \Longrightarrow  \frac{x y}{\left(x + 1\right) \left(y + 1\right)} 
$$
	together(expr)
	
## decomposite$\tiny 分解$ a rational fraction
- single var
	$$
		\begin{gather*}
			\frac{4 x^{3} + 21 x^{2} + 10 x + 12}{x^{4} + 5 x^{3} + 5 x^{2} + 4 x} \Longrightarrow \frac{2 x - 1}{x^{2} + x + 1} - \frac{1}{x + 4} + \frac{3}{x}
		\end{gather*}
	$$
	- apart(expr)
- multi vars
	- apart(expr, deposite_by_which_var/expr)
# Trigonometric$\tiny 三角函数$ Simplification
## simplify
$$
\begin{align*}
	& \sin^{2}{\left(x \right)} + \cos^{2}{\left(x \right)} \Longrightarrow	1 \\
	& \sin^{4}{\left(x \right)} - 2 \sin^{2}{\left(x \right)} \cos^{2}{\left(x \right)} + \cos^{4}{\left(x \right)} \Longrightarrow \frac{\cos{\left(4 x \right)}}{2} + \frac{1}{2} \\
	& \sinh^{2}{\left(x \right)} + \cosh^{2}{\left(x \right)} \Longrightarrow \cosh{\left(2 x \right)} \\
	& \frac{\sinh{\left(x \right)}}{\tanh{\left(x \right)}} \Longrightarrow \cosh{\left(x \right)} \\
\end{align*}
$$
	trigsimp(expr)
## expand
$$
\begin{align*}
	& \sin{\left(x + y \right)} \Longrightarrow \sin{\left(x \right)} \cos{\left(y \right)} + \sin{\left(y \right)} \cos{\left(x \right)} \\
	& \tan{\left(2 x \right)} \Longrightarrow \frac{2 \tan{\left(x \right)}}{1 - \tan^{2}{\left(x \right)}} \\
\end{align*}
$$
	expand_trig(expr)

# Powers
## simplify
$$
\begin{align*}
	& x^{a} x^{b} \Longrightarrow x^{a + b}	\tag{Always True} \\
	& x^{a} y^{a} \Longrightarrow (xy)^{a} \tag{x,y > 0, a$\in$ $ \mathbb{R} $} \\
\end{align*}
$$
	powsimp(expr)
## expand
- expand exponent$\tiny 指数$
$$
x^{a + b} \Longrightarrow x^{a} x^{b} \\
$$
	expand_power_exp(expr)
- expand base$\tiny 基底$
$$
\left(x y\right)^{a} \Longrightarrow x^{a} y^{a} \\
$$
	expand_power_base(expr)

##  logarithms$\tiny 对数$
- expand
$$
\begin{align*}
& \log{\left(x y \right)} \Longrightarrow \log{\left(x \right)} + \log{\left(y \right)} \\
& \log{\left(\frac{x}{y} \right)} \Longrightarrow \log{\left(x \right)} - \log{\left(y \right)} \\
& \log{\left(x^{2} \right)} \Longrightarrow 2 \log{\left(x \right)} \\
& \log{\left(x^{n} \right)} \Longrightarrow n \log{\left(x \right)} \\
\end{align*}
$$
	expand_log(expr)

- combine
$$
\begin{align*}
& \log{\left(x \right)} + \log{\left(y \right)} \Longrightarrow \log{\left(x y \right)} \\
& n \log{\left(x \right)} \Longrightarrow \log{\left(x^{n} \right)} \\
\end{align*}
$$
	logcombine(expr)

# special functions
## create unevaluated functions
$$
\begin{align*}
	& \text{factorial(n) factorial $\tiny \text{阶乘}$ function} && n! \\
	& \text{binomial(n,k) binomial$\tiny \text{二项式}$ coefficient function}  && {\binom{n}{k}} \\
	& \text{gamma(z) gamma function}  && \Gamma\left(z\right) \\
	& \text{hyper([1,2], [3], z) generalized$\tiny \text{广义}$ hypergeometric$\tiny \text{超几何}$ function}  && {{}_{2}F_{1}\left(\begin{matrix} 1, 2 \\ 3 \end{matrix}\middle| {z} \right)} \\
	& \text{meijerg([[1],[1]], [[1], []], -z) Meijer G-function} && {G_{2, 1}^{1, 1}\left(\begin{matrix} 1 & 1 \\1 &  \end{matrix} \middle| {- z} \right)} \\
\end{align*}
$$

## rewrite special functions in terms of one another
$$
\begin{align*}
	& \tan{\left(x \right)} \Longrightarrow \frac{\cos{\left(x - \frac{\pi}{2} \right)}}{\cos{\left(x \right)}} \\
	& x! \Longrightarrow \Gamma\left(x + 1\right) \\
\end{align*}
$$
	tan(x).rewrite(cos)
	factorial(x).rewrite(gamma)
## expand
- normal expand
$$
\Gamma\left(x + 3\right) \Longrightarrow x \left(x + 1\right) \left(x + 2\right) \Gamma\left(x\right) \\
$$
	expand_func(expr)
- hypergeometric expand 
$$
{{}_{2}F_{1}\left(\begin{matrix} 1, 1 \\ 2 \end{matrix}\middle| {z} \right)} \Longrightarrow - \frac{\log{\left(1 - z \right)}}{z} \\
{G_{2, 1}^{1, 1}\left(\begin{matrix} 1 & 1 \\1 &  \end{matrix} \middle| {- z} \right)} \Longrightarrow e^{\frac{1}{z}} \\
$$
hyperexpand(expr)
## simplify combinatorial$\tiny 组合$ special functions 
-  with interger argument
$$
\begin{align*}
& \frac{n!}{\left(n - 3\right)!} \Longrightarrow n \left(n - 2\right) \left(n - 1\right) \\
& \frac{{\binom{n + 1}{k + 1}}}{{\binom{n}{k}}} \Longrightarrow \frac{n + 1}{k + 1} \\
\end{align*}
$$
	combsimp(expr)
- without interger argument
$$
\Gamma\left(x\right) \Gamma\left(1 - x\right) \Longrightarrow \frac{\pi}{\sin{\left(\pi x \right)}} \\
$$
	gammasimp(expr)

