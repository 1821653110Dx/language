# args
## get all args
	expr.args
## get all args in the form of $x^2$
	expr.args[2]
## get args of $y^2$
	y**2.args

# prevent expression evaluation
$$
x + x \Longrightarrow x + x
$$
	sympify('x + x', evaluate=False)
	x + UnevaluatedExpr(x)
## continue the evaluation
	expr.doit()
