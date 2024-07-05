# search
## binary search对分查找
- loop of :
	- for current part
		- if mid_value = value to search
			- exit loop
		- if mid_value > ~
			- goto left part
		- else
			- goto right part
```c
int Binsearch(sqlist r, keytype k)    //对有序表r折半查找的算法//
{  int low, high, mid;  low = 1;high = r.len; 
    while (low <= high)    
    {  mid = (low+high) / 2;   
        if (k == r.data[mid].key)  return (mid);  
        if (k < r.data[mid].key) high = mid-1;  
        else low = mid+1;
    }      
     return(0);
 }  
```
## block search
- Block-wise ordered, meaning that the keys of all records in block i (1≤i≤b-1) are less than the keys of records in block i+1, but the records within a block can be unordered.
![c8f2cb8daf3c49b85e37d3db0204feea.png](../../../_resources/c8f2cb8daf3c49b85e37d3db0204feea.png)
- construction method
	- build index, one block one index
	- $K_{max}$ is the biggest key in the block, link is the index of the 1st item of the block
	![6560cc1d06afaebeca42aa63f8df89c9.png](../../../_resources/6560cc1d06afaebeca42aa63f8df89c9.png)
- steps to seach
	- tranverse each block by its index
	- do sequential search in the block
![6e9b9b4d019dc6eb80ad50ebb0aee6a2.png](../../../_resources/6e9b9b4d019dc6eb80ad50ebb0aee6a2.png)

## hash table search
- when searching a record with key=k, we can directly find it by relation f instead of comparing, which is Hash func and remember as H(key).
- H(key) is actually addr-map function and returns a addr
### def hash type
```c
#define DEBUG 1
#define N 14

typedef int data_t;
typedef struct node   //哈希表结点定义
{
	data_t value;  //存入的数据
	data_t key;    //表中的位置，key = value % N
	struct node *next; //下一结点的指针
}listhash,*linkhash;
typedef struct   //哈希表定义
{
	listhash a[N]; 
}hash;
```
### create a hash table, return its addr
```c
/**
 * @description:哈希表的创建 
 * @param {*}
 * @return {哈希表的地址}
 */
hash *create_hash()
{
	hash *HT = (hash *)malloc(sizeof(hash));  //为表开辟空间  
	if(HT == NULL)
	{
		#if DEBUG
		printf("hash create error!\n");
		#endif
		return 0;
	}

	memset(HT, 0, sizeof(hash));   //表中清0

	return HT;
}
```
### save value to hash HT
```c
/**
 * @description: 数据存入进哈希表 
 * @param {hash} *HT-哈希表指针
 * @param {data_t} value-存入的数据
 * @return {0-函数失败，1-函数成功}
 */
int Add_hash(hash *HT, data_t value)
{
	linkhash p,q;
	if(HT == NULL)
	{
		#if DEBUG
		printf("HT is NULL!\n");
		#endif
		return 0;
	}

	if((p = (linkhash)malloc(sizeof(listhash))) == NULL)  //结点开辟空间
	{
		#if DEBUG
		printf("node create error!\n");
		#endif
		return 0;
	}

	p->value = value;   //结点存入数据
	p->key = value % N;
	p->next = NULL;

	q = &(HT->a[p->key]);   
	while(q->next != NULL && q->next->value < p->value)  //寻找放入哈希表的位置
		q = q->next;

	p->next = q->next;  //放入哈希表
	q->next = p;

	return 1;
}
```
### return the addr of value from hash HT
```c
/**
 * @description: 数据查询
 * @param {hash} *HT-哈希表指针
 * @param {data_t} value-查询的数据
 * @return {返回数据所在哈希表的位置}
 */
linkhash query_hash(hash *HT, data_t value)
{
	int key = value % N;
	linkhash p;
	if(HT == NULL)
	{
		#if DEBUG
		printf("HT is NULL!\n");
		#endif
		return 0;
	}

	p = &(HT->a[key]);
	while(p)
	{
		if(p->value == value)
			return p;
		p = p->next;
	}
	return NULL;
}
```

