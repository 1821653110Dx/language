# exec family
## execl / execlp
```c
#include<stdio.h>
#include<stdlib.h>
#include<errno.h>
#include<unistd.h>	// execl, execlp

int main()
{
	if((execl("/bin/ls","ls","-a","-l","/etc",NULL)) < 0 )	// exec `ls -a -l /etc`, ls from program_path | if fail to exec
	{
		perror("execl") ;	// echo error "execl"

		return -1 ; 	
	}
	if((execlp("ls","-a","-l","/etc",NULL)) < 0)	// exec `ls -a -l /etc`, ls from env_var PATH | if fail to exec
	{
		perror("execlp") ;
		
		return -1 ;
	}

	return 0 ;
}
```
## execv / execvp
```c
#include<stdio.h>
#include<stdlib.h>
#include<errno.h>
#include<unistd.h>	// execv, execvp

int main()
{
	char *arg[] = {"ls", "-a", "-l", NULL} ;	// cmd arg points to : "ls -al /etc"

	if(execv("bin/ls", arg) < 0)	// exec cmd arg points to, ls from program_path | if fail to exec
	{
		perror("execv") ;

		return -1 ;
	}
	if(execvp("ls", arg) < 0)	// exec cmd arg points to, ls from env_var PATH | if fail to exec
	{
		perror("execlp") ;

		return -1 ;
	}

	return 0 ;
}
```
## system
```c
#include  <stdlib.h>
int system(const char *command);    // continuet the process after cmd command points to finished
```

# Deanmon Process 守护进程
Background service
## create
- linux cmd
nohup <cmd> &
- c
```c
#include<stdio.h>
#include<stdlib.h>
#include<errno.h>
#include<unistd.h>	

int main()
{
	pid_t pid, sid ;
    int a ;
	pid = fork() ;	// create subprocess, return 0 if in it, otherwise its PID | save to pid
	
	if (pid > 0)	// current process is parent process
	{
		printf("parent_process exit\n") ; 
		exit(0) ;	// return statue_code 0 to show in parent process, exit current process directly
	}
	else if (pid == 0)	// not previous condition and current process is subprocess
	{
		a = setsid() ;	// create a seession and make current process be the session_leader and group_leader, return 0 if sucess, otherwise < 0 | save to a
		if(sid < 0)	// if fail to create
		{
			perror("setid") ;
			exit(-1) ;	// return status_code -1 to show error occurs , exit current process directly
		}
		/* otherwise */
        sid = getsid(pid) ;    // return sid corresponding to pid of pid | save to sid
        printf("%d\n",sid) ;
		exit(2)	;	// return status code 2 to in subprocess , exit current process directly
	}
}
```
