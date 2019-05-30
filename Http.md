# 初识HTTP

TCP/IP协议按层次分为应用层、传输层、网络层、数据链路层

* 应用层：决定了向用户提供应用服务时通信的行为，HTTP就处于该层。
* 传输层：对于上层应用层，传输层提供了处于网络连接中的两台计算机之前的数据传输
    * 在传输层有两个性质不同的协议
      1. TCP（Transmission Control Protocol）传输控制协议
      2. UDP（User Data Protocol）用户数据报协议
      
* 网络层：处理网络上流动的数据包，该层规定通过什么样的路径到达对方的计算机，将数据传给对方
* 数据链路层（网络接口层）：处理连接网络的硬件部分

TCP/IP通信传输流

* 客户端 -> 服务器

    应用层 -> 传输层 -> 网络层 -> 链路层 --------> 链路层 -> 网络层 -> 传输层 -> 应用层

  *相反也是一样的*

与HTTP关系密切的TCP IP DNS
  IP（Internet Protocol）网际协议，位于网络层
  TCP协议位于传输层
    握手过程使用了TCP的标记 -----SYN和ACK
    三次握手
      
      发送端 ----->(SYN)接收端    
      发送端 <-----(SYN/ACK)接收端
      发送端 ----->(ACK)接收端
  负责域名解析的DNS，位于应用层，提供了域名到IP地址之间的解析服务
  
```java

package com.qyf404.learn.maven;

import org.junit.After;

import org.junit.Assert;

import org.junit.Before;

import org.junit.Test;

public class AppTest {

private App app;

@Before

public void setUp() {app = new App();}

@Test

public void testAdd() throws InterruptedException {

int a = 1;

int b = 2;

int result = app.add(a, b);

Assert.assertEquals(a + b, result);

}

@After

public void tearDown() throws Exception {

}

}

```