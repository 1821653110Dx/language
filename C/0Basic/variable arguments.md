```c
#include <stdio.h>
#include <stdarg.h>

/* declare func to call */
float average(int num, ...) ;

int main()
{
	printf("Average of 2, 3, 4, 5 = %f\n", average(4, 2, 3, 4, 5)) ;	// printf "Average of 2, 3, 4, 5 = { avegrage(4, 2, 3, 4, 5) }\n"{ %f }
	printf("Average of 5, 10, 15 = %f\n", average(3, 5, 10, 15)) ;	// printf "Average of 5, 10, 15 = { avegrage(3, 5, 10, 15) }\n"{ %f }

	return 0 ;
}

float average(int num, ...)	// def func avegrage : arg = [num, variable arg ], dvalue = null, dtype = int, r = double	// ignor dvalue and dtype of variable arg
{
	double sum = 0.0 ;	// create var sum = 0.0, double, auto
	int i ;	// create empty var i, int, auto

	/* save sum of each item of varlist to sum */
	/// save vargs after num to va_list valist	// va_list = variable arguments list
	va_list varlist ;
	va_start(varlist,num) ;
	
	for (i=0 ; i < num ; i ++)	// 0 <= i <= num - 1. d 1. for each
	{
		sum += va_arg(varlist, int) ;	// sum += { current item of valist, dtype = int }
	}
	
	va_end(varlist) ;	// del varlist
	
	return sum/num ;
}
```
