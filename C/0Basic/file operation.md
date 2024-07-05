# mode
	r   read
	w   create, write
	a   create, append
	r+  read_write
	w+  create, read_write
	a+  create, read, append

# write
```c
#include <stdio.h>

int main()
{
	/* if ./test.txt to read and write not found, create it, return its addr | save to fp */
	FILE *fp = NULL ;
	fp = fopen("./test.txt", "w+") ;
	
	fprintf(fp, "This is testing for fprintf...\n") ;	// write "This is testing for fprintf...\n" to fp, fp points to next char
	fputs("This is testing for fputs...\n", fp) ;	// write "This is testing for fputs...\n" to fp, fp points to next char

	/* close opened files */
	fclose(fp) ;
}
```

# read
```c
#include <stdio.h>

int main()
{
	char buff[255] ;
	
	/* open ./test.txt to read, return its addr | save to fp  */
	FILE *fp = NULL ;
	fp = fopen("./test.txt", "r") ;

	fscanf(fp, "%s", buff) ;	// read all chars before ' ' from current char fp points to into buffer buff , fptr points to next char
	printf("1: %s\n", buff) ;	// printf "1: { buff }\n"{ %s }
	
	fgets(buff, 254, (FILE*)fp) ;	// read 254 chars at most from current char fp points to into buffer buff, fptr points to next char
	printf("2: %s\n", buff) ;

	fgets(buff, 254, (FILE*)fp) ;
	printf("3: %s\n", buff) ;
}
```
