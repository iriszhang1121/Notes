# <font color="blue">图解HTTP （CH1-6） —— 上野宣</font>

[TOC]

# 第 1 章　了解 Web 及网络基础

## 1.1　使用 HTTP 协议访问 Web

**流程**：在Web浏览器地址栏中输入制定URL，Web浏览器会从Web服务器获取文件资源resource等信息，从而显示出Web页面

客户端**client**：通过发送请求获取服务器资源的Web浏览器

![image-20251215172517735](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215172517735_OwBQWM.png)

Web使用HTTP（HyperText Transfer Protocol, 超文本传输协议）作为规范，完成从客户端到服务器的一系列运作流程。$\Rightarrow$ Web是建立在HTTP协议上进行通信的。

> 协议：约定的规则

## 1.2　HTTP 的诞生

1989年3月，HTTP诞生。最初设想：借助多文档间相互关联形成超文本HperText，连成可以相互参阅的World Wide Web。

现在已提出**3项WWW构建技术**：把Standard Generalized Markup Language标准通用标记语言SGML作为**页面的文本标记语言**的**HTML**（HyperText Markup Language，超文本标记语言）； 作为**文档传递协议**的**HTTP**；**指定文档所在地址**的**URL**（Uniform Resource Locator，统一资源定位符）。

WWW是Web浏览器当年用来浏览超文本的客户端应用程序时的名称，现在用于表示这一系列的集合，简称为Web。

1990年11月，CERN成功研发世界上第一台Web服务器和浏览器。

1993年，HTML1.0



HTTP/0.9: HTTP于1990问世，但那时并未建立正式标准，所以HTTP1.0正式版之前的版本被称为0.9

HTTP/1.0: 1996年5月作为正式标准被命名，记载于RFC1945。虽然是初期标准，仍在被使用

HTTP/1.1: 1997年1月公布，最初版本RFC2068，修订版RFC2616

HTTP/2.0

HTTP/3.0

## 1.3　网络基础 TCP/IP

通常使用的网络（包括互联网）是在TCP/IP协议族的基础上运作的。HTTP是其中的一个子集

协议Protocol： 不同硬件、操作系统之间通信，需要一种统一的规则

TCP/IP：互联网相关的各类协议族的总称

**TCP/IP分层管理**，按层次可以分4层或者7层。

4层：应用层、传输层、网络层、数据链路层

**层次化的好处**：支持每个层次内部设计的自由改动，同时不影响其他层次，设计相对简单

**应用层**：决定向用户提供应用服务时的通信活动。（FTP、DNS、HTTP...）

**传输层**：对应用层，提供处于网络连接中的两台计算机之间的**数据传输**。（TCP、 UDP）

**网络层**：选择**传输线路**并处理在网络上流动的**数据包**。数据包：网络传输的最小数据单位。规定了通过怎样的路径（传输路线）到达对方计算机，并将数据包传送给对方。

**链路层**：处理连接网络的**硬件**部分。包括控制操作系统、硬件的设备驱动，NIC（Network Interface Card，网络适配器，即网卡），及光纤等物理可见部分（还包括连接器等一切传输媒介）。

![image-20251215174721198](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215174721198_qLgq2d.png)

![image-20251215181852376](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215181852376_6HYwum.png)

**发送端在层与层传输数据时，每经过一层就打上该层所属的首部信息。反之，接收端在层与层传输数据时，每经过一层就消去首部信息。**

**封装encapsulate：包装数据信息**

## 1.4　与 HTTP 关系密切的协议 : IP（网络层）、TCP（传输层） 和 DNS（应用层）

### 负责网络通信的IP协议

IP（Internet Protocol）网际协议：位于网络层。几乎所有使用网络的系统都会用到IP协议。

IP协议作用：把各种数据包传送给对方。可以准确传达的重要条件：IP地址，MAC地址。

IP地址：指明节点被分配到的地址。 MAC地址：网卡所属的固定地址。 IP地址和MAC地址可进行配对。IP地址可变，MAC地址不可变

**使用ARP协议凭借MAC地址进行通信**：IP间通信依赖MAC地址。在网络中，很少有通信双方在同一局域网LAN中，通常需要经过多台计算机和网络设备中转才能连接到对方。进行中转时，会利用下一站中转设备的MAC地址来搜索下一个中转目标，此时，采用ARP地址解析协议，根据通信方的IP地址反查出对应的MAC地址。

**路由选择routing**： 在到达通信目标前的中转过程中，计算机和路由器等网络设备只能获取粗略的传输路线。（无法全面掌握互联网中的细节）

![image-20251215180010706](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215180010706_KwH6z3.png)

### 确保数据可靠传输的TCP协议

TCP位于传输层，可提供可靠的字节流服务

Byte Stream Service字节流服务：为了方便传输，将大块数据分割成以报文段segment为单位的数据包进行管理。

可靠的传输服务：能把数据准确可靠的传给对方。

TCP协议是为了更容易传送大数据才把数据分割，并能确认数据最终是否送达到对方。

三次握手Three-way handshaking：确保数据的准确到达。在数据包传送后进行确认。

1. 发送端 发送一个带有SYN标志的数据包给 接收端
2. 接收端 收到后 回传一个带有SYN/ACK的数据包给 发送端 （表示确认收到）
3. 发送端 回传一个有ACK的数据包给 接收端 （握手结束）

过程中，如果某个阶段莫名中断，TCP协议会再以相同的顺序发送相同的数据包

![image-20251215180612527](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215180612527_Vrk5f0.png)

## 1.5　负责域名解析的 DNS 服务

DNS domain name system服务是和HTTP协议一样位于**应用层**的协议。

DNS：提供域名到IP地址间的解析服务。

用户通常用主机名/域名访问对方的计算机，而非直接通过IP地址访问。

**问题**：相较于一串纯数字的IP地址，对人类来说，用字母和数字表示的名字更容易记忆。但计算机难以理解这些名称，更擅长处理数字。

方案：**DNS协议通过提供域名查找IP地址，或逆向从IP地址反查域名**

![image-20251215181131230](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215181131230_gCavp4.png)

## 1.6　各种协议与 HTTP 协议的关系

![image-20251215181215844](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215181215844_3YPdqD.png)

## 1.7　URI 和 URL

URI uniform resource identifier 统一资源标识符，标识某一互联网资源

URL uniform resource locator 统一资源定位符，网址，表示资源的地点（互联网上所处位置）。URL是URI的子集

绝对URI格式：

![image-20251215181654253](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215181654253_oZhtIT.png)

# 第 2 章　简单的 HTTP 协议

## 2.1　HTTP 协议用于客户端和服务器端之间的通信

客户端：请求访问文本/图像等资源的一端

服务器端：提供资源响应的一端

在两台计算机之间使用HTTP协议通信时，在一条通信线路上必定有一端是客户端，另一端是服务器端。

实际情况，两台计算机可互换客户端和服务器端的角色。但就一条通信线路而言，角色是确定的，HTTP协议能明确区分哪端是客户端，哪端是服务器端。

## 2.2　通过请求和响应的交换达成通信

请求必定由客户端发出，服务器端回复响应

HTTP协议规定，请求从客户端发出，诸侯由服务器端响应请求并返回。（肯定是从客户端先开始建立通信，服务器端在没收到请求前不发送响应）

![image-20251215191909879](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215191909879_FBJmUc_cBleHI.png)

请求报文的构成：请求方法、请求URI、协议版本、可选的请求首部之端、内容实体

![image-20251215191927410](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215191927410_rWlpDy.png)

响应报文的构成：协议版本、状态码（表示请求成功/失败的数字代码）、用于解释状态码的原因短语、可选的响应首部字段、实体主体

![image-20251215192055122](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215192055122_mcMKnX.png)

## 2.3　HTTP 是不保存状态的协议

HTTP是一种不保存状态，即无状态stateless协议。自身不对请求和响应间的通信状态进行保存，不做持久化处理。

![image-20251215192254204](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215192254204_qByMj0.png)

使用HTTP协议，每当有新请求发送，就会产生新的响应。不保留之情的一切请求/响应报文的信息。➡️ <font color="orange">**更快处理大量事务，确保协议的可伸缩性。**</font>

⚠️问题： 随着WEB不断发展，无状态使业务处理变棘手的情况增多。比如：用户登陆购物网站，跳转到其他页面后，也需要保持登录状态。不然就需要不断登陆，非常麻烦。

🌿Sol：引入**cookie**技术，帮助管理状态。

## 2.4　请求 URI 定位资源

指定请求URI的方式很多，比如：

![image-20251215194521312](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215194521312_5N1ofa.png)

客户端请求访问资源，发送请求时，URI需作为请求报文中的请求URI包含在内

除此之外，如果不是访问特定资源，是对服务器本身发起请求，可以用一个*代替请求URI。比如：查询HTTP服务器端支持的HTTP方法种类`OPTIONS * HTTP/1.1`

## 2.5　告知服务器意图的 HTTP 方法

<font color="red">GET：获取资源</font>

请求访问已被URI识别的资源，指定资源经服务器端**解析**后返回响应内容。

请求的资源是：

- 文本 ➡️ 返回文本
- 类似CGI（Common Gateway Interface 通用网关接口）的程序 ➡️ 返回执行后的输出结果

例子：

![image-20251215195129669](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215195129669_wz552s.png)

<font color="red">POST：传输实体主体</font>

虽然GET也可以传输实体主体，但一般不用GET，而用POST。

![image-20251215195223158](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215195223158_yAiWL7.png)

<font color="red">PUT：传输文件</font>

PUT用于传输文件。像FTP协议的文件上传一样，要求在请求报文的主体中保护文件内容，然后保存到URI指定的位置。

HTTP/1.1的PUT方法自身不带验证机制，任何人都可以上传文件，存在安全性问题，一般WEB网站不用该方法。若配合WEB应用程序的验证机制，或架构设计采用REST（REpresentational State Transfer表征状态转移）标准的同类WEB网站，可能会开放使用PUT方法

![image-20251215195730345](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215195730345_UBbmWj.png)

<font color="red">HEAD：获得报文首部</font>

HEAD和GET一样，只是不返回报文主体。HEAD用于确认URI的有效性及资源更新的日期等

<font color="red">DELETE：删除文件</font>

和PUT相反的方法，用于删除文件。按请求URI删除指定资源

HTTP/1.1 的 DELETE 方法本身和 PUT 方法一样不带验证机 制，所以一般的 Web 网站也不使用 DELETE 方法。当配合 Web 应用 程序的验证机制，或遵守 REST 标准时还是有可能会开放使用的。

<font color="red">OPTIONS：询问支持的方法</font>

OPTIONS 方法用来查询针对请求 URI 指定的资源支持的方法。

![image-20251215195946823](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215195946823_KmD6EW.png)

![image-20251215200000531](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215200000531_8RV50u.png)

<font color="red">TRACE：追踪路径</font>

让WEB服务器将之前的请求通信环回给客户端

不常用，且容易引发XST（Cross-Site Tracing跨站追踪）攻击

![image-20251215200146240](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215200146240_6IL2Wa.png)

<font color="red">CONNECT：要求用隧道协议连接代理</font>

CONNECT要求在和代理服务器通信时建立隧道，用隧道协议进行TCP通信。

主要用SSL（Secure Sockets Layer 安全套接层）和TLS （Transport Layer Security 传输层安全）协议对通信内容加密后经隧道传输。

![image-20251215200236925](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215200236925_YZ9hg5.png)

## 2.6　使用方法下达命令

方法的作用：指定请求的资源按期望产生某种行为

方法包括：GET，POST， HEAD等

![image-20251215200538777](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215200538777_KNswOk.png)

## 2.7　持久连接节省通信量

在初始版HTTP协议中，每次HTTP通信都要断开一次TCP连接。

在早期，小文本传输中，问题不大。随着HTTP普及，文档容量变大（大量图片等）。比如，使用浏览器浏览一个包含多张图片的 HTML 页面时，在发送 请求访问 HTML 页面资源的同时，也会请求该 HTML 页面里包含的 其他资源。因此，每次的请求都会造成无谓的TCP 连接建立和断开，增加通信量的开销。

![image-20251215200828306](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215200828306_Cafqwc.png)

为了解决上述TCP连接问题，提出了持久连接（HTTP Persistent Connectins，也称为HTTP keep-alive或者HTTP Connection reuse）方法。

<font color="red">**持久连接keep-alive**</font>

**特点**：只要任意一端没有明确提出断开连接，就会一直保持TCP连接状态。

**好处**：减少了TCP连接的重复建立和断开造成的额外开销，减轻了服务器端负载。HTTP请求和响应能更早结束，WEB显示速度提高

<font color="red">**管线化pipelining**</font>

持久连接使多数请求以管线化pipelining方式发送成为可能。不用等待响应就可以直接发送下一个请求

## 2.8　使用 Cookie 的状态管理 

HTTP是无状态协议，不对之前发生的请求或响应进行管理。

优点：不保存状态，减少服务器的CPU和内存消耗。

缺点：每次都需要重新请求和响应

矛盾点：如果让服务器管理全部客户端状态会成为极大负担

![image-20251215201916696](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215201916696_twI9tT.png)

解决办法：引入Cookie技术，在请求和响应报文中写入Cookie信息来控制客户端状态

流程：Cookie会根据服务端发送的响应报文中的Set-Cookie的首部字段信息，通知客户端保持cookie。下次客户端再往同一个服务器发送请求时，客户端会自动在请求报文中加入cookie后发送出去。服务器端发现客户端发送来的cookie后，会检查是从哪一个客户端发来的请求，对比服务器上的记录，得到之前的状态信息。

![image-20251215201933843](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215201933843_cJ0zDh.png)

![image-20251215201950228](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215201950228_W4DQ4u.png)

![image-20251215202005501](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215202005501_viirY5.png)

# 第 3 章　HTTP 报文内的 HTTP 信息

HTTP通信包括从客户端发往服务器端的请求，从服务器端返回客户端的响应

了解请求和响应如何运作

## 3.1　HTTP 报文

HTTP报文：用于HTTP协议交互的信息。多行（CR+LF作换行符）数据构成的字符串文本。大致分为：报文首部、报文主体。不一定要有报文主体。

请求报文：请求端（客户端）的HTTP报文

响应报文：响应端（服务器端）的HTTP报文

![image-20251215202341128](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215202341128_hhdrUw.png)

## 3.2　请求报文及响应报文的结构

### 请求报文

![image-20251215202402137](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215202402137_3WiRAT.png)

![image-20251215202434220](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215202434220_MQ9qTE.png)

请求行：包含用于请求的方法。请求URI，HTTP版本

首部字段：包含表示请求/响应的各种条件和属性的各类首部。4种首部：通用、请求、响应和实体首部

其他：可能包含HTTP的RFC中未定义的首部（cookie等）

### 响应报文

状态行：包含表明响应结果的状态码、原因短语、HTTP版本

![image-20251215202414841](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215202414841_JUfh9Z.png)

![image-20251215202444340](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215202444340_zb4lEW.png)

## 3.3　编码提升传输速率

HTTP在传输数据时可按数据原貌直接传输，也可以在传输中通过编码提升传输速率。

在传输时编码，能有效处理大量访问请求。但编码需要计算机完成，会消耗更多CPU资源。

### 报文主体VS实体主体

报文message：HTTP通信中的基本单位。8位组字节流octet sequence，其中octet是8个比特组成，通过HTTP通信传输

实体entity：作为请求/响应的有效载荷数据（补充项）被传输，内容由实体首部和实体主体组成

HTTP报文主体用于传输请求/响应的实体主体。

通常，报文主体=实体主体。只有，传输中使用了编码时，实体主体内容变化，导致它和报文主体不同。

### 压缩传输的内容编码

内容编码指明应用在实体内容上的编码格式，保持实体信息原样压缩。内容编码后的实体由客户端接收并负责解码。

常用内容编码：gzip （GNU zip），compresss （UNIX系统的标准压缩），deflate（zlib），identity（不编码）

### 分割发送的分块传输编码

HTTP通信中，请求的编码实体资源尚未全部传输完成前，浏览器无法显示请求页面。在传输大容量数据时，通过把数据分割成多块，让浏览器逐步显示页面。把实体主体分块的功能➡️分块传输编码Chunked Transfer Coding

![image-20251215203655704](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215203655704_wccqh3.png)

分块传输编码把实体主体分成多块，每块用16进制标记块大小，最后一块用“0（CR+LF）”标记。

## 3.4　发送多种数据的多部分对象集合

![image-20251215203847605](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215203847605_KyzLTp.png)

发邮件时，我们可以写文字并添加多附件，因为采用了MIME（Multipurpose Internet Mail Extensions）机制，允许处理不同类型的数据。MIME中会用一种多部分对象集合Mltipart的方法，容纳多份不同类型的数据。

相应地，HTTP协议中也采纳了多部分对象集合Mltipart的方法，发送一份报文主体内可能含有多类型实体。通常是在图片/文本文件等上传时使用。

多部分对象集合multipart包含的对象：

- multipart/form-data 在WEB表单文件上传时使用

	![image-20251215204309851](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215204309851_BcM3vq.png)

- multipart/byteranges 状态码206（Partial Content部分内容）响应报文包含多个范围等内容时使用

![image-20251215204323612](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215204323612_BKrYn7.png)

![image-20251215204332088](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215204332088_aVOBDk.png)

在 HTTP 报文中使用多部分对象集合时，需要在首部字段里加上 Content-type。

使用 boundary 字符串来划分多部分对象集合指明的各类实体。在 boundary 字符串指定的各个实体的起始行之前插入“--”标记（例如：-AaB03x、--THIS_STRING_SEPARATES），而在多部分对象集合对 应的字符串的最后插入“--”标记（例如：--AaB03x--、-THIS_STRING_SEPARATES--）作为结束。

## 3.5　获取部分内容的范围请求

## 3.6　内容协商返回最合适的内容

# 第 4 章　返回结果的 HTTP 状态码

4.1　状态码告知从服务器端返回的请求结果

4.2　2XX 成功

4.3　3XX 重定向

4.4　4XX 客户端错误

4.5　5XX 服务器错误

# 第 5 章　与 HTTP 协作的 Web 服务器

5.1　用单台虚拟主机实现多个域名

5.2　通信数据转发程序 ：代理、网关、隧道

5.3　保存资源的缓存 

# 第 6 章　HTTP 首部

6.1　HTTP 报文首部

6.2　HTTP 首部字段

6.3　HTTP/1.1 通用首部字段

6.4　请求首部字段

6.5　响应首部字段

6.6　实体首部字段

6.7　为 Cookie 服务的首部字段

6.8　其他首部字段

