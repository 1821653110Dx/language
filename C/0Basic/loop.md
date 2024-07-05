# loop
## while
```c

#include <stdio.h>


int main()
{
	int a = 10 ;	// create var a = 10, int, auto
	
	/* 'a' < 20 and d 1, printf every "the value of a is {a}\n"{a:decimal} for each 'a' */
	while(a < 20)	
	{
		printf("the value of a is %d\n",a) ;

		a++ ;
	}

	return 0 ;	
}
```
## for
```c

# include <stdio.h>

int main()
{
	for(int a = 10; a < 20; a += 1)	// for each { item : a } in  [10 ... 19]
	{
		printf("the value of a is %d\n",a) ;	// printf every "the value of a is {a}\n" {a:decimal} corresponding to each 'a'
	}

	return 0 ;	
}
```
## do while
```c

#include<stdio.h>

int main()	/* def main */
{
	int a = 10 ;	

	do	// do the internal
	{
		printf("the value of a is %d\n",a) ;	// printf "the value of a is {a}\n"{a:decimal}

		a = a + 1 ;
	}while(a <= 20); 	// continue while 'a' < 20

	return 0 ;	
}
```
# nested loops
## search all prime-numbers in [2,100)
```c

#include<stdio.h>


int main()
{
	int i, j ;	// create empty var [i,j], int, null

	/* print all prime-numbers in [2,100) */
	for(i = 2; i < 100; i++)	// for each i in [2,99]
	{
		for(j = 2; j <= (i/j); j++)	// j0=2. while j <= i/j, do the internal and j++
		{	
			if(!(i%j)) break ;	// if i%j == 0, break loop
		}

		if(j > (i/j))	printf("%d is print-number\n",i) ;	
	}

	return 0 ; 
}
```
## Yanghui's triangle, numericla
```c

#include<stdio.h>


int main()
{
	int i, j ;
	
	i = 1 ;		// set row = 1	
	while(i <= 5)	// while row <= 5
	{
		j = 1 ;		// set col = 1
		while(j <= i)	// while col <= row	
		{	
			printf("%d",j) ;	

			j++ ;	// next col 
		}

		printf("\n") ;	

		i++ ;	// next row
	}

	return 0 ; 
}
```
## Yanghui's triangle, *
```c

#include<stdio.h>


int main()	
{
	int i, j ; 

	i = 1 ;

	do	// do the internal
	{
		j = 1 ;	// set col = 1

		do	// do the internal
		{	
			printf("*") ;	
			j++ ;	// next col
		}while(j <= i) ;	// continue while col <= row	

		i++ ;		// next row

		printf("\n") ;		
	}while(i <= 5) ;	// continue while row <= 5

	return 0 ;	
}

```
# loop control statement
## break
```c

# include <stdio.h>


int main()
{
	int a = 10 ;

	while( a < 20 )
	{
		printf("the value of a is %d\n",a) ;
		
		a++ ;

		if ( a > 15 )	
		{
			break;
		}
	}

	
	return 0 ;
}
```

## continue
```c

#include <stdio.h>


int main ()	// def main
{
	int a = 10 ;

	do // do the internal
	{
		if( a == 15 )	
		{
			a++ ;

			continue ;	// next a
		}

		printf("the value of a is %d\n",a) ;	

		a++ ;
	}while(a < 20);		// continue while a < 20

	return 0 ;
}
```

## goto
```c

# include <stdio.h>

int main()	
{
	int a = 10 ;

	LOOP: do	// do the internal. LABEL = LOOP
	{
		if ( a == 15 )
		{
			a += 1 ;

			goto LOOP ;	// goto LOOP
		}

		printf("the value of a is %d\n",a) ;	
		
		a++ ;
	}while(a < 20);	// continue while a < 20

	return 0 ;	
}
```