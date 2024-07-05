# introduction
![35fdc19555a4b3e97042edd618ab224a.png](../../../_resources/35fdc19555a4b3e97042edd618ab224a.png)
# Binary Tree二叉树
![324bdd202532ef6d8dcd98c703f85865.png](../../../_resources/324bdd202532ef6d8dcd98c703f85865.png)
## properties
 - The number i layer of a binary tree can have $2^{i-1}$ nodes at most
 - The Binary Tree whose depth equals k has $2^k -1$ nodes at most
# sequential binary tree
![78fb952053ec6c9c27dab9b89fe603b3.png](../../../_resources/78fb952053ec6c9c27dab9b89fe603b3.png)
- when $2*i <= n$, current node has a left child
- when $2*i + 1 <= n$, current node has a right child

# linked binery tree
![22b63761bee54096718d4ac3899ee7c6.png](../../../_resources/22b63761bee54096718d4ac3899ee7c6.png)
### def a bittree type
```c
typedef char data_t ;	// alias char = data_t
typedef struct node_t	// def struct node_t with alias
{
	/*
	 * member = [data, *left_tree, *right_tree]
	 * dtype = [d_type, struct node_t, struct node_t]
	 */
	d_type data ;
	struct node_t *left_tree ;	// left_tree is left_node of current node
	struct node_t *right_tree ;
} bittree ;	// alias of struct = bittree
```
### create a bittree, return addr of its rootnode
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>


typedef char data_t ;	// alias char = data_t
typedef struct node_t	// def struct node_t with alias
{
	/*
	 * member = [data, *left_tree, *right_tree]
	 * dtype = [d_type, struct node_t, struct node_t]
	 */
	data_t data ;
	struct node_t *left_tree ;	// left_tree is left_node of current node
	struct node_t *right_tree ;
} bittree ;	// alias of struct = bittree

/* declare func to call */
bittree *tree_create() ;

int main(int argc, char *argv[])
{	
	bittree *r ;
	r = tree_create() ;
	puts("done") ;
	return 0 ;	// exit current process
}

bittree *tree_create()	// def func tree_create : arg = null, return = bittree *
{
	data_t value ;
	bittree *r ;

	printf("please input a value: ") ;
	scanf("%c", &value) ;	// let usr input "%c", save to value
	if (value == '#')
	{
		return NULL ;
	}

	r = (bittree *)malloc(sizeof(bittree)) ;	// create a bittree, return addr of its rootnode | save to r
	if(r == NULL)
	{
		perror("r") ;

		return NULL ;
	}

	r->data = value ;	// save value to data of rootnode of the bittree
	r->left_tree = tree_create() ;  // create leftnode for current node
	r->right_tree = tree_create() ;	// create rightnode for current node
	
	return r ;
}
```
## traverse
![f26a675227e4b9371a0b57552d266a2f.png](../../../_resources/f26a675227e4b9371a0b57552d266a2f.png)