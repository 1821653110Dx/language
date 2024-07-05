# introduction of linked list(include single linked list)
node$\tiny 节点$ is the fundamental unit to constitute a linked list, including data field$\tiny 数据域$ and next field$\tiny 后继指针域$
- data field is used to store data
- next field is a ptr pointing to next node

linklist is dynamic
# basic operations
## def node type
```c
typedef struct node	// def struct node with alias	//中文： 定义带别名的"node"
{
	/*
	 * member = data, *next	// data = data field, next = next field
	 * dtype = data_t, struct node	// data_t refers to any type
	 */
	data_t data ;
	struct node *next ;
}listnode, *linklist ;	// alias of [it , its ptr_type] = [listnode, linklist]
```

## create a single_linked_varlist, return headnode's addr
```c
linklist linknode_create()	// def func linknode_create : arg = void, r = linklist
{
	linklist H = (listnode *)malloc(sizeof(listnode)) ;	// create a headnode of linklist type, return its addr | save to H
	
	if(H == NULL)	// if node H points to not found
	{
		printf("fail to create node") ;	

		return NULL ;
	}
	/*
	 * otherwise,
	 * set data of node H points to = 0
	 * set next of node H points to = NULL
	 */
	H->data = 0 ;
	H->next = NULL ;

	return H ;
}
```
## append value to the single_linked_varlist with headnode H points to
```c
int linknode_tail_insert(linklist H, int value)	// def func linknode_tail_insert : arg = [var H, value], dvalue = null, dtype = [linklist, int], r= int   // H saves addr of headnode, dtype of H is node ptr, which is linklist
{
	if(H == NULL)	// if headnode H points to not found
	{
		printf("head node invalid") ;

		return -1 ;
	}
	
	/* otherwise */
	linklist p = NULL ; 
	p = (linklist)malloc(sizeof(listnode)) ;	// create a newnode, return its addr | save to p
	
	if (p == NULL)	// if node p points to not found
	{
		perror("fail to create node") ;
		return -1 ;
	}

	p->data = value ;	// save value to data of node p points to
	p->next = NULL ;	// init ptr next of node p points to
	
	/* let p points to last node of the single_linked_varlist */
	linklist q = H ;	// create var q = H, linklist, auto
	while(q->next)	// while q not points to the last node of the list
	{
		q = q->next ;	// q points to the next node of the list
	}

	q->next = p ;	// let ptr next of last node q points to points to the new node p points to 
	
	return 0 ;
}
```
use this func to append values
```c
/* add int usr input to the list until input -1 */
while(1)	// while not break
{
    printf("Please input:\n") ;	// printf "Please input:\n"
    scanf("%d",&value) ;	// let usr input "{ an int }" and newline, save to value as %d
    if(value == -1)// if value = -1
    {
        break ;
    }
    linknode_tail_insert(H, value) ;	// add the int to the list by linknode_tail_insert(H, value)
}
```

## return the ptr points to node at index i of the single_linked_varlist with headnode H points to
```c
linklist linknode_element_inqure(linklist H, int i)	// def func linknode_element_inqure : arg = [H, i], dvalue = null, dtype = [linklist, int], r = linklist
{
	if (H==NULL)	// if the headnode H points to not found
	{
		printf("head node invalid\n") ;	

		return NULL ;	// return NULL and exit // if r = ptr, return NULL
	}

	if  (i == -1)	// if index to seach = index of headnode
	{
		return H ;
	}
	else if (i < -1)	 // if the index invalid
	{
		printf("i value error !\n") ;
		
		return NULL ;
	}

	/* return the ptr points to the node at index i of the list */
	int n = -1 ;	// create var { current index : n } = -1, int, auto
	while(n < i)	// if current index < the index
	{
		H = H->next ;	// H points to next node
		
		if (H == NULL)
		{
			printf("i is too big\n") ;

			return NULL ;
		}

		n++ ;	// current index += 1
	}
	return H ;
}
```
## print every data of the single_linked_varlist with headnode H points to 
```c
int linkshow(linklist H)	// def func linkshow : arg = H, dvalue = null, dtype = linklist, r = int
{
	if (H == NULL)	// if headnode H points to not found
	{
		printf("headnode invaid\n") ;

		return -1 ;
	}
	
	/* print every data of the list */	// data of the list = every non-headnode's data's value
	while( H->next )	// while node H points not NULL
	{
		H = H->next ;	// H points to its next node

		printf("%d ", H->data) ;	// printf "{ data of current node } "{ %d }
	}
	puts("") ;	// newline
	
	return 0 ;
}
```
## insert value at index i of the single_linked_varlist with headnode H points to
```c
int linknode_element_insert(linklist H, int value, int i)	// def func linknode_element_insert : arg = [H, value, i] , dvalue = null, dype = [linklist, int, int], r = int
{
	if(H == NULL)	// if headnode H points to not found
	{
		printf("invaid H") ;

		return -1 ;
	}

	linklist q ;
	q = (listnode *)malloc(sizeof(listnode)) ;	// create a newnode, return its addr | save to q
	if(q == NULL )	// if node q points to not found
	{
		perror("fail to create node") ;	// echo error "fail to create node"
		
		return -1 ;
	}

	linklist p ;
	p = linknode_element_inqure(H, i-1) ;	// return the ptr points to node at index i-1 of the single_linked_varlist with headnode H points to	| save the addr in it to p
	if (p == NULL)	// if node p points to not found
	{
		return -1 ;
	}
	
	q->data = value ;	// set data of node q points to = value
	/* insert node q points to between node p points to and next node */
	q->next = p->next ;
	p->next = q ;

	return 0 ;
}
```
## del node at index i of the dynamic_single_varelist with headnode H points to
```c
int linknode_element_delete(linklist H, int i)	// def linknode_element_delete : arg = [H, i], dvalue = null, dtype = [linklist, int], r = int
{
	linklist p, q ;

	if (H == NULL)	// if headnode H points to not found
	{
		printf("headnode invalid") ;

		return -1 ;
	}

	p = linknode_element_inqure(H, i-1) ;	// return the ptr points to node at index i-1 of dynamic_single_linklist with headnode H points to | save addr in it to p
	if (p == NULL)	// if node p points to not found
	{
		return -1 ;	
	}
	if (p->next == NULL)	// if next node of node p points to not found
	{
		printf("the place of i is NULL!") ;
		return -1 ;
	}

	/* otherwise, make next node of node p points to point to its next node */
	q = p->next ;	// save addr of next node to q
	p->next = q->next ;	// { next node of node p points to } points to { its next node : p->next->next : q->next }
	free(q) ;   // free mem of node q points to
	q = NULL ;

	return 0 ;
}
```
## del single_linked_varlist with headnode H points to
```c
int linknode_delete(linklist H)	// def func linknode_delete : arg = H, dvalue = void, dtype = linklist, r = int
{
	if (H == NULL)	// if headnode H points to not found
	{
		printf("headnode invalid") ;

		return -1 ;
	}

	/* delete all nodes of the list with headnode H points to */
	linklist p ;
	p = H ;	// save addr of headnode H points to to p
	while (p)	// while node p points to exists
	{
		p = p->next ;	// p points to its next node 
		free(H) ;	// free mem for node p previously points to	// for node H points to = node p previously points in 1st loop , so we use H to refer to ~ 
		H = p ;	// H points to node p points to now
	}

	return 0 ;	
}
```
## reverse the dynamic_single_linked_list with headnode H points to
```c
int linknode_invert(linklist H)	// def func linknode_invert : arg = H, dvalue = null, dtype = linklist, r = int
{
	linklist p, q ;

	if (H == NULL)	// if headnode H points to not found
	{
		printf("headnode invalid") ;

		return -1 ;
	}
	if (H->next == NULL)// if next node of node H points to not found
	{
		printf("empty list!\n") ;

		return -1 ;
	}
	
	/* 
	 * insert each node after 1st node into the front of the 1st node in sequence 
	 */
	/* break the connection between 1st and 2nd node of the list, resulting in next node of 1st node != oringinal 2nd node */
	p = H->next ;	// save addr of next node of node H points to p
	q = p->next ;	// save addr of next node of node p points to q
	p->next = NULL ;	// set next node of node p points to = NULL

	while(q)
	{
		p = q ;
		q = q->next ;
		p->next = H->next ;
		H->next = p ;	
	}

	return 0 ;
}
```
## find the max sum of data of 2 adjacent nodes in the single_linked_varlist with headnode H points to, return a ptr pointing to 1st node correspoding to sum and save sum to var value points to
```c
linklist linknode_max_adjoin(linklist H, int *value)	// def func linknode_max_adjoin : arg = [H, *value], dvalue = null, dtype = [linklist, int], r = linklist
{
	linklist p, q, m ;
	int n = 0 ;

	if(H==NULL)	// if headnode H points to not found
	{
		printf("head node invalid") ; 

		return NULL ;
	}

	if(H->next == NULL || H->next->next == NULL)	// if headnode H points to is the last node or last 2nd node
	{
		printf("empty list or only 1 elements") ;

		return NULL ;
	}
	
	/* 
	 * save max sum of 2 adjacent nodes to n, save addr of sum's corresponding 1st node to m
	 */
	/* save addr of 1st 2 adjacent nodes to p,q */
	p = H->next ;	// save addr of headnode to p
	q = p->next ;	// save addr of 2nd node to q

	m = p ;	// save addr of 1st node of the 2 adjacent nodes to m
	n = p->data + q->data ;	// save sum of data of 1st 2 adjacent nodes to n

	while(q->next)	// while node q points to not last 2nd node
	{
		/* p, q points next node of their respective它们各自的 nodes */
		p = q ;	// p points to its next node
		q = q->next ;	// q points to its next node
		
		if (n < p->data + q->data)	// if n not >= sum of data between node p points to and node q points to
		{
			m = p ;	// overwite m with addr saved in p
			n = p->data + q->data ;	// overwite n with ~
		}
	}

	*value = n ;	// save n to var value points to
	return m ;
}
```
##  merge 2 a-order single_linked_varlist(one with headnode H1 points to, another with ...H2...) into a a-order list, overwite to the list corresponding to H1
```c
int linknode_order_merge(linklist H1, linklist H2)	// def func linknode_order_merge: arg = [H1, H2], dvalue = null, dtype = linklist, r = int
{
	linklist p ;

	if(H1 == NULL || H2 == NULL)	// if node pointed to by H1 or H2 noy found
	{
		printf("H1, H2 invalid") ;
		
		return -1 ;
	}

	if(H2->next == NULL)	// if node H2 points to is last node
	{
		printf("list with headnode H2 is empty") ;

		return -1 ;
	}

	/*
	 * merge 2 a-oder dynamic_single_varlist
	 */
	p = H2->next;

	while(p)
	{
		while(H1->next)
		{
			if(H1->next->data > p->data)
				break;
			H1 = H1->next;
		}
		H2 = p;
		p = p->next;

		H2->next = H1->next;
		H1->next = H2;
	}

	return 0 ;
}
```
