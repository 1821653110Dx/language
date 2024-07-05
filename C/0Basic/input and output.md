# scan() & printf()
```c
#include <stdio.h>

int main()	// def main
{
	float f ;	// create empty var f, float, auto
	
	printf("Enter a number: ") ;	// printf "Enter a number: "
	scanf("%f", &f) ;	// let usr input "{ number }" and enter, save to f as %f
	printf("Value = %f", f) ;	// printf "Value = { number }"{ %f }
	
	return 0 ;	// exit program
}
```
# getchar() & putchar()
```c
#include <stdio.h>

int main()	// def main
{
	int c ;	//  create empty var c, int, auto
	
	printf("Enter a digit :") ;	// printf "Enter a value :"
	c = getchar() ;	// let usr input a char and newline | save to c
	
	printf("You entered: ") ;	// printf "You entered: "
	putchar(c) ;	// output char c
	printf("\n") ;	// newline
	
	return 0 ;	// exit program
}
```
# gets() & puts()
```c
#include <stdio.h>

int main()	// def main
{
	char str[100] ;	// create empty static_varstr str[100], auto, non realloc
	
	printf("Enter a value: ") ;	// printf "Enter a value :"
	gets(str) ;	// let usr input a str and newline | save to str
	
	printf("You Entered: ") ;	// printf "You Entered: "
	puts(str) ;	// output str str
	
	return 0 ;	// exit program
}
```


