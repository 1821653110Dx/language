# static array
array whose mem can't be realloc
## fetch items
### 1
```c

#include <stdio.h>

int main() // def main
{
int n[10] ; // create empty static_varlist n[10], int, auto
int i,j ; // create empty var [i,j], int, auto

/* def n[0] -> n[9] */
for( i = 0; i < 10; i++ ) // 0 <= i <= 0, d 1. for each
{
n[i] = i + 100 ; // save {{i} + 100} to n[i]
}

/* printf {n[0] -> n[9]} */
for( j = 0 ; j < 10 ; j++ ) // 0 <= j <= 9, d 1. for each
{
printf("Element[%d] = %d\n",j,n[j]) ; // printf "Element[{j}] = {n[j]}\n"{n[j]:%d}
}

return 0 ; // exit
}
```

### 2
```c

#include<stdio.h>

void printfArray(int arry[], int size)
{
for (int i = 0 ; i < size ; i++)
{
printf("%d ",arry[i]) ; // printf"{arry[i]} "{%d} // printf all items of the scope, delimeter = space
}
}

int main() // def main
{
int myArray[5] = {10, 20, 30, 40, 50} ; // create static_varlist myArray[5] = [10, 20, 30, 40, 50], int, auto

printfArray(myArray, 5) ;

return 0 ; // exit
}
```

## fetch length
### without macro def
```c

#include<stdio.h>

int main() // def main
{
int array[5] = {1, 2, 3, 4, 5} ; // create static_varlist array[5] = [1, 2, 3, 4, 5], int, auto
int length = sizeof(array)/sizeof(array[0]) ; // create var length = { len of array}, int, auto

printf("the length of the list = %d\n",length) ; // printf "the length of the list = {length}\n"{length:%d}

return 0 ; // exit
}
```
### with macro def
```c

#include<stdio.h>

#define LENGTH(array) sizeof(array) / sizeof(array[0]) // def macro LENGTH(array) : sizeof(array) / sizeof(array[0])

int main() // def main
{
int array[5] = {1, 2, 3, 4, 5} ;
int length = LENGTH(array) ; // def length : {the length of 'array' : macro 'LENGTH(array)'}, int, var, auto

printf("the length of the array = %d\n",length) ; // printf "the length of the array = {length}\n"{array:%d}

return 0 ; // exit
}
```

## fetch the address
```c
int myArray[5] = {10, 20, 30, 40, 50} ;
int* ptr = myArray ; // create ptrvar ptr = addr of myArray, int, auto
```

## multi-dim array
```c

#include<stdio.h>
int main() // def main
{
int a[5][2] = { {0, 0}, {1, 2}, {2, 4}, {3, 6}, {4, 8} } ;
int i,j ;

for ( i = 0 ; i < 5 ; i++) // set row scope : [0, 4], current row is represented by 'i'
{
for ( j = 0 ; j < 2 ; j++ ) // set col scope : [0, 1], current col is represented by 'j'
{
printf("a[%d][%d] : %d\n",i,j,a[i][j]) ; // do the following for every item in (row, col) : printf"a[{i}{j} : {a[i][j]}\n"{i,j,a[i][j]:%d}
}
}

return 0 ; // exit
}
```
## transit array to func
```c

#include<stdio.h>

/* decalre func to call: getAverage */
double getAverage(int arryp[], int size) ;

int main() // def main
{
int balance[] = {1000, 2, 3, 17, 50} ;
double avg ;

avg = getAverage( balance, 5 ) ;

printf("average value : %f", avg) ; // printf"average value : {avg}"{avg:%f}

return 0 ; // exit
}

double getAverage(int arry[], int size) // def func getAverage : arg = [list arry, var size], dvalue = null, dtype = int, r = double
{
int i ;
double average ;
double sum = 0 ;

for ( i = 0 ; i < size ; i++) // set {col : i} scope of 'arry' : [0, size)
{
sum += arry[i] ; // save SUM(all items [1, col]) to 'sum'
}

average = sum/size ; // save {sum / size} to 'average'

return average ; // return {average}
}
```
## return arry from func
```c
#include <stdio.h>
#include<stdlib.h>
#include<time.h>

int* getRandom() // def func getRandom : arg = void, r = int ptr
{
static int r[10] ;
int i ;

srand( (unsigned)time(NULL)) ; // set random_seed to sys_time

for (i = 0 ; i < 10 ; i++)
{
r[i] = rand() ; // get a random in [0, RAND_MAX defined in stdlib.h) ; save it to 'r[i]'
printf("r[%d] = %d\n",i,r[i]) ; // printf"r[{i}] = {r[i]}\n"{i, r[i]:%d}
}

return r ; // return {r}
}

int main() // def main
{
int* p ;
int i ;

p = getRandom() ; // p points to fist item of array returned by getRandom()

for (i = 0 ; i < 10 ; i++)
{
printf("*(p + %d) : %d\n", i, *(p + i)) ; // printf"*(p + {i}) : {item at index'i' at addr saved in 'p': *(p + i)}\n"{i, *(p + i) : %d}
}

return 0 ; // exit
}

```
## ptr toward arry
```c

#include <stdio.h>

int main() // def main
{
double balance[5] = {100.0, 2.0, 3.4, 17.0, 50.0} ;
double* p ;
int i ;

p = balance ; // save addr of 'balance' to 'p'

printf("get item of 'balance' by accessing addr saved in 'p'\n") ; // printf"get item of 'balance' by accessing addr saved in 'p'\n"

/* printf all items of 'balance' */
for (i = 0 ; i < 5 ; i++) // set {col:i}_index : [0, 5) . do the internal for each col_index
{
printf("*(p + %d) : %f\n",i, *(p + i)) ; // printf"*(p + {i}) : {item at index'i' at addr saved in 'p': *(p + i)}\n"{i:%d, *(p + i):%d}
}

printf("get item of 'balance' by accessing its addr\n") ; // printf"get item of 'balance' by accessing its addr\n"

/* printf all items of the 'balance' */
for (i = 0 ; i < 5 ; i++) // set {col: i}_index : [0,5). do the internal for each col_index
{
printf("*(balance + %d) : %f\n", i, *(balance + i)) ; // printf"*(balance + {i}) : {item at index'i' at addr of 'balance' : *(balance + i)}\n"{i:%d, *(balance + i):%f}
}

return 0 ; // exit
}

```
# dynamic array
array whose mem can be realloc
```c
#include <stdio.h>
#include <stdlib.h>

int main() // def main
{
/* def dynamic_array : dynamicArray */
int size = 5 ;
int* dynamicArray = (int*)malloc(size * sizeof(int)) ; // create a dynamic_var_array dynamicArray, costed mem = size of 5 int

if ( dynamicArray == NULL )// if failed to allocation mem for 'dynamicArray'
{
printf("Memory allocation falied.\n") ; // printf"Memory allocation failed.\n"
return 1 ; // exit // exit after encountering errors : return 1
}

/* echo hint, let user input a line of elements, save it */
printf("Enter %d elements: ", size) ; // printf"Enter {size} elements: "{size:%d} // prompt for inputing
/* let user input, save the inputs to list 'dynamicArray' */
for (int i = 0 ; i < size ; i++)
{
scanf("%d", &dynamicArray[i]) ; // let user inputs, save it : to = dynamicArray[i], format = %d
}

printf("Dynamic Array: ") ; // printf"Dynamic Array: "
/* printf all items of 'dynamic_array' */

// relieve mem 'dynamicArray' uses
for (int i = 0 ; i < size ; i++)
{
printf("%d ", dynamicArray[i]) ;
}

return 0 ; // exit
}
```