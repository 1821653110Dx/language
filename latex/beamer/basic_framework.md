```tex
\documentclass{beamer}

\usetheme {default}	% 幻灯片主题

% 定义标题页的内容
\title{\LaTeX{} Beamer introduction}
\subtitle{Quick-start guide}
\author{latex-beamer.com}
\institute{Online Education}
\date{\today}
\logo{\includegraphics[width=2.5cm]{Beamer-Logo.png}} 	% 定义logo（logo的位置取决于所用的主题）

\begin{document}

% 标题
\begin{frame}[plain]	% title page
	\titlepage
\end{frame}

% 插入大纲
\begin{frame}{Overview}
    \tableofcontents	% 此时大纲是带子标题的，如果不想要子标题，这一行换成\tableofcontents[hideallsubsections]
\end{frame}

% 当前section起始页
\section{}
\begin{frame}{section}
    This is your first presentation!
\end{frame}
% 当前subsection第一页
\subsection{}
\begin{frame}{section}{subsection}
    \centering\Huge\textbf{}
\end{frame}
% 当前subsection的第二页
\begin{frame}
    This is your first presentation!
\end{frame}

% 最后一页
\begin{frame}	% tail page
		\Huge{\centerline{Thank you all！}}
		\centering{{\normalsize 我们是孩子，但我们精力充沛，勇往直前！}}
\end{frame}
\end{document}
```
