# Markdown学习笔记

本文档是Markdown语言和GFM的学习笔记，主要参考文档为[CommonMark Spec](https://spec.commonmark.org/0.28/)和[GitHub Flavored Markdown Spec](https://github.github.com/gfm/).

## 1. 简介

Markdown是一种轻量级标记语言，它和HTML兼容，可以转换为HTML格式发布。和其他的轻量标记语言相比，MarkDown的撰写并不是最容易的，但是它的一些特性，比如说缩进，使得代码非常容易阅读。

## 2. 语法要素和结构

任意字符串都可以是有效的Markdown文档。

一个*字符*是一个Unicode代码点。规范本身并不指定编码（encoding），但是某个具体的解析器可能会限制编码的类型。
一个*行*由字符（不包括换行`U+000A`和回车`U+000D`)和行结束符组成。行结束符是一个换行符`U+000A`或者回车符`U+000D`或者回车符跟随一个换行符。如果一个行不包含任何字符，或者只包含空格`U+0020`或制表符`U+0009`，侧称作*空行*（blank line）。

行内的*制表符*不会展开为空格。但是，如果空格字符被用于定义块结构的时候，制表符会被替代为能够提供4个字符宽的制表位的空格。比如，行首已经有了一个空格，则制表符会被展开为3个空格。对于Github.com，当indent mode为Tabs时，Tabs不会被展开，否则会展开为空格。制表位宽度也是由indent size指定的。

我们可以认为文档是由一系列的块结构（blocks—structural elements）组成的。块结构内部可以包含其他的块，也可以是行内（inline）元素。块结构语法的优先级总是高于行内元素。

可以包含其他块的块结构类型，称作container blocks。否则，则是leaf blocks。

## 3. Leaf Blocks
### 3.1 Thematic breaks
Thematic break是一个由3个或更多 \-, \_ 或 \* 字符组成的行（字符必须相同），每个字符后面可以选择跟随任意多个空格，行首缩进不能超过3个空格。

注意，thematic break的语法优先级高于list item，但是低于setext heading。

### 3.2 ATX headings
ATX标题行起始为不超过6个的\#字符，行首也可以添加不超过3个的空格。起始的\#字符后的空格和行内容结尾处的空格会被忽略。ATX标题行也可以在行内容末尾添加任意个\#字符表示标题行的结束。注意，起始和末尾的\#字符，都需要和标题行内容用空格隔开。

ATX标题行不需要被空行隔开，它也能够打断段落。

### 3.3 Setext headings
Setext标题行由一个正常的段落行和跟随其后的一个由一系列 \- 或 \= 符号组成的 setext heading underline 构成。行首的缩进都不能超过三个空格字符。Underline 行末尾可以跟随任意空格，但是内部不能含有空格。如果underline只含有一个 \- 或 \= 符号，而且能够被解析为list items，那么会优先解析为list items。

如果 \= 符号被用于 Underline 行，那么标题为一级标题，否则为二级标题。标题的内容为 underline 行前面的行内容。

Setext标题行不需要被空行隔开，但它不能够打断段落。

### 3.4 Indented code blocks
缩进代码块是由空行隔开的 indented chunks。Indented chunks 指的是行首缩进4个及以上空格字符的一系列非空白行。

由于缩进代码块是不能够打断段落的，所以需要空白行和前面的段落隔开, 不过，对于后面的段落，空白行是不需要的。





## GFM
You can use Markdown most places around GitHub:

Gists
Comments in Issues and Pull Requests
Files with the .md or .markdown extension
For more information, see “Writing on GitHub” in the GitHub Help.



## 参考资料
1.Markdown wiki.
https://github.github.com/gfm/#example-116
https://zh.wikipedia.org/wiki/Markdown#Markdown%E8%88%87html%E8%BD%89%E6%8F%9B%E4%B9%8B%E4%BE%8B%E5%AD%90
https://www.cnblogs.com/liugang-vip/p/6337580.html
https://github.com/younghz/Markdown
