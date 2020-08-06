### UDP连接发送文件

![UDP示意图](https://uploadfiles.nowcoder.com/images/20190315/308571_1552654687053_263E6AFD1A48F8511D04B67EB12AA24C)



# recvfrom



## 头文件

> #include <sys/types.h>
>
> #include <sys/socket.h>

## 原型

> ssize_t recv(int sock, void *buf, size_t len, int flags);
>
> ssize_t recvfrom(int sock, void *buf, size_t len, int flags, struct sockaddr *from, socklen_t *fromlen);

 

## 参数  

* sock：索引将要从其接收数据的套接字。

* buf：存放消息接收后的缓冲区。

* len：buf所指缓冲区的容量。

* flags：是以下一个或者多个标志的组合体，可通过or操作连在一起
* from：指向存放对端地址的区域，如果为NULL，不储存对端地址。
* fromlen：作为入口参数，指向存放表示from最大容量的内存单元。作为出口参数，指向存放表示from实际长度的内存单元。

MSG_DONTWAIT：操作不会被阻塞。



## 返回值  

成功执行时，返回接收到的字节数。另一端已关闭则返回0。失败返回-1，errno被设为以下的某个值  

* EAGAIN：套接字已标记为非阻塞，而接收操作被阻塞或者接收超时
* EBADF：sock不是有效的描述词
* ECONNREFUSE：远程主机阻绝网络连接
* EFAULT：内存空间访问出错
* EINTR：操作被信号中断
* EINVAL：参数无效
* ENOMEM：内存不足
* ENOTCONN：与面向连接关联的套接字尚未被连接上
* ENOTSOCK：sock索引的不是套接字



## sendto



## 头文件

> #include <sys/types.h>   
>
> #include <sys/socket.h>



## 原型

> int sendto(int s, const void * msg, int len, unsigned int flags, const struct sockaddr * to, int tolen)



## 参数说明

sendto() 用来将数据由指定的socket 传给对方主机. 

* 参数s 为已建好连线的socket, 如果利用UDP协议则不需经过连线操作. 
* 参数msg 指向欲连线的数据内容
* 参数flags 一般设0, 详细描述请参考send(). 
* 参数to 用来指定欲传送的网络地址, 结构sockaddr 请参考bind(). 
* 参数tolen 为sockaddr 的结果长度.



## 返回值

成功则返回实际传送出去的字符数, 失败返回-1, 错误原因存于errno 中.