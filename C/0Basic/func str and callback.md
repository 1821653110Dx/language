# func_ptr
	ptr pointing to func
```c
/*
return0 = the return value of first cmd
*/

#include<stdio.h>

/* declare func to call */
int max(int, int) ;

int main()	// def main
{
	int (*p)(int, int) = & max ;	// create ptr_var p = addr of max(int, int), int, auto 	
	int a, b, c, d ;	// create empty var [a,b,c,d], int, auto
	
	/* echo "please input 3 digit, with space as sperator: ", let usr input "%d %d %d" | seperately save to a, b, c */
	printf("please intput 3 digit, with space as seprator: ") ;
	scanf("%d %d %d", & a, & b, & c) ;

	d = max( max(a, b), c ) ;	// get the max one between a and b by customed func: max(a, b) | get the max one between return0 and c | save to d
	printf("the largest number : %d\n", d) ;	// printf"the largest number : { d }\n"{ d : %d }

	d = p( p(a, b), c ) ; // get the max one between a and b by customed func p points to : p(a, b) | get the max one between return0 and c | save to d
	printf("the largest number : %d\n", d) ;	// printf"the largest number : { d }\n"{ d : %d }

	return 0 ;	// exit program
}

int max(int x, int y)	// def func max : arg  = [var x, var y], dvalue = null, dtype = int, r = void
{
	int a ;	// create empty var a, int, auto

	a = x > y ? x : y ;// get x if x > y, otherwise get y | save to a 

	return a ;	// return a
}
```

# callback回调函数
use func str as an argument of certain function  
```c
#include <stdlib.h>
#include <stdio.h>

/* declare func to call */
int getNextRandomValue(void) ;
void populate_array(int *array, size_t arraySize, int (*randomInt)(void)) ;

int main()	// def main
{
	int myarry[10] ;	// create empty static_varlist myarry[10], int, auto

	populate_array(myarry, 10, & getNextRandomValue) ;	// save a populate_array to myarry by customed populate_arry(myarry, 10, addr of customed getNextRandomValue(void)) | save to myarry

	for ( int i = 0 ; i < 10 ; i++ )	// 0 <= i <= 9, d 1. for each 
	{
		printf("%d ", myarry[i]) ;	// printf"{ myarry[i] } "{ myarry[i] : %d }
	}
	
	printf("\n") ;	// printf"\n"

	return 0 ;	// exit program
}

int getNextRandomValue(void)	// def func getNextvalue : arg = null, r = int
{
	return rand() ;	// return an randint
}

void populate_array(int *array, size_t arraySize, int (*randomInt)(void))	// def populate_array : arg  = [pvar array, var arraySize, func randomInt(void)], dvalue = null, dtype = int, r = void
{
	for ( size_t i = 0 ; i < arraySize ; i++ ) // 0 <= i <= arraySize-1, d 1. for each
	{
		array[i] = randomInt() ;	// save the return of getNextvalue() to arry[i]
	}
}
```

