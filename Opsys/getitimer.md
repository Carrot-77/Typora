### getitimer/setitimer

获取或设定间歇计时器的值。系统为进程提供三种类型的计时器，每一类以不同的时间域递减其值。当计时器超时，信号被发送到进程，之后计时器重启动。

getitimer 函数得到间隔计时器的时间值.保存在value中 setitimer函数设置间隔计时器的时间值为newval.并将旧值保存在oldval中

getitimer()用计时器的当前值填写value指向的结构体。

setitimer()将value指向的结构体设为计时器的当前值，如果ovalue不是NULL，将返回计时器原有值。

## 头文件

```c
#include <sys/time.h>
```



## 原型

```c
int getitimer(int which, struct itimerval *value);
int setitimer(int which, const struct itimerval *value, struct itimerval *ovalue);
```



## 参数

* which：间歇计时器类型，有三种选择

* ITIMER_REAL //数值为0，计时器的值实时递减，发送的信号是SIGALRM。

  在real   time中计数器减1，然后等计数往比后发送SIGALRM信号。               

​        计时方式：根据系统时间

* ITIMER_VIRTUAL //数值为1，进程执行时递减计时器的值，发送的信号是SIGVTALRM。

  当进程在执行的过程中计数，然后当计数完毕后发送SIGVTALRM信号给该进程。

​        计时方式：只有在用户模式下执行时才可跟踪时间  

* ITIMER_PROF //数值为2，进程和系统执行时都递减计时器的值，发送的信号是SIGPROF。

  在该进程被执行和系统在代表该进程执行的时间都进行计数 发送SIGPROF信号                                           

​        计时方式：从用户进程开始后开始计时

value，ovalue：时间参数，原型如下

```c
struct itimerval {
    /* 计时器重启动的间歇值 *//* next value */
    struct timeval it_interval;
     /* 计时器安装后首先启动的初始值 */ /* current value */
    struct timeval it_value;   
 };
struct timeval {
    long tv_sec;  /* seconds */
    long tv_usec;   /* microseconds */            
};
```



getitimer()用计时器的当前值填写value指向的结构体。

## 返回说明

成功执行时，返回0。失败返回-1，errno被设为以下的某个值

EFAULT：value或ovalue是不有效的指针
EINVAL：其值不是ITIMER_REAL，ITIMER_VIRTUAL 或 ITIMER_PROF之一