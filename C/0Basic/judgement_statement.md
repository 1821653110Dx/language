# if
```c

# include <stdio.h>	/* include stdio.h */

int main()	
{
	int a = 10 ;	// create var a = 10, int, auto
	
	if(a < 20)
	{
		printf("a is less than 20\n");	// printf "a is less than 20 \n"
	}

	printf("the value of a is %d",a) ;	

	return 0 ;
}
```

# if ... else
```c

#include <stdio.h>	/* include stdio.h */

int main()
{
	int a = 100 ;

	if(a < 20)	
	{
		printf("a < 20\n") ;
	}
	else	// otherwise
	{
		printf("a > 20\n") ;
	}

	printf("a = %d",a) ;	// printf "a = {a}"{ %d }

	return 0 ;
}
```

# if ... else if ... else
```c

#include <stdio.h>	/* include stdio.h */

int main()	
{
	int a = 100 ;	

	if(a == 10)	
	{
		printf("a = 10\n") ;	
	}
	else if(a == 20)	// not previous condition and a == 20	
	{
		printf("a = 20\n") ;
	}
	else if(a == 30)	// not previous condition and a = 30
	{
		printf("a = 30\n") ;
	}
	else	// otherwise 
	{
		printf("Not Match\n") ;	
	}

	printf("the value of a = %d",a) ;

	return 0 ;
}
```

# Nested if
```c

#include <stdio.h>	/* include stdio.h */

int main()
{
	int a = 100 ;
	int b = 200 ;

	if(a == 100)
	{
		if(b == 100)	
		{
			printf("the value of a is 100, and value of b is 200\n") ;	
		}
	}

	printf("the value of a is %d\n",a) ;
	printf("the value of b is %d",b) ;

	return 0 ;
}
```

# switch
```c

#include <stdio.h>	/* include stdio.h */

int main()	
{
	char grade = 'B' ;	// create var grade = 'B', char, auto

	switch(grade)	// Switch next step according to 'grade'
	{
		case 'A' :	// if= 'A'
			printf("Great !\n") ;
			break ;		// next step 
		case 'B' :	// if = 'B', then next step 
		case 'C' :	// if = 'C' 
			printf("Nice Try !\n") ; 
			break ;	// next step
		case 'D' :	// if = 'D'
			printf("It's better to do it again.\n") ;	
				break ;
		case 'E' :
			printf("valid grade\n") ;	
	}

	printf("your grade is %d",grade) ;

	return 0 ;
}
```

# nested switch
```c

#include <stdio.h>	/* include stdio.h */

int main()
{
	int a = 100 ;	
	int b = 200 ;

	switch(a)	// switch next step according to a
	{
		case 100 :	// if = 100 
			printf("This is a part of external switch\n") ;		

			switch(b)	// swicth next step accoding to b
			{
				case 200 :
					printf("This is a part of internal switch\n") ;	
			}
	}

	printf("the value of a is %d\n",a) ;	
	printf("the value of b is %d\n",b) ;

	return 0 ;
}
```