# type
## int
- 10-base: 85
- 8-base: 0213
- 16-base: 0x4b
- int: 30
- unsigned int: 30u
- long int: 30l
- unsigned long: 30ul
### instances
```c
const int myint = 10;   // create const myint = 10, int, auto
const long mylong0 = 100000;	// def 'mylong0': 100000, long, const, auto
```
## float
### example
- legal
	- 3.14159
	- 3.14159E - 5L
- illegal
	- 510E
	- 210f
	- .e55
### instances
```c
const float myfloat = 3.14f;
const double mydouble = 3.14159;
```
## char(escape character)
\ | \\
' | \'
" | \"
? | \?
arlarm | \a
backspace | \b
nextapge | \f
nextline | \n
enter | \r
horizontal tab | \t
vertical tab | \v
### instances
```c
const char mychar = 'a' ;	// create const mychar = 'a', char, auto
const int myAsciiValue = (int)mychar ;	// create const myAsciiValue = the ASCII value of char of { mychar }, int, auto
```

