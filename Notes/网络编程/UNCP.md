**MSS 最大分节大小：**每个TCP分节接收的最大数据量

**MTU**最大传输单元

**流量控制**：使用通告窗口，告知对端任一时刻能从对端接收多少字节。缓冲区中当前可用的空间量

**TCP特点**：面向链接，可靠，确认，动态估算RTT，数据排序，全双工

**RTT：**往返时间

**TIME_WAIT作用**

1. 可靠地终止链接：确保可以重发ACK，防止服务端响应RST
2. 允许老的重复分节在网络中消逝。重复分节，漫游的重复分组，路由故障或者断开，分组没有到达目的地，重传的分组已经到达

**以太网MTU** 1500字节

IPv4 根据MSS和MTU限制分节大小，尽量减少分片，IPv6不进行路由分片

**小端字节序：**低序字节存在低地址

**大端字节序：**低序字节存在高地址

Inet_addr失败返回ipv4有限广播地址

Connect 完成三次握手过程

socket创建一个主动套接字，listen将其转换为被动

**内核为一个监听套接字维护两个队列**：

1. 未完成队列：收到SYN，处于SYN_RCV状态，等待完成三次握手
2. 已完成队列：处于ESTABLISHED状态

connect系统调用被信号中断，不能自动恢复，使用select等待链接完成

SIG_CHILD处理函数用waitpid循环处理，由于信号不排队，使用wait处理期间可能有信号被阻塞，子进程无法回收

向已关闭的链接发送数据，第一次写入收到RST，第二次收到sigpipe

服务器崩溃，网络不可达，客户端写入超时后返回ETIMEOUT，或者由路由器返回目的地不可达ICMP报文，

返回EHOSTUNREACH或ENETUNREACH

TCP缓冲区小于带宽延迟积时，tcp管道不会处于满状态

IPPROTO_TCP: TCP_NODELAY:若链接上有未确认的数据，则小于MSS的分组被延迟发送，直到被确认

nagle算法与ACK延滞算法

TCP协议头部

1.16位源端口号

2.16位目的端口号

3.32位序列号

4.32位确认号

5.4位头部长度

6.6位保留

7.6位标志

8.16位窗口大小

9.16位校验和

10.16位紧急指针

11.0~40字节选项

TCP快速重传：接收到重复的三个确认报文

tcp连接非阻塞read

返回<0, errno 为EAGAIN 或EWOULDBLOCK ，监听可读

注意：连接关闭，返回=0，errno也可能为EAGAIN 或EWOULDBLOCK

所以两种情况需要分开处理

非阻塞connect

1.设置描述符非阻塞

2.connect返回0，connect成功，返回-1，错误码为EINPROGRESS，则进行步骤3

3.使用io复用，监听文件描述符上的可写事件。

4.使用getsockopt获取并清除文件描述符的错误，参数SOL_SOCKET,SO_ERROR，错误号为0

Connect 错误码

EINPROGRESS 非阻塞connect，连接无法立即建立，需要用io复用监听可写事件

EISCONN 连接已建立

EINTER 被信号中断，connect被信号中断后无法立即调用connect，会返回EADDRINUSE，监听可写事件

EAGAIN UNIX域错误 关闭fd重试

EADDRINUSE 本地地址已占用 同上

EADDRNOTAVAIL 本地可用端口范围耗尽，可修改/proc/sys/net/ipv4/ip_local_port_range

ECONNECTREFUSED 远端未监听

ENETUNREACH 网络不可达

其它错误 关闭fd

UDP connect已连接的UDP套接字，不进行三次握手，只检查是否存在立即可知的错误；不能使用sendto，recvfromn
