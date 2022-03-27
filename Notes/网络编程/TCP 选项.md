# SOL_SOCKET

## SO_REUSEADDR

在bind调用前设置，可以重复绑定，除非ip和port完全相同。将通配符地址（0.0.0.0）和特定地址对待为不同ip

可以重复绑定到处于TIME_WAIT状态的ip和端口

只检查当前绑定的socket是否设置该选项

| SO_REUSEADDR | socketA        | socketB        | Result             |
| ------------ | -------------- | -------------- | ------------------ |
| ON/OFF       | 192.168.0.1:21 | 192.168.0.1:21 | Error (EADDRINUSE) |
| ON/OFF       | 192.168.0.1:21 | 10.0.0.1:21    | OK                 |
| ON/OFF       | 10.0.0.1:21    | 192.168.0.1:21 | OK                 |
| OFF          | 0.0.0.0:21     | 192.168.0.1:21 | Error (EADDRINUSE) |
| OFF          | 192.168.0.1:21 | 0.0.0.0:21     | Error (EADDRINUSE) |
| ON           | 0.0.0.0:21     | 192.168.0.1:21 | OK                 |
| ON           | 192.168.0.1:21 | 0.0.0.0:21     | OK                 |
| ON/OFF       | 0.0.0.0:21     | 0.0.0.0:21     | Error (EADDRINUSE) |

## SO_REUSEPORT

- 可以重复绑定，即使地址完全相同
- 此选项检查所有绑定同一地址的socket
- 需要同时设置SO_REUSEADDR
- UDP时会均匀分配数据报，TCP时会均匀分配到来的连接

## SO_LINGER

参数为结构体

```C
struct linger
{
int l_onoff; //是否开启
int l_linger; //linger时间
};
```

l_onoff为0，不生效；l_onoff非0，l_linger为0，close时丢弃数据，发送RST，不进行4次挥手；l_linger非0，cLose等待发送缓冲区数据发送完，非阻塞返回EWOULDBLOCK

# IPPROTO_TCP

## TCP_NODELAY

关闭nagle算法
