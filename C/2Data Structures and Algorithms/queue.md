# introduction
![d4754eeb1007d2fb73b2c2b3d58643f3.png](../../../_resources/d4754eeb1007d2fb73b2c2b3d58643f3.png)
# sequential queue
## def s_queue type
```c
#define N = 64     // alias N = 64
typedef struct// def a struct
{
	/*
	 * member = [static_varlist data[N], front, rear]
	 * dtype = [data_t, int]
	 */
	int data[N] ;
	data_t front, rear ;	// front = index of 1st item, rear = index of next item of last item
} s_queue, *squeue ;	// name of [struct, its ptr] = [s_queue, squeue]
```
## create a s_queue, return its addr
```c
squeue squeue_create()	// def func squeue_create : arg = null, r = squeue
{
    squeue queue ;
    queue = (s_queue *)malloc(sizeof(s_queue)) ;	// create a new s_queue, return its addr | save to queue
    if (queue == NULL)	// if fail to create s_queue
    {
        perror("s_queue create error") ;	// echo error "s_queue create error"

        return NULL ;
    }

    /* init the s_queue queue points to */
    memset(queue->data,0,sizeof(queue->data)) ;	// init static_data of s_squeue queue
    queue->front = queue->rear = 0 ;	// set front, rear pf s_queue queue = 0

    return queue ;
}
```
## enter s_queue : add value to the rear of s_queue queue
```c
int squeue_enter(squeue queue, data_t value)	// def func squeue_enter : arg = [queue, value], dvalue = null, dtype = [squeue, data_t], r = int
{
	if(queue == NULL)	// if s_queue queue not found
	{
		perror("s_queue not found") ;

		return -1 ;
	}
	
	if((queue->rear+1)%N == queue->front)	// if s_queue queue is full
	{
		printf("s_queue is full") ;

		return -1 ;
	}

	queue->data[queue->rear] = value ;	// save value to { index rear of queue } of data of s_queue queue
	queue->rear = (queue->rear + 1)%N ;	// update rear
	
	return 0 ;
}
```
## squque out : rm and return value at the front of s_queue queue
```c
int squeue_out(squeue queue)	// def func squeue_out : arg = queue, dvalue = null, dtype = squeue, r = int
{
	int value ;

	if(queue == NULL)	// if s_queue queue not found
	{
		perror("s_queue not found") ;

		return -1 ;
	}

	if(queue->front == queue->rear)	// if s_queue empty
	{
		printf("squeue is empty!\n") ;

		return -1 ;
	}

	value = queue->data[queue->front];	// save value at front of s_queue queue to value
	queue->data[queue->front] = 0 ;	// overwrite value at front of s_queue squeue with 0
	queue->front = (queue->front + 1)%N ;	// update front
	
	return value ;
}
```
## delete s_queue queue
```c
int squeue_free(squeue queue)	// def func squeue_free : arg = queue , dvalue = null, dtype = squeue, r = int
{
	if(queue == NULL)
	{
		perror("s_queue not found") ;
		return -1 ;
	}

	free(queue) ;	// free mem of s_queue queue
	
	return 0 ;
}
```
## clear s_queue queue
```c
int squeue_clear(squeue queue)	// def func squeue_clear : arg = queue, dvalue = null, dtype = squeue, r = int
{
	if (queue == NULL)
	{
		perror("s_queue not found") ;

		return -1 ;
	}

	/* clear squeue queue */
	memset(queue->data, 0 ,sizeof(queue->data)) ;	// init static_varlist data of s_queue queue
	queue->front = queue->rear = 0 ;	// update front, rear of s_queue queue

	return 0 ;
}
```
## return 1 if s_queue queue empty, otherwise 0
```c
int squeue_empty(squeue queue)
{
	if(queue == NULL)
	{
		#if DEBUG
		printf("squeue create error!\n");
		#endif
		return -1;
	}

	return queue->front == queue->rear? 1:0;
}
```

## return 1 if s_queue queue full, otherwise 0
```c
int squeue_full(squeue queue)
{
	if(queue == NULL)
	{
		#if DEBUG
		printf("squeue create error!\n");
		#endif
		return -1;
	}
	
    return (queue->rear+1)%N == queue->front? 1:0 ;
}
```
# list queue
![c7bb2a9b09183bf37e1620f9949f34e2.png](../../../_resources/c7bb2a9b09183bf37e1620f9949f34e2.png)
insert at rear, delete at front
## def list_queue type
```c
typedef struct node	// def struct node with alias
{
	/*
	 * member = [data, *next]
	 * dtype = [data_t, struct node]
	 */
	int data ;
	struct node *next ;
} linklist_t, *linklist ;	// alias of [it, its ptr_type] = [linklist_t, linklist]

typedef struct	// def struct
{
    /*
     * member = [front, rear]
     * dtype = linklist
     */
    linklist front, rear ;
} listqueue, *linkqueue;	// name of [it, its ptr_type] = [listqueue, linkqueue]
```
## create a listqueue, return its addr
```c
linkqueue linkqueue_create()	// def func linkqueue_create : arg = null, return = linkqueue
{
	linkqueue lq ;
	lq = (listqueue *)malloc(sizeof(listqueue)) ;	// create a new listqueue, return its addr | save to lq
	if(lq == NULL)	// if fail to create
	{
		perror("fail to create") ;
		
		return NULL ;
	}

	lq->front = lq->rear = (linklist_t *)malloc(sizeof(linklist_t)) ;	// create a node of linklist type, return its addr | save to [front, rear] of list_queue lq
	if(lq->front == NULL || lq->rear == NULL)	// if fail to create
	{
		perror("fail to create") ;
		
		return NULL ;
	}

	/* init node front */
	lq->front->data = 0 ;	// save 0 to data of node front of listqueue lq 
	lq->front->next = NULL ;	// set next node of node front of listqueue lq = NULL
	
	return lq ;
}
```
## enter listqueue lq : add value to node rear of listqueue lq
```c
int linkqueue_enter(linkqueue lq, int value)	// def func linkqueue_enter : arg = [lq, value], dvalue = null, dtype = [linkqueue, d_type], r = int
{
	linklist node ;
	node = (linklist)malloc(sizeof(linklist_t)) ;	// create a node of linklist type, return its addr | save to node
	if(lq == NULL)	// if listqueue lq not found
	{
		perror("listqueue") ;

		return -1 ;
	}
	if(node == NULL)	// if fail to create node node
	{
		perror("node") ;

		return -1 ;
	}

	/* insert node node to the rear of listqueue lq */
	lq->rear->next = node ;	// set next node of node rear of listqueue lq = node node
	lq->rear = node ;	// let node rear of listqueue lq points to node node
	
	/* save value to node rear of listqueue lq */
	lq->rear->data = value ;
	lq->rear->next = NULL ;
	
	return 0 ;
}
```
## listqueue out : delete front node and return its data
```c
int linkqueue_out(linkqueue lq)	// def func linkqueue_out : arg = lq, dvalue = null, dtype = linkqueue, r = data_t 
{
	linklist node ;
	int value ;
	if(lq == NULL)
	{
		perror("listqueue") ;

		return -1 ;
	}
	if(lq->front == lq->rear)	// if the listquque empty
	{
		printf("empty listqueue") ;

		return -1 ;
	}
	/* del node front */
	node = lq->front ;	// save addr of node front of listqueue lq to node
	value = lq->front->data;
	lq->front = lq->front->next ;	// node front of listqueue lq points to next node
	free(node) ;	// free mem of node
	
	return value ;
}
```

## del listqueue lq
```c
int linkqueue_free(linkqueue lq)	// def func linkqueue_free : arg = lq, dvalue = null, dtype = linkqueue, r = int
{
	linklist node ;

	if(lq == NULL)
	{
		perror("listqueue") ;

		return -1 ;
	}

	while(lq->front)	// while listqueue lq exists
	{
		/* delete cuurent node front */
		node = lq->front ;
		lq->front = lq->front->next ;
		free(node) ;
	}

	free(lq) ;	// delete listqueue lq

	return 0 ;
}
```

## clean listqueue lq
```c
int linkqueue_clear(linkqueue lq)
{
	linklist node;
	if(lq == NULL)
	{
		#if DEBUG
		printf("lq is NULL!\n");
		#endif
		return 0;
	}

	while(lq->front != lq->rear)    // while listqueue lq not empty
	{
        /* delete current node front */
		node = lq->front;   
		lq->front = node->next;
		free(node);
	}

	return 0 ;
}
```

## return 1 if list_queue lq empty, otherwise 0
```c
int linkqueue_empty(linkqueue lq)
{
	if(lq == NULL)
	{
		#if DEBUG
		printf("lq is NULL!\n");
		#endif
		return -1;
	}
	
	return lq->front == lq->rear? 1:0;
}
```
