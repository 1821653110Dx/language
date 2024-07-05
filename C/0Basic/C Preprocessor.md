# predefined macro
similar to env var
```c
#include <stdio.h>
int main()
{
	printf("File : %s\n", __FILE__) ;	// printf "File : {__FILE__}\n}"{ %s }	// __FILE__ = current file
	printf("Date : %s\n", __DATE__) ;	// printf "Date : {__DATE__}\n"{ %S }	// __DATE__ = current date
	printf("Time : %s\n", __TIME__) ;	// printf "Time : {__TIME__}\n"{ %S }	// __TIME__ = current time
	printf("Line : %s\n", __LINE__) ;	// printf "Line : {__LINE__}\n"{ %s }	// __LINE__ = current line num
	printf("ANSI : %s\n",__STDC__) ;	// printf "ANSI : {__STDC__}\n"{ %s }	// __STDC__ = 1 when compiler compiles with the ANSI standard
	
	return 0 ;
}
```

# create macro
```c
#include <stdio.h>

#define message_for(a, b)	printf(#a " and " #b ": we love you!\n")	// def macro message_for(chr a, chr b) = printf { a } + ' and ' + { b } + ": we love you!\n"

int main()
{
	message_for(Carole, Debra) ;
	return 0 ;
}
```
```c
#include <stdio.h>

#if !defined (MESSAGE)	// if macro MESSAGE not def
	#define MESSAGE "You Wish!"	// def macro MESSAGE = "You Wish!"
#endif

int main()
{
	printf("Here is the message : %s\n", MESSAGE) ;	// printf "Here is the message: {macro MESSAGE}\n"{ %s }
	
	return 0 ;
}
```

# macro with arguments参数
```c
#include <stdio.h>

#define MAX(x, y) ((x) > (y) ? (x) : (y))	// def macro MAX(arg x, arg y) = if { x } > { y }, return { x }. Otherwise { y }	// ((x) > (y) ? (x) : (y)) can not be replaced with ( (x) > (y) ? (x) : (y) )

int main()
{
	printf("Max between 20 and 10 is %d\n", MAX(10, 20)) ;

	return 0 ;
}
```
