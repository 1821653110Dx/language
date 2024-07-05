# probability distribution概率分布
## eval the pdf of X following the std normal distribution, where var = x
> pdf = possibility density function 概率密度函数
```python
x = symbols("x")
X = stats.Normal("X", 0, 1) # def var X following the std normal distribution
stats.density(X)(x) # eval the pdf(x) of X	# pdf(x) : the pdf with x as var
```