#### Markdown学习笔记（5）- 非容器文本块（3）

***
##### 本章目标

在[上一篇文章](https://github.com/TiriSane/MarkdownTutorial/blob/master/Markdown_Tutorial_4.md)里，我们已经了解了一些属于Markdown非容器文本块的标记。这篇文章将继续讨论Markdown的非容器文本块。我们把非容器文本块中Markdown语法分成3部分食用，本篇文章将是有关非容器文本块的最后一部分。下一篇文章我们仍然会讨论容器文本块的内容，即引用文本块和列表。

***

##### 1. 参考式链接定义

在[第一篇文章](https://github.com/TiriSane/MarkdownTutorial/blob/master/Markdown_Tutorial_1.md)里我们提到过，Markdown中插入链接有两种方式，一种是内联式（inline links），一种是参考式（reference links）。

下面是一个参考式链接的例子：

`[github首页][R]`

`[R]:https://github.com "这个链接是github首页"`

效果：
[github首页][R]

[R]:https://github.com "这个链接是github首页"

其中，`[R]`开头的那行的文本内容就是**参考式链接定义**（Link reference definitions）。让我们一起看看参考式链接定义的一些具体的格式要求。

###### 1.1 格式说明

首先，参考式链接定义可以用行首0~3个空格作为缩进。之后，需要一个`[链接标签内容]`格式的链接标签来指定链接 标签的内容，之后紧跟一个冒号，冒号后可以有零至多个空白（包括换行符）。再之后需要一个连接目的地文本。再之后需要零至多个空白（包括换行符），和一个可选的由双引号包括起来的链接标题。

如果有链接标题，链接标题和链接目标之间至少要有一个空白。如果有链接标题，本行内链接标题后不得出现非空白文本；如果没有链接标题，本行内链接目标后不得出现非空白文本。否则这段文本将不被视为是一个参考式链接定义。

参考式链接定义作为文本（而非其他的结构时）可以存在于文档的任何地方，它不会显示出来，但会给链接或图像链接提供一个标记。

###### 1.2 链接标签

链接标签不分大小写，因此`[R]`和`[r]`是同样的链接标签。如果一份Markdown文档里有多个链接标签，Markdown将为引用链接标签的链接匹配第一个出现的标签。

例子：
```
[github首页][R]

[r]:https://github.com

[R]:https://buhtig.com
```

效果：
[github首页][R]

[r]:https://github.com

[R]:https://buhtig.com

可以看出，这个链接匹配到了github.com。

###### 1.3 链接标题

链接标题可以包括转义字符、换行符或回车符，但是不能包含空行，链接标题下面的空行文本将会被视为段落的中断。

###### 1.4 链接引用定义和块的关系

链接引用定义并不会中断一个块或者一个段落，它可以紧跟在一个块结构后面（而不会显示出来）。

比如：
```
###### [foo]
[foo]: www.zhihu.com
```

效果：
###### [foo]
[foo]: www.zhihu.com

这个例子我们可以看出，这个链接引用定义是生效的，而且从块结构的角度上看，它和而标题内容同属于一个块。这也导致一个链接引用定义前后不需要空行，而且可以在任何非代码块或Html文本的Markdown容器结构中被定义。而它会在整个文档范围都生效。

##### 2. Html块

Markdown支持插入Html文本，插入的Html文本将会被作为Html内容解析出各种Html样式。虽然Markdown和Html是有渊源的，但一些学习Markdown用户只是想用它做样式不那么复杂的笔记。我们应该认为，会写会读Html文本并非是学习并使用Markdown的条件。如果你不了解Html的语法，可以跳过这一部分。

另外一个很重要的就是，关于Markdown中应该怎样插入Html，Html又该被怎样解析，这并没有一个事实上的统一标准。

如果你是原教旨主义者，你需要意识到John Gruber关于Html块描述的这3点：
1. Html块应该前加空行与文本分隔开。
2. 块级HTML元素，例如：`<div>，<table>，<pre>，<p>`等标签，必须用前后空行和周围内容分离。
3. 开始标签和相对匹配的结束标签不应用制表符或空格缩进。
但是大部分实现并没有完全遵守这一标准（包括John Gruber自己的Markdown.pl）。尽管CommonMark给出了一些描述，但是Github等社区并没有完全遵守CommonMark中所描述的，Html块的规则（比如一些不完整的Html块是否能被解析）。

我认为，对于这种一团糟的情况，尽管把你写的或者拷贝来的html代码贴上去就好了，不用把每个社区支持的关于Html块的Markdown语法都看一遍，那样是繁琐而且没有意义的。

你只需要牢记以下4点，就可以抛离各种奇怪的版本不一的规则，使用Markdown了：
1. 保证这个Html文本是完整的，可以被浏览器正常解析，并显示成你想要的那个样子。
2. 把Html块前后都加上空行。如果一个Html标签的解析不正确，你可以试试让它独占一行，并且前后加上空行。
3. 如果一些文本显示的不正常，或者没有显示出来，你只需要用`<p>`标签将它前后包裹起来。
4. 去掉一行里多余的、无意义的空格。

如果你想了解CommonMark具体规定的，Html块的格式，你可以参考它们的[官方文档](http://spec.commonmark.org/0.28/)。

##### Have A Break

至此，我们已经把非容器文本块都介绍完毕了。在[接下来的一篇文章](https://github.com/TiriSane/MarkdownTutorial/blob/master/Markdown_Tutorial_6.md)中，我们会了解到容器文本块中Markdown符号（主要是用于引用和列表的符号）的那些更富有细节的用法。稍作休息，我们在[下篇文章](https://github.com/TiriSane/MarkdownTutorial/blob/master/Markdown_Tutorial_6.md)再见。
