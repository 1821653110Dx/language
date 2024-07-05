# summary
$$
\begin{equation*}
	\begin{cases}
		\text{logical structures}
		\begin{cases}
			\text{linear structes} 
				\begin{cases}
					\text{linear list }\\
					\text{stack} \\
					\text{quene}
				\end{cases}
			\\
			\text{non linear structures}
				\begin{cases}
					\text{tree structure} \\
					\text{graph structure}
				\end{cases}
		\end{cases}
		\\
		\text{storage structures} 
			\begin{cases}
				\text{sequential storage} \\
				\text{linked storage链式存储} \\
				\text{indexed storage} \\
			\end{cases}
		\\
		\text{data operations : search, sort, insert, add, delete, modify ...}
	\end{cases}
\end{equation*}
$$
# definition of data structures
data structures = logical structures +  storage structures + data operations
## logical structures
- set
    - just data elements belong to the same set
![b5fc5858376c7fc5a311978bf8981b38.png](../../../_resources/b5fc5858376c7fc5a311978bf8981b38.png)

- linear structure
    - one to one(linear list, stack栈, queue队列)
![52558b2e56fd9ffafd8336eacbffe22d.png](../../../_resources/52558b2e56fd9ffafd8336eacbffe22d.png)
> linear list : add and delete operations are allowed everywhere
> stack : add and delete operations are only allowed at the top of the stack
> > stack top : the end一端 that allows operation
>   
> quene : allowing adding elements at the end of the quene and deleting element at the beginning of the quene
- tree structure
    - one to more
![f7b839e17656ec859681edff8bd44f7b.png](../../../_resources/f7b839e17656ec859681edff8bd44f7b.png)
- graph structure
![8605752e96908e807b5b4e15d0a05c29.png](../../../_resources/8605752e96908e807b5b4e15d0a05c29.png)

## storage structure
- sequential storage顺序存储
	- put each elements of the data structure in a continuous storage space according to its logical order
	![92dce30af0e096ce9e8d47a3d7903536.png](../../../_resources/92dce30af0e096ce9e8d47a3d7903536.png)
- linked storage链式存储
	- put each element of the data structure in different places,  linking them together using addr/ptr
	![113790dcdac5f28bf4bff4617b7981b5.png](../../../_resources/113790dcdac5f28bf4bff4617b7981b5.png)
- indexed storage索引存储
	- including data file + indexed tabel索引表
> indexed tabel : a tabel including keys and ptr