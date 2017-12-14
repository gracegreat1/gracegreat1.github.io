---
layout: post
title: Socket编程中遇到的CRLF
date: 2017-12-14 17:30:11.000000000 +09:00
category: Network
tags: Socket
---
### Problem
先说问题：在 Socket 编程的过程中，我遇到了`\r\n\r\n`且不知道为何物，查找资料之后发现背后的故事还是很有趣的，决定拿上来和大家分享。

今天在尝试补齐之前《Computer Network》的应用层编程作业，第一题是这样的：
要求开发一个简单的 Web 服务器，从浏览器请求一个文件后，我们服务器可以返回这个文件的内容，如果找不到，返回 404。（《Computer Network: A Top-Down Approach Sixth Edition》中文版 P120 作业1）

然后我在编写响应报文的时候，遇到换行的问题，发现别人的解决方案是`\r\n\r\n`，感到疑惑。

### Solution
众所周知，一个 HTTP 响应报文的组成是这样的：
``` 
HTTP/1.1 200 OK
.....
```
第一行是状态行，在返回状态行以后，有一个换行的操作。是这里用了`\r\n\r\n`，又称作 `CRLF`。
这里涉及到两个内容：
- RFC 文档中规定，HTTP message 中，message-header 和 message-body 中必须间隔两个 CRLF。
  ![](http://ozjtrx3vo.bkt.clouddn.com/2017-12-14-15132434255139.jpg)
- CRLF 是指**回车（Carriage Return）+换行（Line Feed）**。我以前一直以为回车和换行是一个概念，真心长见识了。回车的意思是，将当前光标移动到同一行中的最左边；换行的意思是，保持当前光标的水平位置位置不变，换到下一行。这个历史竟然是涉及到一个叫“电传打印机”的玩意儿，我会贴链接在后面，感兴趣的各位可以看一下。


### Summary
依稀记得研一好像有 Socket 编程的实验，当时没认真做，所以现在又踩了这个坑。

还请各位学霸们多多嘲讽！！！

### Reference
- [stackoverflow - what is the character of \r\n\r\n in nodejs TCP/IP](https://stackoverflow.com/questions/10171127/what-is-the-character-of-r-n-r-n-in-nodejs-tcp-ip)

- [RFC 文档](https://www.w3.org/Protocols/rfc2616/rfc2616-sec4.html#sec4)

- [【详解】回车 换行 0x0D 0x0A CR LF \r \n的来龙去脉](https://www.crifan.com/detailed_carriage_return_0x0d_0x0a_cr_lf__r__n_the_context/)

