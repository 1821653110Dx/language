# Comparision Operators比较运算符
```txt
>
>=
<
<=
==
!=
```
# Conditional Statements条件语句
```python
temperature = 35

if temperature > 30 :
	print("It's warm")
	print("Drink water")
elif temperature > 20 :
	print("It's nice")
else :
	print(print"It's cold")

print("Done")
```
# Ternary Operator三元运算符
```python
age = 22

message = 'Eligible' if age >= 18 else 'Not eligible'   # return 'Eligible' if age >= 18. Otherwise 'Not Eligible' | save to var message

print(message)
```

# LogicL Operators 逻辑运算符
```python
high_income = False
good_credit = True

if not student and (high_income or good_credit) :	
	print('Eligible')
else :
	print('Not eligible')
```

# Chaining Comparison Operators链接比较运算符
```python
age = 22
if 18 <= age  < 65 :
	print('Eligible')
```
# For Loops
```python
for number in range(3) : 	# do 3 times
	print("Attempt", number + 1, (number + 1) * '·')
```
```python
for number in range(1, 4) :	 # for each number in [1..3]
	print("Attempt", number + 1, (number + 1) * '·')
```
```python
for number in range(1, 10, 2) :		 # i <= i <= 9, d 2. for each
	print("Attempt", number + 1, (number + 1) * '·')
```
# For..Else
```python
successful = False	
for number in range(3) :	# do 3 times
	print('Attempt')	
	if successful :
		print('successful')
		break	# break loop
	else :
		print("Attempt 3 times and failed")	
```
# Nested Loops
```python
for x in range(5) :
	for  y in range(3) :
		print(f"({x}, {y})")
```
# Literables可数的
```python
## print each char in 'Python'
for x in 'Python' :	    # for each char in 'Python'
	print(x)
```
```python
## print each int in [1, 2, 3, 4]
for x in [1 ,2 ,3, 4] : 	
	print(x)
```
# While Loops
```python
number = 100

while number > 0 : 	# while number > 0
	print(number)
	number //= 2 
```	
```python
command = ''

while command.lower() != 'quit' :	
	command = input('>')    # printf '>', let usr input a str | saveto command	
	print('ECHO', command)  # print 'ECHO' and command, with ' ' as seperator, newline
```
# Infinite Loops
```python
while True :    # do forever if not break
	command = input('>')
	print('ECHO', command)
	if command.lower() = 'quit' :
		break   # break loop
```

