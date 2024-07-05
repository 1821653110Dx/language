# condition vars
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<pthread.h>

/* def node of resource link list */
typedef struct resource	// def  struct resource with alias	
{
	/*
	 * member = [*next, num]
	 * dtype = [struct resource, int]
	 */
	struct resource *next ;
	int num ;
} resour, *res ;	// alias of [struct, its ptr_type] = [resour, res]
res head = NULL ;	// create var head = NULL, res, global // head is the head_node of a resour

/* init condition_var and mutex */
pthread_cond_t cond = PTHREAD_COND_INITIALIZER ;	// create and init condition_var cond
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER ;	// create and init muxtex mutex

int i = 1 ;	// create var i = 1, int, global

/* declare func to call */
void *producer(void *arg) ;
void *consumer(void *arg) ;

int main(int argc, const char *argv[])
{
	pthread_t tid1, tid2 ;
	/* create resource */
	pthread_create(&tid1, NULL, producer, NULL) ;	// create thread, [name, attribute, thread_func to execute, func_arg] = [tid1, NULL, producer, NULL]
	sleep(5) ;	// pause for 5 s
	
	/* consume resource */
	pthread_create(&tid2, NULL, consumer, NULL) ;	// create thread, [name, attribute, thread_func to execute, func_arg] = [tid2, NULL, consumer, NULL]
	
	while(1)	// do the internal forever unless break
	{
		sleep(1) ;	// pase for 1 s
	}

	pthread_exit(NULL) ;	// directly exit main_thread
}

/* def producer thread_func */
void *producer(void *arg)	// def thread_func producer : arg = arg
{
	res tx ;

	pthread_detach(pthread_self()) ;	// detach current thread, return 0 / non0
	
	printf("producer create !\n") ;
	
	while(1)	// do the internal forever unless break
	{
		tx = (res)malloc(sizeof(resour)) ;	//  create a node of res type , return its addr | save to tx
		tx->num = i++ ;	//  i++ | save to num of node tx of a resour
		printf("producer %d\n", tx->num) ;

		pthread_mutex_lock(&mutex) ;	// current thread lockes mutex mutex and return 0/non 0 if not locked, otherwise wait until unlocked and then do those
		tx->next = head ;	// next node of node tx of a resour points to head
		head = tx ;	// node head points to node tx
		pthread_cond_signal(&cond) ;	// if wait_queue in cond not empty, wake up any thread, otherwise next step
		pthread_mutex_unlock(&mutex) ;	// unlock mutex mutex, return 0 / non 0
	}

	sleep(1) ;
}
/* def consumer thread_func */
void *consumer(void *arg)	// def thread_func consumer : arg = arg
{
	res tx ;
	pthread_detach(pthread_self()) ;	// detach current thread, return 0 /non 0
	
	printf("consumer create!\n") ;

	while(1)	// do the internal forver unless break
	{
		pthread_mutex_lock(&mutex) ;	// current thread lockes mutex mutex and return 0/non 0  if not locked, otherwise wait until unlocked and then do those

		while(head == NULL)	// while node head is empty
		{
			pthread_cond_wait(&cond, &mutex) ;	// sleep and unlock current mutex
		}
		
		tx = head ;	// node tx points to node head
		head = head->next ;	// node head points to its next node
		printf("consume %d\n", tx->num) ;
		free(tx) ;	// delete node tx
		
		pthread_mutex_unlock(&mutex) ;	// unlock mutex mutex
	}
}
```
# thread pool
task queue stores tasks to be processed by worker threads  
thread pool stores pre-created threads ready to execute tasks in task queue

![863ef969ea29ea3d14622566b0d08f26.png](../../../_resources/863ef969ea29ea3d14622566b0d08f26.png)
## 使用线程池前的要定义的内容
```txt
创建线程池的基本结构：
	任务队列链表
		typedef struct Task;
	线程池结构体
		typedef struct ThreadPool;·
线程池的初始化：
	pool_init()
	{
		创建一个线程池结构
		实现任务队列互斥锁和条件变量的初始化
		创建n个工作线程
	}
线程池添加任务
	 workThread
	{
		while(1)
		{
			等待newtask任务信号
			从任务队列中删除节点
			执行任务
		}
	}
线程池的销毁
	 pool_destory
	{
		删除任务队列链表所有节点，释放空间
		删除所有的互斥锁条件变量
		删除线程池，释放空间
	}
```
## 线程池的使用
```c
int main(int argc, const char *argv[])
{
	/* 使用线程池执行任务 */
	data_t i;
	pool_init();
	for(i = 0; i < 20; i++)
	{
		Add_task(i);
	}
	
	/* 销毁用过的线程池 */
	pool_destroy(pool);

	return 0;
}
```