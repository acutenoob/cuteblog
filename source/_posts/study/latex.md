---
title: latex 科技论文
date: 2026-04-03 18:53:16
tags: [日常,学习]
---

~~没错 我要用 KaTeX 记录 LaTeX 笔记~~

# 欢迎来到 

$$\LaTeX$$

写科论文 ~~好中二~~

# 论文规范

## 论文检索

- SCI 期刊
- CPCI-S(ISTP) 会议
- EI 工程索引

# latex 写作

## hallo world
```latex
\documentclass{article}
\author{Author Name}
\title{Paper Title} % 正文之外
\begin{document}
\maketitle % 补充日期
Hello,world!
\end{document}
```

## 章节划分

- \section{} 一级标题
- \subsection{} 二级标题
- \subsubsection{} 三级

- \paragraph 段落
- \subparagraph
- \par

## 目录和换行

- \tableofcontents  目录
- \\\\  换行

## 数学公式

- \$F = ma\$  不换行 
- \$\$F = ma\$\$  换行
- \\[F = ma\\]  换行 自动编号
- \begin{equation}
- \end{equation}

## 插图

```latex
\begin{figure}
\centering
\includegraphics[width=6.5cm]{fig.eps} % 方括弧指定参数 \linewidth  线宽 半宽是 0.5\linewidth
\caption{Figure Demo} %标题
\end{figure}
```
## 表格
```latex
\begin{table}
\caption{Table Demo}
\begin{tabular}{|l|c|c|} 制定列数 后面指 靠左 居中 居中
\hline  % 画线
Method & Results & Runing Time\\
\hline \hline
M1 & 1 & 0.01\\
M2 & 2 & 0.02 \\
\hline
\end{tabular}
\end{table}
```

## 标记与引用
- \label{}  注意要顾名思义
- \ref{}

## 引文
- \cite{} 本质也是label

- \begin{thebibliography}
- \bibitem{}   引用 citea
- \end{thebibliography} 

- \bibliographystyle{}  指定格式
- \bibliography{} 指定哪个

- bib当成参考文献库 大写要加大括弧
