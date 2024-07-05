# mem mapping 内存映射
map a disk file to a buffer in ram, then a process can access the file as if it were accessing ram, without the need of read and write
## write into shared mem mapping
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/mman.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<string.h>

int main(int argc, const char *argv[])
{
	int fd, len ;
	void *map ;

	fd = open("1.txt", O_RDWR) ;	// open file"1.txt" in mode = [read_nonover-write], return a fd | save fd
	if(fd == -1)
	{
		perror("open:") ;

		return -1 ;
	}
	
	len = lseek(fd, 0, SEEK_END) ;	// mv fptr to last byte of file(file descriptor = fd) and return its index | save to len	// here returned index = len of the file
	map = mmap(NULL, len, PROT_READ|PROT_WRITE, MAP_SHARED, fd, 0) ;	// map file(file_descriptor = fd) to certain buffer in ram, which can be [read, write] and is shared, return addr of map | save to map	// write  = nonover-write + overwirte	// size of a file used to map must > 0
	if(map == MAP_FAILED)	// if fail to map
	{
		perror("open:") ;

		return -1 ;
	}

	while(1)
	{
		memcpy(map++, "a", 1) ;	// cp "a" to mem_region mapped by map, map points to next byte	// 1 = bytes of "a"	// 
	}

	return 0 ;
}
```
## read from shared mem mapping
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/mman.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<string.h>

int main(int argc, const char *argv[])
{
	int fd, len ;
	void *map ;

	fd  = open("1.txt", O_RDWR) ;	// open file"1.txt"	in mode=[read_nonover-write], return a fd | save to fd
	if(fd == -1)
	{
		perror("open:") ;

		return -1 ;
	}

	len = lseek(fd,0,SEEK_END) ;	// mv fptr to last byte of file(file_descriptor = fd) and return len of the file | save to len
	map = mmap(NULL,len,PROT_READ|PROT_WRITE, MAP_SHARED,fd,0) ;	// map file(fd = fd) to certain buffer in ram,which canbe [read, write] and is shared, return addr of map | save to map
	if(map == MAP_FAILED)
	{
		perror("map:") ;

		return -1 ;
	}

	while(1)
	{
		printf("%s\n", (char *)map) ;	// printf"{ (char *)map }\n"{ %s }

		sleep(1) ;
	}

	return 0 ;
}
```
# system v shared mem
system V shared mem allow many processes shares a  block of ram
## write into sys_v_shared_mem
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<sys/mman.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<string.h>

int main(int argc, const char *argv[])
{
	int fd, len ;
	void *map ;

	fd = open("1.txt", O_RDWR) ;	// open file"1.txt" in mode = [read_nonover-write], return a fd | save fd
	if(fd == -1)
	{
		perror("open:") ;

		return -1 ;
	}
	
	len = lseek(fd, 0, SEEK_END) ;	// mv fptr to last byte of file(file descriptor = fd) and return its index | save to len	// here returned index = len of the file
	map = mmap(NULL, len, PROT_READ|PROT_WRITE, MAP_SHARED, fd, 0) ;	// map file(file_descriptor = fd) to certain buffer in ram, which can be [read, write] and is shared, return addr of map | save to map	// write  = nonover-write + overwirte	// size of a file used to map must > 0
	if(map == MAP_FAILED)	// if fail to map
	{
		perror("open:") ;

		return -1 ;
	}

	while(1)
	{
		memcpy(map++, "a", 1) ;	// cp "a" to mem_region mapped by map, map points to next byte	// 1 = bytes of "a"	// 
	}

	return 0 ;
}
```
## read from sys_v_shared_mem
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/ipc.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<sys/shm.h>

int main(int argc, const char *argv)
{
	key_t key ;
	void *buf ;

	key = ftok("keytest", 100) ;	// create key key with [file, subid]=["kettest",100]
	if(key == -1)	// if fail to create key key
	{
		perror("ftok:") ;

		return -1 ;
	}
	printf("%d\n",key) ; 

	buf = shmat(32822, NULL,0) ;	// append shared_mem_seg(shmid=32822) to current process's mem_seg, return its addr | save to buf
	printf("%s\n", (char *)buf) ;
	
	shmdt(buf) ;	// detach shared_mem_seg buf points to from current process's mem_seg
	shmctl(32822, IPC_RMID, NULL) ;	// delete share_mem_seg(shmid=32822)
	
	return 0 ;
}
```