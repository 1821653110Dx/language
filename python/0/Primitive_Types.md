# number
```python
students_count = 1000
ratting = 4.99

print(10 + 3)
print(10 - 3)
print(10 * 3)
print(10 / 3)	# 10 / 3 = float
print(10 // 3)	# 10 //3 = int
print(10 % 3)	# 10 % 3 = 10 modulo余 3
print(10 ** 3)	# 10 ** 3 = 10^3

print(round(2.9))	# round() = round off to the nearest integer四舍五入
print(abs(-2.9))
```
# math module
```python
import math

print(math.ceil(2.2))	# math.ceil(2.2) = return the smallest integer >= 2.2
```

# string
## formated string
```python
first = 'mosh'
last = 'hamedani'
full = f'{len(first)} {last}'
Full = f'{len(first)} {2+2}'

print(full)	# newline print {len{first} {last} 
print(Full)	# newline print {len(first)} {2+2}

name = "Alice"  
age = 25  
print("My name is {} and I'm {} years old.".format(name, age))
```
## string method
```python
course = '  python programming'

print(course.upper()) # cp course, uppercase it | newline print
print(course.lower())
print(course.title())	# cp course, uppercase first char of each word | newline print
print(course.strip())	# cp course, rm all empty char at head and tail | newline print
print(course.find('pro'))	# return the index of the first letter of 'pro' | newline print
print(course.replace('p','j'))	#cp course, replace all 'p' with 'j' | newline print
print('pro' in course)	# print True if 'pro' in couse, otherwise False
print('swift' not in course)
```
# boolean
```python
is_published = True	
```

# excape sequences 转义字符
```python
\n
\'
\"
\\
```

```python
course = 'python \'programming'
print(course)
```


