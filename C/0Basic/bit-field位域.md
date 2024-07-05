# define
bit-field is a kind of struct member that can be specified occupied bits
```c
#include <stdio.h>

struct use_1_bit	// def struct use_1_bit
{
	/* member = [var widthValidated, var hightValidated], dtype = [unsigned int,unsigned int],  mem costed = [1 bit, 1bit] */
	unsigned int widthValidated : 1 ;
	unsigned int hightValidated : 1 ;
} ;

struct use_more_bit	// def struct use_more_bit
{
	/* member = [ var widthValidated, var hightValidated], dtype = [unsigned int, unsigned int], v_type = var, mem costed = auto */
	unsigned int widthValidated ;
	unsigned int hightValidated : 1 ;
} ;

int main()	// def main
{
	struct use_1_bit status1 ;	// create empty var status1, struct use_1_bit, auto
	struct use_more_bit status2 ;	// create empty var status2, struct use_more_bit, auto
	
	printf("Memory size occupied by status1 : %zu\n",sizeof(status1)) ;	// printf "Memory size occupied by status1 : { size of status1 }\n"{ %zu }
	printf("Memory size occupied by status2 : %zu", sizeof(status2)) ;	// printf "Memory size occupied by status2 : { size of status2 }"{ %zu }

	return 0 ;
}
```
```c
#include <stdio.h>
#include <string.h>

struct AGE	// def struct AGE
{
	/*
	 member = var age, dtype = unsigned int, costed bits = 3 bit
	 */
	unsigned int age : 3 ;
} ;

int main()	// def main
{
	struct AGE Age ;	// create empty var Age, struct AGE, auto
	Age.age = 4 ;	// set Age.age = 4
	printf("size of Age : %zu\n", sizeof(Age)) ;	// printf "size of Age : { size of age }\n"{ %zu }
	printf("Age.age = %d\n", Age.age) ;	// printf "Age.age = { Age.age }"{ %d }
	
	Age.age = 7 ;	// overwrite Age.age with 7
	printf("Age.age = %d\n", Age.age) ;	// printf "Age.age = { Age.age }"{ %d }
	
	Age.age = 8 ;	// overwrite Age.age with 8 // 8 = 1000 = 4 bit > 3bit, will occur error
	printf("Age.age = %d\n", Age.age) ;	// printf "Age.age = { Age.age }"{ %d }
	
	return 0 ;
}
```
```c
#include <stdio.h>

struct example1	// def struct example1
{
	/* member = [var a, var b, var c], dtype = int, costed bits = [4, 5, 7] */
	int a : 4 ;
	int b : 5 ;
	int c : 7 ;
} ;

int main()	// def main
{
	struct example1 ex1 ;	//// create empty var ex1, struct example1, auto
	printf("Size of example : %zubytes\n", sizeof(ex1)) ;		// printf "Size of example1 : { size of ex } bytes\n"{ %zu }
	return 0 ;
}
```
# use
```c
#include <stdio.h>

struct bs	//def struct bs
{
	/*
	 member = [var a, var b, var c]
	 dtype = unsigned
	 costed bits = [1, 3, 4]
	 */
	unsigned a : 1 ;
	unsigned b : 3 ;
	unsigned c : 4 ;
} ;

int main()	// def main
{
	struct bs bit ;	// create empty var bit, struct bs, auto
	struct bs *pbit ;	// // create empty ptrvar pbit, struct bs, auto
	
	bit.a = 1 ;	// set bit.a = 1
	bit.b = 7 ;	// set bit.b = 7
	bit.c = 15 ;	// set bit.c = 15
	printf("%d, %d, %d\n", bit.a, bit.b, bit.c) ;	// printf "{ bit.a } ,{ bit.b },{ bit.c }\n"{ %d, %d, %d }
	
	pbit = &bit ;	// pbit points to bit
	pbit->a = 0 ;	// set (var pbit points to).a = 0
	pbit->b &= 3 ;	// set (var pbit points to).b &= 3
	pbit->c |= 1 ;	// set (var pbit points to).c |= 1
	printf("%d, %d, %d\n", pbit->a, pbit->b, pbit->c) ;	// printf "{ (var pbit points to).a } { (var pbit points to).b } { (var pbit points to).c }\n"{ %d %d %d }
	
	return 0 ;
}
```

