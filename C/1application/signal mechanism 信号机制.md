# signal mechanism
a simulation of interupt mechanism at the software level
## common signals
![175ac1bb87b85e32caf00ce7b0c00692.png](../../../_resources/175ac1bb87b85e32caf00ce7b0c00692.png)
## cmd
### check all signals
	kill -l

### send signal
	kill pid	// send signal SIGERM to process(pid = pid)
	kill -sig pid // send signal sig to process(pid = pid)
### kill
	kill -u user	// kill all processes of user user

## send signal
```c
#include  <unistd.h>
#include <signal.h>
int  kill(pid_t pid,  int sig) ;	// send signal sig to process(pid = pid)
int  raise(int sig);	// send signal sig to curreng process
/*
* pid
*	> 0 certain process
*	= 0 process in the same group as current process
*	= -1 all process
*	< -1 all process of the group corrresponding to the pid
*/
```
## timer计时器
```c
unsigned int alarm(unistdunsigned int seconds) ;	// set a timer of seconds seconds, return the remain seconds of previous alarm
useconds_t ualarm(useconds_t usecs, useconds_t interval) ;	// set a timer triggerd after usecs unitseconds and repeated every interval unitseconds, return the remain unitseconds of previous alarm
```
```c
int setitimer(int which, const struct itimerval *new_value,struct itimerval *old_value);	// set a timer, send SIGALARM signal after timeout(can be replaced with "send SIGVTALARM after timeout in usermode" or "send SIGPROF after timeout in usermode/kernel_mode"), init_time and intervals saved in struct itimeval new_value points to, save the previous time to struct itimerval  old_value points to

struct itimerval 
{
	struct timeval it_interval;  // 闹钟触发周期
	struct timeval it_value;    // 闹钟触发时间
};

struct timeval 
{
    time_t      tv_sec;         /* seconds */
    suseconds_t tv_usec;        /* microseconds */
};
```
## capture signal
![1ab30d35e07702bd51a02857c0197549.png](../../../_resources/1ab30d35e07702bd51a02857c0197549.png)
```c
#include <signal.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <linux/posix_types.h>

typedef void(*sighandler_t)(int) ;	// alias void (*)(int) = sighandler_t	// void (*)(int) is a func_ptr type, which receives a int arg and return void
sighandler_t oldact ;	// create empty var oldact, sighandler_t, global

/* decalre func to call */
void handle(int sig) ;


int main()
{
	oldact = signal(SIGINT, handle) ;	// set to call sig_handler handle when current process receives sig SIGINT, return previouss sig_handler | save to oldact
	
	while(1)
	{
		sleep(1) ;
	}

	return 0 ;
}

void handle(int sig)	// def func handle : arg = sig, dvalue = null, dtype = int, r = void
{
	printf("I catch the SIGINT \n") ;
}
```
```c
/*
 * introduction
 *	void (*sa_handler)(int)	// create func_ptr sa_handler : arg_num = 1, dtype = int, r void
 */
#include <signal.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <linux/posix_types.h>


/* decalre func to call */
void handle(int sig) ;

int main()
{
	/* create and init var act of struct sigaction */
	struct sigaction act ;	// create empty var act, struct sigaction
	act.sa_handler = handle ;	// set sig_handler信号处理函数 = handle
	act.sa_flags = 0 ;	// set flags = 0	// 0 means defalut
	sigemptyset(&act.sa_mask) ;	// empty signal blocking set
	
	sigaction(SIGINT, &act, NULL) ;	// set to call sig_handler in var act of struct sigaction when receive signal SIGINT
	alarm(1) ;	// send signal SIGALARM after 1s
	sigaction(SIGALRM, &act, NULL) ;	// set to call sig_handler in var act of struct sigaction when receive signal SIGALARM
	
	while(1)
	{
		sleep(1) ;
	}

	return 0 ;
}

void handle(int sig)	// def func handle : arg = sig, dvalue = null, dtype = int, r = void
{
	if(sig == SIGINT)	// if received signal = SIGINT
	{
		printf("I catch the SIGINT \n") ;
	}
	else if (sig == SIGALRM)
	{
		printf("second timer \n") ;
		alarm(1) ;	// send signal SIGALARM after 1s
	}
}
```
```c
#include<stdio.h>
#include<signal.h>
#include<unistd.h>
#include<sys/wait.h>
#include<stdlib.h>

/* declare func to call */
void handle(int sig) ;

int main(int argc, const char *argv[])
{
	pid_t pid ;
	/* create and init var act of struct sigaction */
	struct sigaction act ;	// create empty var act, struct sigaction
	act.sa_handler = handle ;	// set sig_handler = handle
	act.sa_flags = 0 ;	// set flags = 0
	sigemptyset(&act.sa_mask) ;	// empty signal blocking set
	
	pid = fork() ;	// create subprocess, return 0/-1/PID | save to pid
	if (pid > 0)	// if current process is the parent_process
	{
		sigaction(SIGCHLD, &act, NULL) ;	// set to call sig_handler in var act of struct sigaction when receive signal SIGCHLD
		while(1)
		{
			sleep(1) ;
			printf("father\n") ;
		}
	}
	else if (pid == 0)	// not previous condition and current process is the subprocess
	{
		sleep(2) ;
		exit(0) ;	// return 0 and exit current process directly
	}

	return 0 ;
}

void handle(int sig)	// def func handle : arg = sig, dvalue = null, dtype = int, r void
{
	wait(NULL) ;	// wait for any subprocess to finish
	if (sig == SIGCHLD)	// if received signal = SIGCHILD
	{
		printf("I catch SIGCHLD\n") ;
	}
}
```
# signal set and signal blocking
- through blocking signal阻塞信号 we can handle signals after a while
- block signal : prevent signals from being handling instead of being generating
- status of signal
	- Delivery = actual handling process of a signal
	- Pending = statet between generation and delivery
## signal set handler
```c
sigset_t set;  //自定义信号集。  
//是一个32bit  64bit  128bit的数组。

sigemptyset(sigset_t *set);	//清空信号集

sigfillset(sigset_t *set);	//全部置1

sigaddset(sigset_t *set, int signum); 
//将一个信号添加到集合中

sigdelset(sigset_t *set, int signum); 
//将一个信号从集合中移除

Aigismember(const sigset_t *set，int signum); 
//判断一个信号是否在集合中。



// 设定对信号集内的信号的处理方式(阻塞或不阻塞):
#include <signal.h>
int sigprocmask( int how, const sigset_t *restrict set, sigset_t *restrict oset );
/*
how可选用的值
    SIG_BLOCK ： 把参数set中的信号添加到信号屏蔽字中
    SIG_UNBLOCK： 从信号屏蔽字中删除参数set中的信号
    SIG_SETMASK： 把信号屏蔽字设置为参数set中的信号
*/
```
```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

/* declare func to call */
void handle(int sig) ;

int main()
{
	/* create and init var act of struct sigaction */
	struct sigaction act ;	// create empty var act, struct sigaction
	act.sa_handler = handle ;	// set sig_handler = handle
	act.sa_flags = 0 ;	// set flag = 0
	sigemptyset(&act.sa_mask) ;	// empty signal blockin set	// sig blocking set = the set with signals to block
	
	sigaction(SIGINT, &act, NULL) ;	// set to call sig_handler in struct var act of struct sigaction when receive signal SIGINT
	
	/* create and init signalset set */
	sigset_t set ;	// create empty var set, sigset_t
	sigemptyset(&set) ;	// empty signalset set
	sigaddset(&set, SIGINT) ;	// add signal SIGINT to signalset set
	
	sigprocmask(SIG_BLOCK, &set, NULL) ;	// block signals in signalset set
	sleep(5) ;
	sigprocmask(SIG_UNBLOCK, &set, NULL) ;	// unblock sig in signalset set
	
	while(1)
	{
		sleep(1) ;
	}

	return 0 ;
}

void handle(int sig)	// def func handle : arg = sig, dvalue = null, dtype = int, r void
{
	printf("I get sig=%d\n", sig) ;
}
```
## pause/sigsuspend
```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

/* decalre func to call */
void handle(int sig) ;
void mytask() ;

int main()
{
	/* create and init var act of struct sigaction */
	struct sigaction act ;	// create empty var act, struct sigaction
	act.sa_handler = handle ;	// set sig_handler = handle
	act.sa_flags = 0 ;	// set flag = 0
	sigemptyset(&act.sa_mask) ;	// empty signal blocking set
	
	sigaction(SIGINT, &act, NULL) ;	// set to call sig_handler in var act of struct sigaction when receive signal SIGINT
	sigaction(SIGHUP, &act, NULL) ;	// set to call sig_handler in var act of struct sigaction when receive signal SIGHUP
	
	/* create and init signalset set, set2 */
	sigset_t set, set2 ;	// create empty var [set, set2], sigset_t
	sigemptyset(&set) ;	// empty signalset set
	sigemptyset(&set2) ;	// empty signalset set2
	sigaddset(&set, SIGHUP) ;	// add signal SIGHUP to signalset set
	sigaddset(&set2, SIGINT) ;	// add signal SIGINT to signalset set2
	
	pause() ;	// wait for signal
	
	while(1)
	{
		sigprocmask(SIG_BLOCK, &set, NULL) ;	// block sig in signalset set
		mytask() ;
		sigsuspend(&set2) ;	// suspend current process until receive sig not in sigset set
	}
	printf("after pause") ;
	while(1)
	{
		sleep(1) ;
	}
	
	return 0 ;
}

void handle(int sig)	// def func handle : arg = sig, dvalue = null, dtype = int, r void
{
	printf("I get sig=%d\n", sig) ;
}

void mytask()	// def func mytsak: r void
{
	printf("my task start\n") ;
	sleep(3) ;
	printf("my task end\n") ;
}
```
