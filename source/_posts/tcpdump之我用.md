---
title: tcpdump之我用
date: 2019-03-27 16:42:32
tags:
categories: [工具使用]
---
### 常用tcpdump命令

| 命令 | 解释 |
| --- | --- |
| tcpdump -i any | 抓取所有网卡的数据 |
| tcpdump -i eth0 host 192.168.42.1 and port 1111 | 抓取在eth0上特定IP地址和端口号的数据包 |
| tcpdump -c 5 -nn -i eth0 icmp and src 192.168.100.62 | 抓取5个主机为192.168.100.62对本机的ping的数据包 |
| tcpdump -c 2 -q -XX -vvv -nn -i eth0 tcp dst port 22 | 解析ssh数据包 |
| tcpdump -i eth0 udp port 1111 | 抓取UDP协议并指定端口号 |
| tcpdump -i eth0 udp -w /tmp/br0.pcap & | 抓取UDP协议数据并输出为Wireshark格式的文件（结束抓包killall tcpdump） |

<!--more-->
### tcpdump --help
```
# tcpdump -h
tcpdump version 4.9.2
libpcap version 1.8.1
Usage: tcpdump [-aAbdDefhHIJKlLnNOpqStuUvxX#] [ -B size ] [ -c count ]
		[ -C file_size ] [ -E algo:secret ] [ -F file ] [ -G seconds ]
		[ -i interface ] [ -j tstamptype ] [ -M secret ] [ --number ]
		[ -Q in|out|inout ]
		[ -r file ] [ -s snaplen ] [ --time-stamp-precision precision ]
		[ --immediate-mode ] [ -T type ] [ --version ] [ -V file ]
		[ -w file ] [ -W filecount ] [ -y datalinktype ] [ -z postrotate-command ]
		[ -Z user ] [ expression ]
```