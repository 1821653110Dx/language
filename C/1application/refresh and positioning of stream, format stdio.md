# strem
## refresh
```c
#include <stdio.h>
int fflush(FILE *fp) ;  // refresh stream, if sucessful, return 0, otherwise EOF(-1)
```
## positioning
```c
void rewind(fp) ;   // let fp points to the begining of the file
```
```c
#include <stdio.h>

int main(int argc, char *argv[])
{
	FILE *fp ;

	if((fp = fopen("test.txt","r")) == NULL)	// save the begin_addr of test.txt in mode = [read, write] to fp | if file fp points to not exist
	{
		perror("fopen") ;	// echo error "fopen"

		return -1 ;
	}

	/* print len of the file */
	fseek(fp, 0, SEEK_END) ;	// let fp points to the end of the file
	printf("len is %d", ftell(fp) ) ;	// return the location which file ptr fp points to | printf "len is { ~ }\n"{ %d }
	
	/* close opened files */
	fclose(fp) ;

	return 0 ;
}
```

# stdio
## formated standard output
```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
	int year = 2014, month  = 10, day = 26 ;	// create var [year, month, day] = [2014, 10, 26], int auto
	char buf[64] ;	// create empty buffer buf[64]
	
	FILE *fp ;
	fp = fopen("temp.txt", "r+") ;	// save begin_addr of temp.txt in mode = append to fp
	
	fprintf(fp, "%d-%d-%d\n", year, month, day) ;	// write "{ year }-{ month }-{ day }\n"{ %d } to file fp points to, fp points to next char
	sprintf(buf, "%d-%d-%d\n", year, month, day) ;	// write "{ year }-{ month }-{ day }\n"{ %d } to str buf
	
	printf("%s",buf) ;
	/* close opened files */
	fclose(fp)	;

	return 0 ;
}
```
## formated standard input
```c
int fscanf(FILE *stream, const char *format, ...) ; // read "{ str }"{ format } from stdin into file fp points to, fp points to next char
int sscanf(const char *str, ...) ; // read "{ }"{ } from stdin
```

# log storage program
## requiremennt
write current sys time into 1.txt every 1s.
```c
#include <stdio.h>
#include <unistd.h>
#include <time.h>
#include <string.h>

int main(int argc, char *argv)
{	
	char str[32] ;	// create empty buffer str[32]
	int order = 1 ;	// create var order = 1, int, auto
	long int clock ;	// create an empty var clock, long int, auto
	struct tm *clocktime ;	// create ptr_var clocktime of struct tm type
	
	FILE *p = fopen("1.txt", "a+") ;	// save begin_addr of 1.txt in mode = [create, read, append] to p
	
	if(p == NULL)	// if file p points to not exist
	{
		perror("fopen\n") ;	// echo error "fopen:"

		return -1 ;
	}

	/* get the current last row number of file p points to */
	while(str == fgets(str,32,p))	// read 32 bytes at most from char p points to into buffer str  | while not empty
	{
		if(str[strlen(str) - 1] == '\n')	// if the last non\0-char of buffer str = '\n'	// '\n' != "\n", '\n' is a char, "\n" is a string
		{
			order ++ ;	// { row counts : order } ++
		}
	}

	while(1)	// do the internal forever while not break
	{
		clock = time(NULL) ;	// save current system to clock
		clocktime = localtime(&clock);	// time saved in clock >>> ptr points to struct tm(include local time ) | clocktime points to the ptr

		/* newline print current local time */
		printf("%04d-%02d-%02d %02d:%02d:%02d\n", clocktime->tm_year+1900, clocktime->tm_mon+1, clocktime->tm_mday, clocktime->tm_hour, clocktime->tm_min, clocktime->tm_sec) ;	// printf "{ year }-{ month }-{ day } { hour }:{ min }-{ sec }\n"{ 0:fill=0,len=4,dtype=d; fill= 0,len=2,dtype=d  }

		/* write current local time to file p points to, fp points to next char */
		fprintf(p,"%04d-%02d-%02d %02d:%02d:%02d\n", clocktime->tm_year+1900, clocktime->tm_mon+1, clocktime->tm_mday, clocktime->tm_hour, clocktime->tm_min, clocktime->tm_sec) ;	// write "{ year }-{ month }-{ day } { hour }:{ min }-{ sec }\n"{ 0:fill=0,len=4,dtype=d; fill= 0,len=2,dtype=d  } to file p points to
 

		fflush(p) ;	// make sure all required data have been writen into file fp points to
		
		order++ ;	// update { row counts }

		sleep(1) ;	// pause for 1 s
	}

	/* close opened files */
	fclose(p) ;

	return 0 ;
}
```
