# arithmetic operators
- remain %
- add-self ++
- sub-self --
- plus 1 to the original amount +=
## instances
```c

#include <stdio.h>

int main()	
{
	int a = 21 ;	// create var a = 21, int, auto 
	int b = 10 ;	
	int c ;	// create empty var c, int, auto
	
	c = a++ ;	// overwrite c with a, a += 1
	printf("the value of c is %d\n",c) ;	// printf "the value of c is {c}\n" {c:decimal} 
	c = a-- ;	// overwrite c with a, a -= 1
	printf("the value of c is %d\n",c) ;	
	c = ++a	;	// a += 1, overwirte c with a 
	printf("the value of c is %d\n",c) ;	
	c = --a ;	// a -= 1, overwrite c with a
	printf("the value of c is %d", c) ;	

	return 0 ;	// exit 
}
```

# relational operators
- equal ==
- noequal !=
- greater equal >=
## instances
```c

#include <stdio.h>	

int main()
{
	int a= 21 ;
	int b = 21 ;
	int c ;

	if (a == b)
	{
		printf("a = b\n") ;
	}
	else	// otherwise 
	{
		printf("a != b\n") ;
	}

	if (a < b)
	{
		printf("a < b\n") ;	
	}
	else	// otherwise 
	{
		printf("a !< b\n") ;
	}

	a = 5 ;	// overwite a with 5 
	b = 20 ;	// overwite b with 20 

	if ( a <= b )
	{
		printf("a <= b\n") ; 
	}
	else	// otherwise 
	{
		printf("a !<= b") ;	
	}

	return 0 ;	
}
```

# logic operators
- && and
- || or
- ! not
## instances
```c
 
#include <stdio.h>	

int main()
{ 
	int a = 5 ;	
	int b = 20 ;
	int c ;

	if ( a && b )	// if a and b all True  
	{ 
		printf("True\n") ;
	} 

	if ( a || b )	// if a or b True 
	{
		printf("True\n") ;
	}
	
	a = 0 ;	
	b = 10 ;
	
	if ( a && b )	// if a and b all True 
	{
		printf("True\n") ;
	}
	else	// otherwise 
	{
		printf("False\n") ;	
	}

	if ( !(a && b) )	// if a and b !all True 
	{
		printf("True") ;
	}

	return 0;
} 
```
# bit operators
- &
	- * in bit operation
- | 
	- + in bit operation
- ^ 
	- (if same, then 0; otherwise, 1) in bit operation
- ~ 
	- (to 1, 1 to 0) in bit operation
- << 
	- * 2^n in decimal operation
- >> 
	- \ 2^n in decimal operation

## instances
```c

# include <stdio.h>	

int main()	
{
	unsigned int a = 60 ;	
	unsigned int b = 13 ;
	int c = 0 ;	

	c = a & b ;	// overwite c with {a & b} 
	printf("value of c is %d\n",c) ;
	c = a | b ;	// overwite c with {a | b} 
	printf("value of c is %d\n",c) ;	
	c = a ^ b ;	// overwite c with {a ^ b} 
	printf("value of c is %d\n",c) ;
	c = ~a ;	// overwite c with {~a} 
	printf("value of c is %d\n",c) ;
	c = a << 2 ;	// overwite c with {a << 2} 
	printf("value of c is %d\n",c) ;
	c = a >> 2 ;	// overwite c with {a >> 2} 
	printf("value of c is %d\n",c) ;
		
	return 0 ;	// exit 
}
```

# assignment赋值 operators
- +=
- -=
- \*=
- /=
- %=
- <<=
- >>=
- &=
- ^=
- |=

# miscellaneous杂项 operators
```c

#include <stdio.h>	

int main()
{
	int a = 1 ;	
	short b ;
	double c ;	
	int* ptr ;	

	printf("the size of a is %lu\n",sizeof(a)) ;
	printf("the size of b is %lu\n",sizeof(b)) ;
	printf("the size of c is %lu\n",sizeof(c)) ;

	ptr = &a ;

	printf("the value of a is %d\n",a) ;
	printf("the value of pointer ptr is %d\n",*ptr) ;

	a = 10 ;	// overwite a with 10 
	b = (a == 1) ? 20:30 ;		// return 20 if a = 1, otherwise 30 | save to b 

	printf("the value of b is %d\n",b) ;
		
	b = (a == 10) ? 20:30 ;	// return 20 if a = 10, otherwise 30 | overwite to b

	printf("the value of b is %d",b) ;	
	
	return 0 ;	// exit 
}
```

# priority 
![8cc01402a924e5cb693bfb5c34cd1929.png](../../../_resources/8cc01402a924e5cb693bfb5c34cd1929.png)
