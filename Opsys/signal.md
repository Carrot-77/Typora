

# signal 

**设置某一信号对应动作**



## 头文件

```c
#include <signal.h>
```



## 函数原型

```c
typedef void (*sighandler_t)(int);
sighandler_t signal(int signum, sighandler_t handler);
```



## 参数说明　

* 第一个参数signum：指明了所要处理的信号类型，它可以取除了SIGKILL和SIGSTOP外的任何一种信号。 　 

  设置处理功能的*信号值*

  | 宏      | 信号                                                         |
  | ------- | ------------------------------------------------------------ |
  | SIGABRT | （信号中止）异常终止，例如由...发起 [退出](http://www.cplusplus.com/abort) 功能。 |
  | SIGFPE  | （信号浮点异常）错误的算术运算，例如零分频或导致溢出的运算（不一定是浮点运算）。 |
  | SIGILL  | （信号非法指令）无效的功能图像，例如非法指令。这通常是由于代码中的损坏或尝试执行数据。 |
  | SIGINT  | （信号中断）交互式注意信号。通常由应用程序用户生成。         |
  | SIGSEGV | （信号分段违规）对存储的无效访问：当程序试图在已分配的内存之外读取或写入时。 |
  | SIGTERM | （信号终止）发送到程序的终止请求。                           |


  每个库实现可以提供可以与此函数一起使用的附加宏常量。

* 第二个参数handler：描述了与信号关联的动作

指向函数的指针。这可以是程序员定义的函数，也可以是以下预定义函数之一：

| SIG_DFL | 默认处理：信号由该特定信号的默认操作处理。 |
| ------- | ------------------------------------------ |
| SIG_IGN | 忽略信号：忽略信号。                       |



## 作用

signal()会依参数signum 指定的信号编号来设置该信号的处理函数。当指定的信号到达时就会跳转到参数handler指定的函数执行。

当一个信号的信号处理函数执行时，如果进程又接收到了该信号，该信号会自动被储存而不会中断信号处理函数的执行，直到信号处理函数执行完毕再重新调用相应的处理函数。但是如果在信号处理函数执行时进程收到了其它类型的信号，该函数的执行就会被中断。



## 示例



```c
#include <stdio.h>   
#include <signal.h>     
 
sig_atomic_t signaled = 0;
 
void my_handler (int param) {
  signaled = 1;
}
 
int main () {
  void (*prev_handler)(int);
 
  prev_handler = signal (SIGINT, my_handler);
 
  raise(SIGINT);
   
  printf ("signaled is %d.\n",signaled);
 
  return 0;
}
```

