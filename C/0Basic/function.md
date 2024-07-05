> if pass value of var a  instead of its addr, its value won't be changed
```c

# include <stdio.h>

// declare func to call: max
int max(int, int) ;

int main()	// def main
{
    int a = 100 ;	// create var a = 100, int, auto
    int b = 200 ;	
    int ret ;	

    ret = max(a,b) ;	
    
    printf("Max value is %d\n",ret) ;	// printf "Max value is {ret}\n"{ret:%d}

    return 0 ;	// exit
}

int max(int num1, int num2)		// def func max : arg = [var num1, var num2], dvalue  = null, dtype = int, r = int
{
    int result ;	

    if (num1 > num2)	
        result = num1 ;	
    else	
        result = num2 ;	
    
    return result ;	// return {result}	
}


#include <stdio.h>

// declare func to call: swap
void swap(int *x, int *y) ;

int main()	// def main
{
    int a = 100 ;	
    int b = 200 ;	

    printf("the value of a is %d before its value is swapped\n",a) ;	
    printf("the value of b is %d before its value is swapped\n",b) ;	

    swap(&a, &b) ;	// swap the value of 'a' and 'b': call swap(&a, &b)	// &a = the RAM addr of a

    printf("the value of a is %d before its value is swapped\n",a) ;	
    printf("the value of b is %d before its value is swapped\n",b) ;	

    return 0 ;	// exit
}

void swap(int *x, int *y)	// def func swap : arg = [ptr x, ptr y], dvalue = null, dtype = int, r = void
{
    int temp ;	
    
    // swap the value at RAM addresses saved in '*x' and '*y'
    temp = *x ;	// save {*x} to 'temp'
    *x = *y ;	// overwrite {*x} with {*y}
    *y = temp ;	// overwrite {*y} with {*x}
    
    return ;	// finished
}
```