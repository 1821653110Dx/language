# notion
    struct, union is similar to class
    member is similar to attribute
# difference
	struct : 
		1. every member can have value at any time
        2. use more memory
		3. size = size of every member
	union : 
		1. only one member can have value at any time
        2. use less memory
		3. size = size of the biggest member
# struct
## define
```c
#include <stdio.h>

struct Books	// def struct Books 
{
	/* member = [static_varstr title[50], static_varstr author[50], static_varstr subject[50], var book_id], dtype = [char, char, char, int] */
	char title[50] ;
	char author[50] ;
	char subject[100] ;
	int book_id ;
} ;

struct Books book = {"c语言", "RUNOOB", "编程语言", 123456} ;	// create var book of struct Books type, value of members = ["c语言", "RUNOOB", "编程语言"，123456], store_class = global

int main()	// def main
{
	printf("title : %s\nauthor : %s\nsubject : %s\nbook_id : %d", book.title, book.author, book.subject, book.book_id) ;	// printf"title : { value of member title of book }\nauthor : { value of member author of book}\nsubject : { value of attribuet subject of book } \nbook_id : { value of member book_id of book }"{ 0 : %s ; 1 : %s ; 2 : %s ; 3 : %d }
	
	return 0 ;	
}
```
## access
```c
#include <stdio.h>
#include <string.h>

struct Books	// def struct Books
{
	/* member = [static_varstr title[50], static_varstr author[50], static_varstr subject[50], book_id], dtype = [char, char, char, int] */
	char title[50] ;
	char author[50] ;
	char subject[100] ;
	int book_id ;

} ;

int main()	// def int
{
	struct Books Book1 ;	// craete empty var Book1, struct Books, auto
	struct Books Book2 ;	// create empty var Book2, struct Books, auto
	
	/* set members' value of Book1 */
	strcpy( Book1.title, "C Programming" ) ;	// cp "C Programming" to Book1.title
	strcpy( Book1.author, "Nuha Ali" ) ;	// cp "Nuha Ali" to Book1.author
	strcpy( Book1.subject, "C Programming Tutorial" ) ;	// cp "C Programming Tutorial" to Book1.subject
	Book1.book_id = 6495700 ;	// set Book1.book_id = 6495700

	/* set members' value book2 */
	strcpy( Book2.title, "Telecom Billing" ) ;	// cp "Telecom Billing" to Book2.title
	strcpy( Book2.author, "Zara Ali" ) ;	// cp "Zara Ali" to Book2.author
	strcpy( Book2.subject, "Telecom Billing Tutorial" ) ;	// cp "Telecom Billing Tutorial" to Book2.subject
	Book2.book_id = 6495407 ;	// set Book2.book_id = 6495407

	/* printf members' value of Book1 */
	printf("Book 1 title : %s\n", Book1.title) ;	// printf"Book 1 title : { Book1.title }\n"{ 0 : %s }
	printf("Book 1 author : %s\n", Book1.author) ;	// printf"Book 1 author : { Book1.author }\n"{ 0 : %s }
	printf("Book 1 subject : %s\n", Book1.subject) ;	// printf"Book 1 subject : { Book1.subject }\n"{ 0 : %s }
	printf("Book 1 book_id : %d\n", Book1.book_id) ;	// printf"Book 1 book_id : { Book1.book_id }\n"{ 0 : %d }

	/* printf members' value of Book2 */
	printf("Book 2 title : %s\n", Book2.title) ;	// printf"Book 2 title : { Book1.title }\n"{ 0 : %s }
	printf("Book 2 author : %s\n", Book2.author) ;	// printf"Book 2 author : { Book1.author }\n"{ 0 : %s }
	printf("Book 2 subject : %s\n", Book2.subject) ;	// printf"Book 2 subject : { Book1.subject }\n"{ 0 : %s }
	printf("Book 2 book_id : %d\n", Book2.book_id) ;	// printf"Book 2 book_id : { Book1.book_id }\n"{ 0 : %d }
	
	return 0 ;
}
```
## used as func arguments
```c
#include <stdio.h>
#include <string.h>

struct Books	// def struct Books
{
	/* member = [static_varstr title[50], static_varstr author[50], static_varstr subject[100], var book_id], dtype = [char, char, char, int] */
	char title[50] ;
	char author[50] ;
	char subject[100] ;
	int book_id ;
} ;

/* declare func to call */
void printfBook( struct Books book ) ;

int main()	// def main
{
	struct Books Book1 ;	// craete empty var Book1, struct Books, auto
	struct Books Book2 ;	// craete empty var Book2, struct Books, auto

	/* set attribuets' value of Book1 */
	strcpy( Book1.title, "C Programming" ) ;	// cp "C Programming" to Book1.title
	strcpy( Book1.author, "Nuha Ali" ) ;	// cp "Nuha Ali" to Bokk1.author
	strcpy( Book1.subject, "Programming Tutorial" ) ;	// cp "C Programming Tutorial" to Book1.subject
	Book1.book_id = 6495700 ;	// set Book1.book_id = 6495700 

	/* set attribuets' value of Book2 */
	strcpy( Book2.title, "Telecom Billing") ;	// cp "Telecom Billing" to Book2.title
	strcpy( Book2.author, "Zara Ali" ) ;	// cp "Zara Ali" to Book2.author
	strcpy( Book2.subject, "Telecom Billing Tutorial" ) ;	// cp "Telecom Billing Tutorial" to Book2.subject
	Book2.book_id = 6495407 ;	// set Book2.book_id = 6495407

	printfBook( Book1 ) ;	// call members' value of Book1 by printfBook( Book1 )

	printfBook( Book2 ) ;	// call members' value of Book2 by printfBook( Books2 )

	return 0 ;
}

void printfBook( struct Books book )	// def func printfBook : arg = [ var book ], dvalue = null, dtype = [ struct Books ], r = void
{
	printf("Book title: %s\n", book.title) ;	// printf"Book title: { book.title }\n"{ %s }
	printf("Book author: %s\n", book.author) ;	// printf"Book author: { book.author }\n"{ %s }
	printf("Book subject: %s\n", book.subject) ;	// printf"Book subject: { book.subject }\n"{ %s }
	printf("Book book_id: %d\n", book.book_id) ;// printf"Book book_id: { book.book_id }"{ %d }
}
```
## ptr pointing to struct
```c
#include <stdio.h>
#include <string.h>

struct Books // def struct Books
{
    /* member = [static_varstr title[50], static_varstr author[50], static_varstr subject[50], var book_id], dtype = [char, char, char, int] */
    char title[50] ;
    char author[50] ;
    char subject[100] ;
    int book_id ;
} ;

/* declare func to call */
void printfBook( struct Books *book ) ;

int main()  // def main
{
    struct Books Book1 ;    // craete empty var Book1, struct Books, auto
    struct Books Book2 ;    // craete empty var Book2, struct Books, auto
    
    /* set members's value of Book1 */
    strcpy( Book1.title, "C Programming" ) ;    // cp 'C Programming' to Book1.title
    strcpy( Book1.author, "Nuha Ali" ) ;    // cp 'Nuha Ali' to Book1.author
    strcpy( Book1.subject, "Programming Tutorial" ) ;   // cp 'Programming Tutorial' to Book1.subject
    Book1.book_id = 6495700 ;   // set Boo1.book_id = 6495700

    /* set members' value of book2 */ 
    strcpy( Book2.title, "Telecom Billing" ) ;  // cp 'Telecom Billing' to Book2.title
    strcpy( Book2.author, "Zara Ali" ) ;    // cp 'Zara Ali' to Book2.author
    strcpy( Book2.subject, "Telecom Billing Tutorial" ) ;   // cp 'Telecom Billing Tutorial' to Book2.subject
    Book2.book_id = 6495407 ;   // set Book2.book_id = 6495407

    printfBook(&Book1) ;   // call members' value of Book1 by printfBook( { addr of Book1 } )
    printfBook(&Book2) ;   // call members' value of Book2 by printfBook( { addr of Book2 } )

    return 0 ; 
}

void printfBook( struct Books *book )    // def func printfBook : arg = [ptr var book], dvalue = null, dtype = null, dtype = struct Books, r = void
{
    printf("Book title : %s\n",book->title) ;   // printf"Book title : { book->title }\n"{ %s }    // access member value, for non*, var.member ;  for *, var->member
    printf("Book author : %s\n",book->author) ; // printf"Book author : { book->author }\n"{ %s }
    printf("Book subject : %s\n",book->subject) ;    // printf"Book subject : { book->subject }\n"{ %s }
    printf("Book book_id : %d\n",book->book_id) ;  // printf"Book book_id : { book->book_id }\n"{ %d }
}
```
## size
```c
#include <stdio.h>

struct Person   // def struct Person
{
    /* member = [static_varstr name[50], var age, var height], dtype = [char, int, float] */
    char name[50];
    int age;
    float height;
};

int main()  // def main
{
    struct Person person;   // create empty var person, struct Person, auto

    printf("struct Person's size is %zu byte\n",sizeof(person));   // printf"struct Person's size is { sizeof(person) } bit\n"{ %zu }    // sizeof() -- %zu

    return 0 ; 
}
```
# union
## define
```c
#include <stdio.h>
#include <string.h>

union Data  // def union Data
{
    /* member = [var i, var f, static_varstr str[20]], dtype = [int, float, char] */
    int i;
    float f;
    char str[20];
} ;

int main()  // def main
{
    union Data data ;   // create empty var data, union Data, auto

    printf("Memory size occupied by data : %zu\n", sizeof(data)) ;  // printf"Memory size ocuupied by data : { size of data }\n"{ %zu }

    return 0 ;
}
```
## access
```c
#include <stdio.h>
#include <string.h>

union Data  // def union Data
{
    /* member = [i, f, str], dtype = [int, float, char], v_type = [var, var, str[20]] */
    int i ;
    float f ;
    char str[20] ;
} ;

int main()  // def main
{
    union Data data ;	// create empty var data, union Data, auto
    
    data.i = 20 ;	// set data.i = 10, clear other members value	// if var is union var, you need to add 'clear other members value' when give value to var
    printf("data.i = %d\n", data.i) ;	// printf "data.i = { data.i }\n"{ %d }

    data.f = 220.5 ;	// set data.f = 220.5, clear other members value
    printf("data.f = %f\n", data.f) ;	// printf "data.f = { data.f }\n"{ %f }

    strcpy(data.str, "C Programming") ;	// cp "C Programming" to data.str, clear other members value
    printf("data.str = %s", data.str) ;	// printf "data.str = { data.str }"{ %s }
    
    return 0 ;
}
```

