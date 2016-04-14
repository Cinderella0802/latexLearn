

#LaTeX教学笔记

2016/4/9 12:51:23 

[TOC]

# 基础知识

##关于TeX的介绍

TeX是一个以排版文章及数学公式为目标的计算机程序，在1997年由Knuth发明。其版本号不断趋近于Pi, 现在为3.141592.

LaTeX是一个宏集，它使用一个预先定义好的专业版面，可以使作者们高质量的排版和打印他们的作品。

这个排版系统的优势在于可以着眼于文章的逻辑结构，而非对版面进行修修补补。所以一般不要自定义文档版面布局。

PdfLaTeX支持Pdf格式的TeX文档导出。

下面主要以TeXStudio为编辑工具，自然也可以使用其他的软件。


## TeXStudio、CTeX的安装

> 本文使用环境
> CTeX_2.9.2.164_Full、texstudio-2.10.8-win-qt5.5.1、Windows 8

### CTeX安装 

1.  双击文件CTeX_2.9.2.164_Full.exe。选择权限允许。
2.  耐心等待安装完成



### TexStudio安装

1. 双击文件texstudio-2.10.8-win-qt5.5.1.exe，任意选择安装目录
2. 安装完成后，在`Options->Configuer TexStudio->General->language`中选择`system`，解决中文乱码
3. 同上选项卡中取消检查拼写
4. 在语法高亮中选择LaTex Syntax 中的粉色为白色

## LaTeX源文件
>Latex源文件事实上就是普通的文本文件，可以用任何支持文本编辑的软件编>辑。LaTex将文件翻译为排版的格式。

###空白

空格和制表符等空白字符在LaTeX中被看做相同的空白距离(space)。多个连续的空白字符等同于一个空白字符。在句首的空白距离一般会被忽略，单个空行也被认为是一个“空白距离”。

两行文本间的空白行标志着上段的结束和下段的开始。多个空白行的作用
等同于一个空白行。

以下是一段示例

```tex
不管你输入了多少 空格，最后      渲染出的文本会吃掉多余空格。

新的一行开启新的一段
```

### 特殊字符

在LaTeX中一些字符被赋予了特殊的含义，无法直接打出来，包括

| 特殊字符 |     转义序列     |
| :--: | :----------: |
|  #   |     \\#      |
|  $   |     \\$      |
|  %   |     \\%      |
|  ^   |     \\^      |
|  &   |     \\&      |
|  _   |     \\_      |
|  {   |     \\{      |
|  }   |      \}      |
|  \\  | $\backslash$ |

### LaTeX 命令

LaTeX的主要命令是**大小写敏感**的。

LaTeX忽略命令后的空白字符。

有些命令需一个参数，该参数用花括号`{}`括住并写在命令的后面。一些命令支持可选参数，用方括号`[]`括住并写在命令后面。

```latex
试试看\textsl{Slide}。\newline
还有新的\\一行。
	 
	 这里分段
	 \newpage
	 这里开始了新的一页
```

### 注释

当LaTeX处理一个源文件时，如果遇到一个百分号%，LATEX 将忽略% 后的该行内容，换行符以及下一行前的空白字符，最后他们不会出现在结果中。

较长的注释需要用到verbatim宏包提供的comment环境。

```latex
%在导言中加入下行代码
\usepackage{verbatim}

长注释的演示
\begin{comment}
这是长长的注释
可以随便换行
\end{comment}
```

## 源文件的结构

源文件以如下命令开始

```latex
\documentclass{...}
```

命令指明了你所写的源文档的类型。然后，你就可以加入控制整篇文档样式的命令，或者载入一些为LATEX 增加新特性的宏包(package)。可以用如下命令载入一个宏包

```latex
\usepackage{...}
```

完成设置工作后，可以用下面的命令开始文章的主体

```latex
\begin{document}
```

现在你就可以输入带有LATEX 命令的正文了。在文章末尾使用命令

```latex
\end{document}
```

来告诉LATEX 文档已经结束。LATEX 会忽略此命令后的所有内容。

下方是一个中文文档的示例

```latex
%这行字是指单面输出、A4纸张、11磅字重、ctexbook类型
\documentclass[oneside,a4paper,11pt]{ctexbook}

\begin{document}
	%文章标题
	\title{\LaTeX教学笔记}
	%文章作者
	\author{王尼玛}
	%生成标题页的命令
	\maketitle
	%居中
	\begin{center}
			这会是一本神奇的书
	\end{center}
	
\end{document}
```

## 文档布局

### 文档类

当LATEX 处理源文件时，首先需要知道的就是作者所要创建的文档类型。文档类型可由`\documentclass` 命令来指定。

```latex
\documentclass[options]{class}
```

### 宏包

排版文档时，你可能会发现某些时候基本的LATEX 并不能解决你的问题。如果想插入图形(graphics)、彩色文本(coloured text) 或源代码到你的文档中，你就需要使用宏包来增强LATEX 的功能。可使用如下命令调用宏包

```latex
\usepackage[options]{class}
```

### 页面样式

LATEX 支持三种预定义的页眉/页脚(header/footer) 样式，称为页面样式(page style)。如下命令

```latex
\pagestyle{style}
```

中的style 参数确定了使用哪一种页面样式。

可以通过如下命令改变当前页面的页面样式

```latex
\thispagestyle{style}
```

## LaTeX文件

- .tex 源文件
- .sty 宏包文件
- .eps 矢量图格式
- .pdf Adobe公司创造的文件格式

# 文本排版

## 段落和分行

一般来说，一个空行意味着一段的结束。不加空行，则LaTeX会忽略空格，继续将字符添加到上一段末尾。

```latex
这是第一段
，这样会接上去。

只有这样会重新另起一段。
```

在特殊情形下，有必要命令LATEX 断行

```latex
\\或者\newline
```

另起一行而不另起一段。

```latex
\\*
```

在强制断行后，还禁止分页。

```latex
\newpage
```

另起一页。

## 特殊字符和符号

### 引号

印刷中有专门的左引号和右引号。LaTeX中，用两个`（重音）产生左引号，用两个'（直立引号）产生右引号。一个‘ 和一个’ 产生一个单引号。

```latex
``双引号不能再用中文`输入法'输入''
```

### 破折号和连字号

LATEX 中有四种短划(dash) 标点符号。连续用不同数目的短划，可以得到其中的三种。第四个实际不是标点符号，它是数学中的减号：

```latex
中文一般不用-连字号，除了电话号码.\\
以及短破折``12--13页''这种表述\\
长破折号用于---犹豫等语气\\
$-1$的长度和他们不同
```

### 波浪号

有两种波浪号，比较一下

```latex
\~和$\sim$，后面一种更常用。
```

> 前一种会在CJK中报错

### 省略号

不可以用三个英文句点表示省略号，一般用`\ldots`表示英文的省略号。

## 标题、章和节

为了便于理解，应该把文章分为章、节和子节。LaTeX用专门的命令支持这个工作，这些命令把标题作为参量。

```latex
%如下代码把book类分成章、节、子节
\chapter[王尼玛]{王尼玛在蓉城的故事}
\section[大一]{关于大一混吃混喝的一切}
\subsection{吃}
%之后的层次不会在目录中出现
\subsubsection{火锅}
\paragraph{大宅门}
\subparagraph{某个周五}
```

命令`\appendix`只把章的序号改为字母标记，在article 类中改变节的字号。

命令`\tableofcontents`在当前位置插入目录。

上述列出的分节命令中，带上*号，则生成的节标题既不出现于目录，也不带序号。

分节命令中可选参数为出现在目录中的节标题。

整篇文章的标题由命令`\maketitle`生成。

```latex
\title{一本教学笔记}
\author{王尼玛}
%可选的
\date{\today}
```

下面使一些用于book类的实用命令。

+ `\frontmatter` 接着命令`\begin{document}` 使用。它把页码更换为罗马数字，而且章节不计数。当你使用带星的分节命令(例如`\chapter*{Preface})`时，这些章节就不会出现在目录里。

+ `\mainmatter` 应出现在书的第一章前面。它启用阿拉伯数字的页码计数器，并对页码重新计数。

+ `\appendix` 标志书中附录材料的开始。该命令后的各章序号改用字母标记。

+ `\backmatter` 应该插入与书中最后一部分内容的前面，如参考文献和索引。在标准文档类型中，它对页面没有什么效果。


## 交叉引用

在书籍、报告和论文中，对图、表和文本的特殊段落进行交叉引用。

```latex
%\label{marker}     给节、子节、图、表、公式或定理起个别名marker
%\ref{marker}       将替换为marker相应的序号
%\pageref{marker}   将排印marker所在的页码

\section{第一节}\label{s1}
王尼玛
\section{第二节}
王尼玛在\ref{s1}节中出现，具体在第\pageref{s1}页处。
```

## 脚注

命令`\footnote{text}` 把脚注内容排印与当前页的页脚位置，应该用逗号或句号结尾。

```latex
关于使用脚注\footnote{会引开注意力，而且你一定会看过来}，为什么把这些不写在正文中呢。
```

## 强调

命令`\emph{text}`可以强调文本。

```latex
不同的上下文和字体会有不同的\emph{强调}效果
```

## 环境

为了排版某些专用的文本，LaTeX定义了不同格式的环境：

```latex
%\begin{environment}
%  text
%\end{environment}
\begin{displaymath}
	x^{n}+y^{n}=z^{n}
\end{displaymath}
```

环境可以嵌套。

下方出现的命令为环境名，替换上面代码中的environment。

### 列表环境

LaTeX可以方便的生成各种列表。

+ `\itemize`适用于简单的列表，命令`\item[index]` 可用index作为项目标记。

+ `\enumerate` 适用于有排列序号的列表

  > 使用宏包enumerate可以定制列表的序号。
  >
  > ```latex
  > %导言
  > \usepackage{enumerate}
  >
  > %text可替换为任意字符串
  > %i为罗马数字，a为希腊字母，1为数字
  > \begin{enumerate} [{text} i]
  > 	\item 一二三四五
  > 	\item 上山打老虎
  > \end{enumerate} 
  > ```

+ `\description` 适用于带描述的列表，命令`\item[label]` 可用label作为标签。

```latex
\begin{enumerate}
	\item 带数字的列表
	\item 列表可以嵌套
	\begin{itemize}
		\item 简单列表默认
		\item[+] 可以修改项目标记
		\begin{description}
			\item[标签] 标签列表的标签显示取决于环境
		\end{description}
	\end{itemize}
\end{enumerate}
```

### 对齐

`\flushleft`左对齐，`\flushright`为右对齐，`\center` 为居中。

### 引用

`\quote`引文，`\quotation`为长引文，`\verse` 为诗歌。

### 摘要

一般摘要用于article 类文档。命令为`\abstract` 

### 原文打印

`\begin{verbatim}`和`\end{verbatim}` 之间的文本将直接打印。

在段落中`\verb+text+` 可将分隔符+之间的文本直接打印，其中+可以为除了*和空格的任意字符。

### 表格

tabular环境可用于排版带有水平和垂直表现的漂亮个表格。LaTeX会自动设置单元格的长宽，也就意味着**不会自动换行**。

命令`\begin{tabular}[pos]{table spec}` 的参量*table spec*定义了表格的样式。其中`l` 产生左对齐的列，`r`产生右对齐的列，`c` 产生居中的列。用`p{width}` 产生宽为width且自动断行的列；`|` 产生垂直表线。

参量*Pos* 设定相对于环绕文本基线的垂直位置。使用字母`t`、 `b`和`c` 来设定表格靠上、靠下或者居中放置。

在tabular环境中，用`&`跳入下一列，用`\\` 开始新的一行，用`\hline`插入水平表线。用`\cline{j-i}`可添加部分表线，其中`j`和`i`分别表示表线的起始列和终止列序号。

> 支持宏包diagbox后，可以在tabular环境中用命令`\diagbox{leftBottom}{leftTop}{rightTop}`生成对角线表格。

命令`\multicolumn{cols}{spec}{text}`可以生成一个较宽的列。参量`cols`表示所占列数，`spec` 标记了单元格样式，`text`为文本。

```latex
\usepackage{diagbox}

\begin{tabular}{|c|c|c|}
	\hline
	\multicolumn{3}{|c|}{如何追女孩的建议}\\
	\hline 
	\diagbox{财气}{建议}{颜值} & 帅& 挫\\
	\hline
	有钱花 & 没啥好说的 & 没啥好说的 \\
	\hline
	叮当响 & 没啥好说的 & 没啥好说的  \\
	\hline
\end{tabular}
```

### 浮动体

有时候，安排一张图片和表格的位置是一件令人抓狂的事。LaTeX提供了`\figure`和`\table`环境，专门用于浮动图片和表格的位置。

> LaTeX会按参数要求将浮动体放入先入先出队列中，知道满足条件的位置出现，否则一个浮动体将挡住之后所有的浮动体。一旦惨剧发生，你会发现所有的表格和图片都放在了文档最后。
>
> 当然可以用命令`\clearpage`强制放置等待队列中所有剩下的浮动体

命令格式为

```latex
\begin{figure}[placement specifier] 或 \begin{table}[...]
```

可选参数*placement specifier*是由浮动许可放置参数写成的字符串组成，具体见下表。他们告诉了LaTeX浮动提可以被移放的位置，一般可以有很多可防止参数一起构成字符串，标志了多个可用位置。

| Spec |   浮动体许可放置位置    |
| :--: | :------------: |
|  h   |    在文本的确切位置    |
|  t   |      页面顶部      |
|  b   |      页面底部      |
|  p   |  只有一个浮动体的专门页面  |
|  !   | 忽略阻止浮动体放置的内部参数 |

命令`\caption[short title]{title}` 可以给图片或表格加个标签。

下面是个例子

```latex
懒得打字所以复制了很多遍。
	
%可以尝试换为其他的参数
\begin{table}[hb] 
	\caption[短标题]{装模做样的表格}
	\begin{center}
		\begin{tabular}{c}
			\hline
			这是一个表格\\
			\hline
		\end{tabular}
	\end{center}	
\end{table}
懒得打字所以复制了很多遍。
```

当然交叉引用的两个命令也可以使用。

### 保护脆弱命令

作为命令参量的文本，可能在文档中出现多次。当用于类似`\section`的参量时，一些命令会失效。这些命令就被称为脆弱命令。此时在命令前加`\protect`可以保护它们。

#基础数学公式

LaTeX有强大的排版公式能力，你可以在很短的时间内打印出一份符合规范的数学论文。

**以下均使用宏包`amsmath`**

## 综述

LaTeX有两种特定的模式来排版数学公式，包括行内数学模式和行间数学模式。

行内数学模式将公式排版在一个段落中，使用方式为`\(...\)` 、`$...$`和`\begin{math} ... \end{math}`.

行间数学模式一般用于较长的数学方程或希望单独显示的公式，使用方式为`\[...\]`和`\begin{displaymath}...\end{displaymath}。

> 注意，数学和物理文献中的标点符号全部用英文标点。输入英文的逗号和句号后，需要手动在后面打一个空格。
>
> ```latex
> 一个众所周知的公式: $a^{2}+b^{2}=c^{2}$, 被用作数学的代表.
>
> 一个众所周知的公式:$a^{2}+b^{2}=c^{2}$,被用作数学的代表.
> ```

在TexStudio中，行内数学模式快捷键为`Ctrl+Shift+M` 行间模式快捷键为`Alt+Shift+M`

如果希望将方程编号，并在之后使用标签去交叉引用，就需要用到`equation` 环境。

> 注意，在数学模式中，每个字母都会被认为是一个变量名，并被排版为这种样式。如果需要排版普通的文本，就需要将文本放在`\text{...}`命令中。
>
> ```latex
> $\forall x \in E,\text{ s.t. } x>0$
> ```

## 数学模式的群组

大部分数学模式的命令只对其后的一个字符有效，因此，如果你希望一个命令对多个字符起作用，你必须把它们放在一个群组中，使用花括号：{}

```latex
$ e^{i\pi} =1  $
```

## 数学公式的基本元素

下面介绍一些数学排版中最重要的一些命令。

**希腊字母** 小写输入为`\alpha, \beta, \gamma, ...` 大写输入为`\Gamma, \Delta`

**指数和下标** 可以分别通过`^`和`_` 两个符号指定，注意如果指数和下标超过了一个字符，需要用到群组。即把文本用花括号括起来。惯例是先输下标后输指数。

在TexStudio中，下标的快捷键为`Ctrl+Shift+D` ，指数的快捷键为`Ctrl+Shift+U`



