---
title: 简介如何用LaTeX进行学术写作与排版
date: 2019-07-03 15:10:26
draft: false
toc: true
summary: " "
---

## 简单介绍如何使用LaTeX作为学术编辑软件

### 什么是LaTeX

LaTeX（/ˈleɪ.tɛk/）是Leslie Lamport基于TeX开发的排版系统，而TeX则是由Prof. Donald Knuth发明的排版软件。他发明TeX排版软件最初是用作解决数学公式排版的问题，但在不断推广下，现在已经成为数学、物理、计算机领域几乎最重要的排版、编辑系统。

TeX最大的不同是，它相当于一门宏语言或标记语言。

LaTeX是TeX家族中一种编译引擎。除了LaTeX，还有XeLaTeX、pdfTeX、LuaTeX等等。

### 为什么选择LaTeX

为什么要选择LaTeX而不是word？这是许多生命科学领域的科研工作者第一个要问的。事实上，我们大多数人是没有接触过除了word以外的写作排版软件，但在经历过word格式的折磨(如删除页眉的横线、版本控制)后，才发现别的选择有多好。

生科类的工作者对于写作软件一般关注几个问题：文献管理、投稿格式(包括文献格式)、部分公式，而latex基本就是为了格式和内容分离而诞生的。

| 特性           | LaTeX                                                 | MS Word               |
|----------------|-------------------------------------------------------|-----------------------|
| 收费           | 免费                                                  | ￥400/y               |
| 平台支持       | Linux/MacOS/Windows                                   | 基本只有windows才能用 |
| 数学公式       | 非常好                                                | 只能应付简单的公式    |
| 学术出版商支持 | IEEE/Spring/Weily/Elseiver/Oxford等几乎所有学术出版商 | 同左                  |

### 如何安装LaTeX

完整的TeX需要最基本的TeX引擎、格式支持、各种辅助宏包、一些转换程序、GUI、编辑器、文档查看器等等。这些组成起来就是TeX发行版。就像CentOS、ArchLinux这些和Linux的关系一样。

三大操作系统下支持的发行版会略有不同。一般而言，Windows、Linux下可选择使用[TeX Live](https://www.tug.org/texlive/)，MacOS 可以选择使用[Mactex](http://www.tug.org/mactex/mactex-download.html).

这些发行版安装文件会比较大（几个G），可以选择在清华大学镜像中下载。

不过也有更好的选择，也是越来越流行的选择，就是使用[Overleaf](https://cn.overleaf.com)在线编辑，免安装，免配置。具体如下编辑器介绍。

### 如何选择编辑器

因为.tex源文件是纯文本，所以一款tex编辑器很影响写作体验。好的会让你感觉像某个巧克力品牌一样丝滑流畅，越写越上瘾；差的则会分散你的注意力，造成负作用。私以为，一个好的编辑器应该具有以下几个特性：

- 高亮文本

- 实时预览

- 自动补全

- 好看的主题配色和字体

不过这些还是要自己切身体会比较好，以下呢，就是一些我用过的编辑器与我的截图，大家仅作参考：

- TeXStudio (跨平台的IDE，推荐)
{{< figure library="true" src="texstudio_snap.jpg" title="textstudio" lightbox="true" >}}

- Visual Studio Code (微软推出的轻量级编辑器，可以下载LaTeX Workbench扩展，推荐)
{{< figure library="true" src="vscode_snap.png" title="vscode" lightbox="true" >}}

- [Overleaf](/https://www.overleaf.com) (主打学术编辑的online editor，无需安装配置，简单易用，界面好看，非常推荐)
{{< figure library="true" src="overleaf_snap.png" title="overleaf" lightbox="true" >}}

### 基本的命令介绍

安装好LaTeX看起来像在写代码的原因就是因为它丰富的命令与宏包。这里只做简单介绍，更多还是要靠自己多用多摸索。

一个最基本简单的latex文档框架会有以下命令:

```latex
\documentclass[UTF8]{article} %文档类型，学术写作基本是article, []内是参数选项表示用utf8编码
\begin{document} %开始文档
hello world      %正文区
\end{document}   %结束文档
```

当然还会有其他信息

```latex
\documentclass{article}
\title{my first tex file}
\author{name}  %作者名称
\date{\today}  %这里就可以看出latex的黑魔法了，直接用\today表示日期

\begin{document}
\maketitle     %这里会根据上述的title,author,date信息自动生成一个标题
\section{section1}  %第一节
\section{section2}  %第二节
\subsection{subsection1} %第二节中的第一部分，更多层级标题可以通过\subsubsubsection这样添加
\end{document}
```

#### 添加数学公式

```latex
$....$   %所有行内公式都可以在两个$之间插入
\begin{equation} %行间公式，可以使用equation环境
d = \frac{a}{b} + \sqrt{c}  %使用\frac{}{}表示分式，使用\sqrt{}表示根式
\end{equation}
```

效果如下
{{< figure library="true" src="equation_snap.png" title="" lightbox="true" >}}

更多的数学公式符号可以参考[lshort一份很短的latex入门文档](https://liam.page/2014/09/08/latex-introduction/)

#### 插入表格

`tabular` 环境提供了最简单的表格功能。它用 `\hline` 命令表示横线，在列格式中用 `|` 表示竖线；用 `&` 来分列，用 `\\` 来换行；每列可以采用居左、居中、居右等横向对齐方式，分别用 `l`、`c`、`r` 来表示。

```latex
\begin{tabular}{|l|c|r|}
\hline
species& biomass& abudance\\
\hline
a& 100& 10\\
\hline
b& 10&  10\\
\hline
\end{tabular}
```

这是它的效果

{{< figure library="true" src="tabular_snap.png" title="" lightbox="true" >}}

#### 插入图片

```latex
\documentclass{article}
\usepackage{graphicx}
\begin{document}
\includegraphics{fig1.eps} %这里a.eps在同目录下。这里推荐eps是因为它是矢量图，可以保证图像质量
\end{document}

%对于想控制图像大小的可以添加参数
%\includegraphics[width=5cm]{Fig1}
```

#### 中文排版（其实没什么必要，国内期刊应该基本不接收这种格式，他们也看不懂）

```latex
\documentclass[UTF8]{ctexart}
%其他相同，编译使用xelatex即可
```

### 学术写作你最关心的那些点

/待定

#### 多位作者

/待定

#### 如何插入文献

Word里有Endnote那样的软件配合插入文献。latex当然也有，那就是BibTeX。BibTex生效过程有4大步骤，如下：

- latex编译.tex文件，生成.aux文件（auxiliary之意）, 这个文件将告诉bibtex有哪些引用信息
- BibTeX编译.bib文件，根据.aux文件检测.bib中的相关文献
- LaTeX重编译.tex文件，把参考文献编入文档
- LaTeX再次编译.tex文件，防止交叉引用出错

当然使用的时候不需要知道这么多，只要知道三个命令即可

``` latex
\cite{ref} %在文中引用文献
\bibliographystyle{stylefile}  %同目录下的文献格式文件，由期刊提供
\bibliography{sample} %你的文献库
```

如下图所示，我在Google scholar export我的文章为bib格式并放在同目录下，然后在.tex中的#74行\cite{xxx}引用了它，右边就自动编译出了reference。#85-86行是模板中已经预设好的命令，只需要在\bibliography{}中填上test表示test.bib为文献库既可。
{{< figure library="true" src="bibtex_snap.png" title="" lightbox="true" >}}

事实上文献库不可能只有一个文献，所有可以用endnote这样的文献管理软件导出bib文件(应该没有不能导出的软件，否则它就是失败的)。要注意的是，这样的bib文件在投稿时**一定要一起上传**，否则期刊是不知道你引用了什么文献的。

不过说到文献管理软件的话，这里更推荐Zotero搭配LaTeX，为什么呢，因为它也是**开源免费**的。

### 投稿格式/模板使用

其实如上面所言，投稿时一般的期刊都会提供模板(具体见author guidlines)，例如Journal of Animal Ecology，里面会有所有要求的格式（如上编辑器截图）。作者只需要按照指示，在上面填充自己的内容即可。

但是也有一些不用模板的，例如Ecology Letters（如下）。不过这种反而是种优势？至少你不用改格式了，peer-review时提供pdf，终稿时提供source file、图片还有bst文件就可以了。

Ecology Letters does not have a standard LaTex style file. Manuscripts submitted using LaTeX should be accompanied by a PDF version of the paper. Upon final acceptance for publication, authors will be requested to send their LaTeX source files accompanied by all figures in EPS or TIFF format and also any non-standard LaTeX style files used in the manuscript preparation.
