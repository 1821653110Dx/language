# Path
```python
# for windows
from pathlib import Path

Path(r'C:\Program FIles\Microsoft')

# for linux
## 1
from pathlib import Path

path = Path('ecommerce/__init__.py')	# save Path"ecommerce/__init__.py" to path

path.exists()	# return True if path's path exits
path.is_file()	# return True if path's path is a file
path.is_dir()	# return True if path's path is a dir


Path.home()	# return the home directory of current user

print(path) # print path's path
print(path.name)	# print name of path_object in path'path    # path_object =  end_part in path
print(path.stem)	# name = stem.suffix
print(path.suffix)
print(path.parent)	# print the parent path in path's path

path = path.with_name('init.txt')   # cp path's path, replace path_object's name with "init.txt"  | overwrite to path

print(path)

path = path.with_suffix('.py')	# cp path's path, replace path_object's name's suffix with ".py" | ovwrite to path

print(path)

## 2
from pathlib import Path

path = Path('ecommerce/')	# save Path"ecommerce/" to path

for p in path.iterdir() :	# for each subpath in all subpath of path's path
	print(p)

## 3
from pathlib import Path

path = Path('ecommerce/')

paths = [p for p in path.iterdir()]	# for each { path : p } in all subpath of path's path, append to a list | save to paths
print(paths)

print(5*'---')

paths = [p for p in path.iterdir() if p.is_dir()]	# for each { path : p } in all subpath of path's path, if p is a dir, appen to a list | overwirte to paths

py_files = [ p for p in path.glob('*.py')]	# for each { path : p } in all path of *.py at path's path, append to a list | save to py_files

py_files_r = [p for p in path.rglob('*.py')]    # for each { path : p } in all path of *.py at path's path and its subpath, append to a list | save to py_files

print(paths,'\n')
print(py_files,'\n')
print(py_files_r)	
```
# Working with Files
## basic functions
```python
from pathlib import Path
from time import ctime

path = Path('ecommerce/__init__.py')

# path.exists()					# check whether file of 'path' exists
# path.rename('ecommerce/__init__.txt')		# move the file of 'path'
# path.unlink()					# delete file of 'path'

print(ctime(path.stat().st_ctime))				

print(path.read_text()) 	# print the text of file of path's path
path.write_text('hello world')  # write 'hello world' into the file of path's path
```
## copy
```python
from matplotlib import Path
import shutil

source  = Path('ecommerce/__init__.py')	
target = Path(/'__init__.py') 			

shutil.copy(source, target)			# copy the path of 'source' to target
```
# Working with Zip Files
## create
```python
from pathlib import Path
from zipfile import ZipFile

with ZipFile('files.zip', 'w') as zip :	# open './files.zip' in mode [create, wirte],  save to 'zip'. auto close it after
	for path in Path('ecommerce').rglob('*.*') :	# for each { path : file } in './ecommerce' and its subpaths
		zip.write(path)				# write file into file in zip
```
## read
```python
from pathlib import Path
from zipfile import ZipFile

with ZipFile('files.zip') as zip :		# open 'files.zip' in mode = r, save to 'zip'. auto close files after
	print(zip.namelist())	# create a list with file_names from file in zip | echo

	info = zip.getinfo('ecommerce/__init__.py')	# get info of 'ecommerce/__init__.py' from file in 'zip' | save to info

	print(info.file_size)	# get file_size from info | echo
	print(info.compress_size)	# get compress_size from 'info' | echo
	
	zip.extractall('extract')	# extract all files from file in zip to ./extract
```
# Woring with CSV Files
csv file: txt file for storing table information
## create
```python
import csv

with open('data.csv', 'w') as file :
	writer = csv.writer(file)	# create a csv_writer for file | save to 'writer' 
	writer.writerow(['transactionid', 'product_id', 'product_number'])	# write a row into 'writer': "transactionid, product_id, product_number". fptr points to next char
	writer.writerow([1000, 1, 5])
	writer.writerow([1001, 2, 15])
```
## read
```python
import csv

with open('data.csv') as file :
	reader = csv.reader(file)	# create a csv_reader reading data of file in file | save to reader
	print(list(reader))	    # create a list with data of reader's reader | echo
```

# Working with JSON Files
## write
```python
import json
from pathlib import Path

movies = [
		{'id':1, 'title':'Terminator', 'year':1989},
		{'id':2, 'title':'Kindergarten Cop', 'year':1993}
]

data = json.dumps(movies)	# create a JSON_format str with items in moves | save to data

Path('movies.json').write_text(data)    # write data's file's txt into ./movies.json
```
## read
```python
import json
from pathlib import Path

data = Path('movies.json').read_text()	# read text of 'movies.json' | save to data

movies = json.loads(data)	# cp data's data, conert to Python object | save to 'movies'

print(movies)
print(movies[0])
print(movies[0]['title'])	
```

# Working with Timestamps
```python
import time

def send_emails() :
	for i in range(1000) :
		pass
	
start  = time.time()	# get current timestame | save to start
send_emails()
end = time.time()	
duration = end - start 	
print(duration)
```
# Woring with DateTimes
```python
from datetime import datetime
import time 

dt = datetime(2018, 1, 1)	# create a datetime with 2018, 1, 1 | save to dt
dt1 = datetime.now()	# get the current datetime | save to dt1
dt2 = datetime.strptime('2018/01/01', '%Y/%m/%d')	# convert string '2018/01/01' into '%T/%m/%d' datetime | save to dt2
dt3 = datetime.fromtimestamp(time.time())	# get the current timestamp | convert to datetime_object | save to dt3

print(dt3)
print(f'{dt.year}/{dt.month}')	# newpine print: {year in dt}/{month in dt}
print(dt.strftime('%Y/%m'))	#  create a str with '%Y/%m' in dt | newline print
print(dt > dt1)
```

# Working with Time Deltas
```python
from datetime import datetime, timedelta

dt1 = datetime(2018, 1, 1) + timedelta(days=1, seconds=1000)	# save 2018/1/1 add '1 day and 1000 seconds' to dt1
dt2 = datetime.now()
duration = dt2 - dt1

print(dt1)
print(duration)
print('days',duration.days)	# echo "days { days in duration }"
print('seconds',duration.seconds)
print('total_seconds', duration.total_seconds())
```
# Generating Random Values
```python
import random
import string

print(random.random())	# echo a random value in [0,1)
print(random.randint(1, 10))	# echo an randint in [1,10]
print(random.choice([1,2,3,4]))	# echo an random item in [1,2,3,4]
print(random.choices([1,2,3,4],k=2))	# echo 2 random items in [1,2,3,5]
print(random.choices('abcdefghi', k=4))	# echo 4 random chars in 'abcdefghi'
print(''.join(random.choices('abcdefghi', k=4)))	# get 4 random chars in 'abcdefghi' | join them into a str | echo
print(','.join(random.choices('abcdefghi', k=4)))	# get 4 random chars in 'abcdefghi' | join them into a str with ',' | echo

print(string.ascii_letters)	#  echo all ascii_letters
print(string.digits)	# echo all digits

print(''.join(random.choices((string.ascii_letters + string.digits),k=4)))  # get 4 random chars in (all ascii_letters + all digits) | join into a str | echo

numbers = [1,2,3,4]
random.shuffle(numbers)	# shuffle打乱 list numbers
print(numbers)

```
# Sending Emails
```python
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.image import MIMEImage
from pathlib import Path
from smtplib

message = MIMEMultipart() # create a MIMEMultipart_object, and save it in 'message'

message['from']	= 'Freather Ben'	# the email is from 'Freather Ben'
message['to'] = 'testuser@test.com'		# the email will be sent to 'testuser@codewithfreather.com'
message['subject'] = 'This is a test'	# the name(subject) of email is 'This is a test'
message.attach(MIMEText('Body','plain'))	# the content(body) of the email is 'Body', type=PlainText
message.attach(MIMEImage(Path('mosh.png').read_bytes()))		# img in email: ./mosh.png

with smtplib.SMTP(host='smtp.gmail.com', port=587) as smtp	# open SMTP: host='smtp.gmail.com', port=587, and close it after sending the email
	smtp.ehlo()
	smtp.starttls()
	smtp.login('my mailbox address', 'passwd')
	smtp.send_message(message)
	print('Sent')

```
# Working with Templates
```python
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.image import MIMEImage
from pathlib import Path
from string import Template
from smtplib

template = Template(Path('template.html').read_text)	# read a template: ./template.html, save the data into 'template'

message = MIMEMultipart() 
message['from']	= 'Freather Ben'
message['to'] = 'testuser@test.com'
message['subject'] = 'This is a test'
body = template.substitude(name='John')	# substitue $name with str 'John' in data of 'template', save the results to 'body'
message.attach(MIMEText(body,'html'))	# the content(body) of the email is the data of 'body', type=html
message.attach(MIMEImage(Path('mosh.png').read_bytes()))

with smtplib.SMTP(host='smtp.gmail.com', port=587) as smtp	
	smtp.ehlo()
	smtp.starttls()
	smtp.login('my mailbox address', 'passwd')
	smtp.send_message(message)
	print('Sent')

```

# Command-line Arguments
```python
import sys

if len(sys.argv) == 1 :		# If counts of cmd_arg == 1, then
	print('USAGE: python3 app.py <passwd>')
else:	# Otherwise,
	passwd = sys.argv[1]	# get cmd_arg[1] | save it to 'passwd'
	print('Passwd', passwd)
```
