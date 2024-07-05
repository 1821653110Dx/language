# definition
mem addr
# save & fetch
```c
#include<stdio.h>

int main()	// def main
{
	int var = 20 ;	// create var var = 20, int, auto
	int* ip = NULL ;	// create empty pvar ip, int, auto

	ip = &var ;	// 'ptr' points to 'var'	OR	save {'var'.addr: &var} to 'ip'

	/* printf 'var'.addr */
	printf("var.addr : %p\n", &var) ;	// printf"var.addr : {&var}\n"{~:pointer}

	/* printf the addr of 'var' that 'ptr' points to */
	printf("the addr of 'var' that 'ptr' points to : %p\n", ip) ;	// printf"the addr of 'var' that 'ptr' points to : {ip}\n"{~:%p}
	
	/* printf the value of 'var' that 'ptr' points to */
	printf("the value of 'var' that 'ptr' points to: %d\n", *ip) ;	// printf"value saved at the addr saved in ip : {*ip}\n"{~:%d}

	return 0 ;	// exit
}
```
# calc
## pointer points to next addr
```c
#include<stdio.h>

const int MAX = 3 ;	// create const MAX = 3, int, global

int main()	// def main
{
	int var[3] = {10, 100, 200} ;	// create static_varlist var[3] = [10, 100, 200], int, auto
	int i ;	// create empty var i, int, auto
	int* ptr = NULL ;	// create empty pvar ptr, int, auto

	ptr = var ;	// 'ptr' points to {var[0]}	OR	// save {addr of 1st items of 'var'} to 'ptr'
	
	/* printf every item of 'var' and its addr */
	for (i = 0 ; i < MAX ; i ++)	// 0 <= i <= MAX-1, d 1. for each
	{
		printf("addr:var[%d] = %p\n", i, ptr) ;		// printf"addr:var[{i}] = {ptr}\n"{i:%d, ptr:%p}
		printf("item:var[%d] = %d\n", i, *ptr) ;	// printf"item:var[{i}] = {*ptr}\n"{i:%d, *ptr:%d}

		ptr++ ;		// 'ptr' points to next item
	}

	return 0 ;	// exit
}
```
## pointer points to previous addr
```c
#include<stdio.h>

const int MAX = 3 ;	// create const MAX = 3, int, global

int main()	// def main
{
	int var[3] = {10, 100, 200} ;	// create static_varlist var[3] = [10,100,200], int, auto
	int i ;	// create empty var i, int, auto
	int* ptr = NULL ;	// create empty pvar ptr, int, auto

	ptr = &var[MAX-1] ;	// 'ptr' points to var[0]	OR	// save {addr of last item of 'var'} to 'ptr'

	/* printf every item of 'var' and its addr */
	for (i = MAX - 1; i >= 0 ; i--)	// MAX-1 >= i >= 0, d -1. for each
	{
		printf("addr:var[%d] = %p\n", i, ptr) ;		// printf"addr:var[{i}] = {ptr}\n"{i:%d, ptr:%p}
		printf("item:var[%d] = %d\n", i, *ptr) ;	// printf"item:var[{i}] = {*ptr}\n"{i:%d, *ptr:%d}

		ptr-- ;		// 'ptr' points to previous item
	}

	return 0 ;	// exit
}
```

## compare
```c
#include<stdio.h>

const int MAX = 3 ; // create var MAX  = 3, int, global

int main() // def main
{
	int var[3] = {10, 100, 200} ;	// create static_varlist var[3] = [10, 100, 200], int, auto
	int i ;	// create empty var i, int, auto	
	int* ptr = NULL ;	// create empty pvar ptr, int, auto

	ptr = var ;	// 'ptr' points to {var[0]}

	i = 0 ;		// set i = 0
	
	while ( ptr <= &var[MAX-1] )	// while {the item 'ptr' points to} < var[MAX-1], do the internal. Otherwise, next step
	{
		printf("addr:var[%d] = %p\n",i,ptr) ;	// printf"addr:var[{i}] = {ptr}\n"{i:%d,ptr:%p}
		printf("item:var[%d] = %d\n",i,*ptr) ;	// printf"item:var[{i}] = {*ptr}\n"{i,*ptr:%d}

		i++ ;	// switch to previous var
		ptr++ ;	// 'ptr' points to next item
	}

	return 0 ;	// exit
}
```
# ptr_array
## int
```C
#include <stdio.h>

const int MAX = 3 ;	// create empty const MAX = 3, int, global

int main()	// def main
{
	int var[3] = {10, 100, 200} ;	// create static_varlist var[3] = [10, 100, 200], int, auto
	int i ;	// create empty var i, int, auto	
	int* ptr = NULL ;	// create empty pvar ptr, int, auto
	
	/* save addr of each item of var to ptr[] */
	for ( i = 0 ; i < MAX ; i++ )	// 0 <= i <= MAX-1, d 1. for each
	{
		ptr[i] = &var[i] ;	// save addr_of_var[i] to ptr[i]
	}

	/* printf each item of var with ptr */
	for ( i = 0 ; i < MAX ; i++ )	// 0 <= i <= MAX-1, d 1. for each
	{
		printf("value of var[%d] = %d\n",i,*ptr[i]) ;	// printf"value of var[{i}] = {item ptr[i] points to : *ptr[i]}\n"{i,*ptr:%d}
	}

	return 0 ;	// exit program
}
```
```c
#include <stdio.h>

int main()	// def main
{
	int num1 = 10, num2 = 20, num3 = 30 ;	// create var [num1, num2, num3] = [10, 20, 30], int, auto
	
	int* ptrArray[3] ;	// create empty ptr static_varlist ptrArray[3], int, auto

	/* ptrArray points to different int var */
	ptrArray[0] = &num1 ;	// ptrArray[0] points to num1
	ptrArray[1] = &num2 ;	// ptrArray[1] points to num2
	ptrArray[2] = &num3 ;	// ptrArray[2] points to num3
	
	/* call num1/2/3 with ptrArray */
	printf("Value at index 0 : %d\n",*ptrArray[0]) ;	// printf"Value at index 0 : {item ptrArray[0] points to : *ptrArray[0]}\n"{*#ptrArray[0] : %d}
	printf("Value at index 1 : %d\n",*ptrArray[1]) ;	// printf"Value at index 1 : {item ptrArray[1] points to : {*ptrArray[1]}\n}"{*ptrArray[1] : %d}
	printf("Value at index 2 : %d\n",*ptrArray[2]) ;	// printf"Value at index 2 : {item ptrArray[2] points to : {*ptrArray[2]}\n}"{*ptrArray[2] : %d}

	return 0 ;	// program exit
}
```
## str
```c
#include <stdio.h>

const int MAX = 4 ;	// create const MAX = 3, int, global

int main()	// def main
{
	const char* names[4] = {"Zara Ali", "Hina Ali", "Nuhua Ali", "Sara Ali"} ;	// create ptr static_varlist names[4] = ["Zara Ali", "Hina Ali", "Nuhua Ali", "Sara Ali"], char, auto
	int i = 0 ;	// create var i = 0, int, auto 
	
	/* printf each item of names */
	for ( i = 0; i < MAX ; i++ )	// 0 <= i <= MAX-1, d 1. for each
	{
		printf("value of names[%d] : %s\n", i, names[i]) ;	// printf"value of names[{i}] : {name[i]}\n"{i:%d ; name[i]:%s}	// %s - string
	}

	return 0 ;	// exit program
}
```
# pptr (ptr that points to ptr)
```c
#include<stdio.h>

int main()	// def main
{
	int V ;	// create empty var V, int, auto
	int* Pt1 ;	// create empty ptr var Pt1, int, auto
	int** Pt2 ;	// create empty pptr var Pt2, int, auto
	
	V = 100 ;	// set V = 100
	
	Pt1 = &V ;	// Pt1 points to V
	Pt2 = &Pt1 ;	// Pt2 points to ptr Pt1

	printf("var = %d\n",V) ;	// printf"var = {V}\n"{V:%d}
	printf("Pt1 = %p\n",Pt1) ;	// printf"Pt1 = {Pt1}\n"{Pt1:%p}
	printf("*Pt1 = %d\n",*Pt1) ;	// printf"*Pt1 = {var Pt1 points to : *Pt1}\n"{*Pt1 : %d}
	printf("Pt2 = %p\n",Pt2) ;	// printf"Pt2 = {Pt2}\n"{Pt2:%p}
	printf("**Pt2 = %d\n",**Pt2) ;	// printf"**Pt2 = {var Pt2 finally points to}"{**pt2 : %d}

	return 0 ;	// exit program
}
```
# pass ptr to func
```c
#include<stdio.h>
#include<time.h>

/* declare func to call : getSeconds */
void getSeconds(unsigned long* par) ;

int main()	// def main
{
	unsigned long sec ;	// create empty var sec, unsigned long, auto

	getSeconds(&sec) ;	// save current seconds to sec by calling customed func : name = getSeconds, given_argument = {addr of sec : &sec}

	printf("Number of seconds: %ld\n",sec) ;	// printf("Number of seconds: {sec}\n"){sec:%ld}

	return 0 ;	// exit program
}

void getSeconds(unsigned long* par)	// def func getSeconds : arg = ptr var par, dvalue = null, dtype = unsigned long, r = void
{
	/* save current seconds to *ptr */
	*par = time(NULL) ;	// get current seconds | save to *ptr


	return 0 ;	// exit func without returning value
}
```
```c
#include<stdio.h>

/* declare func to call : getAverage */
double getAverage(int* arr, int size) ;

int main()	// def main
{
	int balance[5] = {1000, 2, 3, 17, 50} ;	// create static_varlist blance[5] = {1000, 2, 3, 17, 50}, int, auto
	double avg ;	// create empty var avg, double, auto

	avg = getAverage( balance, 5 ) ;	// get average value of balance by customed func : getAverage( balance, 5 ) | save to avg

	printf("Average value is %f\n",avg) ;	// printf"Average value is {avg}\n"{ avg : %f }

	return 0 ;	// exit program
}

double getAverage(int* arr, int size)	// def func getAverage : avg = [ptrvar arr, var size], dvalue = null, dtype = int, r = double
{
	int i ;		// create empty var i, int
	int sum = 0 ;	// create var sum = 0, int, auto
	double avg ;	// create empty var avg, double, auto


	/* calc sum of list arry, save to sum */
	for ( i = 0 ; i < size ; i++ )	// 0 <= i <= size-1, d 1. for each
	{
		sum += arr[i] ;	// sum of list arry += arry[i]
	}

	/* calc average of list arry */
	avg = (double)sum / size ;	// type of sum >> double | { average of arry : avg } = sum / size

	return avg ;	// return value of avg
}
```

# return ptr from func
```c
#include <stdio.h>
#include <time.h>
#include <stdlib.h>

/* decalre func to call */
int* getRandom( ) ;

int main()	// def main
{
	int* p = NULL ;	// create empty ptrvar p, int, auto
	int i ;	// create empty var i, int, auto

	p = getRandom() ;	// get an list with randint by customed func: getRandom() | p points to its first item
	for ( i = 0 ; i < 10 ; i++ )	// 0 <= i <= 9, d 1. for each
	{
		printf("*(p + %d) = %d\n", i, *(p+i)) ;	// printf"(p + { i }) = { item at index'i' of list p points to : *(p+i) }\n)"{ *(p+i) : %d }
	}

	return 0 ;	// exit program
}


int* getRandom( )	// dev func getRandom : avg = null, r = int*
{
	int i ;	// create empty var i, int, auto
	static int r[10] ;	// create empty static_varlist r[10], int, static

	/* set random seed */
	srand( (unsigned)time( NULL ) ) ;

	for ( i = 0 ; i < 10 ; i ++ )	// 0 <= i <= 9, d 1. for each
	{
		r[i] = rand() ;	// save an randint to r[i]
		printf("%d\n", r[i]) ;	// printf"{ r[i] }\n"{ r[i] : %d }
	}

	return r ;	// return addr of r[0]
}
```


