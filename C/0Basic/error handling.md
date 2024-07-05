```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

int main()
{
	/* save ./unexist.txt to read to pf, read as binery */
	FILE *pf ;
	pf = fopen("unexist.txt", "rb") ;

	if (pf == NULL)	// if file pf not exsist
	{
		fprintf(stderr,"error is : %d\n",errno) ;	//	printf standard error : "error id : { error id }\n"{ %d }
		perror("output error by perror") ;	//	echo error : "output error by perror" + ":" + "{ current error }" 
		fprintf(stderr,"error opening the file %s\n",strerror( errno )) ;	//	printf stderr : "error opening the file: { current stderr }\n"{ %s }
	}
	else	// otherwise
	{
		fclose(pf) ;	// close file pf
	}

	return 0 ;
}
```
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
	int dividened = 20 ;	// create var dividened = 20, int, auto
	int divisor = 0 ;	// create var divisor = 0, int auto
	int quotinent ;	// create empty var quotinent, int, auto

	if ( divisor == 0 )	// if divisor = 0
	{
		fprintf(stderr, "divisor = 0, exit program ...\n") ;	// printf stderr : "divisor = 0, exit program ...\n"
		exit(-1) ;	// exit program with error
	}
	
	/* otherwise, do the internal */
	quotinent = dividened / divisor ;	// dividened / divisor | save to quotinent
	printf("quotinent = %d\n") ;	// printf "quotinent = { quotinent }\n}"{ %d }

	exit(0) ;	// exit program
}
```
```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
	int dividened = 20 ;	// create var dividened = 20, int, auto
	int divisor = 5 ;	// create var divisor = 5, int, auto
	int quotinent ;	// create empty var quotinent, int auto

	if ( divisor == 0 )	// if divisor = 0
	{
		fprintf(stderr, "divisor = 0, exit program ...\n") ;	// printf std err : "divisor = 5, exit program ...\n"
		return -1 ;	// exit program with error
	}

	/*otherwise, do the internal */
	quotinent = dividened / dividened ;
	printf("quotinent = %d\n", quotinent) ;
	return 0 ;
}
```

