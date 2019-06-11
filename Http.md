## 初识HTTP

TCP/IP协议按层次分为**应用层、传输层、网络层、数据链路层**

* **应用层**：决定了向用户提供应用服务时通信的行为，HTTP就处于该层。
* **传输层**：对于上层应用层，传输层提供了处于网络连接中的两台计算机之前的数据传输
    * 在传输层有两个性质不同的协议
      1. TCP（Transmission Control Protocol）传输控制协议
      2. UDP（User Data Protocol）用户数据报协议
      
* **网络层**：处理网络上流动的数据包，该层规定通过什么样的路径到达对方的计算机，将数据传给对方
* **数据链路层（网络接口层）**：处理连接网络的硬件部分

### TCP/IP通信传输流

* 客户端 -> 服务器

    应用层 -> 传输层 -> 网络层 -> 链路层 --------> 链路层 -> 网络层 -> 传输层 -> 应用层

  *相反也是一样的*

### 与HTTP关系密切的TCP IP DNS
  IP（Internet Protocol）网际协议，位于网络层
  TCP协议位于传输层
    握手过程使用了TCP的标记 -----SYN和ACK
    三次握手
      
      发送端 ----->(SYN)接收端    
      发送端 <-----(SYN/ACK)接收端
      发送端 ----->(ACK)接收端
###  负责域名解析的DNS，位于应用层，提供了域名到IP地址之间的解析服务
  
### HTTP与其他协议的关系
![HTTP与其他协议关系](www.dapanpro.com)

### URL 和 URI
* URI(统一资源标识符)
	1. Unifrom：统一的格式方便处理不同类型的资源
	2. Resource：资源的定义就是“可标识的任何东西“，除了文档文件、图片或服务等能够区别于其他类型的，都可作为资源。
	3. Identifier：可标识的对象，也称为标识符
	
	综上所述，URI就是由某个协议方案表示的资源的定位标识符，协议方案是指访问资源所使用的协议类型名称
	
	使用HTTP协议时，协议方案就是http，还有ftp、file等
	
	URI用字符串标识某一互联网资源，URL标识资源的地址。URL是URI的子集
	
	**URI格式**
	
	表示指定的URI，要使用涵盖全部必要信息的绝对URI、绝对URL以及相对URL。相对URL是指从浏览器中基本URI处指定的URL，形如 */images/test.jpg*
	
	绝对URI格式：http://user:pwd@www.example.com:80/dir/index.html?uid=1#ch1
	
	RFC(Request for Comments, 征求修正意见书) ====> 用来制定HTTP协议技术标准的文档
* URL(统一资源定位符) 

## 简单的HTTP协议

### HTTP协议用户客户端和服务器端之间的通信

请求访问文本或图像等资源的一端称为客户端，而提供资源响应的为服务器端

**请求报文**是由*请求方法*、*请求URI*、*协议版本*、*可选的请求首部字段*、*内容实体*构成

**响应报文**是由*协议版本*、*状态码*、*用以解释状态码的原因短语*、*可选的响应首部字段*、*实体主体*构成

HTTP是**无状态**协议 

### HTTP协议方法：

* GET
* POST
* PUT（传输文件）
* HEAD（获得报文首部，用于确认URI有效性和资源更新的时间）
* DELETE（删除文件）
* OPTIONS（询问查询的方法）
* TRACE（追踪路径）
* CONNECT（用隧道协议连接代理）

### 使用方法下达命令

* 向请求URI指定的资源发送请求报文时，采用称为方法的命令
* 方法的作用是可以指定请求的资源按照期望产生某种行为

### 持久连接节省通信量

* 持久连接
	1. 特点：只要任意一端没有明确提出断开连接，则保持TCP连接状态
* 管线化： 不用等待响应亦可直接发送下一个请求  

### 使用Cookie的状态管理

## HTTP报文内的HTTP信息

### HTTP报文：

* 定义：用于HTTP协议交互的信息
* 请求报文：客户端的HTTP报文
* 响应报文：服务器端的HTTP报文
* 通常分为报文首部和报文主体，两者由最初出现的空行来划分。通常，并不一定有报文主体
	1. 服务器端或客户端需处理的响应或请求的内容和属性

### 请求报文和响应报文的结构
```html
<table>
    <tr>
      <td rowspan='5'>报文首部</td>
      <td>请求行</td>
   </tr>
   <tr>
     
      <td>请求首部字段</td>
   </tr>
   <tr>
      
      <td>通用首部字段</td>
   </tr>
   <tr>
      <td>实体首部字段</td>
   </tr>
   <tr>
      <td>其他</td>
   </tr>
   <tr>
      <td>空行（CR + LF）</td>
      <td></td>
   </tr>
	<tr>
	   <td>报文主体</td>
	   <td></td>
	</tr>
</table>

<table>
   <tr>
      <td rowspan='5'>报文首部</td>
      <td>状态行</td>
   </tr>
   <tr>
     
      <td>响应首部字段</td>
   </tr>
   <tr>
      
      <td>通用首部字段</td>
   </tr>
   <tr>
      <td>实体首部字段</td>
   </tr>
   <tr>
      <td>其他</td>
   </tr>
   <tr>
      <td>空行（CR + LF）</td>
      <td></td>
   </tr>
	<tr>
	   <td>报文主体</td>
	   <td></td>
	</tr>
</table>

```

请求行：包含用于请求的方法、请求URI和HTTP版本

状态行：包含表明响应结果的状态码，原因短语和HTTP版本

首部字段：包含表示请求和响应的各种条件和属性的各类首部

* 一般有四种首部： 通用首部、请求首部、响应首部、实体首部

其他：可能包含HTTP的RFC里未定义的首部（Cookie等）

### 编码提升传输速率

HTTP在传输数据时可以按照数据原貌直接传输，但也可以在传输过程中通过编码提升传输速率。通过在传输时编码，能有效的处理大量的访问请求。但是，编码的操作需要计算机来完成，因此会消耗更多的CPU等资源

#### 报文主体和实体主体的差异

* 报文：是HTTP通信中的基本单位，由八位组字节流组成，通过HTTP通信传输
* 实体：作为请求或相应的有效荷载数据被传输，其内容由实体首部和实体主体组成

HTTP的报文主体用于传输请求或响应的实体主体

通常报文主体等于实体主体，只有当传输中进行编码操作是，实体主体内容会发生变化，导致与保温主体的差异

#### 压缩传输的内容编码
HTTP协议中有一种叫内容编码的功能将内容压缩后传输，常见的内容编码：

* gzip（GNU zip）
* compress（UNIX系统的标准压缩）
* deflate（）
* identity（不进行编码）

#### 分割发送的分块传输编码
传输大容量数据时，把数据分割成多块，能够让浏览器逐步显示页面

### 发送多种数据的多部分对象集合

多部分对象集合包含的对象如下：

* multipart/form-data ----- Web表单文件上传使用
* multipart/byteranges ----- 状态码206响应报文包含了多个范围的内容时使用

多部分对象集合的每个部分类型中，都可以含有首部字段。

### 获取部分内容的范围请求

指定范围发送的请求叫做范围请求

在执行范围请求时，会用到首部字段Range

针对范围请求，响应会返回206 Partial Content的响应报文。另外，对于多重范围的范围请求，响应会在首部字段Contenty-Type标明multipart/byteranges后返回响应报文。

如果服务器无法响应范围请求，则会返回状态码200OK和完整的实体内容。

### 内容协商返回最合适的内容

内容协商机制是指客户端和服务器端就响应的资源内容进行交涉，然后提供给客户端最为合适的资源。内容协商会以响应资源的语言、字符集、编码方式等作为判断的基准

包含在请求报文中的某些首部字段（如下）就是判断的基础
 
 * Accept
 * Accept-Charset
 * Accept-Encoding
 * Accept-Language
 * Content-Langugae

内容协商技术有一下三种类型

* 服务器驱动协商（Server-driven Negotiation）
* 客户端驱动协商（Agent-driven Negotiation）
* 透明协商（Transparent Negotiation）

## 返回结果的HTTP状态码

HTTP状态码负责表示客户端HTTP请求的返回结果、标记服务器端的处理是否正常、通知出现的错误等工作

### 状态码告知从服务器端返回的请求结果

状态码的类别

|      | 类别                         | 原因短语                  |
|----- | --------------------------- | ----------------         | 
|1XX   | Informational(信息性状态码)   | 接收的请求正在处理          |
|2XX   | Success(成功状态码)           | 请求正常处理完毕           |
|3XX   | Redirection(重定向状态码)     | 需要进行附加操作已完成请求   |
|4XX   | Client Error(客户端错误状态码) | 服务器无法处理请求          |
|5XX   | Serve Error(服务器错误状态吗)  | 服务器处理请求错误          |

14个常见的状态码

### 2XX 成功
#### 200 OK
从客户端发出的请求在服务器端被正常处理
#### 204 No Content
服务器接收的请求已成功处理，但返回的报文中不含实体的主体部分
#### 206 Partial Content
客户端进行了范围请求。响应报文中包含有Content-Range指定范围的实体内容

### 3XX重定向
3XX响应结果表明浏览器需要执行某些特殊的处理以正确处理请求
#### 301 Moved Permanently
永久性重定向。该状态码表示请求的资源一杯分配了新的URI，以后应使用资源现在所指的URI
#### 302 Found
临时性重定向。改状态码表示请求的资源已被分配到了新的URL，希望用户（本次）能使用新的URI访问
#### 303 See Other
该状态码表示由于请求对应的资源存在着另一个URI，应使用GET方法定向获取请求资源
#### 304 Not Modified
该状态码表示客户端发送附带条件的请求时，服务器端允许请求访问资源，但为满足条件的情况

附带条件的请求值得是采用GET请求方法的请求报文中包含If-Match,If-Modified-Since,If-None-Match,If-Range,If-Unmodified-Sicne中任一首部
#### 307
临时重定向，与302有相同含义

### 4XX客户端错误
4XX的响应结果表明客户端是发生错误的原因所在。
#### 400 Dad Request
请求报文中存在语法错误。
#### 401 Unnauthorized
请求需要有通过HTTP认证的认证信息，若之前已经进行过一次请求，则表示用户认证失败。返回401的响应必须包含一个适用于被请求资源的WWW-Authenticate首部以质询用户信息。当浏览器初次接收到401响应，会弹出认证的对话窗口。
#### 403 Forbidden
该状态码表明对请求资源的访问被服务器拒绝了。

未获得文件系统的访问授权，访问权限出现某些问题（从未授权的发送源IP地址试图访问）等情况都可能是403的原因

#### 404 Not Found
服务器上无法找到请求的资源。也可以在服务器端拒绝请求且不想说明理由时使用

### 5XX服务器错误
5XX的响应结果表明服务器本身发生错误
#### 500 Internal Server Error
服务器端在执行请求是发生了错误。也有可能是Web应用存在的bug或某些临时的故障
#### 503 Service Unavailable
服务器暂时处于超负载或正在进行停机维护，现在无法进行请求。如果得知解除以上状况需要的时间，最好写入RetryAfter首部字段再返回给客户端

## 与HTTP协作的Web服务器
一台服务器可以搭建多个独立域名的Web网站，也可作为通信路径上的中转服务器提升传输效率
### 用单台虚拟主机实现多个域名
用虚拟主机实现多台服务器

在互联网上，域名通过DNS服务映射到IP地址之后访问目标网站。当请求发送到服务器时，已经是IP地址形式的访问

在相同IP地址下，由于虚拟主机可以寄存多个不同主机名和域名的Web网站，因此在发送HTTP请求时，必须在Host首部内完整指定主机名或域名的URI

### 通信数据转发程序：代理、网关、隧道

HTTP通信时，除了客户端和服务器外，还有一些用于数据转发的应用程序，比如代理、网关、隧道，它们可以配合服务器工作

这些应用程序和服务器能将请求转发给通信线路上的下一站服务，并且可以接收服务器发送到响应再转发给客户端

- 代理

	代理是一种有转发功能的应用程序。接收客户端的请求转发给服务器，同事接收服务器的响应转发给客户端。
- 网关

	网关是转发其他服务器通信数据的服务器，接收客户端请求时，就像自己拥有资源的服务器一样对请求进行处理。
- 隧道

	是在相隔甚远的客户端和服务器端两者之间进行中转，并保持双方通信连接的应用程序
	
#### 代理
代理服务器的基本行为就是接收客户端发送的请求后转发给其他服务器。代理不改变请求URI，会直接发送给前方拥有资源的目标服务器

持有资源实体的服务器称为源服务器。

转发是需要添加Via首部字段以标记出经过的主机信息

使用代理服务器的理由：
	
- 利用缓存技术减少网络带宽的流量
- 组织内部针对特定的网站进行访问控制，以获取访问日志等重要信息

代理有多种使用方法，按两种基准分类。一种是是否使用缓存，另一种是是否会修改报文

缓存代理
	
	代理转发响应是，缓存代理会预先将资源副本保存在代理服务器上
	当代理接收到对相同资源的请求时，就可以不从源服务器那里获取资源，而是将之前缓存的资源作为响应返回

透明代理

	转发请求或响应时，不对报文做任何加工的代理类型被称为透明代理。反之，对报文内容进行加工的代理叫做非透明代理
	
#### 网关
网关的工作机制与代理相似，而网关能够使通信线路上的服务器提供非HTTP协议服务

利用网关能提高通信安全性，因为可以再客户端和网关之间的通信线路上加密以确保连接的安全

#### 隧道
隧道可按要求建立起一条与其他服务器的通信线路，届时使用SSL等加密手段进行通信。隧道的目的是为了确保客户端和服务器端的安全通信。

对到本身不会解析HTTP请求。隧道在通信双方断开连接是结束

### 保存资源的缓存
缓存是指服务器或客户端本地磁盘内保存的资源副本，利用缓存可减少对源服务器的访问，节省了通信流量和时间

#### 保存的有效期限
即便缓存服务器内有缓存，也不能保证每次都会返回对同资源的请求

即使有缓存资源，也会因为客户端的要求、缓存有效期等因素，会向源服务器确认资源有效性
#### 客户端的缓存
在IE中，客户端缓存称为临时网络文件（Temporary Internet File）

在HTTP出现之前的协议

- FTP（File Transfer Protocol）
	
	传输文件时使用的协议
- NNTP（NetWork News Transfer Protocol）

	用于NetNews电子会议室内传递消息的协议
	
- Archie 

	搜索anonymousFTP公开的文件信息的协议
- WAIS（Wide Area Information Servers）

	以关键字检索多个数据库使用的协议
	
- Gopher

	查找与互联网连接的计算机内信息的协议

## HTTP首部

HTTP协议的请求和响应报文必定包含在HTTP首部

### HTTP报文首部

HTTP请求报文

在请求中，HTTP报文由方法、URI、HTTP版本、HTTP首部字段等部分构成

HTTP响应报文

在响应中，HTTP报文由HTTP版本、状态码（数字和原因短语）、HTTP首部字段3部分构成

### HTTP首部字段

#### HTTP首部字段传递重要信息

#### HTTP首部字段结构

HTTP首部字段由首部字段名和字段值构成

#### 4种HTTP首部字段类型

HTTP首部字段根据实际用途分为以下4类

- 通用首部类型（General Header Fields）

	请求和响应都会用到的首部
	
- 请求首部字段

	从客户端向服务器发送请求报文时使用的首部
	
- 响应首部字段

	从服务器端向客户端发送响应报文时使用的字段
	
- 实体首部字段

	针对请求报文和响应报文的实体部分使用的字段

#### HTTP/1.1 首部字段一览表

通用首部字段

|首部字段名|说明|
|---------|---|
|Cache-Control|控制缓存的行为|
|Connection|逐跳首部、连接的管理|
|Date|创建报文的日期和时间|
|Pragma|报文指令|
|Trailer|报文末端的首部一览|
|Transfer-Encoding|指定报文主体的传输编码方式|
|Upgrade|升级为其他协议|
|Via|代理服务器的相关信息|
|Warning|错误通知|

请求首部字段

|首部字段名|说明|
|---|---|
|Accept|用户代理可处理的媒体类型|
|Accept-Charset|优先的字符集|
|Accept-Encoding|优先的内容编码|
|Accept-Language|优先的语言（自然语言）|
|Authorization|Web认证信息|
|Expect|期待服务器的特定行为|
|From|用户的电子邮箱地址|
|Host|请求资源所在服务器|
|If-Match|比较实体标记（ETag）|
|If-Modified-Since|比较资源更新时间|
|If-None-Match|比较实体标记（与If-Match相反）|
|If-Range|资源未更新是发送实体Byte的范围请求|
|If-Unmodified-Since|比较资源更新时间（与If-Modified-Since相反）|
|Max-Forwards|最大传输逐跳数|
|Proxy-Authorization|代理服务器要求客户端的认证信息|
|Range|实体的字节范围请求|
|Referer|对请求中的URI的原始获取方|
|TE|传输编码的优先级|
|User-Agent|HTTP客户端程序的信息|

响应首部字段

|首部字段名|说明|
|---|---|
|Accept-Ranges|是否接受字节范围请求|
|Age|推算资源创建经过时间|
|ETag|资源的匹配信息|
|Location|令客户端重定向指定URI|
|Proxy-Authenticate|代理服务器对客户端的认证信息|
|Retry-After|对再次发起请求的时机要求|
|Server|HTTP服务器的安装信息|
|Vary|代理服务器的管理信息|
|WWW-Authenticate|服务器端对客户端的认证信息|

实体首部字段

|首部字段名|说明|
|---|---|
|Allow|资源可支持的HTTP方法|
|Content-Encoding|实体主体适用的编码方式|
|Content-Language|实体主体的自然语言|
|Content-Length|实体主体的大小（单位：字节）|
|Content-Location|替代对应资源的URI|
|Content-MD5|实体主体的报文摘要|
|Content—Range|实体主体的位置范围|
|Content-Type|实体主体的媒体类型|
|Expires|实体主体的过期的日期时间|
|Last-Modified|资源的最后修改时间|

#### 非HTTP/1.1首部字段

#### End-to-end 首部和 Hop-by-hop 首部

HTTP首部字段将定义成缓存代理和非缓存代理的行为，分为2种类型

- 端到端首部（End-to-end Header）

	分在此类型中的首部会转发给请求/响应对应的最终接收目标，且必须保存在由缓存生成的响应中，另外规定它必须被转发
	
- 逐跳首部（Hop-by-hop Header）
	
	分在此类型中的首部支队首次转发有效，会因通过缓存或代理而不再转发。HTTP/1.1 和之后版本中，如果要使用hop-by-hop首部，需提供Connection首部字段
	
下面列举HTTP/1.1中逐跳首部字段，除这8个首部字段之外，其他所有字段都属于端到端首部

- Connection
- Keep-Alive
- Proxy-Authenticate
- Proxy-Authorization
- Trailer
- TE
- Transfer-Encoding
- Upgrade

### HTTP/1.1通用首部字段

通用首部字段是指，请求报文和响应报文双方都会使用的首部

#### Cache-Control

操作缓存的工作机制

指令操作是可选的，多个指令之间通过“,”分隔。首部字段Cache-Control的指令可用于请求及响应时

	Cache-Control: private, max-age=0, no-cache
	
- Cache-Control指令一览

可用的指令按请求和响应分类如下所示

缓存请求指令

|指令|参数|说明|
|---|---|---|
|no-cache|无|强制向源服务器再次验证|
|no-store|无|不缓存请求或响应的任何内容|
|max-age=[秒]|必需|响应的最大Age值|
|max-stale=[秒]|可省略|接收已过期的响应|
|min-fresh=[秒]|必需|期望在指定时间内响应仍有效|
|no-transform|无|代理不可更改媒体类型|
|only-if-cached|无|从缓存获取资源|
|cache-extension|-|新指令标记（token）|

缓存响应指令

|指令|参数|说明|
|---|---|---|
|public|无|可向任意方提供响应的缓存|
|private|可省略|仅向特定用户返回响应|
|no-cache|可省略|缓存前必须先去人其有效性|
|no-store|无|不缓存请求或响应的任何内容|
|no-transform|无|代理不可更改媒体类型|
|must-revalidate|无|可缓存但必须再向源服务器进行确认|
|proxy-revalidate|无|要求中间缓存服务器对缓存的响应有效性在进行确认|
|max-age=[秒]|必需|响应的最大Age值|
|s-maxage=[秒]|必需|公共缓存服务器响应的最大Age值|
|cache-extension|-|新指令标记（token）|

#####表示是否能缓存的指令

public指令

	Cache-Control: public

当指定使用public指令时，表明其他用户也可利用缓存

private指令

	Cache-Control: private
	
响应只能特定的用户作为对象

no-cache指令

	Cache-Control: no-cache
	
目的是为了防止从缓存中返回过期的资源

客户端发送的请求中如果包含no-cache指令，表示客户端将不会接收缓存过的响应

服务器返回的响应中如果包含no-cache指令，表示缓存服务器不能对资源进行缓存

	Cache-Control: no-cache=Location
	
响应指令可以设置参数值，若有参数则不能缓存

#####控制可执行缓存的对象的指令

no-store指令
	
	Cache-Control: no-store

暗示请求或响应中包含机密文件。该指令规定缓存不能再本地存储请求或响应的任一部分

#####指定缓存期限和认证的指令

s-maxage指令

	Cache-Control: s-maxage=604800（单位：秒）

指令功能与max-age相同，不同点是s-maxage指令只适用于供多位用户使用的公共缓存服务器，当使用s-maxage指令后，忽略对Expires首部字段及max-age指令的处理

max-age指令

	Cache-Control: max-age=604800（单位：秒）
	
当客户端发送的请求包含max-age，如果缓存时间小于指定时间，那么客户端接收缓存的资源，当max-age=0时，缓存服务器将请求转发给源服务器。

当服务器返回的响应包含max-age，缓存服务器将会不对资源的有效性再作确认，而max-age数值代表资源保存为缓存的最长时间

min-fresh指令

	Cache-Control: min-fresh=69（单位：秒）

min-fresh要求缓存服务器返回至少还未指定时间的缓存资源

max-stale指令

	Cache-Control: max-stale=3600（单位：秒）
	
max-stale可只是缓存资源，即使过期也照常接收

only-if-cached指令
	
	Cache-Control: only-if-cached
	
only-if-cached表示客户端只有在缓存服务器本地缓存目标资源的情况下才会要求其返回，若请求缓存服务器的本地缓存无反应，返回状态码504 Gateway Timeout

must-revalidate指令

	Cache-Control: must-revalidate

使用must-revalidate指令，代理会向源服务器再次验证即将返回的响应缓存目前是否仍然有效

使用了must-revalidate指令将会忽略请求的max-stale指令

proxy-revalidate指令

	Cache-Control: proxy-revalidate
	
proxy-revalidate指令要求所有的缓存服务器在接收到客户端带有该指令的请求返回相应之前，必须再次验证缓存有效性

no-transform指令

	Cache-Control: no-transform
	
使用no-transform指令规定无论在请求还是响应中，缓存都不能改变实体主体的媒体类型

防止缓存或代理压缩图片等类似操作

#####Cache-Conrtrol扩展

cache-extension token

	Cache-Control: private, community="UCI"
	
通过cache-extension标记（token），可以扩展Cache-Control首部字段内的指令

#### Connection

Connection首部字段具有如下两个作用：

- 控制不再转发给代理的首部字段
- 管理持久连接

控制不再转发给代理的首部字段

	Connection: 不再转发的首部字段名
	
管理持久连接

	Connection: close
	
	Connection: Keep-Alive
	
旧的HTTP版本协议想要维持持久连接，需要知道Connection首部字段的值为Keep-Alive