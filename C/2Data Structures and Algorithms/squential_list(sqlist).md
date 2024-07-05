# introduction
	sqlist is static
# basic operations of sequential lists(.C)
## create a sequential storage structure
```c
#define N 100	// define macro N = 100

typedef struct // def a struct
{
	/* member = [ dynamic_sequential_varlist data[N], var list ], dtype = int*/
	int data[N] ;
	int list ;  // list = index counts of data
} sqlist, *sqlink ;	// name of [it, its ptr type] = [sqlist, sqlink]
```

## create a  sqlist, return its addr
```c
sqlink sqlist_create()	// def func sqlist_create : arg = void, r = { ptr pointing to sqlist : sqlink }
{
	sqlink sq = (sqlist *)malloc(sizeof(sqlist)) ;	// create a new sqlist, return its addr | save to sq
	if ( sq == NULL )	// if the sqlist sq points to 
	{
		#if DEBUG	// if macro DEBUG has been predefined
			printf("sqlist create error!\n") ;
		#endif
		
		return NULL ;
	}

	/* otherwise, init the squential_varlist of the struct sq points to */
	memset(sq,0,sizeof(sqlist)) ;
	sq->list = -1 ;

	return sq ;	// return addr saved in sq
}
```

## del the dynamic_var_squential_list of the sqlist sq points to
```c
int sqlist_delete(sqlink sq)	// def func sqlist_delete : arg = var sq, dvalue = null, dtype = sqlink, r = int
{
    if( sq == NULL )	// if the sqlist sq points to not found
	{
		#if DEBUG
			printf("sqlist has been del or isn't existing'") ;
		#endif

		return 0 ;
	}

	/* otherwise */
	free(sq) ;	// free mem costed by squential_varlist saved in the addr saved in sq
	
	return 1 ;
}
```

## clear dynamic_sequential_varlist data of the sqlist sq points to 
```c
int sqlist_clear(sqlink sq)	// def func sqlist_clear : arg = var sq, dvalue = null, dtype = sqlink, r = int
{
	if(sq == NULL)	// if the sqlist sq points to not found
	{
		#if	DEBUG	// if macro DEBUG has been predefined
			printf("sqlist isn't exsist!\n") ;
		#endif

		return 0 ;
	}

	if(sq->list == -1)	// if the dynamic_squentical_varlist of the sqlist sq points to is empty    // list isn't the dynamic_sequntial_var list
	{
		#if DEBUG
			printf("sqlist has been cleared !\n") ;
		#endif

		return 0 ;
	}
	else
	{
		/* clear the squential_varlist of the sqlist sq points to */
		memset(sq,0,sizeof(sqlist)) ;	// set size of the sqlist sq points to to 0
		sq->list = -1 ;	// mark the dynamic_sequential_varlist data of the sqlist sq points to as empty 

		return 1 ;	// return 1 to show clearing has been successfully done
	}
}
```

## judge whether dynamic_sequential_varlist sq points to is empty
```c
int sqlist_empty( sqlink sq )	// def func sqlist_empty : arg = var sq, dvalue = null, dtype = sqlink, r = int
{
	if (sq == NULL)	// if the sqlist sq points to not found
	{
		#if DEBUF	// if macro DEBUG  defined
			printf("sqlist isn't existing\n") ;
		#endif

        return -1 ;
	}
	
	if(sq->list == -1)	// if the dynamic_sequential_varlist of the sqlist sq points is empty
	{
		return 1 ;	// return 1 to show the list is empty
	}
	else	// otherwise
	{
		return -1 ;	// return -1 to show the list isn't empty
	}

	return 0 ;
}
```

## evaluating the length of the dynamic_sequential_varlist sq points to
```c
int sqlist_length(sqlink sq)	// def func sqlist_length : arg = var sq, dvalue = null, dtype = sqlink, r = int
{
	if( sq == NULL  )	// if the sqlist sq points to not found
	{
		#if DEBUG	// if macro DEBUG defined
			printf("sqlist isn't exist \n") ;
		#endif

		return -1 ;
	}

	/* otherwise, return { var list of sqlist sq points to } + 1 */
	return sq->list + 1 ;
}
```

##  return element at index x of the dynamic_sequential_varlist sq points to
```c
int sqlist_element_query(sqlink sq, unsigned int i)	// def func sqlist_element_query : arg = [var sq, var i], dvalue = null, dtype = [sqlink, unsigned int], r = int
{
    int i ; // create empty var i, int, auto

	if(sq == NULL)	// if the sqlist sq points not found
	{
		printf("sqlist isn't existing!") ;

		return -1 ;
	}

	if(i > sq->list)	// if i > { list of the sqlist sq points to }
	{
		printf("i is too big\n") ;

		return -1 ;
	}

	/* otherwise, return the data at index i of data of the sqlist sq points to */
	return sq->data[i] ;
}
```

## traverse the dynamic_sequential_varlist sq points to
```c
int sqlist_ergodic(sqlink sq)	// def func sqlist_ergodic : arg = var sq, dvalue = null, dtype = sqlink, r = int
{
	int i ;	// create empty var i, int, auto

	if(sq == NULL)	// if the sqlist sq points to not found
	{
		printf("sqlist create error!\n") ;

		return -1 ;
	}

	if(sq->list == -1)	// if list of the sqlist sq points to = -1
	{
		printf("sqlist is empty\n") ;
		
		return -1 ;
	}

	/* print every item of the dyanamic_sequential_varlist data of the sqlist sq points to */
	for(i = 0 ; i <= sq->list ; i ++)	// for each index in all index of the dynamic_sequential_varlist data of the sqlist sq points to
	{
		printf("%d ", sq->data[i]) ;	// printf "{ item at current index of data of the sqlist sq points to } "{ %d }
	}
	
	printf("\n") ;

	return 0 ;
}
```

## insert element x at index i of dynamic_sequential_varst sq points to, value of the member storing its index counts += 1
```c
int sqlist_insert(sqlink sq, unsigned int i, d_type x)	// def func sqlist_insert : arg = [var sq, var i, var x], dtype = [sqlink, unsigned int, int], r = int		// data_t = the dtype of element you want to insert
{
	int n ;	// create empty var n, int, auto

	if(sq == NULL)// if the sqlist sq points to not found
	{
		printf("sqlist not exsist!") ;

		return -1 ;
	}
	if (sq->list == N-1)	// if current index counts = { max index counts }
	{
		printf("the list already full!") ;

		return -1 ;
	}
	if (i > sq->list )	// if given index > current index counts of data
	{
		printf("i is too big") ;

		return -1 ;
	}

	/*
	 * otherwise,
	 * move items after index i one unit backward,
	 * save element x at index i, member list += 1
	 */
	 /* move items after index i one unit backward */
	for (n = sq->list ; n >= i ; n--)	//  last index >= { index : n } >= i, d -1. for each
	{
		sq->data[n+1] = sq->data[n] ;	// mv item at current index of data of the sqlist fp points one unit backward
	}
	/* save elemnt x at index i, member list += 1 */
	sq->data[i] = x ;
	sq->list++ ;

	return 1 ;	// retrun 1 to show operation successfuly done
}
```

## remove element at index i of dynamic_sequential_varlist sq points to, value of the member storing its index counts += 1
```c
int sqlist_element_delete(sqlink0 sq, unsigned int i)	// def func sqlist_element_delete: arg = [var sq, var i], dvalue = null, dtype = [sqlink, unsigned int], r =  int
{
	int j ;
	if(sq == NULL)	// if the sqlist sq points to not found
	{
		printf("sqlist not exist!\n") ;

		return -1 ;
	}
	
	if(i > sq->list) // if given index > current index counts of data
	{
		printf("i is too big\n") ;

		return -1 ;
	}

	/* otherwise,
	 * rm the item at index i
	 * member list --
	 */
	/* rm the item at index i */
	for(j = i ; j <= sq->list-1 ; j++)	// for each { index : j } in [i, last index]
	{
		sq->data[j] = sq->data[j+1] ;	// overwrite item at current index of data of the sqlist sp points to with item at next index of data of the sqlist sp points to
	}
    
	sq->list-- ;	//  member list --

	return 1 ;	// return 1 to show operation successfully done
}
```

## find the union of squential_varlist [sq0, sq1] sq points to, overwite to sq0
```c
int sqlist_union(sqlink0 sq0, sqlink1 sq1)	// def func sqlist_union: arg = var[sq0, sq1], dvalue = null, dtype = [sqlink0, sqlink1], r = int
{
	int i,j ;

	if(sq0 == NULL || sq1 == NULL)	// if ( the sqlist sq0 points to not found  ) or ( the sqlist sq1 points to not found  )
	{
		printf("sqlist isn't exist!\n") ;

		return -1 ;
	}

	if(sq1->list == -1)	// if current index counts of the sqlist sq1 points to = -1
	{
		printf("sqlist1 is empty") ;
		
		return -1 ;
	}

	/* find the union of two lists */
	for(i = 0; i <= sq1->list-1; i++)   // for each index in all index of list corresponding to sq1
	{
        /* next i if current item corresponding to sq1 in list corresponding to sq0 */
		int isExist = 0;
		for(j = 0; j <= sq0->list-1; j++)
		{
			if(sq0->data[j] == sq1->data[i])
			{
				isExist = 1;
				break;
			}
		}
        /* otherwise, 
           append the item to list corresponding to sq0 if not full, otherwise exit function
         */
		if(!isExist)
		{
			if(sq0->list == N)
			{
				printf("The list is full, cannot insert more elements.\n");
				return -1;
			}
			sqlist_insert0(sq0, sq0->list, sq1->data[i]);
		}
	}

	return 1 ;
}
```
## rm the duplicates of dynamic_sequential varlist sq points to
```c
int sqlist_repeat_delete(sqlink0 sq)	// def func sqlist_repeat_delete : arg = var sq, dvalue = null, dtype = sqlink0, r = int
{
	int i, j ;

	if(sq == NULL)	// if the sqlist sq points to not found
	{
		printf("sqlist isn't exisit\n") ;

		return -1 ;
	}

	if(sq->list == -1)	// if current index counts of the sqlist sq points to = -1
	{
		printf("sqlist is empty") ;

		return -1 ;
	}

	/* rm the duplicates for the list */
	for(i = 1 ; i <= sq->list-1 ; i++)	// for each { index : i } in [1, last index]
	{
		for(j = 0; j < i ; j++)	// for each { index : j } in all index before i
		{
			if(sq->data[j] == sq->data[i])	// if in the list of sqlist sq points to, item at index j = item at index i
			{
				sqlist_element_delete(sq, j) ;	// rm item at index j by sqlist_element_delete(sq, j)
                j-- ;
			}
		}
	}

	return 1 ;
}
```