# basic process
	gcc -g test.c -o test
	gdb test, then
		set break point
			b line OR b main
		run the program
			r
		next step
			n
		...
# options
- check file
	- l
- break point(break point = where program runing stops)
	- set
		- b { line }, such as b main
	- check 
		- info b
- run
	- run  to break point
		- r
	- run  by step
		- start
	- next step
		- n
	- restore running
		- c
- process
	- debug child
		- set follow-fork-mode child
	- debug parent
		- set follow-fork-mode parent
	- set 
		- debug current process only
			- set schedule-multiple off
		- debug all process
			- set schedule-multiple on
	- ls
		- info inferiors
	- switch
		- inferiors { num }
- func
	- enter func at current step
		- s
- var
	- check
		- p { var }
- help
	- help [cmd]
		
		