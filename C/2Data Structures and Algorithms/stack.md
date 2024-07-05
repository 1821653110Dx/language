# dynamic_sequential_stack
## def sqstack type
```c
typedef struct  // def a struct
{
	/*
	 * member = [*data, maxlen, top]	// *data = a ptr pointing to elements saved in the sqstack ; maxlen = size of sqstack ; top = index of stack top
	 * dtype = [dtype, int, int]
	 */
    dtype *data ;
    int maxlen ;
    int top ;
} sqstack ; 	// name = sqstack
```

## create a dynamic_sequential_stack
```c
sqstack *s ;
s = stack_create(10) ;	// create a dynamic_sequential_stack with size=10, return its addr | save to s
```
### create a dynamic_sequential_stack with size=len, return its addr
```c
sqstack* stack_create(int len)	// def func stack_create : arg = len, dvalue = null, dtype = int, r = sqstack*
{
	sqstack *s ;
	s = (sqstack*)malloc(sizeof(sqstack)) ;	// create a new sqstack, return its addr | save to s
	
	if(s == NULL)	// if fail to create sqstack
	{
		perror("malloc sqstack failed") ;	// echo error "malloc sqstack failed"

		return NULL ;
	}

	s->data = (int *)malloc(len * sizeof(int)) ;	// create a int dynamic_varlist , return its addr | save to data of sqstack s points to
	
	if(s->data == NULL)	// if fail to create the list
	{
		perror("malloc data failed") ;	// echo error "malloc data failed"
		
		return NULL ;
	}

	/* init the stack s points to */
	memset(s->data, 0, len*sizeof(int)) ;	// init dynamic_varlist data of sqstack s points to
	s->maxlen = len ;	// set size of the stack = len	// set maxlen of sqstack s points to = len
	s->top = -1 ;	// set index of stact top of the stack = -1	// set top of sqstack s points to = -1

	return s ;
}
```
### dynamic_sequential_stack push(进栈) : add value to stack_top of dynamic_sequential_stack spoints to
```c
int stack_push(sqstack *s, dtype value)	// def func stack_push : arg = [*s, value], dvalue = null, dtype = [sqstack, int], r = int
{
	if (s == NULL)	// if sqstack s points to not found
	{
		printf("stack not exists") ;

		return -1 ;
	}
	
	if (s->top == s->maxlen-1)	// if the stack s points to is full
	{
		printf("stack is full") ;

		return -1 ;
	}

	s->top++ ;	// move index of stack_top 1 unit forward
	s->data[s->top] = value ;	// save value to stack_top 
	
	return 0 ;
}
```
## dynamic_sequential_stack pop(出栈) : rm valua at stack_top of dynamic_sequential_stack s points to, return the value
```c
d_type stack_pop(sqstack *s)	// def func stack_pop : arg = *s, dvalue = null, dtype = sqstack, r = int
{
	if (s == NULL)	// if sqstack s points to not found
	{
		printf("stack not exists") ;

		return -1 ;
	}
	
	s->top-- ;	// move index of stack_top 1 unit backward
	
	return(s->data[s->top + 1]) ;	// return value at next index of stack_top
}
```
## del the dynamic_sequential_stack s points to
```c
d_type stack_free(sqstack *s)	// def func stack_free : arg = *s, dvalue = null, dtype = sqstack, dtype = int, r = int
{
		if (s == NULL)	// if sqstack s points to not found
		{
			printf("stack not exists") ;

			return -1 ;
		}
	
		if (s->data != NULL)	// if the stack has data
		{
			free(s->data) ;	// clear the stack's data
		}
		/* otherwise, delete the stack s points to */
		free(s) ;
		
		return 0 ;
}
```
## clear the dynamic_sequential_stack s points to
```c
dtype stack_clear(sqstack *s)	// def func stack_clear : arg = *s, dvalue = null, dtype = sqstack, r = int
{
	if (s == NULL)	// if sqstack s points to not found
	{
		printf("stack not exists") ;

		return -1 ;
	}

	s->top = -1 ;

	return 0 ;
}
```
## return 1 if dynamic_sequential_stack s points to is empty, otherwise 0
```c
dtype stack_empty(sqstack *s) 
{
	if (s == NULL)	// if sqstack s points to not found
	{
		printf("stack not exists") ;

		return -1 ;
	}

	return (s->top == -1 ? 1 : 0);
}
```
# dynamic_single_linked_list_stack(stacklist)
## def stacklist type
```c
typedef struct node	// def struct node with alias
{
	/*
	 * member = [data, *next]
	 * dtype  = [data_t, struct node]
	 */
	data_t data ;
	struct node *next ;
}stacklist, *stacklink ;	// alias of [it, its ptr_type] = [stacklist,stacklink]
```
## create a stacklist, return top_node栈顶节点's addr 
```c
stacklink stacklist_create()	// def func stacklist_create : arg = void, r = stacklink
{
	stacklink top ;
	top = (stacklist *)malloc(sizeof(stacklist)) ;	// create a top_node栈顶节点 of stacklink type, return its addr | save to top
	if(top == NULL)	// if stacklist with top_node top points to not found
	{
		perror("stacklist create error!") ;

		return NULL ;	// exit function abnormally
	}

	/* init top_node */
	top->data = 0 ;	// set data of top_node top points to = 0
	top->next = NULL ;	// set next node of top_node top points to = NULL
	
	printf("success\n") ;
	return top ;
}
```
## append value's value to stacklist with top_node top points to(insert a new top_node)
```c
int stacklist_top_insert(stacklink top, data_t value)	// def func stacklist_top_insert : arg = [top, value], dvalue = null, dtype = [stacklink, int], r = int
{
	stacklink sl ;
	
	if(top == NULL)	// if stacklist with top_node top points to not found
	{
		perror("stacklist not found") ;	// echo error "stacklist not found"

		return 0 ;
	}
	
	sl = (stacklink)malloc(sizeof(stacklist)) ;	// create node sl of stacklink type	// create a node of stacklist type, return its addr | save to sl
	if(sl == NULL)	// if node sl points to not found
	{
		perror("node create error") ;	// echo error "node create error"
		
		return -1 ;
	}

	/* append value's value to the list */
	sl->data = value ;	// save value to data of node sl 
	sl->next = top->next ;	// set next node of node sl as next node of headnode top	// next node of node sl points to points to next node of node headtop points to
	top->next = sl ;	// set next node headnode top as node sl	// headnode top points to points to node sl points to
	
	return 0 ;
}
```

## rm top_node of the stacklist with top_node top, return its data(出栈)
```c
int stacklist_out(stacklink top)	// def func stacklist_out : arg = top, dvalue = null, dtype = stacklink, r = int
{
	int value ;
	stacklink sl ;

	if(top == NULL)	// if stacklist with top_node top not found
	{
		perror("stacklist not found") ;

		return -1 ;
	}
	if (top->next == NULL)	// if stacklist with top_node top is empty
	{
		printf("stacklist is empty!\n") ;

		return -1 ;
	}

	sl = top->next ;	// save addr of next node of topnode top to sl
	sl->next = top->next ;	// set next node of topnode top as next node of node sl
	value = sl->data ;	// save data of node sl to value
	
	return value ;
}

```
