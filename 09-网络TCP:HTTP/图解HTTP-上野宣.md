# 图解HTTP —— 上野宣

# 第 1 章　了解 Web 及网络基础

## 1.1　使用 HTTP 协议访问 Web

**流程**：在Web浏览器地址栏中输入制定URL，Web浏览器会从Web服务器获取文件资源resource等信息，从而显示出Web页面

客户端**client**：通过==发送请求获取服务器资源==的Web浏览器

![image-20251215172517735](https://raw.githubusercontent.com/iriszhang1121/images/master/uPic/image-20251215172517735_OwBQWM.png)

Web使用HTTP（HyperText Transfer Protocol, 超文本传输协议）作为规范，完成从客户端到服务器的一系列运作流程。$\Rightarrow$ Web是建立在HTTP协议上进行通信的。

> 协议：约定的规则

## 1.2　HTTP 的诞生

1989年3月，HTTP诞生。最初设想：借助多文档间相互关联形成超文本HperText，连成可以相互参阅的World Wide Web。

现在已提出**==3项WWW构建技术==**：把Standard Generalized Markup Language标准通用标记语言SGML作为**页面的文本标记语言**的**HTML**（HyperText Markup Language，超文本标记语言）； 作为**文档传递协议**的**HTTP**；**指定文档所在地址**的**URL**（Uniform Resource Locator，统一资源定位符）。

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

**==应用层==**：决定向用户提供应用服务时的通信活动。（FTP、DNS、HTTP...）

**==传输层==**：对应用层，提供处于网络连接中的两台计算机之间的**数据传输**。（TCP、 UDP）

**==网络层==**：选择**传输线路**并处理在网络上流动的**数据包**。数据包：网络传输的最小数据单位。规定了通过怎样的路径（传输路线）到达对方计算机，并将数据包传送给对方。

**==链路层==**：处理连接网络的**硬件**部分。包括控制操作系统、硬件的设备驱动，NIC（Network Interface Card，网络适配器，即网卡），及光纤等物理可见部分（还包括连接器等一切传输媒介）。

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



## 2.2　通过请求和响应的交换达成通信

## 2.3　HTTP 是不保存状态的协议

## 2.4　请求 URI 定位资源

## 2.5　告知服务器意图的 HTTP 方法

## 2.6　使用方法下达命令

## 2.7　持久连接节省通信量

## 2.8　使用 Cookie 的状态管理 

# 第 3 章　HTTP 报文内的 HTTP 信息

3.1　HTTP 报文

3.2　请求报文及响应报文的结构

3.3　编码提升传输速率

3.4　发送多种数据的多部分对象集合

3.5　获取部分内容的范围请求

3.6　内容协商返回最合适的内容 

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

# 第 7 章　确保 Web 安全的 HTTPS

7.1　HTTP 的缺点

7.2　HTTP+ 加密 + 认证 + 完整性保护 =HTTPS 

# 第 8 章　确认访问用户身份的认证

8.1　何为认证

8.2　BASIC 认证

8.3　DIGEST 认证

8.4　SSL 客户端认证

8.5　基于表单认证

# 第 9 章　基于 HTTP 的功能追加协议

9.1　基于 HTTP 的协议

9.2　消除 HTTP 瓶颈的 SPDY

9.3　使用浏览器进行全双工通信的 WebSocket

9.4　期盼已久的 HTTP/2.0

9.5　Web 服务器管理文件的 WebDAV 

# 第 10 章　构建 Web 内容的技术

10.1　HTML

10.2　动态 HTML

10.3　Web 应用

10.4　数据发布的格式及语言 

# 第 11 章　Web 的攻击技术

11.1　针对 Web 的攻击技术

11.2　因输出值转义不完全引发的安全漏洞

11.3　因设置或设计上的缺陷引发的安全漏洞

11.4　因会话管理疏忽引发的安全漏洞

11.5　其他安全漏洞