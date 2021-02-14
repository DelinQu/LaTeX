# LaTeX 快速入门



## Hello World！

```latex
\documentclass{article}
% 这里是导言区
\begin{document}
Hello, world!
\end{document}
```

- 第一行 `\documentclass{article}` 中包含了一个**控制序列**（或称命令/标记）。所谓控制序列，是以反斜杠 `\` 开头，以第一个***空格或非字母\*** 的字符结束的一串文字。它们不被输出，但是他们会影响输出文档的效果。这里的控制序列是 `documentclass`，它后面紧跟着的 `{article}` 代表这个控制序列有一个必要的参数，该参数的值为 `article`。这个控制序列的作用，是调用名为 `article` 的文档类。
- 部分控制序列还有被方括号 `[]` 包括的可选参数。所谓文档类，即是 TeX 系统预设的（或是用户自定的）一些格式的集合。不同的文档类在输出效果上会有差别。
- 控制序列 `begin`。这个控制序列总是与 `end` 成对出现。这两个控制序列以及他们中间的内容被称为**「环境」**；它们之后的第一个必要参数总是**一致的**，被称为环境名。只有在 `document` 环境中的内容，才会被正常输出到文档中去或是作为控制序列对文档产生影响。也就是说，在 `\end{document}` 之后插入任何内容都是无效的。

- **导言区**：从 `\documentclass{article}` 开始到 `\begin{document}` 之前的部分被称为导言区。你可以将导言区理解为是对整篇文档进行设置的区域——在导言区出现的控制序列，往往会影响整篇文档的格式。



## 宏的概念

- **宏包**：就是一系列控制序列的合集。这些控制序列太常用，以至于人们会觉得每次将他们写在导言区太过繁琐，于是将他们打包放在同一个文件中，成为所谓的宏包（台湾方面称之为「巨集套件」）。`\usepackage{}` 可以用来调用宏包。



## 中英混排

- 中文支持：XeTeX 原生支持 Unicode，并且可以方便地调用系统字体，我们只需要使用几个简单的宏包，就能完成中文支持。
- 中文的版式处理和标点禁则： `CTeX` 宏集一次性解决了这些问题。`CTeX` 宏集的优势在于，它能适配于多种编译方式；在内部处理好了中文和中文版式的支持，隐藏了这些细节；并且，提供了不少中文用户需要的功能接口。

> 注意：`CTeX` 宏集和 `CTeX` 套装是两个不同的东西。`CTeX` 宏集本质是 LaTeX 宏的集合，包含若干文档类（`.cls` 文件）和宏包（`.sty` 文件）。`CTeX` 套装是一个**过时的** TeX 系统。新版 `CTeX` 宏集的默认能够自动检测用户的操作系统，并为之配置合适的字库。对于 Windows 用户、Mac OS X 用户和 Linux 用户，都无需做任何配置，就能使用 `CTeX` 宏集来排版中文。

- 使用 `CTeX` 宏集来处理中英文混排的文档：

```latex
\documentclass[UTF8]{ctexart}
\begin{document}
你好，世界!
\end{document}
```

- 文档类从 `article` 变为 `ctexart`
- 增加了文档类选项 `UTF8`



## 组织文章

### (1) 定义 标题 作者 日期

```latex
\documentclass[UTF8]{ctexart}

\title{如何组织文章}
\author{LinXiaoDe}
\date{\today}

\begin{document}
\maketitle
你好，世界！
\end{document}
```

- 在 `document` 环境中，多了一个控制序列 `maketitle`：将在导言区中定义的标题、作者、日期按照预定的格式展现出来。

- 使用`titling`宏包可以修改上述默认格式。参考[TeXdoc](http://texdoc.net/texmf-dist/doc/latex/titling/titling.pdf)。



### (2) 章节和段落

在文档类 `article`/`ctexart` 中，定义了五个控制序列来调整行文组织结构。他们分别是：

- `\section{·}`
- `\subsection{·}`
- `\subsubsection{·}`
- `\paragraph{·}`
- `\subparagraph{·}`

> 在`report`/`ctexrep`中，还有`\chapter{·}`；
>
> 在文档类`book`/`ctexbook`中，还定义了`\part{·}`。

```latex
\documentclass[UTF8]{ctexart}

\title{如何组织文章}
\author{LinXiaoDe}
\date{\today}

\begin{document}
\maketitle

\section{章节section}
章节内容
\subsection{子章节subsection}
子章节内容
\subsubsection{子子章节}
\paragraph{段落1}
段落内容
\subparagraph{子段落}
子段落内容
\subsection{子章节2}
\paragraph{段落2} 
段落2内容
\end{document} 
```





### (3) 目录

- 在`\maketitle`下面插入控制序列 `\tableofcontents`
- 保存并用 XeLaTeX 编译**两次**

```latex
\documentclass[UTF8]{ctexart}

\title{如何组织文章}
\author{LinXiaoDe}
\date{\today}

\begin{document}
\maketitle
\tableofcontents
\section{章节section}
章节内容
\subsection{子章节subsection}
子章节内容
\subsubsection{子子章节}
\paragraph{段落1}
段落内容
\subparagraph{子段落}
子段落内容
\subsection{子章节2}
\paragraph{段落2} 
段落2内容
\end{document} 
```



## 数学公式

### (1) 基本方法：

**在导言区加载 `amsmath` 宏包。**在行文中，使用 `$ ... $` 可以插入行内公式，使用 `\[ ... \]` 可以插入行间公式，如果需要对行间公式进行编号，则可以使用 `equation` 环境：

```latex
\documentclass{article}
\usepackage{amsmath}

\begin{document}
    % 行内
    $ \beta = \alpha * \kappa  $
    % 行间
    \[ \delta = \lambda * \xi  \]
    % 标号
    \begin{equation}
    c = a^2 + b^2
    \end{equation}
\end{document}
```



### (2) 上下标

- **公式标点使用的规范：**行内公式和行间公式对标点的要求是不同的：行内公式的标点，应该放在数学模式的限定符之外，而行间公式则应该放在数学模式限定符之内。

```latex
\documentclass{article}
\usepackage{amsmath}
\begin{document}
Einstein 's $E=mc^2$.

\[ E=mc^2. \]

\begin{equation}
E=mc^2.
\end{equation}
\end{document}
```

- 在数学模式中，需要表示上标，可以使用 `^` 来实现（下标则是 `_`）
- **它默认只作用于之后的一个字符**，如果想对连续的几个字符起作用，请将这些字符用花括号 `{}` 括起来，例如：

```

```

