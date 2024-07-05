# message queue
- message queue is a list with messages
- one messages one ID

# usage
## sending end
①申请Key

②打开/创建消息队列   msgget

③向消息队列发送消息   msgsnd
## receiving end
①打开/创建消息队列   msgget

②从消息队列接收消息   msgrcv

③控制（删除）消息队列   msgctl

## create a message queue
```c
#include <sys/ipc.h>
#include <sys/msg.h>
int msgget(key_t key, int msgflg);
```
```c
if((key = ftok(".", 'q')) == -1)    // create key key with [file,subid]=[".",ascii of 'q'] | if fail to create
{
    perror("ftok") ;
    exit(-1) ;
} 
if((msgid = msgget(key, IPC_CREAT|0666)) <  0)    // if message_queue(key = key) not found, create it  and set permissions of [usr, group,  others]=rw. return message_queue's id |     save to msgid | if fail to create
{   
    perror("msgget") ;
    exit(-1) ;
}
```
## send messages
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
#include<string.h>

/* def MSG type */
typedef struct	// def a struct
{
	/* member = [msg_type, buf[128]]	// msg_type = message type ;	buf = message text
	 * dtype = [long, char]
	 */
	long msg_type ;
	char buf[128] ;
} MSG; // name of struct = MSG
#define MSGSIZE (sizeof(MSG) - sizeof(long))	// define MSGSIZE  = sizeof(msgT) - sizeof(long)


int main(int argc, const char *argv[])
{
	int get ;
	key_t key ;

	key = ftok(".", 100) ;	// create key key with [file, subid] = [".", 100]
	if(key < 0)	// if fail to create
	{
		perror("ftok:") ;

		exit(-1) ;
	}

	get = msgget(key, IPC_CREAT|0666) ;	// if message_queue(key = key) not found, create it and set permissions of [usr, group, others] = rw. return message_queue's ID | save to get
	if(get < 0)	// if fail to create
	{
		perror("msgget:") ;

		exit(-1) ;
	}

	MSG msg ;	// create empty message msg
	msg.msg_type = 1 ;	// set mtype of message msg = 1
	strcpy(msg.buf, "The message 1") ;	// cp "The message 1" to buf of message msg
	
	if((msgsnd(get, &msg, MSGSIZE, 0)) < 0)	// send buf of message msg to message_queue(msgid = get) | if failed
	{
		perror("msgsnd :") ;

		exit(-1) ;
	}

	return 0 ;
}
```
## receive messages
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/msg.h>
#include<string.h>

/* def MSG type */
typedef struct	// def a struct
{
	/* member = [msg_type, buf[128]]	// msg_type = message type ;	buf = message text
	 * dtype = [long, char]
	 */
	long msg_type ;
	char buf[128] ;
} MSG; // name of struct = MSG
#define MSGSIZE (sizeof(MSG) - sizeof(long))	// define MSGSIZE  = sizeof(msgT) - sizeof(long)

int main(int argc, const char *argv[])
{
	int count ; 
	MSG msg ;	// create empty message msg

	key_t key ;
	key = ftok(".", 100) ;	// create key key with [file, subid] = [".", 100]
	if(key < 0)	// if fail to create
	{
		perror("ftok:") ;

		exit(-1) ;
	}

	int get  ;
	get = msgget(key, IPC_CREAT|0666) ;	// if message_queue(key = key) not found, create it and set permissions of [usr, group, others] = rw. return message_queue's ID | save to get
	if(get < 0)	// if fail to create
	{
		perror("msgget:") ;

		exit(-1) ;
	}

	while(1)
	{
		if((msgrcv(get, &msg, MSGSIZE, 0, 0)) < 0)	// receive message(mtype = 0) from message_queue(msgid = get) to message buf | if failed
		{
			perror("msgrcv") ;

			exit(-1) ;
		}
		count++ ;
		if (count == 4)
			break ;
		printf("msgrcv %s\n", msg.buf) ;
	}
	
	msgctl(get, IPC_RMID, NULL) ;	// del message_queue(msgid = get)

	return 0 ;		
}
```
# Semaphore
## operation
- P operation
```c
if (信号量的值大于0) 
{  
		申请资源的任务继续运行；
       信号量的值减一；
} 
else 
{   
		申请资源的任务阻塞；
} 
```
- v operation
```c
信号量的值加一；
if (有任务在等待资源)
{   
	唤醒等待的任务，让其继续运行 
}
```
## Named Semaphore(有名信号灯)
### release signal
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>

#include<sys/ipc.h>
#include<sys/shm.h>
#include<signal.h>

#include <fcntl.h>           
#include <sys/stat.h>        
#include <semaphore.h>

/* declare func to call */
void handle(int handle) ;

int main(int argc, const char *argv[])
{
	/* create and init var act of struct sigaction */
	struct sigaction act ;	// create empty var act, struct sigaction
	act.sa_handler = handle ;	// set sig_handler = handle
	act.sa_flags = 0;	// set flags = 0
	sigemptyset(&act.sa_mask) ;	// empty signal blocking set 
	
	sigaction(SIGINT, &act, NULL) ;	// set to call sig_handler in var act of struct sigaction when receive signal SIGINT
	
	key_t key ;
	key = ftok(".", 100) ;	// create key key with [file, subid] = [".", 100]
	if(key < 0)	// if failed
	{
		perror("key :") ;

		exit(-1) ;
	}
	
	int shmid ;
	shmid  = shmget(key, 256, 0666|IPC_CREAT) ;	// if not share_mem(key = key) not found, alloc 256 bytes and set permissions of [usr, group, others]=rw. return shmid | save shimid	// shmid = share memory ID
	if(shmid < 0)	// if failed
	{
		perror("shmid:") ;

		exit(-1) ;
	}

	char *shmaddr ;
	shmaddr = shmat(shmid, NULL, 0) ;	// append share_mem_seg(shmid = shmid) to current process's mem_seg, return its addr | save to shmaddr
	if(shmaddr < 0)	// if failed
	{
		perror("shmaddr:") ;

		exit(-1) ;
	}
	
	sem_t *sem_w, *sem_r;
	sem_w = sem_open("sem_write", O_CREAT|O_RDWR, 0666, 1) ;	// if semaphore_write named "sem_write" to read and non-overwite not found, create it, set permissions of [usr, group, others]=rw. return semaphore id | save to sem_w	// after this, sem_r will do write_protection for shared_mem_seg shaddr
	sem_r = sem_open("sem_read", O_CREAT|O_RDWR, 0666, 0) ;	// if semaphore_read named "sem_read" to read and non-overwite not found, create it, set permissions of [usr, group, others]=rw. return semaphore id | save to sem_r	// after this, sem_r will do read_protection for shared_mem_seg shaddr
	
	while(1)
	{
		sem_wait(sem_w) ;	// wait for mem_seg write_protected by named_semaphore sen_w to be writable
		printf(">") ;
		fgets(shmaddr, 5, stdin) ;	// read 5 bytes at most from stdin to shared_mem shmaddr
		sem_post(sem_r) ;	// allow other threads read mem_seg protected by named_semaphore sem-r
	}

	return 0 ;
}

void handle(int handle)	// def func handle : arg  = arg, dvalue = void, dtype = int, r void
{
	sem_unlink("sem_write") ;	// make semaphore "sem_write" unaccessible不可被调用
	
	exit(-1) ;
}
```
### receive signal
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>

#include<sys/ipc.h>
#include<sys/shm.h>
#include<signal.h>

#include <fcntl.h>           
#include <sys/stat.h>        
#include <semaphore.h>

/* declare func to call */
void handle(int handle) ;

int main(int argc, const char *argv[])
{
	/* create and init var act of struct sigaction */
	struct sigaction act ;	// create empty var act, struct sigaction
	act.sa_handler = handle ;	// set sig_handler = handle
	act.sa_flags = 0;	// set flags = 0
	sigemptyset(&act.sa_mask) ;	// empty signal blocking set 
	
	key_t key ;
	key = ftok(".", 100) ;	// create key key with [file, subid] = [".", 100]
	if(key < 0)	// if failed
	{
		perror("key :") ;

		exit(-1) ;
	}
	
	int shmid ;
	shmid  = shmget(key, 256, 0666|IPC_CREAT) ;	// if not share_mem(key = key) not found, alloc 256 bytes and set permissions of [usr, group, others]=rw. return shmid | save shimid	// shmid = share memory ID
	if(shmid < 0)	// if failed
	{
		perror("shmid:") ;

		exit(-1) ;
	}

	char *shmaddr ;
	shmaddr = shmat(shmid, NULL, 0) ;	// append share_mem_seg(shmid = shmid) to current process's mem_seg, return its addr | save to shmaddr
	if(shmaddr < 0)	// if failed
	{
		perror("shmaddr:") ;

		exit(-1) ;
	}
	
	sem_t *sem_w, *sem_r;
	sem_w = sem_open("sem_write", O_CREAT|O_RDWR, 0666, 1) ;	// if semaphore_write named "sem_write" to read and non-overwite not found, create it, set permissions of [usr, group, others]=rw. return semaphore id | save to sem_w	// after this, sem_r will do write_protection for shared_mem_seg shaddr
	sem_r = sem_open("sem_read", O_CREAT|O_RDWR, 0666, 0) ;	// if semaphore_read named "sem_read" to read and non-overwite not found, create it, set permissions of [usr, group, others]=rw. return semaphore id | save to sem_r	// after this, sem_r will do read_protection for shared_mem_seg shaddr
	
	while(1)
	{
		sem_wait(sem_r) ;	// wait for mem_seg read_protected by named_semaphore sem_r to be readable
		printf("%s\n", shmaddr) ;
		sem_post(sem_w) ;	// allow other threads wirte into mem_seg proceted by named_semaphore sem_w
	}
}

void handle(int handle)	// def func handle : arg  = arg, dvalue = void, dtype = int, r void
{
	sem_unlink("sem_read") ;	// make semaphore "sem_read" unaccessible不可被调用
	
	exit(-1) ;
}
```
## unamed Semaphore
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>

#include<sys/ipc.h>
#include<sys/shm.h>
#include<signal.h>

#include <fcntl.h>           
#include <sys/stat.h>        
#include <semaphore.h>
#include<pthread.h>

/* decalre func to call */
void handle(int arg) ;
void *thread1(void *arg) ;

sem_t sem_r, sem_w ;	// create unnamed_semaphore sem_r, sem_w ;

char *shmaddr ;

int main(int argc, const char *argv[])
{
	/* create and init var act of struct sigaction */
	struct sigaction act ;	// create empty var act, struct sigaction
	act.sa_handler = handle ;	// set sig_handler = handle
	act.sa_flags = 0;	// set flags = 0
	sigemptyset(&act.sa_mask) ;	// empty signal blocking set 
	
	sigaction(SIGINT, &act, NULL) ;	// set to call sig_handler in var act of struct sigaction when receive signal SIGINT
	
	key_t key ;
	key = ftok(".", 100) ;	// create key key with [file, subid] = [".", 100]
	if(key < 0)	// if failed
	{
		perror("key :") ;

		exit(-1) ;
	}
	
	int shmid ;
	shmid  = shmget(key, 256, 0666|IPC_CREAT) ;	// if not share_mem(key = key) not found, alloc 256 bytes and set permissions of [usr, group, others]=rw. return shmid | save shimid	// shmid = share memory ID
	if(shmid < 0)	// if failed
	{
		perror("shmid:") ;

		exit(-1) ;
	}

	shmaddr = shmat(shmid, NULL, 0) ;	// append share_mem_seg(shmid = shmid) to current process's mem_seg, return its addr | save to shmaddr
	if(shmaddr < 0)	// if failed
	{
		perror("shmaddr:") ;

		exit(-1) ;
	}

	sem_init(&sem_r, 0, 0) ;	// init unnamed_semaphore sem_r as semaphore_read
	sem_init(&sem_w, 0, 1) ;	// init unnamed_semaphore sem_W as semaphore_write
	
	pthread_t tid ;
	pthread_create(&tid, NULL, thread1, NULL) ;	// create thread, [name, attribute, thread_func to exec, fun_arg] = [tid, NULL, thread1, NULL]
	
	while(1)
	{
		sem_wait(&sem_w) ;	// wait for mem_seg write_protected by unnamed_semaphore sen_w to be writable
		printf(">") ;
		fgets(shmaddr, 5, stdin) ;	// read 5 bytes at most from stdin to shared_mem shmaddr
		sem_post(&sem_r) ;	// allow other threads read mem_seg protected by unnamed_semaphore sem-r
	}

	return 0 ;
}

void handle(int arg)	// def func handle : arg = arg, dvalue = void, dtype = int, r void
{
	sem_destroy(&sem_r) ;	// destroy semaphore sem_t
	sem_destroy(&sem_w) ;	// destroy semaphore sem_w
	
	exit(-1) ;
}

void *thread1(void *arg)	// def thread_func thread1: arg = arg
{
	while(1)
	{
		sem_wait(&sem_r) ;	// wait for mem_seg read_protected by unnamed_semaphore sem_r to be readable
		printf("%s\n", shmaddr) ;
		sem_post(&sem_w) ;	// allow other threads wirte into mem_seg proceted by unnamed_semaphore sem_w
	}

	exit(0) ;
}
```
# system-V 信号量集(semaphore set)
- Semaphore_set is a Semaphore_set with 1/more Semaphores
- P operation
	- if semaphore value > 0 , -1. if = 0, block current process	(先执行第一个if,再第二个if)
- V operation
	- awaken current process if bloked. semaphore += 1. 
```c
#include <semaphore.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>

#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/types.h>
#include <sys/sem.h>

#define SEM_READ 0	// define {index of semaphore_read in a Semaphore_set : SEM_READ} = 0
#define SEM_WRITE 1	// define {index of semaphore_write in a Semaphore_set : SEM_WRITE} = 1

/* declare func to call */
void Poperation(int semid, int semindex) ;
void Voperation(int semid, int semindex) ;

/* def union used to store semaphore_value */
union semun	// def union semun
{
	/*
	 * member = val
	 * dtype = int
	 */
	int val ;
} ;

int main(int argc, const char *argv[])
{
	key_t key ;
	key = ftok(".", 100) ;	// create key key with [file, subid] = [".", 100]
	if(key < 0)	// if failed
	{
		perror("key :") ;

		exit(-1) ;
	}
	
	int shmid ;
	shmid  = shmget(key, 500, 0666|IPC_CREAT) ;	// if not share_mem(key = key) not found, alloc 256 bytes and set permissions of [usr, group, others]=rw. return shmid | save shimid	// shmid = share memory ID
	if(shmid < 0)	// if failed
	{
		perror("shmid:") ;

		exit(-1) ;
	}

	char *shmaddr ;
	shmaddr = shmat(shmid, NULL, 0) ;	// append share_mem_seg(shmid = shmid) to current process's mem_seg, return its addr | save to shmaddr
	if(shmaddr < 0)	// if failed
	{
		perror("shmaddr:") ;

		exit(-1) ;
	}
	
	int semid ;
	semid = semget(key,2,IPC_CREAT |0666);	// if Semaphore_set(key = key, semaphore_num = 2) not fouynd, create it and set permissions of [usr, group, others]=rw. return semid | save to semid
	if(semid < 0)
	{
		perror("semget") ;

		exit(-1) ;
	}
	
	union semun mysem ;	// create empty var mysem, union semun
	mysem.val = 0 ;	// set val of union var mysem = 0
	semctl(semid, SEM_READ, SETVAL, mysem) ;	// init value of semaphore_read in Semaphore_set semid to union var semun's val
	mysem.val = 1 ;	// set val of union var mysem = 1
	semctl(semid, SEM_WRITE, SETVAL, mysem) ;	// init value of semaphore_write in semaphore_set semid to unin var semun's val
	
	pid_t pid ;
	pid = fork() ;	// create subprocess, retrun 0/-1/PID | save to pid
	if(pid < 0)
	{
		perror("fork") ;
		shmctl(shmid,IPC_RMID,NULL);	// rm sharemem_seg(id = shmid)
		semctl(semid,0,IPC_RMID);	// rm semaphore_set(id = semid)
		
		exit(-1) ;
	}
	else if(pid == 0)	// not previous condition and current process is the subprocess
	{
		while(1)
		{
			Poperation(semid, SEM_READ) ;	// do P operation for semaphore_read in semaphore_set by func Poperation
			printf("%s\n", shmaddr) ;

			Voperation(semid, SEM_WRITE) ;
		}
	}
	else
	{
		while(1)
        {
            Poperation(semid,SEM_WRITE);	// do P operation for semaphore_write in semaphore_set smid by func Voperation
            printf(">");
            fgets(shmaddr,32,stdin);
            
            Voperation(semid,SEM_READ);
		}
	}
}

/* def P operation func */
void Poperation(int semid, int semindex)	// def func Poperation : arg = [semid, semindex], devalue = void, dtype = int, r void
{
	/* def p operation */
	struct sembuf sbuf ;	// create empty var sbuf, struct sembuf
	sbuf.sem_num = semindex ;	// set semaphore index of semaphore to operate
	sbuf.sem_op = -1 ;	// set p opration = -1
	sbuf.sem_flg = 0 ;	// set default_flag = 0	// 0 means default
	
	semop(semid, &sbuf, 1) ;	// do operation saved in var sembuf of struct sbuf sbuf  for semaphore_set semid
}

/* def V operation func */
void Voperation(int semid, int semindex)	// def func Voperation : arg = [semid, semindex], devalue = void, dtype = int, r void 
{
	
	/* def V operation */
	struct sembuf sbuf ;	// create empty var sbuf, struct sembuf
	sbuf.sem_num = semindex ;	// set semaphore index of semaphore to operate
	sbuf.sem_op = 1 ;	// set V opration = 1
	sbuf.sem_flg = 0 ;	// set default_flag = 0	// 0 means default
	
	semop(semid, &sbuf, 1) ;	// do operation saved in var sembuf of struct sbuf sbuf  for semaphore_set semid
}
```

