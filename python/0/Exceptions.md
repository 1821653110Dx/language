# Handling Exceptions
```python
# 0
try :	# try the internal
	age = int(input('Age: ')) 
	xfactor = 10 / age	
except ValueError as ex :	# when meet ValueError, save to ex and do
	print("You didn't enter a valid age")	
	print(ex)
	print(type(ex))
except ZeroDivisionError :	# when meet ZeroDivisionError,
	print('Age cannot be 0')
else :	# otherwise,
	print('No exceptios were thrown')
# 1
try :
	file = open('app.py')	# open app.py in mode = r, save to file
    age = int(input('Age:'))
	xfactor = 10 /age
except (ValueError, ZeroDivisionError) :	# when meet [ValueError, ZeroDivisionError]
	print("You didn't enter a valid age")
else :
	print('No exceptios were thrown')
finally :	# finally,
	file.close()	# close file responding to 'file'

# with statement
try :
	with open('app.py') as file, open('another.txt') as target :    # open [app.py, another.txt] in mode = r, save to [file, target]. auto close them after
		print('file opened')

	age = int(input('Age:'))
	xfactor = 10 /age
except (ValueError, ZeroDivisionError) :    # when meet [valid,ZeroDivisionError]
	print("You didn't enter a valid age")
else :  # otherwise, 
	print('No exceptios were thrown')
```
