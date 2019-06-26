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

#### Date

表明HTTP报文创建的时间

	Date: Tue, 03 Jul 2012 04:40:40 GMT
	
#### Pragma

是HTTP/1.1之前的遗留字段，与HTTP/1.0向后兼容

	Pragma: no-cache
	
通用首部字段，但仅在客户端发送。要求所有的中间服务器不返回缓存资源

如果服务器都以HTTP/1.1为基础  那则以Cache-Control: no-cache 表示 不接收缓存的资源。但并不是所有的中间服务器都使用HTTP/1.1  因此发送的请求都会包含

	Cache-Control: no-cache
	Pragram: no-chche
	
#### Trailer

首部字段Trailer会事先说明在报文主体后记录了哪些字段

#### Transfer-Encoding

传输报文主体时采用的编码方式

#### Upgrade

用于检测HTTP协议及其他协议是否可使用更高的版本进行通信，参数可指定一个完全不同的通信规则

首部字段使用Upgrade时，必须额外指定Connection: Upgrade

首部字段有Upgrade的时候   服务器可用101 Switching Protocols状态码作为返回

#### Via

追踪客户端和服务器之间请求和响应的传输路径

报文经过代理和网关时，会在Via字段中添加自身服务器的信息，然后再转发。

经常和Trace方法一起使用

#### Warning

告知用户一些与缓存相关的问题的警告

	Warning: [警告码][警告的主机：端口号]”[警告的内容]“（[日期时间]）  日期时间可省略
	
警告码

|警告码|警告内容|说明|
|----|---|---|
|110|Response is Stale（响应已过期）|代理返回已过期的资源|
|111|Revaidation failed（再验证失败）|代理再验证资源有效性时失效|
|112|Disonnection operation（断开连接操作）|代理和互联网连接被故意切断|
|113|Heuristic Expiration（试探性过期）|响应的试用期超过24小时（有效缓存的设定时间大于24小时的情况下）|
|199|Miscellaneous warning（杂项警告）|任意的警告内容|
|214|Transformation applied（使用了转换）|代理对内容编码或媒体类型等执行了某些处理|
|299|Miscellaneous persistent warning（持久杂项警告）|任意的警告内容|

### 请求首部字段

请求首部字段是从客户端往服务器端发送请求报文中所使用的字段

#### Accept

	Accept: text/html, applucation/xhtml+xml, application/xml; q=0
	
Accept首部字段可通知服务器，用户代理能够处理的媒体类型以及媒体类型的优先级 可使用type/subtype这种格式

- 文本文件
	
	text/html,text/plain,text/css ...

- 图片文件

	img/jepg, image/gif, image/png ...
	
- 视频文件

	video/mpeg, video/quicktime ...
	
- 应用程序使用的二进制文件

	application/octet-stream, application/zip ...
	
q来额外表示权重值 0-1之间  1为最大

服务器优先返回权重最高的媒体类型

#### Accept-Charset

 Accept-Charset: iso-8859-5,unicode-1-1; q=0.8
 
通知服务器用户代理支持的字符集及字符集的相对优先顺序

该字段应用于内部协商机制的服务器驱动协商

#### Accept-Encoding

	Accept-Encoding: gzip, deflate
	
通知服务器用户代理支持的内容编码及内容编码的优先级

- gzip
	
	由文件压缩程序gzip（GUN zip）生成的编码格式（RFC1952），采用Lenpel-Ziv算法（LZ77）及32位循环冗余校验（Cyclic Redundancy Check，简称CRC）
	
- compress

	由UNIX文件压缩程序compress生成的编码格式，采用Lenpel-Ziv-Welch算法（LZW）
	
- deflate

	组合使用zlib格式及由deflate压缩算法生成的编码格式
	
- idenity

	不执行压缩或不会变化的默认编码格式
	
#### Accept-Language

	Accept-language: zh-cn,zh;q=0.7,en-us,en;q=0.3
	
告知服务器用户代理能够处理的自然语言

#### Authorization

	Authorization: Basic dsdsdsdsds==
	
告知服务器，用户代理的认证信息

#### Expect

	Expect: 100-continue
	
客户端告知服务器期望出现的某种特定操作。因服务器无法理解客户端的期望作出回应而发生错误时，返回状态码417 Expection Failed

#### From

告知服务器使用用户代理的用户的电子邮件地址

#### Host

	Host: www.hackr.jp

告知服务器请求的资源所处的互联网主机名和端口号。Host首部字段是唯一一个在HTTP/1.1协议中必须添加在请求内的首部字段

#### If-Match

形如If-xxx这样形式的请求首部字段，都可称为条件请求，服务器接收到附带条件的请求后，只有判断指定条件为true时，才会执行请求

If-Match 告知服务器匹配资源所用的实体标记（ETag）值，若不匹配返回412 Precondition Failed

还可以指定*为If-Match字段值，服务器将会忽略ETag值

#### If-Modified-Since

如果在If-Modified-Since字段指定的日期时间后，资源发生了更新，服务器就会接受请求。如果没有更新，则返回304 Not Modified

#### If-None-Match

与If-Macth相反的作用， 在If-None-Match与ETag字段值不一致时，可处理该请求

在GET和HEAD方法中使用首部字段If-None-Match可获得最新的资源

#### If-Range

	If-Range: '123456'
	
告知服务器若指定的字段值（ETag值或者时间）和请求资源的ETag值或时间相一致，则作为范围请求处理。反正，返回全体资源

#### If-Unmodified-Since

	If-Unmodified-Since: Thu, 03 Jul 2012 00:00:00 GMT
	
与If-Modified-Since相反

#### Max-Forwards

	Max-Forwards: 10
	
通过Trace和OPTIONS方法，发送包含首部字段Max-Forwards的请求时，指定可经过的服务器最大数目

#### Proxy-Authorization
	
	Proxy-Authorization: Basic dsfafafafeae

接收到代理服务器发来的认证质询是，客户端发送包含首部字段Proxy-Authorization的请求，以告知服务器所需的认证信息，发生在客户端与代理之间

#### Range

	Range: bytes=5001-10000
	
接收到附带Range首部字段的请求的服务器，会在处理请求之后返回状态吗206 Partial Content的响应。无法处理范围请求是，则会返回状态码200 OK的响应及全部资源

#### Referer

	Referer: http://xxx
	
首部字段Referer告知服务器请求的原始资源的URL

#### TE

	TE: gzip, deflate; q=0.5

告知服务器能够处理相应的传输编码方式及相对优先级，用于传输编码

还可以指定伴随trailer字段的分块传输编码的方式。应用后者时，只需把trailers赋值给该字段值

	TE: trailers
	
#### User-Agent

用于传达浏览器的种类

	User-Agent: Mozilla/5.0 xxxxx
	
会创建请求的浏览器和用户代理名称等信息传达给服务器。此外，如果请求经过代理，那么中间也可能被添加上代理服务器的名称

### 响应首部字段

由服务器向客户端返回报文中所使用的字段。用于补充响应的附加信息、服务器信息，以及对街护短的附加要求等。

#### Accept-Ranges

	Accept-Ranges: bytes
	
当不能处理范围请求时，Accept-Ranges: none

告知用户是否能处理范围请求，以指定获取服务器某个部分的资源，指定字段值为bytes or none

#### Age

	Age: 600
	
告知客户端，源服务器在多久前创建了响应。

若创建该响应的服务器时缓存服务器，Age值是指缓存后的响应再次发起认证到认证完成的时间值。代理创建响应时必须加上首部字段Age。

#### ETag

	ETag: "xxxx"
	
告知客户端实体标识，将资源以字符串形式作唯一性标识的方式。另外，当资源更新时，ETag值也需要更新

##### 强ETag和弱ETag

强ETag

强ETag，不论实体发生多么细微的变化都会改变其值
	
	ETag: ”usagi-1234“
	
弱ETag

弱ETag只用于提示资源是否相同。只有资源发生了根本改变，产生差异时才会改变ETag值。这时，会在字段值最开始处附加W/。

	ETag: W/"usagi-1234"
	
#### Location

	Location: http://xxxxx
	
使用首部字段Location可以将响应接收方引导至某个与请求URI位置不同的资源

基本上，该字段会配合 3XX : Redirection 的响应，提供重定向的URI

几乎所有浏览器在接收到包含Location首部字段的响应后，都会强制常识性的访问已提示的重定向资源

#### Proxy-Authenticate

	Proxy-Authenticate: Basic realm="Usagidesign Auth"
	
会把代理服务器所要求得认证信息发送给客户端，发生在客户端和代理之间

#### Retry-After

	Retry-After: 120
	
告知客户端在多久之后再次发送请求，主要配合503 Service Unavailable响应，或3XX响应一起使用。

字段值可以是具体的时间或者创建响应后的秒数

#### Server

	Server: Apache/2.2.17（Unix）
	
告知客户端当前服务器上安装的HTTP服务器应用程序的信息

#### Vary

	Vary: Accept-Language
	
对缓存进行控制。

从代理服务器接收到源服务器返回的包含Vary指定的响应之后，若要进行缓存，仅对请求中含有相同Vary的请求进行缓存。即对相同资源进行请求，但是由于Vary指定的首部字段不相同，因此需要向源服务器请求重新获取资源。

#### WWW-Authenticate

	WWW-Authenticate: Basic realm="Usagidesign Auth"
	
用于HTTP访问认证，告知客户端适用于访问请求URI所指定认证方案（Basic或Digest）和带参数提示的质询（chanllenge）

### 实体首部字段

包含在请求报文和响应报文中的实体部分所使用的首部，用于补充内容的更新时间等与实体相关的信息

#### Allow
	Allow: GET, HEAD
	
用于通知客户端能够支持Request-URI指定资源的所有HTTP方法，如果接收到不支持的HTTP方法，返回状态码405 Method Not Allowed。同时还会把所有能够支持的HTTP方法写入首部字段Allow后返回。

#### Content-Encoding

	Content-Encoding: gzip
	
告知客户端服务器对实体的主体部分宣统的内容编码方式

-  gzip
-  compress
-  deflate
-  identity

#### Content-Length

	Content-Length: 15000
	
表明实体主体部分的大小（单位是字节）。对实体主体进行内容编码时，不能再使用Content-Length首部字段

#### Content-Location

	Content-Location: http://www.hackr.jp/index-ja.html
	
给出与报文主体部分相对应的URI，Content-Location表示的是报文主体返回资源对应的URI

#### Content-MD5

	Content-Location: xxxxxxx
	
是一串由MD5算法生成的值，目的在于检查报文在传输过程中是否保持完整，以及确认其传输到达

#### Content-Range

	Content-Range: bytes 5001-10000/10000
	
针对范围请求，返回响应的Content-Range，告知客户端返回的实体的那个部分符合范围请求，字段值以字节为单位。

#### Content-Type

	Content-Type: text/html; charset=UTF-8
	
实体主体内的对象的媒体类型

#### Expires

	Expires: Wed, 04 Jul 2012 08:26:05 GMT
	
将资源失效日期告知客户端。缓存服务器在接收到含有首部自担Expires的响应后，会议缓存来应答，在Expires字段指定的时间之前，响应的副本会一直被保存。当超过指定的时间后，缓存服务器在请求发送过来时，会转向源服务器请求资源。

当首部字段Cache-Control有指定max-age时，比起Expires，优先处理max-age指令

#### Last-Modified

	Last-Modified: xxxxx
	
指明资源最终修改的时间

### 为Cookie服务的首部字段

Cookie的工作机制是用户识别和状态管理

Cookie的规格标准文档

- 由网景公司颁布的规格标准

	网景公司设计开发了Cookie

- RFC2109

- RFC2965

- RFC6265

为Cookie服务的首部字段

|首部字段名|说明|首部类型|
|---|---|---|
|Set-Cookie|开始状态管理所使用的Cookie信息|响应首部字段|
|Cookie|服务器接收到的Cookie信息|请求首部字段|

#### Set-Cookie
	
	Set-Cookie: static=enable; expires=Tue, 05 Jul 2011 07:26:31

当服务器准备开始管理客户端状态时，会事先告知各种信息，

Set-Cookie字段属性

|属性|说明|
|---|---|
|NAME=VALUE|赋予Cookie的名称和其值（必需项）|
|expires=DATE|Cookie的有效期（若不明确指定则默认浏览器关闭前为止）|
|path=PATH|将服务器上的文件目录作为Cookie的适用对象（若不指定则默认为文档所在的文件目录）|
|domain=域名|作为Cookie适用对象的域名（若不指定则默认为创建Cookie的服务器的域名）|
|Secure|仅在HTTPS安全通信时才会发送Cookie|
|HttpOnly|加以限制，使Cookie不能被JavaScript脚本访问|

##### expires 属性

指定浏览器可发送的Cookie的有效期

一旦Cookie从服务器发送到客户端，服务器端就不存在可以显示删除Cookie的方法，但可以通过覆盖已过期的Cookie，实现对客户端Cookie的实质性删除

##### path属性

指定Cookie的发送范围的文件目录

##### domain属性

通过domain属性指定的域名可做到与结尾匹配一致。

##### secure属性

限制Web页面仅在HTTPS安全连接是，才可以发送Cookie

	Set-Cookie: name=value; secure
	
##### HttpOnly

使JavaScript无法获取Cookie，主要目的是为了防止跨站脚本攻击对Cookie的信息获取

	Set-Cookie: name=value; HttpOnly
	
#### Cookie

	Cookie: status=enable
	
首部字段Cookie会告知服务器，当客户端想获得HTTP状态管理支持时，就会在请求中包含从服务器接收到的Cookie，接收到多个Cookie时，同样可以以多个Cookie形式发送

### 其他首部字段

HTTP首部字段可以自行扩展

- X-Frame-Options
- X-XSS-Protection
- DNT
- P3P

#### X-Frame-Options

	X-Frame-Options: DENY

属于HTTP响应首部，用于控制网站内容在其他Web网站的Frame标签内的显示问题。其主要目的是为了网址点击劫持攻击

有两个可指定的字段值
	
- DENY: 拒绝
- SAMEORIGIN: 仅在同源域名下的页面匹配时许可

#### X-XSS-Protection

属于HTTP响应首部。针对跨站脚本攻击的一个对策，用于控制浏览器XSS防护机制的开关。

可指定的字段值

- 0：将XSS过滤设置成无效状态
- 1：将XSS过滤设置成有效状态

#### DNT

	DNT: 1

属于HTTP请求首部。DNT是Do Not Track的简称，意为拒绝个人信息被收集，是表示拒绝被精准广告追踪的一种方法。

首部字段DNT可指定的字段值

- 0：统一被追踪
- 1：拒绝被追踪

由于DNT的功能具备有效性，所以服务器需要对DNT做对应的支持

#### P3P

	P3P: CP="CAO DSP LAW xxxxxxxx"
	
属于响应首部，通过利用P3P(The Platform for Privacy Perferences，在线隐私偏好平台)技术，可以让Web网站上的个人隐私变成一种仅供程序可理解的形式，已达到保护用户隐私的目的

要进行P3Pde设定，需要按照以下操作步骤进行

* 步骤一：创建P3P隐私
* 步骤二：创建P3P隐私对照文件后，保存命名在/w3c/p3p.xml
* 步骤三：从P3P隐私中新建Compaict policies后，输出到HTTP响应中

## 确保Web安全的HTTPS

在HTTP协议中有可能存在信息窃听或者身份伪装等安全问题，使用HTTPS通信机制可以有效防止这些问题

### HTTP的缺点

HTTP的不足之处：

- 通信使用明文（不加密），内容可能会被窃听
- 不验证通信方的身份，因此有可能遭遇伪装
- 无法证明报文的完整性，所以有可能已遭篡改

#### 通信使用明文可能会被窃听

HTTP报文使用明文（未经过加密的报文）方式发送

- TCP/IP是可能被窃听的网络
- 加密处理防止被窃听
	
	目前最普及的防止窃听保护信息的集中对策中，最普及的是加密技术。加密对象有以下几个：

	1. 通信的加密
		
		HTTP协议中没有加密机制，但可以通过SSL（Secure Socket Layer，安全套接层）或TLS（Transport Layer Security，安全层传输协议）的组合使用，加密HTTP的通信内容
		
		用SSL建立安全通信西安路支行，就可以在这条线路上进行HTTP通信了。与SSL组合使用的HTTP被称为HTTPS（HTTP Secure，超文本传输安全协议）或HTTP over SSL
	
	2. 内容的加密

		参与通信的内容本身的加密的方式，即把HTTP报文的所有内容进行加密处理

#### 不验证通信方的身份就可能遭遇伪装

HTTP协议中的请求和响应不会对通信方进行确认

- 任何人都可以发起请求

	在发送端的IP和端口号没有被Web服务器设定限制的情况下，服务器只要接收到请求变回返回一个响应
	
	HTTP下一的实现本身非常简单，不论是谁发送过来的请求都会返回响应，因此不确认通信方，会存在以下各种隐患
	
	- 无法确定请求发送至目标的Web服务器是否是按照真实意图返回的那台服务器。有可能是伪装的Web服务器
	- 无法确定响应返回到的客户端是否是按真实意图接收的那个客户端，可能是伪装的客户端
	- 无法确定正在通信的对方是否具有访问权限。因为某些Web服务器上保存着重要的信息，只想发给特定用户的通信的权限
	- 无法确定请求来自何方，出自谁手
	- 即使是无意义的请求也会照单全收。无法阻止海量请求下的DoS攻击（Denial of Service，拒绝服务攻击）
- 查明对手的证书
	
	虽然HTTP无法确定通信方，但是SSL可以。SSL不仅提供加密处理，还使用了一种被称为证书的手段，可用于确认方。
	
	通过使用证书，以证明通信方就是意料之中的服务器，这对使用者个人来说，也减少了个人信息泄露的危险性
	
	客户端持有证书即可完成个人身份的确认，也可用于对Web网站的认证环节
	
#### 无法证明报文完整性，可能已遭篡改

所谓完整性是指信息的准确性。若无法证明其完整性，通常也就意味着无法判断信息是否准确。

-	接收到的内容可能有误

	由于HTTP协议无法证明通信的完整性。因此，在请求或响应送出之后知道对方接收之前的时间段内，即使请求或响应内容遭到篡改，也无法获悉。
	
	中间人攻击（Man-in-the-Middle attack, MITM）
	
- 如何防止篡改

### HTTP+加密+认证+完整性保护=HTTPS

#### HTTP加上加密处理和认证以及完整性保护后即是HTTPS

我们把添加了加密以及认证机制的HTTP称为HTTPS（HTTP Secure）

#### HTTPS是身披SSL外壳的HTTP

HTTPS并非应用层的一种新协议，只是HTTP通信接口部分用SSL（Secure Socket Layer）和TLS（Transport Layer Security）协议代替

通常HTTP直接和TCP通信，当使用SSL时，和SSL先通信，再由SSL和TCP通信了

在采用SSL后，HTTP就拥有了HTTPS的加密、证书和完整性保护

#### 互相交换密钥的公开密钥加密技术

SSL采用一种叫做公开密钥加密（Public-key cryptography）的加密处理方式

- 共享密钥和加密的困境

	加密和解密同用一个密钥的方式成为共享密钥加密（Common key crypto system），也被叫做对称密钥加密
	
- 使用两把密钥的公开密钥加密
- HTTPS采用混个加密机制

	HTTPS采用了共享密钥加密和公开密钥加密两者并用的混合加密机制
	
#### 证明公开密钥正确性的证书

- 可证明组织真实性的EV SSL证书
- 用以确认客户端的客户端证书
- 认证机构信誉第一
- 自由认证机构颁发的证书称为自签名证书

	在互联网上不可作为证书使用
	
#### HTTPS的安全通信机制

CBC模式（Cipher Block Chaining）又名密码分组链接模式。在此模式下，将前一个明文块加密处理后和下一个明文块做XOR运算，使之重叠，然后再对运算结果做加密处理。对第一个明文块做加密处理时，要么使用前一段密文的最后一块，要么利用外部生成的初始向量。

- SSL和TLS

	HTTPS使用SSL（Secure Socket Layer）和TLS（Transport Layer Security）这两个协议
	
- SSL速度慢吗

	当使用SSL时，速度会变慢
	
	SSL的慢分两种。一种是通信慢，一种是由于大量消耗CPU及内存等资源，导致处理速度变慢
	
## 确认访问用户身份的认证

### 何为认证

核对信息通常指的是：

- 密码：只有本来才会知道的字符串信息
- 动态令牌：仅限本人持有的设备内显示的一次性密码
- 数字证书：仅限本人（终端）持有的信息
- 生物认证：指纹和虹膜等本人的生理信息
- IC卡等：仅限本人持有的信息

HTTP使用的认证方式：

HTTP/1.1使用的认证方式如下：

- BASIC认证（基本认证）
- DIGEST认证（摘要认证）
- SSL客户端认证
- FormBase认证（基于表单认证）

此外还有windows统一认证

### BASIC认证

BASIC认证是从HTTP/1.1就定义的认证方式。即使是现在仍有一部分的网站会使用这种认证方式。是Web服务器和通信客户端之间进长的认证方式

BASIC认证步骤

BASIC认证虽然采用的是Base64编码方式，但这不是加密处理。不需要任何附加信息即可对其解码

### DIGEST认证

DIGEST统一使用质询/响应的方式（challenge/response），但不会像BASIC认证那样直接发送明文密码 

服务器会随着401返回待WWW-Authenticate首部字段的信息，必须包含nonce和realm字段

接收到返回401状态码的客户端，返回的响应中包含DIGEST认证必须的首部字段Authorization信息。首部字段Authorization中必须包含username、realm、nonce、uri和response信息。其中nonce和realm就是之前从服务器接收到的响应中的字段

### SSL客户端认证

利用SSL客户端认证可以避免ID密码被盗被第三者利用的情况

SSL客户端认证借由HTTPS的客户端证书完成认证的方式

#### SSL客户端认证的认证步骤

为达到SSL客户端认证的目的，需要实现将客户端证书分发给客户端，且客户端必须安装此证书

步骤1：接收到需要认证资源的请求，服务器会发送Certificate-Request的报文，要求客户端提供客户端证书

步骤2：用户选择将发送的客户端证书后，客户端会把客户端证书信息以Client Certificate报文方式发送给服务器

步骤3：服务器验证客户端证书验证通过后可领取证书内客户端的公开密钥，然后开始HTTPS加密通信

#### SSL客户端认证采用双因素认证

在多数情况下，SSL客户端认证不会仅依靠证书完成认证，一般会和基于表单认证形成一种双因素认证来使用。

#### SSL客户端认证必要的费用

#### 基于表单认证

#### 认证多半为基于表单认证

#### Session管理及Cookie应用

一般会使用Cookie来管理Sission

步骤1：客户端吧用户ID和密码等登陆信息放入报文的实体部分，通常以POST方式把请求发送给服务器

步骤2：服务器会发放用以识别用户ID的Session ID。会在首部字段Set-Cookie内写入Session ID

步骤3：客户端接收到从服务器发来的Session ID之后，将其作为Cookie保存在本地。下次请求时，自动发送Cookie

## 基于HTTP功能追加协议

### 基于HTTP的协议

### 消除HTTP瓶颈的SPDY

开发主旨是为了解决HTTP的性能瓶颈，缩短Web页面的加载时间

#### HTTP的瓶颈

- 一条连接上只可发送一个请求
- 请求只能从客户端开始，客户端不可以接收除响应以外的指令
- 请求/响应首部未经过压缩就发送。首部信息越多延迟越大
- 发送冗长的首部，每次互相发送相同的首部造成的浪费较多
- 可任意选择数据压缩格式

Ajax的解决方法

通过JavaScript脚本语言的调用就能和服务器进行HTTP通信。借由这种手段，能从已加载完毕的Web页面上发起请求，只更新局部页面

利用Ajax实时从服务器获取内容，可能导致大量的请求产生。未解决HTTP协议本身存在的问题

Comet的解决方法

一旦服务器的内容有更新，Comet不会让请求等待，而是直接给客户端返回响应。只是一种通过延迟应答，模拟实现服务器向客户端推送的功能。

但为了保存响应，一次连接的时间变长了。期间。为了维持连接会消耗更多的资源

SPDY目标：为了在协议级别消除HTTP所遭遇的瓶颈

#### SPDY的设计与功能

SPDY没有完全改写HTTP协议，而是在TCP/IP的应用层与运输层之间通过新加会话的形式运作。同时，考虑到安全性的问题，SPDY规定通信中使用SSL

使用SPDY之后，HTTP获得以下额外的功能。

- 多路复用流

  通过单一的TCP连接，可以无限制处理多个HTTP请求

- 赋予请求优先级

  可以给请求诸葛分配优先级顺序
  
- 压缩HTTP首部

  压缩HTTP请求和响应的首部，通信产生的数据包数量和发送的字节数更少了
  
- 推送功能

  支持服务器主动向客户端推送数据的功能
  
- 服务器提示功能
	
  服务器可以主动提示客户端请求所需的资源
  
### 使用浏览器进行全双工通信的WebSocket

#### WebSocket的设计与功能

WebSocket协议由IETF制定

#### WebSocket协议

WebSocket协议的主要特点

推送功能

支持由服务器向客户端推送数据

减少通信量

只要建立起WebSocket协议，就希望一直保持连接状态，而且WebSocket协议首部信息很小，通信量也相应减少了

- 握手-请求

  需要用到HTTP的Upgrade首部字段，告知服务器通信协议发生改变
  
- 握手-响应

  返回状态码101 Switching Protocols的响应
  
  Sec-WebSocket-Accept的字段值是由握手请求中的Sec-WebSocket-Key的字段值生成的
  
- WebSocket API

```javaScript
	var socket = new WebSocket('')
	socket.onopen = function() {
 		socket.send()
 	}
```

### HTTP/2.0

HTTP/2.0的特点

HTTP/2.0的7项技术化讨论

|||
| ------- | ---- |
|压缩|SPDY、Friendly|
|多路复用|SPDY|
|TKS义务化|Speed + Mobility|
|协商|Speed + Mobility，Friendly|
|客户端拉拽(Client Pull)/服务器推送(Server Push)|Speed + Mobility|
|流量控制|SPDY|
|WebSocket|Speed + Mobility|

### Web服务器管理文件WebDAV

WebDAV除了创建、删除文件等基本功能，它还具备文件创建者管理、文件编辑过程中机制其他用户内容覆盖的加锁功能，以及对文件内容修改的版本控制功能

#### 扩展HTTP/1.1 的 WebDAV

针对服务器上的资源，WebDAV增加了一些概念

集合（Collection）：是一种统一管理多个资源的概念。以集合为单位可进行各种操作。也可实现类似集合的集合这样的叠加

资源（Response）：把文件或集合称为资源

属性（Property）：定义资源的属性。定义以“名称=值”的形式执行

锁（Lock）：把文件设置成无法编辑状态。多人同时编辑时，可防止在同一时间进行内容写入。

#### WebDAV内新增的方法及状态码

WebDAV为实现远程文件管理。向HTTP/1.1中追加了以下方法

__PROPFIND__：获取属性

__PROPPATCH__：修改属性

__MKCOL__：创建集合

__COPY__：复制资源及属性

__MOVE__：移动资源

__LOCK__：资源加锁

__UNLOCK__：资源解锁

为配合扩展的方法，状态码也随之扩展

__102 Processing__：可正常处理请求，但目前是处理中状态

__207 Multi-Status__：存在多种状态

__422 Umprocessible Entity__：格式正确，内容有误

__423 Locked__：资源已被加锁

__424 Failed Dependency__：处理与某请求关联的请求失败，因此不再维持依赖关系

__507 Insuffcient Storage__：保存空间不足

## 构建Web内容的技术

### HTML

#### Web页面几乎全由HTML构建

#### HTML的版本

#### 设计应用CSS

### 动态HTML

#### 让Web页面动起来的动态HTML

#### 更易控制HTML的DOM

### Web应用

#### 通过Web提供功能的Web应用

#### 与Web服务器及程序协作的CGI

CGI（Common GateWay Interface，通用网关接口）是指web服务器在接收到客户端发送过来的请求后转发给程序的一组机制

#### 因Java而普及的Servlet

Servlet是一种能在服务器上创建动态内容的程序

CGI每次请求程序要启动一次

### 数据发布的格式和语言

#### 可扩展标记语言

#### 发布更新信息的RSS/Atom

RSS（简易信息聚合，也叫聚合内容）和Atom都是发布新闻或博客日志等更新信息文档的格式的总称。

用于订阅博客更新信息的RSS阅读器，这种应用几乎支持RSS的所有版本以及Atom

#### JavaScript衍生的轻量级易用JSON

JSON能够处理的数据类型有 false、null、true、对象、数组、数字、字符串

## Web的攻击技术

### 针对Web的攻击技术

#### HTTP不具备必要的安全功能

#### 在客户端可篡改请求

通过URL查询字段或者表单、HTTP首部。Cookie等途径把攻击代码传入

#### 针对Web应用的攻击模式

- 主动攻击
- 被动攻击
- 以服务器为目标的主动攻击  

  主动攻击是指攻击者直接访问Wweb应用，把代码注入的攻击模式
  
  主动攻击最具代表的是SQL注入和OS命令注入攻击
  
- 以服务器为目标的被动攻击

  被动攻击是指利用圈套策略执行攻击代码的攻击模式，在被动攻击过程中，攻击者不直接对目标的web应用访问发起攻击
  
  被动攻击最具代表的是跨站脚本攻击和跨站点请求伪造
  
### 因输出值转义不完全引发的安全漏洞

实施Web应用的安全对策可大致分为以下两部分

- 客户端的验证
- web应用端（服务器端）的验证

  - 输入值验证
  - 输出值转义

#### 跨站脚本攻击

跨站脚本攻击（Cross-Slit Scripting，XSS）是指通过存在安全漏洞的Web网站注册用户的浏览器内运行非法的HTML标签或JavaScript进行的一种攻击

跨站脚本攻击有可能造成以下影响

- 利用虚假输入表单片区用户信息
- 利用脚本窃取用户的Cookie
- 显示伪造的文件或图片

#### SQL注入

- 会执行非法的SQL的SQL注入攻击

  SQL注入是指针对Web应用使用的数据库，通过运行非法的SQL而产生的攻击
  
#### OS命令注入攻击

OS命令注入攻击是指通过Web应用，执行非法的操作系统命令达到攻击目的

#### HTTP首部注入攻击

HTTP首部注入攻击，是指攻击者通过在响应 首部字段内插入换行，添加任意响应主体的一种攻击。属于被动攻击模式

#### 邮件首部注入

邮件首部注入（mail header injection）是指Web应用中的邮件发送功能，攻击者通过向邮件首部To或Subject内任意添加非法内容发起的攻击

#### 目录遍历攻击

目录遍历攻击（Directory Traversal）是指对本无意公开的文件目录，通过非法截断器目录路径后，达成访问目的的一种攻击

#### 远程文件包含漏洞

是指当部分脚本内容需要从其他文件读入时，攻击者利用指定外部服务器的URL充当依赖文件，让脚本读取后，就可以执行任意脚本的攻击

### 因设置或设计上的缺陷引发的安全漏洞  
错误设置Web服务器，或由设计上的一些问题引起的安全漏洞

#### 强制浏览

从安置在Web服务器的公开目录下的文件中，浏览那些原本非自愿公开的文件

强制浏览可能会造成以下一些影响

- 泄露顾客的个人信息等重要情报
- 泄露原本需要具体访问权限的用户才可查阅的信息内容
- 泄露未连接到外界的文件

#### 不正确的错误消息处理

Web应用的错误信息内包含对攻击者有用的信息。与Web应用有关的主要错误信息如下所示

- Web应用抛出的错误消息
- 数据库等系统抛出的错误消息

#### 开放重定向

对指定的任意URL作重定向跳转的功能，而于此功能相关联的安全漏洞是指，假如指定的重定向URL到某个具有恶意的Web网站，那么用户就会被诱导至那个Web网站

### 因会话管理疏忽引发的安全漏洞

会话管理是用来管理用户状态的必备功能。

#### 会话劫持

指攻击者通过某种手段拿到了用户的会话ID，并非法使用此会话ID伪装成用户，达到攻击的目的

#### 会话固定攻击

对以窃取目标会话ID为主动攻击手段的会话劫持而言，会话固定攻击会强制用户使用攻击者指定的会话ID，属于被动攻击

#### 跨站点请求伪造  
指攻击者通过设置好的陷阱，强制对已完成认证的用户进行非预期的个人信息或设定信息等某些状态更新，属于被动攻击

造成以下影响   

- 利用已通过认证的用户权限更新设定信息
- 利用已通过认证的用户权限购买商品
- 利用已通过认证的用户权限在留言板上发表言论

### 其它安全漏洞

#### 密码破解

即算出密码，突破认证。

密码破解的两种手段

- 通过网络的密码试错
- 对已加密的密码的破解（指攻击者入侵系统，已获得加密或散列处理的密码数据的情况）

#### 点击劫持

指利用透明的按钮或链接做成陷阱，覆盖在Web页面上。然后诱导用户在不知情的情况下，点击那个链接访问内容

#### Dos攻击

指一种让运行中的服务器呈停止状态的攻击，有时也叫做服务器停止攻击或者拒绝服务攻击

主要有以下两种Dos攻击方式

- 集中利用访问请求遭横资源过载，资源用尽的同时，实际上服务业就呈现停滞状态
- 通过攻击安全漏洞使服务停止

#### 后门程序

指开发设置的隐藏入口，可不按正常步骤使用受限功能。利用后门程序就能够使用原本受限制的功能

后门程序分三类

- 开发阶段作为Debug调用的后门程序
- 开发者为了自身利益植入的后门程序
- 攻击者通过某种方法设置的后门程序

