---
title: "浅析URL"
date: 2021-10-29T20:25:40+08:00
draft: false
categories: [HTML]
---
## URL

英文：Uniform Resource Locator

[https://zh.wikipedia.org:443/w/index.php?title=随机页面](https://zh.wikipedia.org:443/w/index.php?title=随机页面」)

- https，是协议；
- zh.wikipedia.org，是服务器；
- 443，是服务器上的网络端口号；
- /w/index.php，是路径；
- ?title=Special:随机页面，是询问。

  <br/>

## DNS

英文：Domain Name System

### 作用：

根据域名查出IP地址

### nslookup 命令

用于互动式地查询域名记录

进入交互模式，总共有两种方法。

1. 第一种方法，直接输入 nslookup 命令，不加任何参数，则直接进入交互模式，此时 nslookup 会连接到默认的域名服务器（即 /etc/resolv.conf 的第一个 dns 地址）。
2. 第二种方法，是支持选定不同域名服务器的。需要设置第一个参数为“-”，然后第二个参数是设置要连接的域名服务器主机名或 IP 地址。

如果你直接在 nslookup 命令后加上所要查询的 IP 或主机名，那么就进入了非交互模式。当然，也可以在第二个参数位置设置所要连接的域名服务器。

**例子**

交互模式下查询域名

```
nslookup
> www.douban.com
Server:    127.0.1.1   // 往上连接的 DNS 服务器
Address:    127.0.1.1#53    // DNS 服务器 IP 地址与端口

Non-authoritative answer:    // 非权威答案，从上连 DNS 服务器本地缓存中读取，非实际查询得到
Name:    www.douban.com
Address: 115.182.201.6    // IP 地址
Name:    www.douban.com
Address: 115.182.201.7
Name:    www.douban.com
Address: 115.182.201.8
```

交互模式下更改 DNS

进入交互模式之后，使用 `server dns-server `来改变上连 DNS 服务器地址

查询域名 ip 地址

```
nslookup www.douban.com [dns-server]
//如果没有指定 dns-server，使用系统默认的 DNS 服务器。
```

<br/>

## IP

[ip138-查询本机ip](https://ip138.com/)

### IP地址：

互联网协议地址

IP地址是人们在Internet上为了区分数以亿计的主机而给每台主机分配的一个专门的地址，通过IP地址就可以访问到每一台主机。

### ping 命令

[Ping 命令详解](https://blog.csdn.net/hebbely/article/details/54965989)

输入`ping /?` ，列出ping的相关参数

用法:

```
ping [-t] [-a] [-n count] [-l size] [-f] [-i TTL] [-v TOS]
            [-r count] [-s count] [[-j host-list] | [-k host-list]]
            [-w timeout] [-R] [-S srcaddr] [-c compartment] [-p]
            [-4] [-6] target_name
```

- -t ：Ping 指定的计算机直到中断。
- -a ：将地址解析为计算机名。
- -n count ：发送 count 指定的 ECHO 数据包数。默认值为 4。
- -l size ：发送包含由 size 指定的数据量的 ECHO 数据包。默认为 32 字节；最大值是65,527。
- -f ：在数据包中发送"不要分段"标志。数据包就不会被路由上的网关分段。
- -i ttl :将"生存时间"字段设置为 ttl 指定的值。
- -v tos :将"服务类型"字段设置为 tos 指定的值。
- -r count :在"记录路由"字段中记录传出和返回数据包的路由。count 可以指定最少 1 台，最多 9 台计算机。
- -s count :指定 count 指定的跃点数的时间戳。
- -j host-list :利用 host-list 指定的计算机列表路由数据包。连续计算机可以被中间网关分隔（路由稀疏源）IP 允许的最大数量为 9。
- -k host-list :利用 host-list 指定的计算机列表路由数据包。连续计算机不能被中间网关分隔（路由严格源）IP 允许的最大数量为 9。
- -w timeout :指定超时间隔，单位为毫秒。
- destination-list :指定要 ping 的远程计算机。

## 域名

[域名-维基百科](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D)

域名是由一串用点分隔的字符组成的互联网上某一台计算机或计算机组的名称，用于在数据传输时标识计算机的电子方位。

www.xiedaimala.com和xiedaimala.com 不是同一域名

- com是顶级域名
- xiedaimala.com是二级域名(俗称一级域名)
- www.xiedaimala.com是三级域名(俗称二级)
- 上面的两是父子关系

**例如**

- github. io把子域名 XXX.github.io免费给你使用
- 所以www.xiedaimala.com和xiedaimala. com可以不是同一家公司,也可以是
- www是多余的,非常多余。
