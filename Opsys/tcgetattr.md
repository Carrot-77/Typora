# tcgetattr函数和tcsetattr函数



> int tcgetattr(int fd, struct termios *termios_p);
>
> int tcsetattr(int fd, int optional_actions, const struct termios *termios_p);

说明：tcgetattr函数用于获取与终端相关的参数。参数fd为终端的文件描述符，返回的结果保存在termios结构体中，该结构体一般包括如下的成员：

```objc
tcflag_t c_iflag;      
tcflag_t c_oflag;      
tcflag_t c_cflag;      
tcflag_t c_lflag;     
cc_t     c_cc[NCCS];
```


c_iflag：输入模式标志，控制终端输入方式，具体参数如表6.3所示。

c_iflag参数表

| 键    值 | 说    明                                                     |
| -------- | ------------------------------------------------------------ |
| IGNBRK   | 忽略BREAK键输入                                              |
| BRKINT   | 如果设置了IGNBRK，BREAK键的输入将被忽略，如果设置了BRKINT ，将产生SIGINT中断 |
| IGNPAR   | 忽略奇偶校验错误                                             |
| PARMRK   | 标识奇偶校验错误                                             |
| INPCK    | 允许输入奇偶校验                                             |
| ISTRIP   | 去除字符的第8个比特                                          |
| INLCR    | 将输入的NL（换行）转换成CR（回车）                           |
| IGNCR    | 忽略输入的回车                                               |
| ICRNL    | 将输入的回车转化成换行（如果IGNCR未设置的情况下）            |
| IUCLC    | 将输入的大写字符转换成小写字符（非POSIX）                    |
| IXON     | 允许输入时对XON/XOFF流进行控制                               |
| IXANY    | 输入任何字符将重启停止的输出                                 |
| IXOFF    | 允许输入时对XON/XOFF流进行控制                               |
| IMAXBEL  | 当输入队列满的时候开始响铃，Linux在使用该参数而是认为该参数总是已经设置 |

c_oflag：输出模式标志，控制终端输出方式，具体参数如表6.4所示。

c_oflag参数

| 键    值 | 说    明                                                     |
| -------- | ------------------------------------------------------------ |
| OPOST    | 处理后输出                                                   |
| OLCUC    | 将输入的小写字符转换成大写字符（非POSIX）                    |
| ONLCR    | 将输入的NL（换行）转换成CR（回车）及NL（换行）               |
| OCRNL    | 将输入的CR（回车）转换成NL（换行）                           |
| ONOCR    | 第一行不输出回车符                                           |
| ONLRET   | 不输出回车符                                                 |
| OFILL    | 发送填充字符以延迟终端输出                                   |
| OFDEL    | 以ASCII码的DEL作为填充字符，如果未设置该参数，填充字符将是NUL（‘\0’）（非POSIX） |
| NLDLY    | 换行输出延时，可以取NL0（不延迟）或NL1（延迟0.1s）           |
| CRDLY    | 回车延迟，取值范围为：CR0、CR1、CR2和 CR3                    |
| TABDLY   | 水平制表符输出延迟，取值范围为：TAB0、TAB1、TAB2和TAB3       |
| BSDLY    | 空格输出延迟，可以取BS0或BS1                                 |
| VTDLY    | 垂直制表符输出延迟，可以取VT0或VT1                           |
| FFDLY    | 换页延迟，可以取FF0或FF1                                     |

c_cflag：控制模式标志，指定终端硬件控制信息，具体参数如表6.5所示。



LINUX 使用tcgetattr函数与tcsetattr函数控制终端二



# fcntl

