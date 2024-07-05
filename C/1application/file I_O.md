# introduction
file I/O, also known as system I/O, is a system call
# fd = file descriptor$\tiny 文件描述符$
a number in [0,1023], representing the file

# application of file I/O
## open/close
```c
#include <fcntl.h>
int open(cost char *pathname, int flags, mode_t mode) ;
/*
	flags(the follwoing is applicable for pure file, not dir)
		O_RDONLY(read)
		O_WRONLY(nonover-write)
		O_WRONLY|O_TRUNC(overwite)
		O_RDWR(read_nonover-write)
		O_RDWR|I_TRUNC(read_over-write)
		O_CREAT(create)
		O_APPEND(append)

		O_NOCTTY(add when current file can't be used as the terminal for current process进程)
		O_EXCL
	mode(add when )
		1 x
		2 w
		4 r
		for example, 0664 = (set)(owner's permission = 2(write)+4(read))(group' permission = 2+4)(others' permission = 4)
*/
```
```c
#include <stdio.h>
#include <fcntl.h>
#include <errno.h>	// for errno, EEXIST

int main(int argc, char *argv[])
{
	int fd ;
	if( ( fd = open("1.txt", O_RDWR|O_CREAT|O_EXCL, 0666) ) < 0 )	// if 1.txt to read and non-overwite not found, create it and set permissions of [usr, group, others] = rw， return its fd. Otherwise do nothing | save to fd | if opening fails
	{
		if(errno == EEXIST)	// if file has alread exists
		{
			perror("exist error") ;	// echo error "exist error"

			return -1 ;
		}
		else
		{
			perror("other error") ;	// echo error "other error"

			return -1 ;
		}
	}

    /* close opened files */
    close(fd) ;     // close file corresponding to fd of fd

    return 0 ;
}
```
## write
```c
#include <stdio.h>
#include <errno.h>
#include <fcntl.h>
#include <string.h>
#include  <unistd.h>	// write(), close()

int main(int argc, char *argv[])
{
	int fd ;
	char buf[20] ;
	if( (fd = open(argv[1], O_RDWR | O_CREAT | O_TRUNC, 0666)) < 0 )	// if 1.txt to read and overwite not found, create it and set permissions of [usr, group, others] = rw。 return its fd| save to fd | if opening fails	// 。can not be replaced with ,
	{
		perror("open") ;	// echo error "open"

		return -1 ;
	}
	/* otherwise */
	while ((fgets(buf, 20, stdin)) != NULL)	// read 20 bytes at most from stdin to buffer buf | while not break
	{
		/* if inputed "quit\n", break loop */
		if(strcmp(buf, "quit\n") == 0)	// if str buf = "quit\n"
		{
			break ;
		}
		/* otherwise */
		write(fd, buf, strlen(buf)) ;	// write str in buffer buf into file corresponding to fd of fd, fptr points to next char
	}

	/* close opened files */
	close(fd) ;	// close file corresponding to fd of fd

	return 0 ;
}
```
## read
```c
#include <stdio.h>
#include <errno.h>
#include <fcntl.h>
#include <string.h>
#include  <unistd.h>	// write(), close(), read()

int main(int argc, char *argv[])
{
	int fd, n ;
	int total = 0 ;
	char buf[64] ;
	
	if(argc < 2)	// if received arg counts < 2	// if user don't give names of files
	{
		printf("file names are required\n") ;

		return -1 ;
	}

	if ( (fd = open(argv[1], O_RDONLY)) < 0 )	// open file(name = first argument ) to read, return a fd | save to fd | if open fails
	{
		perror("open") ;	// echo error : "open"

		return -1 ;
	}

	/* count total bytes of the file */
	while( (n = read(fd, buf, 64))  > 0 )	// read 64 bytes at most from current char correspond to fd's fd into buffer buf, return counts of bytes read , fptr points to next char | save to n | while > 0 	// bytes read 实际读取的字节数
	{
		total += n ;	// { total bytes : total } += { bytes current read }
	}

	printf("%d", total) ;

	return 0 ;
}
```

## positioning
```c
#include <unistd.h>
off_t lseek(int fd, off_t offset, int whence) ; // make fptr corresponding to fd of fd points to no.offset bytes from whence    // no.offset = number offset
/*
whence =
    SEEK_SET = 1st char
    SEEK_CUR = current char
    SEEK_END = last char
*/
```

## write a log program using file IO functions
```c
#include <stdio.h>
#include<unistd.h>
#include<time.h>
#include<string.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>

int main(int argc, char *argv[])
{
	long int clock ;
	struct tm *clocktime ;
	int p ;
	int order = 1 ;
	char str[32], buff[32] ;
	if ( (p = open("1.txt", O_CREAT | O_RDWR | O_APPEND , 0664)) < 0 )	// if 1.txt to read and non-overwite and append not found, create it and set permissions of [usr, group, others] = rw-rw-w. return its fd| save to p | if opening fails
	{
		perror("fopen:") ;	// echo error "fopen:"
		
		return -1 ;
	}

	/* count row counts to order */
	while(read(p, str, 32) != 0)	// read 32 bytes at most from current char of file corresponding to fd of p into buffer str, return counts of bytes read, fptr points to next char | while != 0
	{
		if( str[strlen(str)] == '\0')	// if last char of str is \0	// last char != last non\0 char
		{
			order++ ;	// row counts ++
		}
	}

	while(1)	// do the internal while not break 
	{
		clock = time(NULL) ;	// save current systime to clock
		clocktime = localtime(&clock) ; // time saved in clock >>> prt points to struct tm(incle local time) | clocktime points to the ptr
		
		/* mewline print current local time */
		sprintf(buff, "%04d-%02d-%02d %02d:%02d:%02d\n", clocktime->tm_year+1900, clocktime->tm_mon+1, clocktime->tm_mday, clocktime->tm_hour, clocktime->tm_min, clocktime->tm_sec) ;	// write "{ year }-{ month }-{ day } { hour }:{ min }--{ sec }\n"{0:fill=0,len=4,dtype=d; foll=0,len=2,dtype=2} into buffer buff
		printf("%s", buff) ;

		/* write current local time to file correspinding to fp of p, fptr points to next char */
		if (write(p, buff, strlen(buff)) == -1)	// write str in buffer buff into file corresponding to fd of p | if write fails
		{
			perror("write:") ;	// echo error "write:"

			return -1 ;
		}

		memset(buff, 0, sizeof(buff)) ;	// clear buffer buff
		order++ ;	// row counts ++

		sleep(1) ;	// pause for 1s
	}

	return 0 ;
}
```
