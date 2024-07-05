# define
```c

#include<stdio.h>

enum DAY	// def enum_class : DAY
{
	MON = 1, TUE, WED, THU, FRI, SAT, SUN	// members = [MON, TUE, WED, THU, FRI, SAT, SUN], value = [1..7]
};

int main()	// def main
{
	/* def enum_var day: value = WED, class = DAY */
	enum DAY day ;
	day = WED ;

	printf("%d", day) ;	// printf"{day}"{day:%d}
	
	return 0 ;	// exit
}
```
```c

#include<stdio.h>

enum DAY	// def enum_class : DAY
{
	MON = 1, TUE, WED, THU, FRI, SAT, SUN	// members = [MON, TUE, WED, THU, FRI, SAT, SUN], value = [1..7]
}day;	// var of the type : day


int main()	// def main
{
 	for (day = MON ; day <= SUN ; day++)	// MON <= day <= SUN, d 1. for each  
	{
		printf("the enum element: %d\n",day) ;	// printf"the enum element: {day}\n"{day:%d}
	}

	return 0 ;	// exit
}
```

# use with SWITCH
```c

#include<stdio.h>
#include<stdlib.h>

int main()	// def main
{
	enum color {red = 1, green, blue} ;	// def enum_class : name = color, members = [red, green, blue], value = [1..3]

	/* def enum_var favorite_color: value = null, calss = color */
	enum color favorite_color ;

	/* echo hint. let user input a line of elements, save it */
	printf("please input your favorite color: (1 .red, 2. green, 3. blue) : ") ;	// printf"please input your favorite color: (1 .red, 2. green, 3. blue) : "
	scanf("%u",&favorite_color) ;	// let user input, save it: to = 'favorite_color', format = %u
	
	/* output results */
	switch (favorite_color)	// switch next step accoding to 'favorite_color'
	{
		case red :	// if = 'red'
			printf("you favorite_color is red") ;	// printf"you favorite_color is red"
			break ;	// next step
		case green :	// if = 'green'
			printf("your favorite_color is green") ;	// printf"your favorite_color is green"
			break ;	// next step
		case blue :	// if = 'blue'
			printf("your favorite_color is blue") ;	// printf"your favorite_color is blue"
			break ;	// next step
		default :	// otherwise
			printf("your haven' selected your favorite_color") ;	// printf "your haven' selected your favorite_color"
	}

	return 0 ;	// exit
}
```
