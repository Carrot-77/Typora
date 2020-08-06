# setsockopt

socket关闭之后并不会立即收回，而是要经历一个TIME_WAIT的阶段。windows下最多可以达到4分钟。

所以在这个时候对这个端口进行重新绑定就会出错。所以需要先设置 SO_REUSEADDR.

或者在closesocket的时候，使用setsockopt设置SO_DONTLINGER。也不会有TIME_WAIT的阶段.

通常使用这个设置来加强网络程序的健壮性。

## 头文件

> #include <sys/types.h>
> \#include <sys/socket.h>



## 函数原型

```c
int getsockopt(int sock, int level, int optname, void *optval, socklen_t *optlen);
int setsockopt(int sock, int level, int optname, const void *optval, socklen_t optlen);
```



## 参数 

* sock：将要被设置或者获取选项的套接字。
* level：选项所在的协议层。

level指定控制套接字的层次.可以取三种值:
1)SOL_SOCKET:通用套接字选项.
2)IPPROTO_IP:IP选项.
3)IPPROTO_TCP:TCP选项.　

* optname：需要访问的选项名。

**SO_DEBUG**，打开或关闭调试信息。
    当option_value不等于0时，打开调试信息，否则，关闭调试信息。它实际所做的工作是在sock->sk->sk_flag中置 SOCK_DBG(第10)位，或清SOCK_DBG位。

**SO_REUSEADDR**，打开或关闭地址复用功能。
    当option_value不等于0时，打开，否则，关闭。它实际所做的工作是置sock->sk->sk_reuse为1或0。

**SO_DONTROUTE**，打开或关闭路由查找功能。
    当option_value不等于0时，打开，否则，关闭。它实际所做的工作是在sock->sk->sk_flag中置或清SOCK_LOCALROUTE位。

**SO_BROADCAST**，允许或禁止发送广播数据。
    当option_value不等于0时，允许，否则，禁止。它实际所做的工作是在sock->sk->sk_flag中置或清SOCK_BROADCAST位。

 **SO_SNDBUF**，设置发送缓冲区的大小。
    发送缓冲区的大小是有上下限的，其上限为256 * (sizeof(struct sk_buff) + 256)，下限为2048字节。该操作将sock->sk->sk_sndbuf设置为val * 2，之所以要乘以2，是防
止大数据量的发送，突然导致缓冲区溢出。最后，该操作完成后，因为对发送缓冲的大小 作了改变，要检查sleep队列，如果有进程正在等待写，将它们唤醒。

 **SO_RCVBUF**，设置接收缓冲区的大小。
    接收缓冲区大小的上下限分别是：256 * (sizeof(struct sk_buff) + 256)和256字节。该操作将sock->sk->sk_rcvbuf设置为val * 2。

**SO_KEEPALIVE**，套接字保活。
    如果协议是TCP，并且当前的套接字状态不是侦听(listen)或关闭(close)，那么，当option_value不是零时，启用TCP保活定时 器，否则关闭保活定时器。对于所有协议，该操
作都会根据option_value置或清 sock->sk->sk_flag中的 SOCK_KEEPOPEN位。

**SO_OOBINLINE**，紧急数据放入普通数据流。
    该操作根据option_value的值置或清sock->sk->sk_flag中的SOCK_URGINLINE位。

**SO_NO_CHECK**，打开或关闭校验和。
    该操作根据option_value的值，设置sock->sk->sk_no_check。

**SO_PRIORITY**，设置在套接字发送的所有包的协议定义优先权。Linux通过这一值来排列网络队列。
    这个值在0到6之间（包括0和6），由option_value指定。赋给sock->sk->sk_priority。

**SO_LINGER**，如果选择此选项, close或 shutdown将等到所有套接字里排队的消息成功发送或到达延迟时间后>才会返回. 否则, 调用将立即返回。
    该选项的参数（option_value)是一个linger结构：
        struct linger {
            int   l_onoff;   
            int   l_linger;  
        };
如果linger.l_onoff值为0(关闭），则清 sock->sk->sk_flag中的SOCK_LINGER位；否则，置该位，并赋sk->sk_lingertime值为 linger.l_linger。

 **SO_PASSCRED**，允许或禁止SCM_CREDENTIALS 控制消息的接收。
    该选项根据option_value的值，清或置sock->sk->sk_flag中的SOCK_PASSCRED位。

**SO_TIMESTAMP**，打开或关闭数据报中的时间戳接收。
    该选项根据option_value的值，清或置sock->sk->sk_flag中的SOCK_RCVTSTAMP位，如果打开，则还需设sock->sk->sk_flag中的SOCK_TIMESTAMP位，同时，将全局变量
netstamp_needed加1。

 **SO_RCVLOWAT**，设置接收数据前的缓冲区内的最小字节数。
    在Linux中，缓冲区内的最小字节数是固定的，为1。即将sock->sk->sk_rcvlowat固定赋值为1。

**SO_RCVTIMEO**，设置接收超时时间。
    该选项最终将接收超时时间赋给sock->sk->sk_rcvtimeo。

**SO_SNDTIMEO**，设置发送超时时间。
    该选项最终将发送超时时间赋给sock->sk->sk_sndtimeo。

 **SO_BINDTODEVICE**，将套接字绑定到一个特定的设备上。
    该选项最终将设备赋给sock->sk->sk_bound_dev_if。

**SO_ATTACH_FILTER**和**SO_DETACH_FILTER**。
    关于数据包过滤，它们最终会影响sk->sk_filter。

* optval：对于getsockopt()，指向返回选项值的缓冲。对于setsockopt()，指向包含新选项值的缓冲。
* optlen：对于getsockopt()，作为入口参数时，选项值的最大长度。作为出口参数时，选项值的实际长度。对于setsockopt()，现选项的长度。



## 返回 


成功执行时，返回0。失败返回-1，errno被设为以下的某个值  
EBADF：sock不是有效的文件描述词
EFAULT：optval指向的内存并非有效的进程空间
EINVAL：在调用setsockopt()时，optlen无效
ENOPROTOOPT：指定的协议层不能识别选项
ENOTSOCK：sock描述的不是套接字



## 常用用法

1. closesocket（一般不会立即关闭而经历TIME_WAIT的过程）后想继续重用该socket：

  > BOOL bReuseaddr=TRUE;
  > setsockopt (s,SOL_SOCKET ,SO_REUSEADDR,(const char*)&bReuseaddr,sizeof(BOOL));


2. 如果要已经处于连接状态的soket在调用closesocket后强制关闭，不经历
  TIME_WAIT的过程：

  > BOOL bDontLinger = FALSE;
  > setsockopt (s,SOL_SOCKET,SO_DONTLINGER,(const char*)&bDontLinger,sizeof(BOOL));


3. 在send(),recv()过程中有时由于网络状况等原因，发收不能预期进行,而设置收发时限：

  > int nNetTimeout=1000;//1秒
  > //发送时限
  > setsockopt (socket，SOL_S0CKET,SO_SNDTIMEO，(char *)&nNetTimeout,sizeof(int));
  > //接收时限
  > setsockopt (socket，SOL_S0CKET,SO_RCVTIMEO，(char *)&nNetTimeout,sizeof(int));


4. 在send()的时候，返回的是实际发送出去的字节(同步)或发送到socket缓冲区的字节
  (异步);系统默认的状态发送和接收一次为8688字节(约为8.5K)；在实际的过程中发送数据
  和接收数据量比较大，可以设置socket缓冲区，而避免了send(),recv()不断的循环收发：

  > // 接收缓冲区
  > int nRecvBuf=32*1024;//设置为32K
  > setsockopt (s,SOL_SOCKET,SO_RCVBUF,(const char*)&nRecvBuf,sizeof(int));
  > //发送缓冲区
  > int nSendBuf=32*1024;//设置为32K
  > setsockopt (s,SOL_SOCKET,SO_SNDBUF,(const char*)&nSendBuf,sizeof(int));


5. 如果在发送数据的时，希望不经历由系统缓冲区到socket缓冲区的拷贝而影响
  程序的性能：

  > int nZero=0;
  > setsockopt (socket，SOL_S0CKET,SO_SNDBUF，(char *)&nZero,sizeof(nZero));


6. 同上在recv()完成上述功能(默认情况是将socket缓冲区的内容拷贝到系统缓冲区)：

  > int nZero=0;
  > setsockopt (socket，SOL_S0CKET,SO_RCVBUF，(char *)&nZero,sizeof(int));


7. 一般在发送UDP数据报的时候，希望该socket发送的数据具有广播特性：

  > BOOL bBroadcast=TRUE;
  > setsockopt (s,SOL_SOCKET,SO_BROADCAST,(const char*)&bBroadcast,sizeof(BOOL));


8. 在client连接服务器过程中，如果处于非阻塞模式下的socket在connect()的过程中可
  以设置connect()延时,直到accpet()被呼叫(本函数设置只有在非阻塞的过程中有显著的
  作用，在阻塞的函数调用中作用不大)

  > BOOL bConditionalAccept=TRUE;
  > setsockopt (s,SOL_SOCKET,SO_CONDITIONAL_ACCEPT,(const char*)&bConditionalAccept,sizeof(BOOL));

9 .如果在发送数据的过程中(send()没有完成，还有数据没发送)而调用了closesocket(),以前我们
一般采取的措施是"从容关闭"shutdown(s,SD_BOTH),但是数据是肯定丢失了，如何设置让程序满足具体
应用的要求(即让没发完的数据发送出去后在关闭socket)？

> struct linger {
> u_short l_onoff;
> u_short l_linger;
> };
> linger m_sLinger;
> m_sLinger.l_onoff=1;//(在closesocket()调用,但是还有数据没发送完毕的时候容许逗留)
> // 如果m_sLinger.l_onoff=0;则功能和2.)作用相同;
> m_sLinger.l_linger=5;//(容许逗留的时间为5秒)
> setsockopt (s,SOL_SOCKET,SO_LINGER,(const char*)&m_sLinger,sizeof(linger));

