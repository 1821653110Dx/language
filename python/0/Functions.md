# Custom Functions
## Not Return a value
### normal
```python
def greet() :   # def func : arg = null	
	print('Hi there')	

greet()
```
#### Arguments参数
```python
def greet(first_name, last_name) :	# def func greet : arg = [first_name, last_name], dvalue = null
	print(f"Hi {first_name} {last_name}")

greet('Mosh', 'Hamedani')
greet('John', 'Smith')
```
## Return a value
```python
def get_greeting(name) :
	return f"Hi {name}"

message = get_greeting("Mosh")
```
```python
def increment(number, by = 1) : # def func increment : arg = [number, by], dvalue = [null, 1]
	return number + by 

print(increment(number = 2))    # call increment(number = 2) | newline print return
print(increment(2,5))
```
# \*arg
```python
def multiply(*numbers) :    # def func multiply : arg = empty tuple numbers
    ## save the product of each number in variable arg numbers
	total = 1	
	for number in numbers : # for each number in variable arg numbers :
		total *= number		

	return total	

print(multiply(2, 3, 4, 5))
```
# \*\*args
```python
def save_user(**user) : 	# def func save_user : arg = empty dict user
	print(user)

save_user(id=1, name='John', age=22) 
```
