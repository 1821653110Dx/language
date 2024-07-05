# func
```c
	strcpy(s1,s2)	// cp static_varstr s2 to static_varstr s1
	strcat(s1,s2)	// append static_varstr s2 to static_varstr s1
	strlen(s1)	// get the len of static_varstr s1
```

# example
```c
#include <stdio.h>
#include <string.h>

int main()	// def main
{
	char str1[14] = "runoob" ;	// create static_varstr str1[14] = "runoob", char, auto
	char str2[14] = "google" ;	// create static_varstr str2[14] = "google", char, auto
	char str3[14] ;	// create empty static_varstr str3[14], char, auto
	int len ;	// create empty var len, int, auto

	strcpy(str3, str1) ;	// cp static_varstr str1 to static_varstr str3
	printf("strcpy( str3, str1 ) : %s\n",str3) ;	// printf"strcpy( str3, str1 ) : { str3 }\n"{ str3 : %s }

	strcat(str1, str2) ;	// append static_varstr str2 to static_varstr str1
	printf("strcat( str1, str2 ) : %s\n", str1) ;	// printf"strcat( str1, str2) : { str1 }\n"{ str1 : %s }

	len = strlen(str1) ;	// save len of str1 to len
	printf("strlen( str1 ) : %d", len) ;	// printf"strlen( str1 ) : { len }"{ len : %d }

	return 0 ;	// exit program
}
```


