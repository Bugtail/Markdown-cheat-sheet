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

由于缩进代码块是不能够打断段落的，所以需要空白行和前面的段落隔开。不过，对于后面的段落，空白行是不需要的。

### 3.5 Fenced code blocks
代码围栏由至少三个连续的撇号字符（\`）或波浪字符（\~）组成（不能混用）。围栏式代码块是由代码围栏围起来的代码块，省去了代码块每行都需要缩进的麻烦。被围起来的所有行都会被当作字面意义的文本处理，而不会当作行内元素解析。如果结束处的围栏缺失，那么剩下的所有内容都会当作代码处理，直至文档结束。

需要注意的是，代码围栏本身的缩进不能超过3个空格字符。代码块结束处的围栏字符要和开始处使用的一样，并且个数不能少于开始处的围栏，不过缩进空格数可以不一样。另外，开始处的代码围栏如果缩进了N个字符，那么代码行如果有缩进的话，会被移除最多N个字符的缩进，或者所有缩进。

另外，开始出的围栏后面可以跟随一个字符串作为Info String（开始和末尾的空格会被去掉）。Info String不能含有任何撇号字符，它的第一个word通常用于指定代码的语言，将代码渲染为code tag相应的类属性。

围栏式代码块不需要被空行隔开，它也能够打断段落。

### 3.6 HTML块
总共有7类HTML标签可以直接在Markdown文档内直接使用。

### 3.7 链接引用定义
链接引用定义（link reference definition）由一个缩进不超过3个空格的链接标签，一个冒号（\:），可选的空格（可以包含换行），一个目标，可选的空格（可以包含换行）和可选的链接标题（必须由空格和目标隔开）组成。链接引用可以定义在链接使用之前或者之后。

链接标签必须包含在方括号([]）内，标签不能为空，最多999个字符，不能含有未转义的方括号。

链接引用定义不能够打断段落，但是它可以直接跟在其他的块元素后面，比如标题和thematic breaks。而且后面不需要跟空行。多个链接引用定义可以连续定义，之间不需要空行隔开。

链接引用定义也可以定义在 block containers 里面，比如 lists 和 block quotations，但是他们能对整个文档起作用，而不是仅仅作用于 container 内部。

### 3.8 段落
A sequence of non-blank lines that cannot be interpreted as other kinds of blocks forms a paragraph. The contents of the paragraph are the result of parsing the paragraph’s raw content as inlines. The paragraph’s raw content is formed by concatenating the lines and removing initial and final whitespace.

### 3.9 空行
Blank lines between block-level elements are ignored, except for the role they play in determining whether a list is tight or loose.

Blank lines at the beginning and end of the document are also ignored.

## 4. Container blocks
A container block is a block that has other blocks as its contents. There are two basic kinds of container blocks: block quotes and list items. Lists are meta-containers for list items.
### 4.1 块引用
块引用的标记有0-3个缩进空格和一个 ">" 字符组成，后面也可以再跟一个空格。

### 4.2 列表元素
列表标记有两种：1）bullet list marker：-, +, 或 * 字符；2）ordered list marker： 由1-9位数字和一个 . 或 ) 字符组成。

在定义列表元素时，标记后需要有1-4个空格，元素内的内容的缩进应该不小于标记的缩进+标记的本身的宽度+跟随的空格。如果两行之间没有用大于一个空行隔开，则认为后续还是属于列表元素内容。

### 4.3 列表
A list is a sequence of one or more list items of the same type. The list items may be separated by any number of blank lines.

A list is an ordered list if its constituent list items begin with ordered list markers, and a bullet list if its constituent list items begin with bullet list markers.

The start number of an ordered list is determined by the list number of its initial list item. The numbers of subsequent list items are disregarded.

## 5 Inlines
### 5.1 转义字符

    \!  \"  \#  \$  \%  \&  \'  \(  \)  \*  \+  \,  \-  \.  \/  \:  
\!  \"  \#  \$  \%  \&  \'  \(  \)  \*  \+  \,  \-  \.  \/  \:  

    \;  \<  \=  \>  \?  \@  \[  \\  \]  \^  \_  \`  \{  \|  \}  \~
\;  \<  \=  \>  \?  \@  \[  \\  \]  \^  \_  \`  \{  \|  \}  \~

### 5.2 字符实体引用
在SGML、 HTML与XML文档，如果某些Unicode字符在文档的当前编码方式(如ISO-8859-1)中不能直接表示，那么可以通过字符值引用或者字符实体引用两种转义序列来表示这些不能直接编码的字符。 

在Markdown文档中，字符实体引用（Entity references）由\"\&\"，任意有效的HTML5实体名称，和\"\;\"组成。而字符值引用（numeric character references）使用的是字符的代码点（code points）。如果采用的是10进制，字符值引用由\"\&\#\"，1-8为阿拉伯数字，和\"\;\"组成。如果采用的是16进制，则由\"\&\#\"，"X"或"x"，1-8位16进制数字，和\"\;\"组成。

有效的实体引用和相应的代码点可以参考文档https://html.spec.whatwg.org/multipage/entities.json

### 5.3 代码Spans
span元素是用來对行内元素进行分组，以便通过样式对它们进行格式化。它本身沒有任何意思。

Code Span由1个或多个撇号字符\(\`\)开始，由同样个数的撇号字符\(\`\)结束。撇号字符\(\`\)中间的字符就是code span的内容。内容开始和结尾处的空格和行结束符会被移除，多个连续空格会被合并为一个。

### 5.4 强调和重点
由一个星号\(\*\)或下划线\(\_\)包裹的文本会被强调（emphasis)，被两个星号\(\*\)或下划线\(\_\)包裹的文本会被重点强调（strong emphasis）。

### 5.5 链接
链接（links）包含链接文本（link text），链接目的地（link destination, the URI that is the link destination）和可选的链接标题（link title). 在Morkdonw里有两类链接：1）行内链接（inline links），目的地和标题都是紧挨着链接文本定义的；2）引用链接（reference links），目的地和标题定义于文档其他地方。

**链接文本**由方括号括起来\(\[\]\)，可以为空。**链接目的地**如果非空的话，可以不需要用尖括号括起来\<\>。**链接标题**需要用单/双引号或者圆括号括起来。

行内链接由一个链接文本，紧接一个左括号\(，一个可选的空格，一个可选的链接目的地，一个可选的链接标题（和目的地用空格隔开），一个可选的空格，和一个右括号\)组成。网站地址需要加上https\:\/\/等，否者会当作文档内部地址处理。

引用链接有三种类型：

- full reference link，由链接文本紧接一个链接标签（link label）组成，链接标签要和在文档其他地方定义的链接引用（link reference）匹配。链接标签由方括号包裹。
~~~
    [foo][bar]

    [bar]: /url "title"
~~~
- 

A full reference link consists of a link text immediately followed by a link label that matches a link reference definition elsewhere in the document.

A link label begins with a left bracket ([) and ends with the first right bracket (]) that is not backslash-escaped. Between these brackets there must be at least one non-whitespace character. Unescaped square bracket characters are not allowed inside the opening and closing square brackets of link labels. A link label can have at most 999 characters inside the square brackets.

One label matches another just in case their normalized forms are equal. To normalize a label, strip off the opening and closing brackets, perform the Unicode case fold, strip leading and trailing whitespace and collapse consecutive internal whitespace to a single space. If there are multiple matching reference link definitions, the one that comes first in the document is used. (It is desirable in such cases to emit a warning.)

The contents of the first link label are parsed as inlines, which are used as the link’s text. The link’s URI and title are provided by the matching link reference definition.



[aaa](<htps://www.baidu.com> "why")

### 5.6

## GFM
GibHub Flavored Markdown 除了支持 CommonMark的各种功能以外，还具备一些自己定义的功能：

- 可以定义 tables
- 可以使用Task list items, 在正常的list marker后面跟一个空格和一个 [ ] 或 [x]符号来显示一个check box
- 可以使用两个波浪符号\(\~\)包裹文本来定义删除线





## 参考资料
1.Markdown wiki.
https://github.github.com/gfm/#example-116
https://zh.wikipedia.org/wiki/Markdown#Markdown%E8%88%87html%E8%BD%89%E6%8F%9B%E4%B9%8B%E4%BE%8B%E5%AD%90
https://www.cnblogs.com/liugang-vip/p/6337580.html
https://github.com/younghz/Markdown
