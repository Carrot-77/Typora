# open()

## 头文件

> #include<sys/types.h>
> #include<sys/stat.h>
> #include<fcntl.h>

## 原型

> int open( const char * pathname, int flags);
> int open( const char * pathname,int flags, mode_t mode);



## 参数说明：

参数pathname 指向欲打开的文件路径字符串。下列是参数flags 所能使用的旗标:

* O_RDONLY 以只读方式打开文件
* O_WRONLY 以只写方式打开文件
* O_RDWR 以可读写方式打开文件。上述三种旗标是互斥的，也就是不可同时使用，但可与下列的旗标利用OR(|)运算符组合。
* O_CREAT 若欲打开的文件不存在则自动建立该文件。
* O_EXCL 如果O_CREAT也被设置，此指令会去检查文件是否存在。文件若不存在则建立该文件，否则将导致打开文件错误。此外，若O_CREAT与O_EXCL同时设置，并且欲打开的文件为符号连接，则会打开文件失败。
* O_NOCTTY 如果欲打开的文件为终端机设备时，则不会将该终端机当成进程控制终端机。
* O_TRUNC 若文件存在并且以可写的方式打开时，此旗标会令文件长度清为0，而原来存于该文件的资料也会消失。
* O_APPEND 当读写文件时会从文件尾开始移动，也就是所写入的数据会以附加的方式加入到文件后面。
* O_NONBLOCK 以不可阻断的方式打开文件，也就是无论有无数据读取或等待，都会立即返回进程之中。
* O_NDELAY 同O_NONBLOCK。
* O_SYNC 以同步的方式打开文件。
* O_NOFOLLOW 如果参数pathname 所指的文件为一符号连接，则会令打开文件失败。
* O_DIRECTORY 如果参数pathname 所指的文件并非为一目录，则会令打开文件失败。

## 返回值

若所有欲核查的权限都通过了检查则返回0值，表示成功，只要有一个权限被禁止则返回-1。

# write()

## 头文件

> #include<unistd.h>

## 原型：

> ssize_t write(int fd,const void*buf,size_t count)



## 参数说明：

* fd:是文件描述符（write所对应的是写，即就是1）
* buf:通常是一个字符串，需要写入的字符
* count：是每次写入的字节数

## 返回值：

 成功：返回写入的字节数
 失败：返回-1并设置errno
  ps： 写常规文件时，write的返回值通常等于请求写的字节数count， 而向终端设备或者网络写时则不一定

# read()

## 头文件

> #include<unistd.h>

功能：用于从文件描述符对应的文件读取数据（从打开的设备或文件中读取数据）

## 原型：

> ssize_t read(int fd,void*buf,size_t count)

## 参数说明：

* fd:  文件描述符
* buf: 为读出数据的缓冲区；
* count: 为每次读取的字节数（是请求读取的字节数，读上来的数据保存在缓冲区buf中，同时文件的当前读写位置向后移）

## 返回值：

 成功：返回读出的字节数
 失败：返回-1，并设置errno，如果在调用read之前到达文件末尾，则这次read返回0

