# types
- stdin 标准输入流
- stdout 标准输出流
- stderr 标准错误流
> the buffering of stdin and stdout is row buffering by default
> stderr has no buffering

# file
## definition
a squential collection of data
## types
	r = routing file
	d = dir file
	c = characte device file
	b = block device file
	l = symbolic link(symlik) file

# introcution of standard I/O
standard I/O(not system I/O),  also known as stdio.h, use struct FILE to store data of opened files. all options of std I/O revolve around$\tiny 围绕$ the FILE

> I(Input) are input dev, such as keyboars, mouses
> O(output) are output dev, such as monitors.

# system calls$\tiny 系统调用$ and library functions$\tiny 库函数$
- system calls
	-	interface functions$\tiny 接口函数$ provided by the system
	-	library functions are functions that encapsulate$\tiny 封装$ system calls. for example, printf is a library function calling system calls

# stream
FILE is also refered to as a stream, including txt stream and binary stream

# buffering$\tiny 缓冲$
buffering is the process of storing temporary data
## types
- full buffering
	- output when the buffer is full
- row buffering
	- out put when meeting \n
- non buffering
	- directly write data without buffering of stream

# the input and output
## for single char
- read single char
```c
#include <stdio.h>

int main(int argc, char *argv[])
{
	int ch = 0 ;	// create var ch = 0, int, auto	// ch save the return fgetc(), its dtype = int
	int counts = 0 ;	// create var counts = 0, int, auto
	
	ch = fgetc(stdin) ;	// read a char from stdin(standard input) | save to ch
	printf("%c\n", ch) ;	// printf "{ ch }\n"{ %c }

	FILE *fp ;
	if ( (fp=fopen(argv[1],"r")) == NULL )	// save file(name = 1st argument) in mode = read to fp | if file saved in fp not exist		// EOF = end-of-file char
	{
		perror("fopen") ;	// echo error : "fopen"
		return -1 ;	
	}

	/* otherwise, calc char counts of file saved in fp */
	while( (ch = fgetc(fp)) != EOF )	//  read a char from file saved in fp | save to ch | while char saved in ch not EOF
	{
		counts ++ ;	// { char counts : counts } += 1
	}

	/* close opened files */
	fclose(fp) ;

	printf("total %d bytes\n", counts) ;	// printf "total { counts } bytes\n"{ %d }

	return 0 ;
}
```
- write single char
```c
#include <stdio.h>

int main(int argc, char *argv[])
{
	FILE *fp ;
	int ch ;	create empty var ch, int, auto
	if((fp = fopen(argv[1],"w")) == NULL)	// save file(name = 1st argument) in mode = write to fp | if the file not exsist
	{
		perror("fopen") ;	// echo error : "fopen"
		
		return -1 ;
	}

	/* otherwise, write every char from ['a'...'z'] into file fp */
	for (ch = 'a' ; ch <= 'z' ; ch++ )	// for each char in ['a'...'z']
	{
		fputc(ch, fp) ;	// write current r into fp, fp points to netx char
	}

	return 0 ;
}
```
## for entire row
- read a row
```c
#include<stdio.h>
#include<string.h>

#define N 6

int main(int argc, char *argv[])
{
	char buf[N+1] ;	// create empty buffer buf[N+1]
	fgets(buf, N, stdin) ;	// read N bytes at most from standard_input to buffer buf
	
	printf("%s", buf) ;	// printf "{ buf }"{ %s }
	return 0 ;
}
```
- append a row
```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
	puts("hello world") ;	// newline print "hello world"
	
	char buf[] = "hello world" ;	// create static_varstr buf[] = "hello world", char, auto
	
	FILE *fp ;
	if((fp = fopen(argv[1],"a")) == NULL)	// save file(name = 1st argument) in mode = append to fp | if the file not exist
	{
		perror("fopen") ;	// echo error : "fopen"

		return -1;
	}

	/* otherwise, write "{ buf }" to fp, fp points to next char */
	fputs(buf, fp) ;

	/* close opened files */
	fclose(fp) ;

	return 0 ;
}
```

## for binary files
txt files store text only, while binary files can store data of any types
```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
	int s[11] ;	// create empty static_varlist s[10], int, auto
	
	FILE *fp ;
	fp = fopen(argv[1], "w+") ;	// save file(name = 1st argument) in mode = [read, write] to fp

	if(fread(s, sizeof(int), 10, fp) > 0)	// read 10 bytes at most from file fp to static_varlist s in binary form, each size = int | if num of data read < 0
	{
		perror("fread") ;	// echo error "fread" ;

		return -1 ;
	}

	struct student	// def struct student
	{
		/* member = [var no, static_varstr name[8], var score],
		   dtype  = [int, char, float] */
		int no ;
		char name[8] ;
		float score ;
		
	} stud[] = {{1, "zhang", 97}, {2, "wang", 95}} ; // create a static_varlist stud[] of this type, its value = {{ no, name, score }} = {{1 "zhang", 97}, {2, "wang", 95}}
	
	fwrite(stud, sizeof(struct student), 2, fp) ;	// write items from stud of student type to file fp in binary form, 2 items in total, fp points to next char
	
	/* close opened files */
	fclose(fp) ;

	return 0 ;
}
```
