# thread cancellation
> cancel = not direcly exit current thread
```c
#include <pthread.h>	// pthread_cancel, pthread_setcancelstate, pthread_setcanceltype, pthread_testcancel
#include <stdio.h>  
#include <stdlib.h>  
#include <unistd.h>
#include <errno.h>

/* declare func to call */
void *thread_function(void *arg) ;

int main()
{
	pthread_t thread1 ;
	int rc, oldstate ;

	rc = pthread_create(&thread1, NULL, thread_function, NULL) ;	// create thread, [name, attribute, thread_func to execute, func_arg] = [thread1, NULL, thread_function, NULL], return 0 or non 0| save to rc
	if(rc)	// if fail to create thread1
	{
		perror("thread1") ;

		 pthread_exit(NULL) ;	// directly exit main_thread
	}

	rc = pthread_setcancelstate(PTHREAD_CANCEL_ENABLE, &oldstate) ;	// set cancel_state to can_be_cancled for thread1, save previous cancel_state to addr of oldstate, return 0 or non 0 | overwite to rc	// cancel_state = [can_be_cancled, cannot_be_cancled] = [PTHREAD_CANCEL_ENABLE, PTHREAD_CANCEL_DISABLE]
	if(rc)	// if fail to set cancel_state for thread1
	{
		perror("thread1") ;

		 pthread_exit(NULL) ;	// directly exit main_thread
	}
	
	rc = pthread_setcanceltype(PTHREAD_CANCEL_DEFERRED, &oldstate) ;	// set cancel_type to cancle_only_at_cancel_point for thread1, overwite previouse cancel_state to oldstate, return 0/non 0 | overwite to rc	// cancel_type = [Cancel_only_at_cancel_point, directly_cancle] = [PTHREAD_CANCEL_DEFERRED, PTHREAD_CANCEL_ASYNCHRONOUS]
	if(rc)	// if fail to set cancel_point for thread1
	{
		perror("thread1") ;

		 pthread_exit(NULL) ;	// directly exit main_threaed
	}

	/* recycle resources of thread1 */
	rc = pthread_join(thread1, NULL) ;	// recycle resources of thread1, return 0 / non 0 | overwite to rc
	if(rc)	// if rail to recycle
	{
		perror("pthread_join()") ;

		 pthread_exit(NULL) ;	// directly exit main_thread
	}

	printf("successful") ;

	pthread_exit(NULL) ;	//	directly exit main_thread
}

void *thread_function(void *arg)	// def thread_func thread_function : arg = arg
{
	pthread_testcancel() ;	// set a cancel_point
	
	pthread_exit(NULL) ;	// directly exit current thread if could	// when could ? cancel_type != PTHREAD_CANCEL_DEFERRED
}
```
# clean threads terminated abnormally
```c
#include <pthread.h>
/* cleanup current thread if terminated abnormally */
pthread_cleanup_push(cleanup_function, "Cleanup argument") ;	// push thread_cleanup_func cleanup_function("cleanup argument") on to the cleanup stack	// resouces of thread terminated abnormally doesn't have to be recycled by thread_cleanup_func
pthread_cleanup_pop(0) ;	// temporarily pop the recently pushed thread_cleanup_func
```

# create and destroy mutex互斥锁
> code from locking mutex to unlocking mutex can't be executed by other threads
## create
outside all functions
```c
#include <pthread.h>
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER ;   // create and init mutex mutex1
```
inside a function
```c
#include <pthread.h>
pthread_mutex_t mutex2;  // create mutex mutex2
int rc ;
rc = pthread_mutex_init(&mutex2, NULL);  // init mutex2 ,attribute = NULL, return 0/non 0 | save to rc // NULL = default
```
## destroy
```c
pthread_mutex_destroy(&mutex3);  // destroy mutex mutex3
```
## lock and unlock
```c
pthread_mutex_lock(&mutex1) ;  // current thread lockes mutex mutex1 and return 0/non 0 if not locked, otherwise wait until unlocked and then do those
pthread_mutex_trylock(&mutex1) ;    // thread try to lock mutex mutex1, return 0/non 0/EBUSY
pthread_mutex_unlock(&mutex1) ;    // unlock mutex mutex1, return 0 /non 0
```

# readwrite lock
> resources(such as var, file) from readlock rwlock to unlock rwlock can't be written into by other threads but can be read
> resources from writelock rwlock to unlock rwlock can't be neither written or read by other threads
```c
#include <stdio.h>  
#include <stdlib.h>  
#include <pthread.h>  

/* create share data: shared_data */
int shared_data = 0;  // create var shared_data = 0, int, global

pthread_rwlock_t rwlock;  	// create rwlock rwlock

// 读取共享数据的函数  
void *reader(void *arg) {  
    pthread_rwlock_rdlock(&rwlock); // current thread readlock(动词，读锁定) rwlock rwlock and reaturn 0 / non 0 if not locked, otherwise wait until unlocked and then do those
	// previouse canbe replaced with : pthread_rwlock_tryrdlock(&rdlock) : current thread try to readlock rwlock rwlock, return 0 /non0 / EBUSY

    printf("Reader %ld is reading shared_data: %d\n", (long)arg, shared_data);  

    pthread_rwlock_unlock(&rwlock); // current thread unlock rwlock rwlock

    return NULL;  
}  

// 写入共享数据的函数  
void *writer(void *arg) {  
    pthread_rwlock_wrlock(&rwlock); // current thread writelock rwlock rwlock and reaturn 0 / non 0 if not locked, otherwise wait until unlocked and then do those 
	// previouse canbe replaced with : pthread_rwlock_trywrlock(&rdlock) : current thread try to writelock rwlock rwlock, return 0 /non0 / EBUSY

    shared_data += 1;  

    printf("Writer %ld wrote to shared_data: %d\n", (long)arg, shared_data);  

    pthread_rwlock_unlock(&rwlock); // current thread unlock rwlock rwlock  

    return NULL;  
}  

int main() {  
    if (pthread_rwlock_init(&rwlock, NULL) != 0) {  // init rwlock rwlock, attrubute = NULL, return 0 /non 0 | if != 0

        perror("pthread_rwlock_init");  

        exit(EXIT_FAILURE);  

    }  

    // 创建一些读取线程和写入线程  
    pthread_t threads[5];  
    for (int i = 0; i < 3; ++i) {  
        if (pthread_create(&threads[i], NULL, reader, (void *)(long)i) != 0) {  
            perror("pthread_create reader");  
            exit(EXIT_FAILURE);  
        }  
    }  
    for (int i = 3; i < 5; ++i) {  
        if (pthread_create(&threads[i], NULL, writer, (void *)(long)i) != 0) {  
            perror("pthread_create writer");  
            exit(EXIT_FAILURE);  
        }  
    }  

    // 等待所有线程完成  
    for (int i = 0; i < 5; ++i) {  
        if (pthread_join(threads[i], NULL) != 0) {  
            perror("pthread_join");  
            exit(EXIT_FAILURE);  
        }  
    }  

    // 销毁读写锁  
    if (pthread_rwlock_destroy(&rwlock) != 0) {  // destroy rwlock rwlock , return 0 / non0 | if != 0
        perror("pthread_rwlock_destroy");  
        exit(EXIT_FAILURE);  
    }  
    return 0;  
}
```

# deadlock(死锁/死循环)
thread 1 has resource1 and want to resource2, thread2 has resource2 and want to resource1, in that case, thread1 and thread2 will fall into a deadlock
