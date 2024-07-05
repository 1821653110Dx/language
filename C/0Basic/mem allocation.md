# dynamic mem allocation
- mem dynamically allocated can be reallocated, while mem statically allocate can't be reallocated
- used to create varlist whose size can be changed(size of varlist directly def can't be changed)
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
	char name[100] ;	// create empty static_varstr name[100], non alloc	// size of varlist created this way can't be changed
	char *description = ( char * )malloc( 200 * sizeof(char) ) ;	// create an empty dynamic_varlist description, costed mem = size of 200char

	strcpy(name, "Zara Ali") ;	// cp "Zara Ali" to name

	if( description == NULL )
	{
		fprintf(stderr,"Error - unable to allocate required memory\n") ;	// printf standard error : "Error - unable to allocate required memory\n"
	}
	else
	{
		strcpy(description, "Zara ali a DPS student in class 10th") ;	// cp "Zara ali a DPS student in class 10th" to addr description points to
	}

	printf("Name = %s\n", name) ;	// printf "Name = { name }\n"{ %s }
	printf("Description : %s", description) ;	// printf "Description: { value at mem description points to }"{ %s }

	free(description) ;	// free mem costed by description 
	return 0 ;
}
```
# realloc mem dynamically allocated
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
	char name[100] ;	// create empty static_varstr name[100], non alloc
	char *description  = (char*)malloc(30*sizeof(char));	// create an empty dynamic_varlist description, costed mem = size of 30char

	strcpy(name, "Zara Ali") ;	// cp "Zara Ali" to name

	if ( description == NULL )
	{
		fprintf(stderr,"Error - unable to allocate memory\n") ;	// printf stderr : "Error - unable to allocate memory\n"
	}
	else
	{
		strcpy(description, "Zara ali a DPS student.") ;	// cp "Zara ali a DPS student." to mem description points to
	}

	description = (char*)realloc(description, 100*sizeof(char)) ;	// set mem costed by description = sizeof 100 char

	if (description == NULL )
	{
		fprintf(stderr,"Error - unable to allocate memory\n") ;	// printf stderr : "Error - unable to allocate memory\n"
	}
	else
	{
		strcat(description,"She is in class 10th") ;	// append "She is in class 10th" to mem description points to
	}

	printf("Name = %s\n", name) ;	// printf "Name = { name }\n"{ %s }
	printf("Description: %s", description) ;	// printf "Description: { value at mem description points to }"{ %s }

	free(description) ;	// free mem costed by description

	return 0 ;
}
```


