#socket

##定义

###套接字家族

+   AF_UNIX

    用于unix进程间通信（IPC）。

+   AF_INET

    用于网络通信。

+   AF_INET6

    基于IPv6的网络通信。

+   AF_NETLINK

    linux套接字，用于用户代码和内核代码的IPC。


###套接字类型

+   面向连接

    使用之前要先建立一条连接。
    实现这种连接的主要协议是TCP，套接字类型为SOCK_STREAM。
    数据传输是顺序，可靠，不重复的。

+   无连接

    实现这种连接的主要协议是UDP，套接字类型为SOCK_DGRAM。
    数据传输的顺序性，可靠性和数据不重复性无法保证。


##socke模块

```
import socket
from socket import *
```


##方法

###socket

```
socket(family=AddressFamily.AF_INET, type=SocketType.SOCK_STRAM, 
    proto=0, fileno=None)
```

创建一个socket对象。

```
sock=socket()
sock=socket(AF_INET, SOCK_DGRAM)
```

##服务器端方法

###bind

```
bind((host, port))
```

绑定地址到套接字。

###listen

```
listen(backlog)
```

开始监听。

backlog至少为0，为负会被设置为0。定义了未处理连接的队列的大小。

###accept

```
accept() -> (socket object, address info)
```

等待客户端的连接。阻塞式的。
info是一个元组(hostaddr, port)。


##客户端方法

###connect

```
connect((host, port))
```

连接到服务器，出错抛异常。

###connect_ex

```
connect_ex((host, port)) -> errno
```

连接到服务器，出错不抛异常。

##公共用途方法

###recv

```
recv(buffersize[, flags]) -> data
```

接受TCP数据。
buffersize，最多接收多少字节。
如果没有数据将阻塞，直到有数据或连接断开。
当连接断开或数据接收完，返回empty string。

###send

```
send(data[, flags]) -> count
```

发送TCP数据。
返回发送的字节数。
发送的数据可能小于len(data)如果网络忙。

###sendall

```
sendall(data[, flags])
```

发送TCP数据。
会循环调用send直到数据发送完。

###recvfrom

```
recvfrom(buffersize[, flags]) -> (data, address info)
```

接收UDP数据。

###sendto

```
sendto(data[, flags], address) -> count
```

发送UDP数据。

###getpeername

```
getpeername() -> (host, port)
```

连接到当前套接字的远端地址。

###getsockname

```
getsockname() -> (host, port)
```

当前套接字地址。

###close

关闭套接字

###settimeout

```
settimeout(timeout)
```

设置阻塞套接字的超时时间。

###gettimeout

```
gettimeout() -> timeout
```

取超时时间。

###setblocking

```
setblocking(flag)
```

flag : True | False。

setblocking(True) 相对于 settimeout(None)。
setblocking(False) 相对于 settimeout(0.0)。

##例子

###TCP

server:

```
from socket import *
import codecs

addr=('',12345)
ss=socket()
try:
    print('server start...')
    ss.bind(addr)
    ss.listen(5)

    while True:
        cs, csaddr=ss.accept()
        print(codecs.decode(cs.recv(1024)))
        cs.send('hello from server'.encode())
        cs.close()
finally:
    ss.close()
```

client:

```
from socket import *
import codecs

svraddr=('10.58.120.170', 12345)
with socket() as cs:
    cs.connect(svraddr)
    cs.sendall('hello from client'.encode())
    print(codecs.decode(cs.recv(1024)))
```

---
###UDP

server:

```
from socket import *
import codecs

addr=('', 12348)
ss=socket(AF_INET, SOCK_DGRAM)
ss.bind(addr)
try:

    while True:
        data, ad = ss.recvfrom(1024)
        print(codecs.decode(data))
        ss.sendto('hello from server'.encode(), ad)

finally:
    ss.close()
```

client:

```
from socket import *
import codecs

addr=('10.58.120.170',12348)
with socket(AF_INET, SOCK_DGRAM) as cs:
    cs.sendto('hello from client'.encode(), addr)
    data, ad = cs.recvfrom(1024)
    print(codecs.decode(data))
```