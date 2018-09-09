## Unix Network Programming

* starting on: Sept. 9, 2018

* tool: man func_name in Linux to check function details

  ---

* sockaddr, sockaddr_in: 

```
struct sockaddr 这个结构体是linux的网络编程接口中用来表示IP地址的标准结构体，bind、connect等函数中都需要这个结构体，这个结构体是兼容IPV4和IPV6的。在实际编程中这个结构体会被一个struct sockaddr_in所填充。
```

```
struct sockaddr {
           sa_family_t sa_family;    //所选协议族AF_INET
           char        sa_data[14];    //ip地址及端口号
       }
```

```
struct sockaddr_in {
    __SOCKADDR_COMMON (sin_);
    in_port_t sin_port;             /* Port number.  */
    struct in_addr sin_addr;        /* Internet address.  */

    unsigned char sin_zero[sizeof (struct sockaddr) -
                           __SOCKADDR_COMMON_SIZE -
                           sizeof (in_port_t) -
                           sizeof (struct in_addr)];
  };
```



* families

  * families are defined in <sys/socket.h>

  * AF_INET: AF, address family

  * PF_INET: PF, protocol family

* TCP/IP, UDP

  * TCP/IP（Transmission Control Protocol/Internet Protocol）即传输控制协议/网间协议，是一个工业标准的协议集，它是为广域网（WANs）设计的          
  * UDP（User Data Protocol，用户数据报协议）是与TCP相对应的协议。它是属于TCP/IP协议族中的一种
  * TCP/IP协议族包括运输层、网络层、链路层