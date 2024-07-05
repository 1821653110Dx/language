```c
#include <stdio.h>

/* declare func to call */
double factorial(int i) ;


int main()
{
	int i = 15 ;	// create var i = 15, int, auto
	printf("the factorial of %d : %f\n", i, factorial(i)) ;	// printf " the factorial of { i } = { factorial(i) }\n"{ %d %f }
	return 0 ;
}

double factorial(int i)	// def func factorial : arg = i, dvalue = null, dtype = int, r = double
{
	if ( i <= 1 )
	{
		return 1 ;
	}
	/* otherwise, do the internal */
	return i * factorial(i - 1) ;
}
```
```c
#include <stdio.h>

/* declare func to call */
int fibonaci(int i) ;

int main()
{
	int i ;	//  create empty var i, int, auto
	
	for (i=0 ; i < 10 ; i ++)	// 0 <= i <= 9, d 1. for each
	{
		printf("%d\t\n", fibonaci(i));	// printf "{ fibonaci(i) }\t\n"{ %d }
	}

	return 0;
}

int fibonaci(int i)	// def func factorial : arg = i, dvalue = null, dtype = int, r = int
{
	if (i == 0)
	{
		return 0 ;
	}
	if ( i == 1 )
	{
		return 1 ;
	}
	return fibonaci(i-1) + fibonaci(i - 2) ;
}
```
