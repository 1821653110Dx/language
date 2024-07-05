# dir
## read and close dir
```c
#include <dirent.h>

DIR *dir; 
struct dirent *entry;  
dir = opendir("/etc");  // save addr of dir /etc to ptr dir
entry = readdir(dirp) ; // save addr of next dir_entry of dir dirp points to entry  // dir entries目录项 include both dir and files 
closedir(DIR *dirp) ;   // close dir dirp points to

int fd ;
DIR *dirp ;
fd = open("/etc", O_RDONLY | O_DIRECTORY);  // open dir "/etc" in mode = [read directory], return a fd | save to fd
dirp = fdopendir(fd);   // save addr of dir corresponding to fd of fd to dirp
```
```c
#include<stdio.h>
#include<stdlib.h>
#include<errno.h>
#include<dirent.h>

int main(int argc, char *argv[])
{
	DIR *dirp ;
	struct dirent *dp ;

	if (argc < 2)	// if received arg counts < 2
	{
		printf("please give directory") ;

		return -1 ;
	}
	if( ( dirp = opendir( argv[1] ) ) == NULL )	// save addr of dir(path = 1st arg) to ptr dirp | if dir dir points to not found
	{
		perror("opendir:") ;	// echo error "opendir:"

		return -1 ;
	}

	/* otherwise, print all dir_entry of dir dirp points to */
	while((dp = readdir(dirp)) != NULL)	// save addr of next dir_entry of dir drip points to dp | while exits
	{
		printf("%s\n", dp->d_name ) ;	// printf "{ name of dir_entry dp points to }\n"{ %s }
	}

	/* close opened dir and files */
	closedir(dirp) ;	// close dir dirp points to
	
	return 0 ;
}
```
## chmod
```c
#include <sys.stat.h>

chmod("myfile.txt", 0666)    // ch permission of ./myfile.txt : [owner, group_user, others] = rw

int fd ;
fchmod(fd, 0666)    // ch permission of file corresponding to fd's fd : [owner, group_user, others] = rw
```

## fetch file attributes
```c
#include<sys/stat.h>

struct stat fileStat ;
stat("myfile.txt", &fileStat) ;   // save attributes of ./myfile.txt to fileStat

struct stat buf ;
lstat("myfile.txt", &buf) ;  // save attributets of ./myfile.txt to BUF

fd = open("myfile.txt", O_RDONLY) ;
struct stat BUF ;
fstat(fd, &BUF) ;   // save attributes of file corresponding to fd' fd BUF
/*
attributes :
    dev_t         st_dev;    //文件的设备编号
    ino_t         st_ino;    //节点
    mode_t        st_mode;   //文件的类型和访问权限
    nlink_t       st_nlink;  //连到该文件的硬连接数目，刚建立的文件值为1
    uid_t         st_uid;    //用户ID
    gid_t         st_gid;    //组ID
    dev_t         st_rdev;   //(设备类型)若此文件为设备文件，则为其设备编号
    off_t         st_size;   //文件字节数(文件大小)
    unsigned long st_blksize;   //块大小(文件系统的I/O 缓冲区大小)
    unsigned long st_blocks;    //块数
    time_t        st_atime;     //最后一次访问时间
    time_t        st_mtime;     //最后一次修改时间
    time_t        st_ctime;     //最后一次改变时间(指属性)        
*/  
```
```c
/*
文件类型
    S_IFMT                 0170000     文件类型的位遮罩
    S_ISREG(st_mode)        0100000    是否常规文件
    S_ISDIR(st_mode)        0040000    是否目录
    S_ISCHR(st_mode)        0020000    是否字符设备
    S_ISBLK(st_mode)        0060000    是否块设备
    S_ISFIFO(st_mode)       0010000    是否FIFO文件
    S_ISLNK(st_mode)        0120000    是否链接文件
    S_ISSOCK(st_mode)       0140000    是否SOCKET文件
*/

if(S_ISREG(buf.st_mode))    // if file corresponding to struct_stat buf is regular_file
{
    ...
}
```
```c
/*
文件访问权限
    S_IRUSR         00400        bit:8    所有者有读权限
    S_IWUSR         00200            7    所有者拥有写权限
    S_IXUSR         00100            6    所有者拥有执行权限								  						 	
    S_IRGRP         00040            5   群组拥有读权限
    S_IWGRP         00020            4   群组拥有写权限
    S_IXGRP         00010            3   群组拥有执行权限
    S_IROTH         00004            2   其他用户拥有读权限
    S_IWOTH         00002            1   其他用户拥有写权限
    S_IXOTH         00001            0   其他用户拥有执行权限
*/

/* print permissions of [owner, group, others] */
for(i = 8;i >= 0; i--)  // for each {bit : i} in [8..0]
{
       if(buf.st_mode & (1<<i)) // if permission corresponding to bit exists
       {
          switch(i%3)
          {
          	case 2:   //8、5、2-r
              	printf("r");
              	break;
          	case 1:
              	printf("w"); // 7、4、1-w
              	break;
          	case 0:
              	printf("x"); // 6、3、0-x
              	break;
          }
       }
       else
       {
           printf("-");
       }
}
```
# library
> Static library updates will result in a recompilation of the file, while dynamic library updates will not.
## static library
- create static_library libxxxx.a with target_file xxx.o /append xxx.o to static_library libxxx.a
    - `ar -rsv libxxxx.a xxx.o`

> extra options of ar
>> c = not output non-error message
>> q = append .o to the end
>> t = output dir of the library to std_output

- generate a exec(without .o) with source.c, link <topath>/<static_lib.a> to it 
    - `gcc -o <exec> <source.c> -L <path> -l <static_lib.a>`

- check symbols of static_lib(such as var, function)
    - `$nm <static_lib>`
> extra options
>> -a : show all symbols
>
> explanation of key_word
>> T/t defined in code_section
>> U undefinded

## dynamic library
- complie *.c into target_files with PIC(position-independent-code)
    - `gcc -c -fPIC xxx.c xxxx.c …`
- link target_files into a dynamic_library libxxx.so
    - `gcc -shared -o libxxxx.so xxx.o xxx.o ...`
- generate a exec with souce.c, link <path>/<dynamic_lib.so> to it
    - `gcc -o <exec> <source.c> -L <path> -l <dynamic_lib.so>`
```c
执行动态库的可执行文件错误
./test: error while loading shared libraries: libmyheby.
so: cannot open shared object file:
 No such file or directory
含义：可执行文件所使用的动态库找不到
解决办法：
① 找到动态库，添加到/usr/lib里面
② 使用export  LD_LIBRARY_PATH=文件路径(recommend)
③ 动态库目录加在~/.bashrc 文件里面,使用source ~/.bashrc 生效。
```
- check dynamic_lib called by exec
    - `ldd <exec>`






    

