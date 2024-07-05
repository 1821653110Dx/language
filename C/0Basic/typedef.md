```c
#include <stdio.h>
#include <string.h>

typedef struct Books	// def struct Books, which has an alias
{
	/* 
	 member = [static_varstr title[50], static_varstr author[50], static_varstr subject[100], book_id]
	 d_type = [char, char, char, int]
	*/
	char title[50] ;
	char author[50] ;
	char subject[100] ;
	int book_id ;
} Book ; // alias = Book

int main()	// def main
{
	Book book ;	// create empty var book, Book, auto
	
	strcpy(book.title, "C 教程") ;	// cp "C 教程" to book.title
	strcpy(book.author, "Runboob") ;	// cp "Runoob" to book.author
	strcpy(book.subject, "编程语言") ;	// cp "编程语言" to book.subject
	book.book_id = 12345 ;	// set book.book_id = 12345
	
	printf("title = %s\n", book.title) ;	// printf "title = { book.title }\n"{ %s }
	printf("author = %s\n", book.author) ;	// printf "author = { book.author }\n"{ %s }
	printf("subject = %s\n", book.subject) ;	// printf "subject = { book.subject }\n"{ %s }
	printf("ID = %s\n", book.book_id) ;	// printf "ID = { book.book_id }"{ %d }

	return 0 ;	// exit program
} ;
```


