# Markdown学习笔记

本文档是Markdown语言和GFM的学习笔记，主要参考文档为[CommonMark Spec](https://spec.commonmark.org/0.28/)和[GitHub Flavored Markdown Spec](https://github.github.com/gfm/).

## 简介

Markdown是一种轻量级标记语言，它和HTML兼容，可以转换为HTML格式发布。和其他的轻量标记语言相比，MarkDown的撰写并不是最容易的，但是它的一些特性，比如说缩进，使得代码非常容易阅读。

## 语法要素和结构

任意字符串都可以是有效的Markdown文档。

一个*字符*是一个Unicode代码点。规范本身并不指定编码（encoding），但是某个具体的解析器可能会限制编码的类型。
一个*行*由字符（不包括换行`U+000A`和回车`U+000D`)和行结束符组成。行结束符是一个换行符`U+000A`或者回车符`U+000D`或者回车符跟随一个换行符。如果一个行不包含任何字符，或者只包含空格`U+0020`或制表符`U+0009`，侧称作*空行*（blank line）。

行内的制表符不会展开为空格。但是，如果空格字符
Tabs in lines are not expanded to spaces. However, in contexts where whitespace helps to define block structure, tabs behave as if they were replaced by spaces with a tab stop of 4 characters.

Thus, for example, a tab can be used instead of four spaces in an indented code block. (Note, however, that internal tabs are passed through as literal tabs, not expanded to spaces.)


  test


### 优先级
块结构（block structure），比如段落，块引用，列表，

Indicators of block structure always take precedence over indicators of inline structure. So, for example, the following is a list with two items, not a list with one item containing a code span:

structural elements like paragraphs, block quotations, lists, headings, rules, and code blocks. Some blocks (like block quotes and list items) contain other blocks; others (like headings and paragraphs) contain inline content—text, links, emphasized text, images, code spans, and so on.


### Tab字符


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
