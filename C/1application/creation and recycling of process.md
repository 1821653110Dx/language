# introduction
## concepts
- program
    - exec, which is static
- process
    - an execution process of a program, which is dynamic and includes creation, scheduling调度, execution, killing
## the status of a process
- running status : the process is running or preparing to run
- wating status : process is waiting for a certain event to occur or for resources
- stopping status : process is suspended中止（不止终止）
- dead status : process has been terminated but PCD hasn't been released
## types of processes
- interactive process : used for real-time interaction with the user
- batch processes批处理进程 : used for the automated execution of a series of tasks
- daemon processes守护进程 : provide system-level services and management in the background.

# check process
## view the processes mentioning <name>
    ps -elf | grep <name>
> meaning of parameters
```txt
F: process flag标志. 
    if 1, process can be cp but can't be execueted ; if 4, process use super user permission
S: process status.
    if -D, can't awakened
    if -R, running
    if -S, sleeping and can be awakened
    if -T, stopped
    if -X, dead status
    if -Z, terminated but costs mem
    if -s, includes subprocess
    if -l, multithreading
    if -+, background
    if -<, high priority
    if -N, low priority
    if -L, locked in mem
UID : user ID
PID : progress ID
PPID : parent progress父进程 ID
C : CPU%
PRI : original priority 
NI : current priority = PRI + NI
ADDR : mem addr
SZ : mem used
WCHAN : if - , running
TTY : terminal generating the process
TIME : time process occupy CPU
CMD : cmd generating the process
```
## check certain PID
    top -p <PID>
> short cuts of top
>> next page, S >

## fg/bg
- check forground progress
    - jobs
- execute suspened process in the bg
    - bg
- execute cmd in the bg
    - <cmd> &
- put current cmd in the bg and suspend it
    - C z
- execute background process in the fg
    - fg

## priority
- execute cmd according to the specified priority
    - nice-n <value> cmd
> for normal user, value in [0,19] and next value should > this value
> for root, value in [-20,19]

-  change priority
    - renice <value> <PID>

# create subprocess and terminate progress
## create subprocess
> the execution order between parent_process and child_process is determined by os
> Subprocesses only execute the code following the fork() that creates it
> subprocess is the cp of its parent_process
> subprocess and parent process exec in parallel
```c
#include<stdio.h>
#include<stdlib.h>
#include<errno.h>
#include<dirent.h>
#include<sys/stat.h>
#include <unistd.h>	// fork()


int main(int argc, char *argv[])
{
	pid_t pid ;
	pid = fork() ;	// create subprocess, return 0/-1/PID  | save to pid
	if (pid < 0)	// if fail to create subprocess
	{
		perror("fork!!") ;	// echo error "fork" ;
		
		return -1 ;	//  return -1 to show encountring error and exit current process 
	}
	if (pid == 0)	// not previous condition and current process is the subprocess
	{
		printf("child process : my pid is %d\n", getpid()) ;	// get current process's pid | printf "child process : my pid is { the return }\n"{ %d }
														
		return 0 ;	// return 0 to show encounting no error, exit current process   // return in main() will kill  current process, "return" in customed func won't kill current process but cause the exit of it
	}
	else
	{
		printf("parent process : my pid is %d\n", getpid()) ;

		return 0 ;	//  return 0 to show encounting no error, exit current process
	}
}
```
## exit process
```c
#include<stdio.h>
#include<stdlib.h>

int main()
{
	printf("this process will exit") ;
	exit(0) ;	// exit current process
	printf("never be displayed") ;
}
```
exit函数作用是直接结束进程，wait函数作用是等待子进程结束，并返回子进程的进程号
## recycle process
```c
#include<stdio.h>
#include<stdlib.h>
#include<errno.h>
#include<dirent.h>
#include<sys/stat.h>
#include<unistd.h>	// fork()
#include<sys/wait.h>	// wait()

int main(int argc, char *argv[])
{
	pid_t pid ;
	int status ;
	pid = fork() ;	// create subprocess, return 0/-1/PID | save to pid
	
	if (pid < 0)	// if fail to create subprocess
	{
		perror("fork!") ;	// echo error "fork!"

		exit(-1) ;	// return status_code -1 to show encountering error, exit current process directly
	}
	else if (pid == 0)	// not previous condition and current process is the subprocess
	{
		sleep(1) ;	// pause for 1s

		exit(2) ;	// return status_code 2 to show in subprocess, exit current process directly
	}
	else
	{
		wait(&status) ;	// wait for the subprocess to exit, save its exit status and other imformation to addr of status	// if func is used to modify arg'value, pass addr of arg
		printf("%x\n", status) ;	// printf "{ status }\n"{ %x }
	}

	return 0 ;
}
```
```c
// the following are macroes
WIFEXITED(status)   // check exit status of subprocess in status, return > 0 if exit normally, otherwise 0    // exit subprocess normally = the subprocess isn't terminated for receiving a signal
WEXITSTATUS(status) // cp exit status of subprocess in status
WIFSIGNALED(status) // check exit status of subprocess in status, return 0 if exit normally, otheriwse != 0
WTERMSIG(status)    // cp the signal number causing the termination of subprocess
```
```c
#include<sys/wait.h>
pid_t waitpid(pid_t pid, int *status, int option);  // wait(&status) = waitpid(-1,&status, 0)
```
