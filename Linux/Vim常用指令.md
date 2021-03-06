设置ctags

> :set 路径/tags



## 4.1 基本移动

以下移动都是在normal模式下。

I是定位到行首，A是定位到行末。

- h或退格: 左移一个字符；
- l或空格: 右移一个字符；
- j: 下移一行；
- k: 上移一行；
- gj: 移动到一段内的下一行；
- gk: 移动到一段内的上一行；
- +或Enter: 把光标移至下一行第一个非空白字符。
- -: 把光标移至上一行第一个非空白字符。
- w: 前移一个单词，光标停在下一个单词开头；
- W: 移动下一个单词开头，但忽略一些标点；
- e: 前移一个单词，光标停在下一个单词末尾；
- E: 移动到下一个单词末尾，如果词尾有标点，则移动到标点；
- b: 后移一个单词，光标停在上一个单词开头；
- B: 移动到上一个单词开头，忽略一些标点；
- ge: 后移一个单词，光标停在上一个单词末尾；
- gE: 同 ge ，不过‘单词’包含单词相邻的标点。
- (: 前移1句。
- ): 后移1句。
- {: 前移1段。
- }: 后移1段。
- fc: 把光标移到同一行的下一个c字符处
- Fc: 把光标移到同一行的上一个c字符处
- tc: 把光标移到同一行的下一个c字符前
- Tc: 把光标移到同一行的上一个c字符后
- ;: 配合f & t使用，重复一次
- ,: 配合f & t使用，反向重复一次

上面的操作都可以配合n使用，比如在正常模式(下面会讲到)下输入3h， 则光标向左移动3个字符。

- 0: 移动到行首。
- g0: 移到光标所在屏幕行行首。
- ^: 移动到本行第一个非空白字符。
- g^: 同 ^ ，但是移动到当前屏幕行第一个非空字符处。
- : 移动光标所在屏幕行行尾。
- n|: 把光标移到递n列上。
- nG: 到文件第n行。
- :n<cr> 移动到第n行。
- :$<cr> 移动到最后一行。
- H: 把光标移到屏幕最顶端一行。
- M: 把光标移到屏幕中间一行。
- L: 把光标移到屏幕最底端一行。
- gg: 到文件头部。
- G: 到文件尾部。

## [4.2 翻屏](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id65)

- ctrl+f: 下翻一屏。
- ctrl+b: 上翻一屏。
- ctrl+d: 下翻半屏。
- ctrl+u: 上翻半屏。
- ctrl+e: 向下滚动一行。
- ctrl+y: 向上滚动一行。
- n%: 到文件n%的位置。
- zz: 将当前行移动到屏幕中央。
- zt: 将当前行移动到屏幕顶端。
- zb: 将当前行移动到屏幕底端。

## [4.3 标记](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id66)

使用标记可以快速移动。到达标记后，可以用Ctrl+o返回原来的位置。 Ctrl+o和Ctrl+i 很像浏览器上的 后退 和 前进 。

- m{a-z}: 标记光标所在位置，局部标记，只用于当前文件。
- m{A-Z}: 标记光标所在位置，全局标记。标记之后，退出Vim， 重新启动，标记仍然有效。
- `{a-z}: 移动到标记位置。
- ‘{a-z}: 移动到标记行的行首。
- `{0-9}：回到上[2-10]次关闭vim时最后离开的位置。
- “: 移动到上次编辑的位置。”也可以，不过“精确到列，而”精确到行 。如果想跳转到更老的位置，可以按C-o，跳转到更新的位置用C-i。
- `”: 移动到上次离开的地方。
- `.: 移动到最后改动的地方。
- :marks 显示所有标记。
- :delmarks a b – 删除标记a和b。
- :delmarks a-c – 删除标记a、b和c。
- :delmarks a c-f – 删除标记a、c、d、e、f。
- :delmarks! – 删除当前缓冲区的所有标记。
- :help mark-motions 查看更多关于mark的知识。



# [5. 插入文本](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id67)

## [5.1 基本插入](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id68)

- i: 在光标前插入；一个小技巧：按8，再按i，进入插入模式，输入=， 按esc进入命令模式，就会出现8个=。 这在插入分割线时非常有用，如30i+<esc>就插入了36个+组成的分割线。
- I: 在当前行第一个非空字符前插入；
- gI: 在当前行第一列插入；
- a: 在光标后插入；
- A: 在当前行最后插入；
- o: 在下面新建一行插入；
- O: 在上面新建一行插入；
- :r filename在当前位置插入另一个文件的内容。
- :[n]r filename在第n行插入另一个文件的内容。
- :r !date 在光标处插入当前日期与时间。同理，:r !command可以将其它shell命令的输出插入当前文档。

## [5.2 改写插入](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id69)

- c[n]w: 改写光标后1(n)个词。
- c[n]l: 改写光标后n个字母。
- c[n]h: 改写光标前n个字母。
- [n]cc: 修改当前[n]行。
- [n]s: 以输入的文本替代光标之后1(n)个字符，相当于c[n]l。
- [n]S: 删除指定数目的行，并以所输入文本代替之。

注意，类似cnw,dnw,ynw的形式同样可以写为ncw,ndw,nyw。



# [6. 剪切复制和寄存器](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id70)

## [6.1 剪切和复制、粘贴](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id71)

- [n]x: 剪切光标右边n个字符，相当于d[n]l。
- [n]X: 剪切光标左边n个字符，相当于d[n]h。
- y: 复制在可视模式下选中的文本。
- yy or Y: 复制整行文本。
- y[n]w: 复制一(n)个词。
- y[n]l: 复制光标右边1(n)个字符。
- y[n]h: 复制光标左边1(n)个字符。
- yor D: 删除（剪切）当前位置到行尾的内容。
- d[n]w: 删除（剪切）1(n)个单词
- d[n]l: 删除（剪切）光标右边1(n)个字符。
- d[n]h: 删除（剪切）光标左边1(n)个字符。
- d0: 删除（剪切）当前位置到行首的内容
- [n] dd: 删除（剪切）1(n)行。
- :m,nd<cr> 剪切m行到n行的内容。
- d1G或dgg: 剪切光标以上的所有行。
- dG: 剪切光标以下的所有行。
- daw和das：剪切一个词和剪切一个句子，即使光标不在词首和句首也没关系。
- d/f<cr>：这是一个比较高级的组合命令，它将删除当前位置 到下一个f之间的内容。
- p: 在光标之后粘贴。
- P: 在光标之前粘贴。

## [6.2 文本对象](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id72)

- aw：一个词
- as：一句。
- ap：一段。
- ab：一块（包含在圆括号中的）。

y, d, c, v都可以跟文本对象。

## [6.3 寄存器](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id73)

- a-z：都可以用作寄存器名。”ayy把当前行的内容放入a寄存器。
- A-Z：用大写字母索引寄存器，可以在寄存器中追加内容。 如”Ayy把当前行的内容追加到a寄存器中。
- :reg 显示所有寄存器的内容。
- “”：不加寄存器索引时，默认使用的寄存器。
- “*：当前选择缓冲区，”*yy把当前行的内容放入当前选择缓冲区。
- “+：系统剪贴板。”+yy把当前行的内容放入系统剪贴板。



# [7. 查找与替换](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id74)

## [7.1 查找](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id75)

- /something: 在后面的文本中查找something。
- ?something: 在前面的文本中查找something。
- /pattern/+number: 将光标停在包含pattern的行后面第number行上。
- /pattern/-number: 将光标停在包含pattern的行前面第number行上。
- n: 向后查找下一个。
- N: 向前查找下一个。

可以用grep或vimgrep查找一个模式都在哪些地方出现过，

其中:grep是调用外部的grep程序，而:vimgrep是vim自己的查找算法。

用法为： :vim[grep]/pattern/[g] [j] files

g的含义是如果一个模式在一行中多次出现，则这一行也在结果中多次出现。

j的含义是grep结束后，结果停在第j项，默认是停在第一项。

vimgrep前面可以加数字限定搜索结果的上限，如

:1vim/pattern/ % 只查找那个模式在本文件中的第一个出现。

 

其实vimgrep在读纯文本电子书时特别有用，可以生成导航的目录。

比如电子书中每一节的标题形式为：n. xxxx。你就可以这样：

:vim/^d{1,}./ %

然后用:cw或:copen查看结果，可以用C-w H把quickfix窗口移到左侧，

就更像个目录了。



## [7.2 替换](http://www.cnblogs.com/jiqingwu/archive/2012/06/14/vim_notes.html#id76)

- :s/old/new - 用new替换当前行第一个old。
- :s/old/new/g - 用new替换当前行所有的old。
- :n1,n2s/old/new/g - 用new替换文件n1行到n2行所有的old。
- :%s/old/new/g - 用new替换文件中所有的old。
- :%s/^/xxx/g - 在每一行的行首插入xxx，^表示行首。
- :%s/表示行尾。
- 所有替换命令末尾加上c，每个替换都将需要用户确认。 如：%s/old/new/gc，加上i则忽略大小写(ignore)。

还有一种比替换更灵活的方式，它是匹配到某个模式后执行某种命令，

语法为 :[range]g/pattern/command

例如 :%g/^ xyz/normal dd。

表示对于以一个空格和xyz开头的行执行normal模式下的dd命令。

关于range的规定为：

- 如果不指定range，则表示当前行。
- m,n: 从m行到n行。
- 0: 最开始一行（可能是这样）。
- $: 最后一行
- .: 当前行
- %: 所有行