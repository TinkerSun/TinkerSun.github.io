---
title: wireshark之我用
date: 2019-03-27 16:37:23
tags:
categories: [工具使用]
---
## 过滤器
### 1、捕获过滤器（CaptureFilters）
捕获过滤器设置于抓包前，决定想要抓取什么样的报文，捕获过滤器只能过滤协议，不能过滤内容。  
打开wireshark软件，依次点击`捕获`->`捕获过滤器`，可看到wireshark默认的过滤器规则有：

| 名称 | 过滤器 |
| --- | --- |
| "Ethernet address 00:00:5e:00:53:00" | ether host 00:00:5e:00:53:00 |
| "Ethernet type 0x0806 (ARP)" | ether proto 0x0806 |
| "No Broadcast and no Multicast" | not broadcast and not multicast |
| "No ARP" | not arp |
| "IPv4 only" | ip |
| "IPv4 address 192.0.2.1" | host 192.0.2.1 |
| "IPv6 only" | ip6 |
| "IPv6 address 2001:db8::1" | host 2001:db8::1 |
| "IPX only" | ipx |
| "TCP only" | tcp |
| "UDP only" | udp |
| "TCP or UDP port 80 (HTTP)" | port 80 |
| "HTTP TCP port (80)" | tcp port http |
| "No ARP and no DNS" | not arp and port not 53 |
| "Non-HTTP and non-SMTP to/from www.wireshark.org" | not port 80 and not port 25 and host www.wireshark.org |

我们可以借助示例来写出我们自己想要的过滤规则，比如
>(host 192.168.1.1 or src net 10.58.0.0/16) and tcp dst portrange 80-8080 and dst net 172.0.0.0/8

<!--more-->
### 2、显示过滤器（DisplayFilters）
显示过滤器用于过滤所抓取的报文，方便处理和排查，它不但支持协议过滤而且还支持内容过滤。  
#### 2.1 协议过滤
根据具体协议
`ppp || pppoe || pppoed || pppoes` 过滤ppp相关报文
根据协议的属性值  
`tcp.flags.syn == 1`  
`tcp.port == 49264`  
`tcp.srcport == 49264`    
`ip.addr != 192.168.1.1`  
`ip.src == 192.168.1.1`  
`http.request.method == "GET"`  
`dns.qry.name == "zyx.qq.com"`  
**不知道属性值怎么过滤时，可以在wireshark中找到该属性值，右击选中`作为过滤器应用`->`选中`**
#### 2.2 内容过滤 
`tcp contains "USER"`  
`udp[8:3] == 02:37:61` udp报文的payload前3个字节  
在遇到大小写敏感的时候，还可以使用函数：  
upper(string－field)－把字符串转换成大写  
lower(string－field)－把字符串转换成小写  
如 lower(http.request.uri) contains "img"
## 其他
查找可以通过按`Ctrl+F`键，可选`显示过滤器`、`十六进制值`、`字符串`、`正则表达式`

另外在`统计`菜单栏里，IO图表，流量图等也均是分析协议的利器
