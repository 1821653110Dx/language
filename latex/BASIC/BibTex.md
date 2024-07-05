```tex
\documentclass{ctexart}

\bibliographystyle{plain}	% 设置参考文献的引用风格为: plain

\begin{document}
	这是一个参考文献的引用: \cite{article1}

	这是另一个参考文献的引用：\cite{book1}
		
	\begin{thebibliography}{99}	% 开始编写参考文献，参考文献编号最多为99
		\bibitem{article1}张三，李四. \emph{基于LaTex的Web数学公式提取方法研究}. 计算机科学. 2014(06)	% 会自动编号;这处文献用标签'article1'指代，想要引用这个文献是用\cite{article}; \cite{标签1,标签2, ...}
		\bibitem{book1}William H. Press, Saul A. Teukolsky, William T. Vettering,Brain P. Flannery, \emph{Numerical Recipes 3rd Edition: The Art of Scientific Computing } Cambrige University Press, New York, 2007.
	\end{thebibliography}	
\end{document}
```