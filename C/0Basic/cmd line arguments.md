	complile the code
```c
#include <stdio.h>

int main(int argc, char *argv[])	// def main : argc = received arg counts + 1, argv = program_name and received arg 
{
	printf("Program name %s\n",argv[0]) ;	// printf "Program name { program name }\n"{ %s }

	if ( argc == 2 )	// if arg counts = 1
	{
		printf("The argument supplied is %s\n", argv[1]) ;	// printf "The argument supplied is { first argument }\n"{ %s }
	}
	else if ( argc > 2 )
	{
		printf("Too many arguments supplied.\n") ;
	}
	else
	{
		printf("One argument expected.\n") ;
	}

	return 0 ;
}
```
	then do the following
		./a.out arg
		./a.out arg1 arg2
		./a.out	// when not giving arg, the arg counts = 1
		./a.out "arg arg"	// "arg arg" is one arg include space. when you give a arg include space, you need to do it this way
