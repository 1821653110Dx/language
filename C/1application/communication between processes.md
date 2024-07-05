# pipe无名管道
```c
#include  <unistd.h>
int  pipe(int pfd[2]);
// pdf[2] save fd, pdf[0] = read_pipe, pdf[1] = write_pipe
```
![0de717607d81cd019bf4c56eaccfbb63.png](../../../_resources/0de717607d81cd019bf4c56eaccfbb63.png)
```c
#include<stdio.h>
#include<unistd.h>
#include<string.h>

int main(int argc, const char *argv[])
{
	char buf[20]  ;	// create empty buffer buf[20]
	pid_t pid ;

	int pipefd[2], pi, i ;
	pi = pipe(pipefd) ;	// create a pipe and return read_fd and write_fd to pipfd, return 0 / -1 | save to pi
	if (pi == -1)	// if creating pipe failed
	{
		perror("pipe") ;

		return -1 ;
	}
	
	/* create 2 subprocesses */
	for(i=0 ; i < 2 ; i++)	// for i in [0,1]
	{
		pid = fork() ;	// create subprocess, return 0/-1/PID | save to pid
		if(pid < 0)	// if fail to create subprocess
		{
			perror("pid create:") ;
			return 0 ;
		}
		else if(pid == 0)	// not previous condition and current process is the subprocess
		{
			break ;
		}
	}
	if(i == 2)	// if current process is parent process
	{
		close(pipefd[1]) ;	// close write_end of pipe corresponding to pipefd
		while(1)
		{
			memset(buf, 0, 20) ;	// init buffer buf	// 20 is the size of buf
			read(pipefd[0], buf, 20) ;	// read 20 bytes at most from read_end of pipe corresponding to pipefd into buffer buf, fptr points to next char

			printf("pipe read %s\n", buf) ;	// printf "pipe read { buf }\n"{ %s }

			usleep(2) ;
		}
	}
	if(i == 0)	// if current process is the 1st subprocess
	{
		close(pipefd[0]) ;	// close read_end of pipe corresponding to pipefd
		while(1)
		{
			memset(buf, 0, 20) ;	// init buffer buf
			strcpy(buf, "this is b") ;	// cp "this is b" to buf
			write(pipefd[1], buf, strlen(buf)) ;	// write str in buf into write_end of pipe corresponding to pipefd
			
			usleep(2) ;
		}
	}
	if(i == 1)	// if current process is the 2nd subprocess
	{
		close(pipefd[0]) ;
		while(1)
		{
			memset(buf, 0, 20) ;
			strcpy(buf, "this is a") ;
			write(pipefd[1], buf, strlen(buf)) ;
			usleep(2) ;
		}
	}
	
	return 0 ;
}
```
# 有名管道
```c
#include  <unistd.h>
#include <fcntl.h>
int  mkfifo(const char *path, mode_t mode);

open(const char *path, O_RDONLY);//1
open(const char *path, O_RDONLY | O_NONBLOCK);//无阻塞读
open(const char *path, O_WRONLY);//3
open(const char *path, O_WRONLY | O_NONBLOCK);//无阻塞写
```
## write pipe
```c
#include<stdio.h>
#include<unistd.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<sys/types.h>
#include<string.h>

int main(int argc, const char *argv[])
{
	int re, fd ;
	char buf[20] ;

	re = mkfifo("./myfifo", 0666) ;	// create pipe"/myfifo", permissions of [own, group, others] = rw, return 0/non 0 | save to re
	if (re < 0)	// if fail to create pipe
	{
		perror("mkfifo") ;

		return -1 ;
	}

	fd = open("./myfifo", O_WRONLY) ;	// open pipe"/myfifo" in mode = [nonover-write], return a fd | save to fd
	if(fd <0)	// if fail to open pipe
	{
		perror("open:") ;

		return -1 ;
	}

	while(1)
	{
		fgets(buf, 20, stdin) ;	// read 20 chars at most from stdin to buffer buf 
		write(fd, buf, strlen(buf)) ;	// write str in buffer buf into pipe corresponding to fd's fd, fptr points to next char
	}

	return 0 ;
}
```
## read pipe
```c
#include<stdio.h>
#include<unistd.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<sys/types.h>
#include<string.h>

int main(int argc, const char *argv[])
{
	int fd ;	
	char buf[20] ;
	
	fd = open("./myinfo", O_RDWONLY) ;	// open pipe"./myfifo" in mode = [read], return a fd | save to fd
	if (fd == -1)	// if fail to open pipe
	{
		perror("open:") ;

		return -1 ;
	}

	while(1)
	{
		read(fd, buf, 20) ;	// read 20 bytes at most from current char corresponding to fd's fd into buffer buf, fptr points to next char, return counts of bytes read
		
		printf("read = %s\n", buf) ;	// printf "read = { buf }\n"{ %s }
	}

	return 0 ;
}
```
