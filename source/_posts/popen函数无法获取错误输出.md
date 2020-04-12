---
title: popen函数无法获取错误输出
date: 2019-04-11 19:28:02
tags:
---

    有时候在编程时，我们需要调用外部命令，并获取该命令的输出。linux提供了popen()函数来帮我们解决这个难题。
```
    #include <stdio.h>
    FILE *popen(const char *command, const char *type);
    int pclose(FILE *stream);
```
    当设置type为'r'时，便可以获取到该命令的标准输出了，但是却不能获取到标准错误输出。
    要解决的话其实很简单，那就是在执行命令时重定向就好了2>&1。

```
int main(int argc, char **argv)
{
    FILE *fp = NULL;
    char buff[256] = {0};

    fp = popen("ping -I epon0.2 -c 5 www.baidu.com 2>&1", "r");
    if (NULL == fp)
    {
        printf("popen error\n");
        return 0;
    }

    while (NULL != fgets(buff, sizeof(buff), fp))
    {
        printf("buff: %s\n",buff);
    }

    pclose(fp);
    return 0;
}
```