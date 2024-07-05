# for little scale sequence
## bubble sort(Ascending)
for each element, move it forward/backward until comparison fails
```c
#include <stdio.h>

/* declare func to call */
void bubble_Ascending_sort(int arr[], int len) ;

int main()
{
	int arr[] = {22,34,3,32,82,55,89,50,37,5,64,35,9,70} ;	// create static_varlist arr[] = [22,34,3,32,82,55,89,50,37,5,64,35,9,70], int
	int len = (int) sizeof(arr) / sizeof(*arr) ;	// create var len = { len of arr }, int, auto

	bubble_Ascending_sort(arr, len) ;	// sort static_varlist by bubble_Ascending_sort(arr, len)

	for (int i = 0 ; i < len ; i++ )	// 0 <= i <= len - 1, i = i + 1. for each
	{
		printf("%d ", arr[i]) ;
	}

	return 0 ;
}

void bubble_Ascending_sort(int arr[], int len)	// def func bubble_Ascending_sort : arg=[static_varlist arr, len], dvalue=null, dtype=int, r = void
{
	int temp ;	// create empty var temp, int, auto
	
	for ( int i=0 ; i < len -1 ; i ++ )	// 0 <=i <= len-1, i=i+1. for each
		for (int j = 0 ; j < len -1 - i ; j ++ )	// 0 <= j <= len-1-i-1, j = j + 1. for each
			if (arr[j] > arr[j+1] )// if arr[j] not < next item
			{
				/* swap the value of two items */
				temp = arr[j] ;
				arr[j] = arr[j+1] ;
				arr[j+1] = temp ;
			}
}
```
## selection sort
from 1st to last / last to 1st, directlt place each element to the corresponding place
```c
void selection_Ascending_sort(int a[], int len)	// def func selection_sort : arg=[arry a, len], dvalue = null, dtype = int, r = void
{
	int i,j,temp ;	// create empty var [i,j,temp,min], int, auto
	
	for (i = 0 ; i < len-1 ; i++)	// 0 <= i <= len-1 -1. d 1. for each
	{
		int min = i ;	// create { index of min value : min } = i , int, auto
		
		/* find the index of smaller item */
		for (j = i + 1 ; j < len ; j++)
		{
			if (a[j] < a[min])
			{
				min = j ;
			}
		}

		if ( min != i )	// if index of min value changed
		{
			/* swap value between current and original min value  */
			temp = a[min] ;
			a[min] = a[i] ;
			a[i] = temp ;
		}	
	}
}
```
## insertion sort(ascending)
insert each unsorted item into a sorted sequnce
```c
void insertion_A_sort(int arr[],int len)	// def func insertion_A_sort : arg = [arry arr, len], dvalue = null, dtype = int, r = void
{
	int i,j,temp ;	// create empty var [i, j, temp], int, auto
	
	for (i = 0 ; i < len ; i++ )	//  0 <= i <= len - 1, d 1. for each
	{
		temp = arr[i] ;	// set { temp min item : temp } = arr[i]
		for(j = i ; j >= 1 && temp < arr[j-1] ; j--)// i >= j >= 1, d -1. for each, if temp < arr[j-1]
		{
			arr[j] = arr[j-1] ;	// overwite current item to compare with its previous item
		}
		arr[j] = temp ;	// overwite arr[j] with temp
	}
}
```
# for large scale sequence
## Shell sort
```c
void shell_A_sort(int arr[], int len)	// def func shell_A_sort : arg = [arry arr, len], dvalue = null, dtype = int, r = void
{
	int gap,i,j ;	// create empty var [gap, i, j], int, auto
	int temp ;	// create empty var temp, int, auto

	for ( gap = len >> 1 ; gap > 0 ; gap = gap >> 1 )	// len/2 <= gap <= 1, gap = gap / 2. for each
	{
		for ( i = gap ; i < len ; i ++ )	// gap <= i <= len-1, i = i + 1. for each
		{
			temp = arr[i] ; 
			for ( j = i - gap ; j >= 0 && arr[j] > temp ; j -= gap )// i - gap >= j >= 0, j = j - gap. for each,  if arr[j] > temp
			{
				arr[j + gap] = arr[j] ;
			}
			arr[j + gap] = temp ;
		}
	}
}
```
## merge sort
```c
void merge_sort_recursive(int arr[], int reg[], int start, int end)	// def func merge_sort_recursive : arg = [arr[], reg[], start, end], dvalue = null, dtype = int, r = void
{
	if ( start >= end )
	{
		return ;	// return nothing
	}
	
	int len = end - start, mid = (len>>1) + start ;	// create var [len, mid] = [end - start, len/2 + start], int, auto
	int start1 = start, end1 = mid ;	// create var [start1, end1] = [start, mid], int, auto
	int start2 = mid + 1, end2 = end ;	// create var [start2, end2] = [mid + 1, end], int, auto
	merge_sort_recursive(arr, reg, start1, end1) ;
	merge_sort_recursive(arr, reg, start2, end2) ;

	int k = start ;
	while (start1 <= end1 && start2 <= end2)	// while start1 <= en1 and start2 <= end2
	{
		reg[k++] = arr[start1] < arr[start2] ? arr[start1++] : arr[start2++] ;	// if arr[start1] < arr[start2], return arr[start1] and arr points to arri[start1+1]. Otherwise return arr[start2] and arr points to arr[start2+1] | save to reg[k], reg[] points to reg[k+1]
	}

	while ( start1 <= end1 )
	{
		reg[k++] = arr[start1++] ;
	}

	while (start2 <= end2)
	{
		reg[k++] = arr[start2++] ;
	}

	for (k = start ; k <= end ; k++)	// start <= k <= end, d 1. for each
	{
		arr[k] = reg[k] ;
	}
}

void merge_sort(int arr[], int const len)	// def func merge_sort: arg = [arr[], const len], dvalue = null, dtype = int, r = void
{
	int reg[len] ;	// create empty static_vararry reg[len], int
	
	merge_sort_recursive(arr, reg, 0, len - 1) ;
}
```
## quick sort
```c
void swap(int *x, int *y)	// def func swap : arg = [ptr x , ptr y], dvalue = value, dtype = int, r = void
{
	/* swap value x points to and value y points to */
	int t = *x ; // happens when t not create and *x.type = int
	*x = *y ;
	*y = t ;
}

void quick_sort_recursive(int arr[], int start, int end)	// def func quick_sort_recursive : arg = [static_varlist arr, var start, var end], dvalue = null, dtype = int, r = void
{
	/* quit function if start >= end  */
	if (start >= end)
	{
		return ;
	}

	int mid = arr[end] ;	// create var mid = arr[end], int, auto
	int left = start, right = end - 1 ;	// create var [left, right] = [start, end - 1], int, auto
	
	while(  left < right )	// while start < right
	{
		while ( arr[left] < mid && left < right )	// while arr[left] < mid and left < right
		{
			left++ ;	// left += 1
		}
		while( arr[right] >= mid && left < right )	// while arr[right] >= mid and left < right
		{
			right-- ;	// right -= 1
		}

		swap(&arr[left], &arr[right]) ;	// swap value of arr[left] and arr[right] by calling swap()
	}

	if (arr[left] >= arr[end] )
		swap(&arr[left], &arr[end]) ;	// swap value of arr[left] and arr[right] by calling swap()
	else
		left++ ;
	
	if (left)	// if left not empty
	{
		quick_sort_recursive(arr, start, left - 1) ; 
	}

	quick_sort_recursive(arr, left + 1, end) ;
}

void quik_sort(int arr[], int len)	// def func quik_sort : arg = [ static_varlist arr, var len], dvalue = null, dtype = int, r void
{
	quick_sort_recursive(arr, 0, len - 1) ;
}
```

