---
layout: post
title: “使用Python和TCP协议实现邮件客户端”踩坑553小记
date: 2017-12-19 20:30:11.000000000 +09:00
category: Network
tags: Socket
---
开始做《Computer Networking: A Top-Down Approach》应用层的编程作业3：邮件客户端。

题目要求时创建一个能向任何接收方发送电子邮件的简单邮件客户。这个客户需要通过TCP协议与邮件服务器进行连接，然后通过SMTP协议与邮件服务器交换数据。

好吧，首先套路式地创建 TCP 连接，serverName 自然是我们要进行连接的 SMTP 服务器地址，通过查询我找到了[163免费邮客户端设置的POP3、SMTP、IMAP地址](http://help.163.com/09/1223/14/5R7P3QI100753VB8.html)，如图所示：
![](http://ozjtrx3vo.bkt.clouddn.com/2017-12-19-15136877801688.png)
所以我们的 serverName 是 smtp.163.com，serverPort 为 SMTP 的默认端口 25。请求发送出去，我们能收到服务器传回来的 `220 163.com Anti-spam GT for Coremail System (163com[20141201])`，好的没有问题。

#### 坑在哪里？
按照中文第六版 P82 所形容的 SMTP 交换报文的格式，我创建了以下消息并用 socket 的 send 方法发送：
- "HELO 163.com\r\n"
- "MAIL FROM: <joker@163.com>\r\n"
- "RCPT TO: <111000@qq.com>\r\n"
- "DATA"
- ...

结果，从第二条开始就出错了。服务器给我返回了：
```
220 163.com Anti-spam GT for Coremail System (163com[20141201])

250 OK

553 authentication is required,163 smtp11,D8CowACnytCrxzhaT7gLEQ--.52662S2 1513670571
```
令人沮丧，说需要认证，好吧。

#### 出坑

查了半天资料发现，这是由于 163.com 的**反垃圾邮件**策略决定的，我们简单地通过这种方式发送的邮件难以通过反垃圾邮件的检测而到达邮箱。所以我们需要增加一个用来认证的 **AUTH LOGIN** 过程。

具体实现过程就是，在 `MAIL FROM` 之前，添加如下代码：
```
# Auth
clientSocket.send('AUTH LOGIN\r\n')
recv = clientSocket.recv(1024)
print(recv)
if (recv[:3] != '334'):
    print('334 reply not received from server')
 
clientSocket.send((username + '\r\n').encode())
recv = clientSocket.recv(1024).decode()
print(recv)
if (recv[:3] != '334'):
    print('334 reply not received from server')

clientSocket.sendall((password + '\r\n').encode())
recv = clientSocket.recv(1024).decode()
print(recv)
if (recv[:3] != '235'):
    print('235 reply not received from server')
```
而其中的 username 和 password 又是需要 base64 编码的。

#### 相关资料
- [python模块之smtplib: 用python发送SSL/TLS安全邮件](http://blog.csdn.net/welber/article/details/6312610)
- [作业3-邮件客户端](https://github.com/moranzcw/Computer-Networking-A-Top-Down-Approach-NOTES/blob/master/SocketProgrammingAssignment/%E4%BD%9C%E4%B8%9A3-%E9%82%AE%E4%BB%B6%E5%AE%A2%E6%88%B7%E7%AB%AF/source/SMTPClient.py)



