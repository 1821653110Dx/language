# Lists
```Python
letters = ['a', 'b', 'c']
matrix = [[0, 1], [2, 3]]	
zeros = [0] * 5		
conbined = zeros + letters	# append items of letters to zeros | save to combined
numbers = list(range(20))
chars = list("Hello World")	# create a list with chars of 'Hello World'

print(len(chars))	
```
# Accessing Items 访问列表元素
```python
letters = ['a', 'b', 'c', 'd']
letters[0] = "A" 	# exchange letters[0] with A 

print(letters[0])	
print(letters[-1])	
print(letters[: 3])	
print(letters[1:3])	
print(letters[1:-1])	
```
```python
numbers = list(range(20))

print(numbers[::2])	# print every 2nd item of numbers
print(numbers[::-1])	# print all the items of numbers in reverse order
```
# Unpacking Lists
## method 1 (the number of varables before the '= numbers' must equal to the number of the items of numbers)
```python
numbers = [1, 2, 3]
first, second, third = numbers	o
```
## method 2 (the number of varables before the '= numbers' don't necessarily equal to the number of items of numbers)
```python
# situation 1
numbers = [1, 2, 3, 4, 4, 4, 4, 4, 4]
first, second, *other = numbers	# other = numbers[2:]
print(first, second)

# situation 2
numbers = [1, 2, 3, 4, 4, 4, 4, 4, 4]
first, *other, last = numbers	# first = numbers[0]
				# last = numbers[-1]
				# other = number[1:-2]

print(first, last)
print(other)
```
# Looping over Lists
```python
letters = ['a', 'b', 'c']

for index, letter in enumerate(letters) :	# for each index and letter in letters
    print(index,letter)	# print all index and letter
```
# Adding/Removing items
```python
letters = ['a', 'b', 'c']

# Add
letters.append('d')
letters.insert(0,'-')	# insert '-' at index 0 of letters
# Remove a item
letters.pop()	# remove last item for letters
letters.pop(0)	# rm item at index 0 for letters
letters.remove('b')	# rm first 'b' for letters

# remove a range of items
del letters[0:3]	# del items within the index range from 0 to 2 for letters

# remove all the items
letters.clear() # clear letters
```
# Finding Items
```python
letters = ['a', 'b', 'c']

print(letters.count('d'))	# counts the num of 'd' | newline print

if 'd' in letters :
    print(letters.index('a'))	# get the index of 'a' for letters | newline print
```
# Sorting Lists
## basic
```python
numbers = [3, 51, 2, 8, 6]

numbers.sort() # sort items in a-order for numbers
numbers.sort(reverse=True)	# sort items in d-order for numbers
sorted(numbers)		# cp items of numbers, sort in a-order
sorted(numbers, reverse=True)
```
## topple
```python
items = [
	('product1', 10),
	('product2', 9),
	('product3', 12),
	]


items.sort(key=lambda x:x[1])	# sort items in a-order by elements at col1 for items  # col1 = 2nd col
print(items)
```
# Map Function
```python
items = [
	('product1', 10),
	('product2', 9),
	('product3', 12),
	]

## print every items at col1 of items
x = map(lambda item: item[1], items)	# get the map of col1 of items | save to x
for item in x : 	# for each item in items corresponding to map x
    print(item)	
```
```python
items = [
	('product1', 10),
	('product2', 9),
	('product3', 12),
	]

prices = list(map(lambda item: item[1], items))		# create a list with items at col1 of items | save to prices

print(prices)
```
# Filter Function
```python
items = [
	('product1', 10),
	('product2', 9),
	('product3', 12),
	]

filtered = list(filter(lambda item: item[1] >= 10, items))	# create a list with items whose index1 elements >= 10 from list items | save to filtered

print(filtered)
```
# List Comprehension
```python
items = [
	('product1', 10),
	('product2', 9),
	('product3', 12),
	]

prices = [item[1] for item in items]	# for each item in items, append element at index1 to a list | save the list to prices
filtered = [item[1] for item in items if item[1] >= 10]	# for each item in items, if element at index1 >= 10, append the element to a list | save the list to filtered
```
# zip function
```python
list1 = [1, 2, 3]
list2 = [10, 10, 10]

print(zip(list1, list2))

print(list(zip(list1, list2, 'abc')))	# create a list whose item at index x = (list1[x], list2[x], 'abc'[x]) | newline print
```
# Stacks
stacks includes list
```python
browsing_session = []
browsing_session.append(1)	
browsing_session.pop()		# rm last item for browsing_session
browsing_session[-1]	# git the top item of browsing_session
if not browsing_session :	# if browsing_session not empty
    print('empty')
```
# Queues
```python
from collections import deque	# for deque, every item is continuous in memory

queue = deque([])	# queue = an empty deque
queue.append(1)		# append '1' to queue
queue.append(2)
queue.append(3)
queue.popleft()		# remove 1st item of queue
if not queue :
	print(queue)
```
# Tuples元组
```python
point = (1, 2, 3)	# save (1, 2, 3) t Point
Point = (1, 2) + (3, 4)	# tuple Point = (1, 2, 3, 4)
ppoint = (1, 2) * 3	# tuple ppoint = (1, 2, 1, 2, 1, 2)
pppoint = tuple([1, 2])	# convert [1, 2] to tuple | save to ppoint
p4oint = tuple('hello world')	# p4oint = ('h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd')

x, y, z = point	
if 10 in point :
	print('exists')

print(point[0:2])
```
# Swapping Variables
```python
x = 10
y = 11

x, y = y, x	# swap the values between x and y
```
# Arrays
```python
from array import array

number = array('i', [1, 2, 3])	# create an array with ('i', [1, 2, 3]) | save to number

number[0]
number.append(0)	# for array, type of item you append must = type of last item
number.pop()
number[0] = 'a'		# for array, type of the left must = type of the right
```

# Sets
 we can not fetch the items of a set, so we can't write the following code :  
 	print(set[0])
```python
numbers = [1, 1, 2, 3, 4]
first = set(numbers)		# create a set wuth number | save to first # set doesn't include the duplicates
second = {1, 5}		# set 'second' = {1, 3}

print(first | second)       # print the union between first and second
print(first & second)	# print the intersection between first and second
print(first - second)	# print the difference 差集 between two sets 
print(first ^ second)	# print the symmetry difference between two sets

if 1 in first :
	print('yes')
```
# Dictionaries
```python
point = {'x':1, 'y':2}	 
point_0 = dict(x=1, y=2)	# create a dic with x=1, y=2 | save to point_0
point['x'] = 10		# set point['x'] to 10
point['z'] = 20		# add 'z':20 to dic point
if 'a' in point :	# if key 'a' in keys of point
    print(point['a'])	

print(point.get('a', 0))	# print point['a'] if key 'a' in point, otherwise 0
del point['x']	# del key'x' and its key value for point

"print eveyr key and its key value from point"
for key in point :	# for each key in keys of point
	print(key, point[key])	

"print every (key, value) from all (key, value) corresponding to dic point"
for x in point.items() :    # for each (key, value) in all (key, value) corresponding to
    print(x)    # print current (key, value)	
```
# Dictionary Comprehensions
```python
values = {x * 2 for x in range(5)}  # for each x in [0..5], append x*2 to a set | save to values

Values = {x: x * 2 for x in range(5)}	# for each x in [0..5], append x:x*2 to a dic | save to values
```
# Generators
```python
from sys import getsizeof

values = {x * 2 for x in range(10)}	# for each x in [0..10], append x*2 to a set | save to values

print('gen:',getsizeof(values)) # getsizeof(values) = size of set values

for x in values :	# for each element in set values
	print(x)

```
# Unpacking Operator
```python
# 1
numbers = [1, 2, 3]

print(*numbers)	# print each items of list numbers
values = [*range(5), *'hello']	# save items of [0..5], items of 'hello' to list values
# 2
first = [1, 2]
second = [3]

values =[*first,*second]	# save items of list first and items of list second to list values

# 3
first = {'x':1}
second = {'x':10, 'y':2}

combined = {**fist, **second, 'z':1}	# cp items of dic frist and items of dic second, rm the duplicates, save to dic combined
```

