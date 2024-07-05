# 概率分布probability distribution

正态分布N($\mu$,$\sigma^2$)中$\mu$=数学期望, $\sigma^2$=方差,$\sigma$=标准差(standard deviation)

标准正态分布N（0，1）

## respectively eval the mean, median中位数, standard deviation, variance of the standard normal distribution标准正态分布

```py
from scipy import stats


x = stats.norm(0,1)    # create a normal_distribution with [u, sigma] = [0, 1] | save to x

x.mean()    # eval the mean of normal distribution x
x.median()    # eval the median of normal distribution x
x.std()    # eval the standard deviation(std) of distribution x
x.var()# eval the variance of distribution x
```

## describe the nobs数据量, minmax最大值和最小值, mean算术平均值, variance方差, skewness偏度, kurtosis峰度 of array x

```python
from scipy import stats

print(stats.describe(x))    # print the description of array x
```

## eval the mean, variance, skewness, kurtosis of the standard normal distribution标准正态分布

```py
from scipy import stats
x = stats.norm(0,1)    # create a normal_distribution with [u,sigma]=[0,1] | save to x # create standard_normal_distribution x
x.stats('mvsk')    # eval the [mean, variance, skewness, kurtosis] of normal_distribution x
```

## eval the probability density function values

```py
from scipy import stats

x = stats.norm(0,1) # create a normal_distributio with [u,sigma] = [0,1] | save to x

x.pdf([0, 1])   # eval the probability_density_function values of normal_distribution x at [0, 1]
```

## method rsv

```py
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt
init_printing(use_unicode=True)

X = stats.norm(0,1)
" def array: x "
x = np.linspace(X.ppf(0.01), X.ppf(0.99), num=100)  # create an array with 100 numbers uniformly distributing in [X.ppf(0,01), X.ppf(0.99)] |  save to x

"generate figure1: "
fig, ax = plt.subplots(constrained_layout=True)    # create a figure and axel, save to [fig, ax]

np.random.seed(0)
ax.hist(X.rvs(5000), label="samples", density=True, bins=30, alpha=0.5)   # randomly extract抽取 5000 samples from random_var X | divide these samples into 30 intervals区间 and eval their density, plot the hist(label="samples", alpha = 0.5) # density = samples of an interval / all samples
ax.plot(x, X.pdf(x), "k", label="PDF")  # plot (x, X.pdf(x)), color=dark, label='pdf'

ax.legend() # display labels

"show figures"
plt.show()
```