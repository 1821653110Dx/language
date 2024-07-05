```c
#include <stdio.h>  
#include <stdlib.h>  
#include <pthread.h>  

/* declare func to call */
void *print_hello(void *threadid) ;

int main()
{
	pthread_t thread1, thread2, thread3 ;
	int iret1, iret2, iret3;
	iret1 = pthread_create(&thread1, NULL, print_hello, (void *)1) ;	// create thread, [name, attribute, thread_func to execute, func_arg] = [thread1, NULL, print_hello, (void *)1], return 0 or non 0| save to iret1	// attribue's NULL means default, fun_arg's NULL means no arg
	iret2 = pthread_create(&thread2, NULL, print_hello, (void *)2) ;	// create thread, [name, attribute, thread_func to execute, func_arg] = [thread2, NULL, print_hello, (void *)2], return 0 or non 0 | save to iret2

	iret3 = pthread_create(&thread3, NULL, print_hello, (void *)3) ;
	iret3 = pthread_detach(thread3) ;	// detach thread3, return 0 or non 0 | overwite to iret3	// 这里我偷懒直接用thread3,detached 线程的线程函数是不用手动退出的
	
	
	/* recycle resources of thread1, thread2 */	// for detached threads, [its resource, itself] will be automatically [free, exit] 
	pthread_join(thread1, NULL) ;
	pthread_join(thread2, NULL) ;

	printf("Main: completed\n") ;

	pthread_exit(NULL) ;	// directly exit main_thread
}


void *print_hello(void *threadid)	// def thread func print_hello : arg = [threadid]	// the thread func is the task the thread to execute
{
	long tid = (long)threadid ;	// void *threadid >> long tid 	// if func has arg will be called, you must convert them into other non arg first
	pthread_t thread_id ; 
	
	thread_id = pthread_self() ;	// save id of current thread to thread_id

	printf("Hello World! It's me, thread #%ld!\n", tid) ;
	printf("%ld!\n", thread_id) ;
	
	pthread_exit(NULL) ;	// directly current thread if coucld
}
```
