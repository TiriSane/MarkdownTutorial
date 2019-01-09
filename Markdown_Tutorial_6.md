#### Markdown学习笔记（6）- 容器文本块

***
##### 本章目标

在[上一篇文章](https://github.com/TiriSane/MarkdownTutorial/blob/master/Markdown_Tutorial_5.md)里，我们已经全面地了解了Markdown非容器文本块的标记。这篇文章我们将讨论Markdown的容器文本块，即引用文本块和列表的内容。在下一章里，我们将讨论一些内联结构的写法。

***

##### 1. 引用文本块

**引用文本块**是一种常见的结构。要引用一段文本，新起一行，在行首使用`>`符号，加上0或1个空格分割`>`和将要引用的文本内容。如果这行引用没有任何内容，`>`后可以什么都不加。

引用文本块有以下3个基本规则：

1. 如果几行文本（Ls）构成一个块（Bs），那么在Ls中的第一行前面加上`>`符号的结果是对Bs整体内容的块引用。也就是说，对于每一个块结构，在它最开始的第一行前加上`> `就可以使整个块结构文本成为引用内容。
2. 可以删除一行前的`>`符号，但使这行内容仍是引用文本块：只要它前面和它处于相同块的一行也是块引用文本就可以了。
3. 如果文档内一行里同时存在多个作为引用文本块的`>`符号，那么它们将被视为多重引用。

例子：
```
> Foo
> bar
baz
```

效果：
> Foo
> bar
baz

我们可以看出，正如第2条规则描述的一样，baz也成为了引用文本块的一部分。
但如果baz换成`- - - -`（分隔线），那么`- - - -`就不会被解析为引用文本，因为`- - - -`构成了一个新的文本块。我们建议你在所有要引用的文本行之前都加上`>`来规避和CommonMark标准不同的实现。

***

##### 2. 列表

###### 基本规则

如果几行文本（Ls）构成一系列的块（Bs），并且当这些行都以一个非空白字符开始，并且没有被超过一行的空行分离开，设列表标记为M，W为M的宽度，N为M后面1~4个空格的宽度；则这样做的效果就是Ls第一行前置的M标记、空格还有Ls后的缩进为W+N的缩进行会随着Bs这一块的整块文本构成了一整个列表项。

列表项的类型（无序列表项或者顺序列表项）是列表标记M的样式所决定的。注意，类似分隔线`- -- -`的文本是无法成为列表项的。

列表项之间可以有多个空行，这仍然会使空行前后的列表项被视为构成同一个列表的几个部分。列表项标记和列表项内容文本之间至少要有一个空格进行分隔。

###### 特殊的规则

当列表中的第一个列表项中断了一个段落（即这个列表项和其上的文本是一段没有其他块结构阻隔的连续文本）时，那么一个列表项的内容不能为空；并且如果列表项是有序的，起始编号必须为1，否则将不被视为一个列表项。

（这一条规则我个人感觉很奇怪，而且连CommonMark.NET库都没有尊重这个规则进行实现，只有commonmark.js这个库严格遵守了这条。可见标准文档和实现还是有所差距的，为了保持Markdown文档的兼容性，我建议大家用新的一个段落进行列表的书写）。

###### 作为参考的ComomMark原文

> The following rules define list items:
> 
> 1. **Basic case**. If a sequence of lines Ls constitute a sequence of blocks Bs starting with a non-whitespace character and not separated from each other by more than one blank line, and M is a list marker of width W followed by 1 ≤ N ≤ 4 spaces, then the result of prepending M and the following spaces to the first line of Ls, and indenting subsequent lines of Ls by W + N spaces, is a list item with Bs as its contents. The type of the list item (bullet or ordered) is determined by the type of its list marker. If the list item is ordered, then it is also assigned a start number, based on the ordered list marker.
>
>     Exceptions:
>
>     1. When the first list item in a list interrupts a paragraph—that is, when it starts on a line that would otherwise count as paragraph continuation text—then (a) the lines Ls must not begin with a blank line, and (b) if the list item is ordered, the start number must be 1.
>     2. If any line is a thematic break then that line is not a list item.

###### 由多行文本组成的单个列表项

一个列表项可能由多行文本组成，这时除第一行外，其他行的文本如果想和第一行文本一起被视为一个整体组成列表项，那么这些其它行文本需要缩进N个格，N为列表项标识与其后空格所占的总宽度。

例子：
```
- one

  two
```

效果：
- one

  two
  
如果two前面的空格少于2个，则two不会被视为列表项的文本。缩进代码块应该在N格缩进的基础上再缩进4格：
```
  1. A paragraph
with two lines.

          indented code

      > A block quote.
```

效果：
  1. A paragraph
with two lines.

          indented code

      > A block quote.

可以看出，列表项中的空白行不会中断一整个段落。

###### 有序列表项

有序列表项的数字不得为负数，这个数字最多9位（太多的话一些浏览器上会溢出）。有趣的是，起始的数字标号可以以数字0加上其他的数字开始。

例子：
```
003. a
```

效果：
003. a

###### 子列表

在Markdown中你可以构成子列表，就像下面这样：

```
- foo
  - bar
    - baz
      - boo
```

效果：
- foo
  - bar
    - baz
      - boo
      
可以看出，构造一个子列表时，子列表项文本前的字符总长度需要是其父列表项文本长度的一倍或更多（通过空格）。这个例子里最开始父列表列表项文本前的字符长度是两个字符。所以其子节点列表项前字符长度就为4。

###### John Gruber关于列表项的Markdown规范

1. 列表项标记通常从一行的最左侧开始，前面可以有0到3个空格，列表标记后面必须有1至多个空格或tab分隔标识和列表项文本内容。
2. 如果你想让列表项看起来好看一点，你可以对列表项进行悬挂缩进。但如果你不想这样也可以不做。
3. 列表项可以包含多个段落，对于后续的每一个段落从段首内容，你都需要将它们缩进4个空格或者1个tab。
4. 你可能会把列表项段落中的每行都进行缩进，这很好，但Markdown允许你懒一些（暗示可以不缩进每行文本）。
5. 如果想要在列表项文本里加入块引用，块引用的`>`符号需要被缩进。
6. 要将缩进式代码块放在列表项中，代码块需要缩进两次，共计8个空格，或使用两个制表符。

如果你发现你的Markdown编辑器不支持CommonMark的规范，你可以试试Markdown作者提出的规范。

##### Have A Break

至此，我们已经把非容器文本块都介绍完毕了。在接下来的一篇文章中，我们会了解到容器文本块中Markdown符号（主要是用于引用和列表的符号）的那些更富有细节的用法。稍作休息，我们在[下篇文章](https://github.com/TiriSane/MarkdownTutorial/blob/master/Markdown_Tutorial_7.md)再见。
