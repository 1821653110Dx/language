```c
#include <stdio.h>

int main()
{
	int sum = 17, count = 5 ;	// create var [sum, count] = [17, 5], int, auto
	double mean ;	// create empty var mean, double, auto

	mean = (double) sum/count ;	// sum / count | type of the return >> double | save to mean
	printf("Value of mean : %f\n", mean) ;	// printf "Value of mean : { mean }\n"{ %f }
	return 0 ;
}
```
```c
#include <stdio.h>

int main()
{
	int i = 17 ;	// create var i = 17, int, auto
	char c = 'c' ;	// create var c = 'c', char, auto
	int sum ;	// create empty var sum, int, auto
	
	sum = i + c ;	// i + ascii of char of c | save to sum
	printf("Value of sum : %d\n", sum)	;// printf "Value of sum : { sum }\n"{ %d }

	return 0 ;
}
```
```c
#include <stdio.h>

int main()
{
	int i = 17 ;	// create var i = 17, int, auto
	char c = 'c' ;	// create var c = 'c', char, auto
	float sum ;	// create empty var sum, float

	sum = i + c ;	// i + ascii of char of c | save to sum
	printf("Value of sum : %f\n", sum) ;	// printf "Value of sum : { sum }\n"{ %f }

	return 0 ;
}
```
