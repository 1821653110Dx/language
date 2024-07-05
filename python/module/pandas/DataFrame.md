# introduction
```python
import pandas

df = pandas.read_csv('../data/gapminder.csv', sep = ',')	# read data of  csv'../data/gapminder.csv' using ',' as sep | save to df
print(df.head())	# cp first 5 rows of DataFrame df | newline print
print(df.shape)	# cp shape of df  df | echo
print(df.columns) # cp columns of df | echo
print(df.dtypes) # cp dtype of each column of df | echo
print(df.info())	# echo more infor about df
```

# check the specific col, row and cell
## col
```python
```