# LaTeX 快速入门  :star2:

<img src="https://www.latex-project.org/img/latex-project-logo.svg" width = 250 /> 

- 参考自一份其实很短的 LaTeX 入门文档：[https://liam.page/2014/09/08/latex-introduction/](https://liam.page/2014/09/08/latex-introduction/)
- 我的LaTeX仓库：[https://github.com/LinXiaoDe/LaTeX](https://github.com/LinXiaoDe/LaTeX)

## Install<img src="https://i.loli.net/2021/02/14/uOl4JX8sBNw9a3V.png" alt="VS Code + LaTeX" width = 200 /> 

- archLinux

```zsh
yay -S texlive-full
```

- 添加环境变量

<img src="https://i.loli.net/2021/02/13/T4IuDldRy5wAK6a.png" alt="image-20210213230531038" style="zoom:55%;" /> 

- 添加环境变量

```zsh
# 方法
export TexMan="/opt/texlive/2021/texmf-dist/doc/man"
export TexInfo="/opt/texlive/2021/texmf-dist/doc/info"
export TexLive="/opt/texlive/2021/bin/x86_64-linux"

export MANPATH="$MANPATH:$TexMan"
export INFOPATH="$INFOPATH:$TexInfo"
export PATH="$PATH:$TexLive"
```





# Quick Start :high_brightness:

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

- 推荐一个在线公式编辑器： [https://www.latexlive.com/](https://www.latexlive.com/)
- 在VsCode的symbols中也有相应的符号

### (1) 基本方法：

**在导言区加载 `amsmath` 宏包。**在行文中，使用 `$ ... $` 可以插入行内公式，使用 `\[ ... \]` 可以插入行间公式，如果需要对行间公式进行编号，则可以使用 `equation` 环境（还有很多其他的环境在下面介绍）：

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

```latex
\begin{equation}
    z = r\cdot e^{2\pi i}
\end{equation}
```



### (3) 根式与分式

- 根式用 `\sqrt{·}` 来表示
- 分式用 `\frac{·}{·}` 来表示（第一个参数为分子，第二个为分母）

```latex
\begin{equation}
    \sqrt{x}
\end{equation}

\begin{equation}
    \frac{a}{b}
\end{equation}
```

- 在行间公式和行内公式中，分式的输出大小是有差异的。如果要强制行内模式的分式显示为行间模式的大小，可以使用 `\dfrac`, 反之可以使用 `\tfrac`。
- 在**行内写分式**，`xfrac` 宏包提供的 `\sfrac` 命令的效果更佳。
- 排版繁分式，你应该使用 `\cfrac` 命令。



### (3) 运算符

> **基础运算符**

```latex
\[ \pm\; \times \; \div\; \cdot\; \cap\; \cup\;\geq\; \leq\; \neq\; \approx \; \equiv \]
```

<img src="https://i.loli.net/2021/02/15/abm7v1dfKUYoVCS.png" alt="image-20210215184147370" style="zoom:80%;" />

> **大型运算符**

- 连加、连乘、极限、积分等大型运算符分别用 `\sum`, `\prod`, `\lim`, `\int` 生成
- 他们的上下标在行内公式中被压缩，以适应行高。我们可以用 `\limits` 和 `\nolimits` 来强制显式地指定是否压缩这些上下标。

```latex
\begin{equation}
    \sum_{i=1}^n i
    \prod_{i=1}^n 
    \sum\limits _{i=1}^n i
    \prod\limits _{i=1}^n 
    \lim_{x\to0}x^2
    \int_a^b x^2 dx 
    \lim\nolimits _{x\to0}x^2
    \int\nolimits_a^b x^2 dx
\end{equation}
```

<img src="https://i.loli.net/2021/02/15/SmL7zVyt9srbxPA.png" alt="image-20210215191333051" style="zoom: 67%;" />

> 多重积分

- 多重积分可以使用 `\iint`, `\iiint`, `\iiiint`, `\idotsint` 等命令输入

```latex
\begin{equation}
    \int_a^b x^2 dx
    \iint_a^b x^2 dx dy
    \iiint_a^b x^2 dx dy dz
\end{equation}
```

<img src="https://i.loli.net/2021/02/15/ISjZbz6vVeafMWE.png" alt="image-20210215192854443" style="zoom: 67%;" />



### (4) 界符

- 各种括号用 `()`, `[]`, `\{\}`, `\langle\rangle` 等命令表示；因为 LaTeX 中 `|` 和 `\|` 的应用过于随意，amsmath 宏包推荐用 `\lvert\rvert` 和 `\lVert\rVert` 取而代之。
- 调整这些定界符的大小，amsmath 宏包推荐使用 `\big`, `\Big`, `\bigg`, `\Bigg` 等一系列命令放在上述括号前面调整大小。

```latex
\begin{equation}
    () [] \{\} \langle\rangle \lvert\rvert \lVert\rVert\Big 
    \{ \Big\}
\end{equation}
```

<img src="https://i.loli.net/2021/02/15/uabWTKwmFVkSdE2.png" alt="image-20210215193812715" style="zoom:80%;" />

### (5) 省略号

省略号用 `\dots`, `\cdots`, `\vdots`, `\ddots` 等命令表示。`\dots` 和 `\cdots` 的纵向位置不同，前者一般用于有下标的序列。

```latex
\begin{equation}
    x_1,x_2,\dots ,x_n\quad 1,2,\cdots ,n\quad \vdots\quad \ddots   
\end{equation}
```

<img src="https://i.loli.net/2021/02/15/eWRUqtYjbLAaBKF.png" alt="image-20210215194347265" style="zoom:67%;" />

### (6) 矩阵

- `amsmath` 的 `pmatrix`, `bmatrix`, `Bmatrix`, `vmatrix`, `Vmatrix` 等**子环境**可以在矩阵两边加上各种分隔符。

```latex
\begin{equation}
    \begin{pmatrix} a&b\\c&d \end{pmatrix} \quad
    \begin{bmatrix} a&b\\c&d \end{bmatrix} \quad
    \begin{Bmatrix} a&b\\c&d \end{Bmatrix} \quad
    \begin{vmatrix} a&b\\c&d \end{vmatrix} \quad
    \begin{Vmatrix} a&b\\c&d \end{Vmatrix} \quad
\end{equation}
```

<img src="https://i.loli.net/2021/02/15/Sif7xbIhMuN8zUQ.png" alt="image-20210215195057106" style="zoom:67%;" />

- 使用 `smallmatrix` 环境，可以生成行内公式的小矩阵。

```latex
Marry has a little matrix $ ( \begin{smallmatrix} a&b\\c&d \end{smallmatrix} ) $.
```

<img src="https://i.loli.net/2021/02/15/s3lNpH948kgSTC2.png" alt="image-20210215195652668" style="zoom:80%;" />

### (7) 多行公式

有的公式特别长，我们需要手动为他们换行；有几个公式是一组，我们需要将他们放在一起；还有些类似分段函数，我们需要给它加上一个左边的花括号。

#### 长公式

- 不对齐：无须对齐的长公式可以使用 `multline` 环境，默认自带标号，如果不想用标号，则使用`multline*`环境

```latex
\begin{multline}
    z = x_1+x_2+x_3+x_4+{} \\
    x_5 + x_6 + x_7
\end{multline}
```

<img src="https://i.loli.net/2021/02/15/Q2SC8lINhZ5qOjt.png" alt="image-20210215202201533" style="zoom:80%;" />

- 对齐：需要对齐的公式，可以使用 `aligned` ***次环境***来实现，它必须包含在数学环境之内。

```latex
\begin{equation}
    \begin{aligned}
        z = &x_1+x_2+x_3+x_4+{} \\
            &x_5 + x_6 + x_7
    \end{aligned}
\end{equation}
```

<img src="https://i.loli.net/2021/02/15/9XUB7empROG6u12.png" alt="image-20210215202519568" style="zoom:67%;" />



#### 公式组

- 无需对齐的公式组可以使用 `gather` 环境 / `gather*` 环境 
- 需要对齐的公式组可以使用 `align` 环境 /  `align*` 环境 

```latex
\begin{gather}
    X = \alpha x_1 + \beta x_2 +\gamma x_3 \\
    Y = \mu  y_1 + \nu y_2
\end{gather}

\begin{align}
    X &= \alpha x_1 + \beta x_2 +\gamma x_3\\
    Y &= \mu  y_1 + \nu y_2   
\end{align}
```

<img src="https://i.loli.net/2021/02/15/CgFucPwd9SJNeX8.png" alt="image-20210215203448056" style="zoom:80%;" />

- 用花括号包络的公式组可以在equation环境中嵌套`aligned`，并且在公式内部加上`\left\{ \right`

```latex
\begin{equation}
	\left\{
	\begin{aligned}
		m & = x + y + z + 1 \\
		n & = 2x - y + 3z \\
		r & = 5x + z
	\end{aligned}
	\right.
\end{equation}
```

<img src="https://i.loli.net/2021/02/15/dNtB6Avkwo9sIKL.png" alt="image-20210215204616717" style="zoom:50%;" />

#### 分段函数

- 分段函数可以用`cases`**次环境**来实现，它必须包含在数学环境之内。

```latex
\[
    F(x) = 
    \begin{cases}
        -x,x\leq 0 \\
        x ,x>0    
    \end{cases}
\]
```

<img src="https://i.loli.net/2021/02/15/LfMp7sePEWuwG4i.png" alt="image-20210215203838955" style="zoom:80%;" />

## 插入图片和表格

### 图片

- `graphicx` 宏包提供的 `\includegraphics` 命令。比如你在你的 TeX 源文件同目录下，有名为 `a.jpg` 的图片，你可以用这样的方式将它插入到输出文档中：

```latex
\documentclass{article}
\usepackage{graphicx}
\begin{document}
    \includegraphics[width = .5\textwidth]{a.jpg}
\end{document}
```

- 一个比较全面的模板

```latex
\begin{figure}[htbp]	% 浮动
    \centering
    \includegraphics[width=1\linewidth]{a}
    \caption{\LaTeX 蜘蛛侠示意图}
    \label{fig:figure1latexintro}
\end{figure}
```

<img src="https://i.loli.net/2021/02/15/tdozFxr9ALe7wEn.png" alt="image-20210215220611397" style="zoom:67%;" />

- 子图模板

```latex
\begin{figure}[htbp]
	\centering
	\subfigure[子图\#1]
	{
		\label{fig:sub1}		
		\includegraphics[width=0.45\textwidth]{Figures/Subfigure_1.eps}
	}
	\subfigure[子图\#2]
	{
		\label{fig:sub2}		
		\includegraphics[width=0.45\textwidth]{Figures/Subfigure_2.eps}
	}
	\subfigure[子图\#3]
	{
		\label{fig:sub3}		
		\includegraphics[width=0.45\textwidth]{Figures/Subfigure_3.eps}
	}
	\subfigure[子图\#4]
	{
		\label{fig:sub4}		
		\includegraphics[width=0.45\textwidth]{Figures/Subfigure_4.eps}
	}
	\caption{这里是子图(subfigure)的示例。}
	\label{fig:subfigure}
\end{figure}
```



### 表格

- 一个在线表格网站：[https://www.tablesgenerator.com/](https://www.tablesgenerator.com/)

```latex
\begin{tabular}{|l|c|r|}
 \hline
操作系统& 发行版& 编辑器\\
 \hline
Windows & MikTeX & TexMakerX \\
 \hline
Unix/Linux & teTeX & Kile \\
 \hline
Mac OS & MacTeX & TeXShop \\
 \hline
通用& TeX Live & TeXworks \\
 \hline![image-20210215222331352](/home/qdl/.config/Typora/typora-user-images/image-20210215222331352.png)
 
\end{tabular}
```

<img src="https://i.loli.net/2021/02/16/MhtjDdkZyI6XzOU.png" alt="image-20210215222331352" style="zoom:80%;" />

### 浮动体

- 插图和表格通常需要占据大块空间，所以在文字处理软件中我们经常需要调整他们的位置。`figure` 和 `table` 环境可以自动完成这样的任务；这种自动调整位置的环境称作浮动体(float)。我们以 `figure` 为例。

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics{a.jpg}
    \caption{有图有真相}
    \label{fig:myphoto}
\end{figure}
```

`htbp` 选项用来指定插图的理想位置，这几个字母分别代表 here, top, bottom, float page，也就是就这里、页顶、页尾、浮动页（专门放浮动体的单独页面或分栏）。`\centering` 用来使插图居中；`\caption` 命令设置插图标题，LaTeX 会自动给浮动体的标题加上编号。注意 `\label` 应该放在标题命令之后。



## 版面设置

### 页边距

设置页边距，推荐使用 `geometry` 宏包。可以在[这里](http://texdoc.net/texmf-dist/doc/latex/geometry/geometry.pdf)查看它的说明文档。使用举例：将纸张的长度设置为 20cm、宽度设置为 15cm、左边距 1cm、右边距 2cm、上边距 3cm、下边距 4cm，可以在导言区加上这样几行：

```latex
\usepackage{geometry}
\geometry{papersize={20cm,15cm}}
\geometry{left=1cm,right=2cm,top=3cm,bottom=4cm}
```

### 页眉页脚

设置页眉页脚，推荐使用 `fancyhdr` 宏包。可以在[这里](http://texdoc.net/texmf-dist/doc/latex/fancyhdr/fancyhdr.pdf)查看它的说明文档。比如我希望，在页眉左边写上我的名字，中间写上今天的日期，右边写上我的电话；页脚的正中写上页码；页眉和正文之间有一道宽为 0.4pt 的横线分割，可以在导言区加上如下几行：

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\lhead{\author}
\chead{\date}
\rhead{152xxxxxxxx}
\lfoot{}
\cfoot{\thepage}
\rfoot{}
\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\headwidth}{\textwidth}
\renewcommand{\footrulewidth}{0pt}
```

### 首行缩进

CTeX 宏集已经处理好了首行缩进的问题（自然段前空两格汉字宽度）。因此，使用 CTeX 宏集进行中西文混合排版时，我们不需要关注首行缩进的问题。

> 如果你因为某些原因选择不适用 CTeX 宏集（不推荐）进行中文支持和版式设置，则你需要做额外的一些工作。
>
> - 调用 `indentfirst` 宏包。具体来说，中文习惯于每个自然段的段首都空出两个中文汉字的长度作为首行缩进，但西文行文习惯于不在逻辑节（`\section` 等）之后缩进。使用改宏包可使 LaTeX 在每个自然段都首行缩进。
> - 设置首行缩进长度 `\setlength{\parindent}{2\ccwd}`。其中 `\ccwd` 是 `xeCJK` 定义的宏，它表示当前字号中一个中文汉字的宽度。

### 行间距

我们可以通过 `setspace` 宏包提供的命令来调整行间距。比如在导言区添加如下内容，可以将行距设置为字号的 1.5 倍：

```latex
\usepackage{setspace}
\onehalfspacing
```

具体可以查看该宏包的[文档](http://texdoc.net/texmf-dist/doc/latex/setspace/README)。

> 注意:
>
> - 行距是字号的 1.5 倍；
> - 1.5 倍行距。
>
> 事实上，这不是设置 1.5 倍行距的正确方法，请参考[这篇博文](https://liam.page/2013/10/17/LaTeX-Linespace/)。另外，[RuixiZhang](https://github.com/RuixiZhang42) 开发了 [zhlineskip](https://github.com/CTeX-org/ctex-kit/tree/master/zhlineskip) 宏包，提供了对中西文混排更细致的行距控制能力。

### 段间距

我们可以通过修改长度 `\parskip` 的值来调整段间距。例如在导言区添加以下内容

```latex
\addtolength{\parskip}{.4em}
```

## 其他技巧

- 去除section首行缩进

```latex
\noindent
```

- 无序列表

```latex
\begin{itemize}
    \item 
    \item
\end{itemize}
```

- 有序列表

```latex
\begin{enumerate}
    \item 
    \item 
\end{enumerate}
```

- 插入图像

```latex
\begin{figure}[htbp]	            % 浮动
    \centering
    \includegraphics[width=0.8\linewidth]{Figure/create.png}
    \caption{name}
    \label{fig:figure1latexintro}
\end{figure}
```

- 插入子图

```latex
\begin{figure}[htbp]
	\centering
    \subfigure[name1]{
        \label{fig:sub1}		
		\includegraphics[width=0.48\textwidth]{Figure/create.png}
    }
    \subfigure[name2]
	{
		\label{fig:sub2}		
		\includegraphics[width=0.48\textwidth]{Figure/add.png}
	}
    \caption{Name}
    \label{fig:subfigure}
\end{figure}
```

- 插入代码

```latex
\begin{lstlisting}[language=c]
	code 
\end{lstlisting}
```

- 从外部引入代码

```
-----
```



## 网站汇总

- 入门教程：[https://liam.page/2014/09/08/latex-introduction/](https://liam.page/2014/09/08/latex-introduction/)

- 截屏识别：[https://mathpix.com/ ](https://mathpix.com/)
- 绘图识别：[http://detexify.kirelabs.org/classify.html ](http://detexify.kirelabs.org/classify.html)
- 在线LaTeX公式编辑器：[https://www.latexlive.com/](https://www.latexlive.com/)
- 一个在线表格网站：[https://www.tablesgenerator.com/](https://www.tablesgenerator.com/)
- 我的LaTeX仓库：[https://github.com/LinXiaoDe/LaTeX](https://github.com/LinXiaoDe/LaTeX)