# class
purpose: let a variable using customed methods and attributes
## define method
```python
class Point :	# def class Point
	def draw(self) :	# def method draw: arg = null
		print('draw')	

a = Point()	# create var a of Point class
a.draw()		# call method draw() of a 
```
## define attributes
```python
class Point :   # def class Point
	default_color = 'red'	# create attribute default_color = 'red'
	def __init__(self, x, y) :	# def method __init__ : arg = [x, y]    # __init__ is used to init specified attributes
		self.x = x + 3	# init attribute x = x + 3
		self.y = y + 6  # init attribute y = y + 6
	def draw(self) :	# def method draw : arg = null
		print(f'Point ({self.x}, {self.y})')		# print Point ({the value of attribute x}, {the value of attribute y})

Point.default_color = 'yellow'	# init attribute 'default_color' of class 'Point' to 'yellow'
point = Point(1, 2)	# create point of Point class, init attributes (x,y) with (1, 2)

print(point.x)	# cp value of attribute x of point | newline print
print(Point.default_color) # newlineprint the value of attribute default_color of class Point
point.draw()	# call method draw of point
```
## define classmethod
```python
class Point :
	def __init__(self, x, y) :  # def method __init__ : arg = [x, y]
		self.x = x  # init attribute x = x
        self.y = y

	@classmethod	# add this before def class method
	def zero(cls) :	# def classmethod zero : arg = cls, dvalue = null
		return cls(0 ,0)	# init attributes (x, y) by given (x=0,y=0)

point = Point.zero()	# create point of class point, init arttibues (x,y) by classmethod zero()
```
## define magic method
```python
class Point 
	def __init__(self, x, y) :  # def method __init__ : arg = [x, y]
		self.x = x
		self.y = y
	def __str__(self) :	# def introduction of the class
		return f'({self.x}, {self.y})'	# ({ x }, { y })

point = Point(1, 2) # create point of Point class, init attributes (x, y) by (1, 2)

print(point)	# newline print introduction of point
```
## Comparing Objects of customed class
```python
class Point :   # def class point 
	def __init__(self, x, y) :  # def method __init__ : arg = [x, y]
		self.x = x  # init attribute x = x
		self.y = y
	
	def __eq__(self, other) :	# def criteria标准 for equalty for var of this class: arg = other
		return self.x == other.x and self.y == other.y	# x or y are same	

	def __gt__(self, other) :	# def criteria for greater_than for var of this class : arg = other    
		return self.x > other.x and self.y > other.y # both x and y are greater
a = Point(1, 2)
b = Point(1, 2)
c = Point(0, 0)

print(a == b)	# newline print whether a == b
print(a > c)
print(a < c)
```
## Supporting Arithmetic Operations
```python
class Point :
	def __init__(self, x, y) : 
		self.x = x
		self.y = y
	
	def __add__(self, other) :	# def the criterion for addition for var of the class: arg = other
		return Point(self.x + other.x, self.y + other.y) # add each x, add each y

a = Point(10, 20)
b = Point(1, 2)

## newline print x of a + b
sum = a + b	    
print(sum.x)
```
## Custom Containers
```python

class TagCloud :	# def class Tagcloud
	def __init__(self) :	# def method __init__ :
        self.tags = {}  # init attribute tags = {}
	
	def add(self, tag) :	# def method add: arg = tag
		self.tags[tag.lower()] = self.tags.get(tag.lower(), 0) + 1  # add key { tag.lower() } to dic tags if not in, otherwise, its counts + 1

	def __getitem__(self, tag) : # def the creterion for getting lowercased item for var of the class: arg = tag
		return self.tags.get(tag.lower(), 0)	# add key tag.lower() to dic tags if not in and its value = 0, otherwise do nothing
	
	def __setitem__(self, tag, count) : # define the creterion for setting the getted lowercased item for var of the class : arg = [tag, count]
		self.tags[tag.lower()] = count	# add tag.lower():count to dic tags
	
	def __len__(self) :	# def the creterion for getting the length of attribute dic tags
		return len(self.tags)   # return len of attribute dic tags of var of the class

	# def __iter__(self) : 	## def the creterion for geting one item at a time
	#	return iter(self.tags)

cloud =  TagCloud()

cloud.add('Python')	# add key "Python".lower to attribute dic tags of cloud if not in, otherwise its count + 1 by method add()
cloud.add('python')
cloud.add('python') 

cloud['Python'] = 10	# add "python".lower():10 to attribute dic tags to cloud

len(cloud)	# return len of attribute dic tags of cloud

print(cloud.tags)	# print the items of attribute dic tags of cloud

```
## Properties
### have the same without using Properties
```python
class Product :
	def __init__(self, price) :	
		self.set_price(price)	# init specified attributes by set_price(price)

	def get_price(self) :	
		return self.__price	# return the value of attribute __price

	def set_price(self, value) :	# def method set_price : arg = value
		if value < 0 :	# if value < 0, then
			raise ValueError('Price cannot be negative') # raise a ValueError called 'Price cannot be negative'
		self.__price = value	# otherwise, init attribute __price = value

product = Product(50)
```
### have the same result with properties
```python
class Product :
	def __init__(self, price) :
		self.price = price	# init attribute __price = price
	
	@property	# add this before declare property
    ## declare property price : return attribute __price
	def price(self) :	
		return self.__price 

	@price.setter	# add this before def property
	def price(self, value) :	# def property price : arg = value
		if value < 0 :	
			raise ValueError('Price cannot be negative') 
		self.__price = value 
	
product = Product(50)	# create var product of Product class, init attributes __price by price = 50

product.price = 1  # set attribute __price of 'product' = 1

print(product.price)	# newline print attribute __price of product
```
## inheritance
```python
class Animal :
	def __init__(self) :
		self.age = 1

	def eat(self) :
		print('eat')

class Mammal(Animal) :  # def class Mammal, if not def attributes, auto inherite all features of Animal, otherwise methods only
	def __init__(self) :	
		self.weight = 2
		super().__init__()	# inherit attributes of 'Animal'    # here auto inherite methods only, so in order to inherit attributes, you need manually inherite them

	def walk(self) :
		print('walk')

class Fish(Animal) :
	def swim(swim) :
		print('swim')

class MemoryStream(Stream) :


m = Mammal()

m.eat()	
print(m.age)	# print the value of attribute 'age' of 'm'
print(m.weight)
```
## Multi-Level Inheritance(limited to 1 / 2 levels)
```python
class Animal :
	def eat(self) :
		print('eat')

class Bird(Animal) :
	def fly(self) :
		print('fly')

## def class chicken with all features of Bird
class chicken(Bird) :	
	pass		
```
## Multiple Inheritance
```python
class Employee :
	def greet(self) :
		print('Employee Greet')

class Person :
	def greet(self) :
		print('Person Greet')

## def class Manager with all featrues of Employee, Person
class Manager(Employee, Person) :	
	pass	
	
manager = Manager()	
manager.greet()	# call method 'greet()' of 'manager', but both 'Employee' and 'Person' have greet() and 'Employee' is infront of 'Person' at 'class Manager(Employee, Person)', so it will call the 'greet()' of 'Employee'

```
## A Good Example of Innheritance
```python
from abc import ABC, abstractmethod	

## def class InvalidOperationError with all features of built-in class Exception
class InvalidOperationError(Exception) :	
	pass	

class Stream(ABC) :	# def calss Mammal, if not def attributes, auto inherit all features of ABC(not def yet), Otherwise method only
	def __init__(self) :
		self.opened = False	

	def open(self) :
		if self.opened :	
			raise InvalidOperationError('Stream is already opened')	

		self.opened = True	


	def close(self) :
		if not self.opened :	
			raise InvalidOperationError('Stream is already closed')

		self.opened = False	
	
    ## def method read which hasn't start being building
	@abstractmethod
	def read(self) :
		pass
	

class FileStream(Stream) :  # def class FileStream, if not def attrubutes, auto inderit all features of ABC(not def yet), otherwise method only
	def read(self) :    # def method read of Stream
		print('Reading data from a file')

class NetworkStream(Stream) :
	def read(self) :    # def method read of Stream
		print('Reading data from a network')

## def class MemoryStream with all features of class Stream
class MemoryStream(Stream) :
	pass

stream = Stream()	# there is "@abstruct" in stream(), indicating the class hasn't been finished ,so you can't create var stream of stream class

stream_1 = MemoryStream()	# Memory inherits all freatures of class Stream which hasn't been finished, so you can't create var stram of MemoryStream

stream.open()   # even though stream hasnt been finished, you can call its finished methods
```
# Duck Typing
```python
class TextBox : 
	def draw(self) :
		print('TextBox')

class DropDownList:
	def draw() :
		print('DropDownList')

def draw(controls) :    # def func draw : arg = list controls, dvalue = null
	for control in controls :	# for every control in list controls
		control.draw()	# call method draw() of  control

a = DropDownList()	# create var a of class DropDownList
b = TextBox()

draw([a, b])
```
# Extending Built-in classs
let customed classes inherit built-in classes
```python
class Text(str) :	# def calss Text, if not def attributes, auto inherit all features of built-in class str, otherwise methods only
	def duplicate(self) :
		return self + self	# duplicate its attribute value

class TrackableList(list) : # def class list, if not def attributes, auto inherited all features of built-in clss list, ...
	def append(self, object) :	# modify method 'append()' inherited from list : arg = object, dvalue = void
		print('Apend called')
		super().append(object)	# call original append(object) 

text = Text('Python')	# create var text of class Text, init its attriburtes with "Python"

list =  TrackableList()

print(text.lower())	
print(text.duplicate())	

list.append('1')
```
# Data Classes
a better way to save numorous data
```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])		# create data_class Point with attrutes [x, y] 
p1 = Point(1, 2)	# create var p1 of data class Point, init attributes (x, y) = (1, 2)
p2 = Point(1, 2)

p1 = Point(10, 2)   # init p1's attrubute (x, y) = (10, 2)  # p1.x = 5 is invalid

print(p1 == p2)		# you can compare data_class directly without def criteria
```

