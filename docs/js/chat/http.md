## 前言
http是你无论从事前端还是后端都绕不开的协议，对基础及核心部分的深入学习才是成为一名专业技术人员的前提，以不变应万变才是立足之本；

## 1.了解Web与网络基础；
这章主要概述了一下web是建立在何种技术之上，以及http协议是如何诞生并发展的；
### 1.1 什么是http
我们在使用浏览器的时候，从输入url到页面展示出来，经理了几个阶段 如下  
1、输入网址  
2、DNS解析  
3、建立tcp连接  
4、客户端发送HTPP请求  
5、服务器处理请求　  
6、服务器响应请求  
7、浏览器展示HTML  
8、浏览器发送请求获取其他在HTML中的资源。  
致此，浏览器将会显示网页了，我们今天主要讲一下http，其他的以后再说；  

HTTP协议，即超文本传输协议(Hypertext transfer protocol)。是一种详细规定了浏览器和万维网(WWW = World Wide Web)服务器之间互相通信的规则，通过因特网传送万维网文档的数据传送协议。

HTTP协议作为TCP/IP模型中应用层的协议也不例外。HTTP协议通常承载于TCP协议之上，有时也承载于TLS或SSL协议层之上，这个时候，就成了我们常说的HTTPS。
> 敲黑板！！！ HTTP常被译作 超文本传输协议  其实是不严谨的，严谨的译名 超文本转移协议；
### 1.2 http的诞生
其实http最初是由创始人WWW之父蒂姆·贝纳斯·李（TimBerners—Lee）提出来共享知识的设想，后来WWW联盟（WWW Consortium）成立，组织了IETF（Internet Engineering Task Force）小组进一步完善和发布HTTP协议。90年发布0.9，96年发布1.0，97年发布1.1，2.0还在制定中；
### 1.3 网络基础TCP/IP
为了理解 HTTP，我们有必要事先了解一下 TCP/IP 协议族。
通常使用的网络（包括互联网）是在 TCP/IP 协议族的基础上运作 的。而 HTTP 属于它内部的一个子集。
TCP/IP 协议族里重要的一点就是分层。
TCP/IP 协议族按层次分别分 为以下 4 层：应用层、传输层、网络层和数据链路层。

#### 应用层
应用层决定了向用户提供应用服务时通信的活动。 TCP/IP 协议族内预存了各类通用的应用服务。比如，FTP（File Transfer Protocol，文件传输协议）和 DNS（Domain Name System，域 名系统）服务就是其中两类。 HTTP 协议也处于该层。
#### 传输层
传输层对上层应用层，提供处于网络连接中的两台计算机之间的数据 传输。 在传输层有两个性质不同的协议：TCP（Transmission Control Protocol，传输控制协议）和 UDP（User Data Protocol，用户数据报 协议）。
#### 网络层
网络层（又名网络互连层） 网络层用来处理在网络上流动的数据包。数据包是网络传输的最小数 据单位。该层规定了通过怎样的路径（所谓的传输路线）到达对方计 算机，并把数据包传送给对方。
#### 数据链路层
链路层（又名数据链路层，网络接口层） 用来处理连接网络的硬件部分。包括控制操作系统、硬件的设备驱 动、NIC（Network Interface Card，网络适配器，即网卡），及光纤等 物理可见部分（还包括连接器等一切传输媒介）。硬件上的范畴均在 链路层的作用范围之内。
举个例子
* 我想看个某个网页，这时我会发起想看某个网页的一个请求，这是应用层；
* 接着，为了传输方便，在传输层（TCP 协议）把从应用层处收到的数 据（HTTP 请求报文）进行分割，并在各个报文上打上标记序号及端 口号后转发给网络层。这是传输层；
* 在网络层（IP 协议），增加作为通信目的地的 MAC 地址后转发给链 路层。这样一来，发往网络的通信请求就准备齐全了。

接收端的服务器在链路层接收到数据，按序往上层发送，一直到应用 层。当传输到应用层，才能算真正接收到由客户端发送过来的 HTTP 请求。

发送端在层与层之间传输数据时，每经过一层时必定会被打上一个该层所属的首部信息。反之，接收端在层与层传输数据时，每经过一层 时会把对应的首部消去。 这种把数据信息包装起来的做法称为封装（encapsulate）。

# http1.0/1.1
## 缓存
http1.0缓存主要用了If-Modified-Since,Expires，而1.1加入了Entity tag，If-Unmodified-Since, If-Match，If-None-Match等
## 带宽优化及网络连接的使用
HTTP1.0中，存在一些浪费带宽的现象，例如客户端只是需要某个对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能，HTTP1.1则在请求头引入了range头域，它允许只请求资源的某个部分，即返回码是206（Partial Content），这样就方便了开发者自由的选择以便于充分利用带宽和连接。
## 错误通知的管理
在HTTP1.1中新增了24个错误状态响应码，如409（Conflict）表示请求的资源与资源的当前状态发生冲突；410（Gone）表示服务器上的某个资源被永久性的删除。
## Host头处理
在HTTP1.0中认为每台服务器都绑定一个唯一的IP地址，因此，请求消息中的URL并没有传递主机名（hostname）。但随着虚拟主机技术的发展，在一台物理服务器上可以存在多个虚拟主机（Multi-homed Web Servers），并且它们共享一个IP地址。HTTP1.1的请求消息和响应消息都应支持Host头域，且请求消息中如果没有Host头域会报告一个错误（400 Bad Request）。
## 长连接
HTTP 1.1支持长连接（PersistentConnection）和请求的流水线（Pipelining）处理，在一个TCP连接上可以传送多个HTTP请求和响应，减少了建立和关闭连接的消耗和延迟，在HTTP1.1中默认开启Connection： keep-alive，一定程度上弥补了HTTP1.0每次请求都要创建连接的缺点。
## 新增
HTTP1.1增加了OPTIONS, PUT, DELETE, TRACE, CONNECT这些Request方法.

## 1.x的缺点
* 只允许一次发送一个请求，会出现阻塞问题；
* 单向请求；
* 请求响应头信息冗余量大；
* 数据未压缩；

# HTTP2.0
## 二进制分帧传输；
2.0为了突破HTTP1.1的性能限制，改进传输性能，实现低延迟高吞吐量在应用层（HTTP）和传输层（TCP）之间增加一个二进制分帧层。  
2.0中引入了新的编码机制，所有传输的数据都会被分割，并采用二进制格式编码。
## 首部压缩
2.0使用了HPACK（HTTP2头部压缩算法）压缩格式对传输的header进行编码，减少了header的大小。并在两端维护了索引表，用于记录出现过的header，后面在传输过程中就可以传输已经记录过的header的键名，对端收到数据后就可以通过键名找到对应的值。
## 多路复用
2.0中,基于二进制分帧层，HTTP2.0可以在共享TCP连接的基础上同时发送请求和响应。HTTP消息被分解为独立的帧，而不破坏消息本身的语义，交错发出去，在另一端根据流标识符和首部将他们重新组装起来。 通过该技术，可以避免HTTP旧版本的队头阻塞问题，极大提高传输性能。
## 请求优先级
把HTTP消息分为很多独立帧之后，就可以通过优化这些帧的交错和传输顺序进一步优化性能。
## 服务器推送
。在HTTP2.0中，服务器可以对一个客户端的请求发送多个响应。如果一个请求是由你的主页发送的，服务器可能会响应主页内容、logo以及样式表，因为他知道客户端会用到这些东西。这样不但减轻了数据传送冗余步骤，也加快了页面响应的速度，提高了用户体验。

推送的缺点：所有推送的资源都必须遵守同源策略。换句话说，服务器不能随便将第三方资源推送给客户端，而必须是经过双方的确认才行。

## 2.0的缺点
* 建立连接时间长(本质上是TCP的问题)
* 队头阻塞问题
* 移动互联网领域表现不佳(弱网环境)


# HTTP3.0

网络环境的改变速度很快，但是TCP协议相对缓慢，正是这种矛盾促使谷歌做出了一个看似出乎意料的决定-基于UDP来开发新一代HTTP协议。

我们单纯地看看TCP协议的不足和UDP的一些优点：

* 基于TCP开发的设备和协议非常多，兼容困难
* TCP协议栈是Linux内部的重要部分，修改和升级成本很大
* UDP本身是无连接的、没有建链和拆链成本
* UDP的数据包无队头阻塞问题
* UDP改造成本小
从上面的对比可以知道，谷歌要想从TCP上进行改造升级绝非易事，但是UDP虽然没有TCP为了保证可靠连接而引发的问题，但是UDP本身不可靠，又不能直接用。
谷歌决定在UDP基础上改造一个具备TCP协议优点的新协议也就顺理成章了，这个新协议就是QUIC协议。

## QUIC协议和HTTP3.0
QUIC其实是Quick UDP Internet Connections的缩写，直译为快速UDP互联网连接。

### 机制一：自定义连接机制
一条tcp连接是由四元组标识的，分别是源ip、源端口、目的端口，一旦一个元素发生变化时，就会断开重连，重新连接。在次进行三次握手，导致一定的延时
在TCP是没有办法的，但是基于UDP，就可以在QUIC自己的逻辑里面维护连接的机制，不再以四元组标识，而是以一个64
位的随机数作为ID来标识，而且UDP是无连接的，所以当ip或者端口变化的时候，只要ID不变，就不需要重新建立连接

### 机制二：自定义重传机制
tcp为了保证可靠性，通过使用序号和应答机制，来解决顺序问题和丢包问题
任何一个序号的包发过去，都要在一定的时间内得到应答，否则一旦超时，就会重发这个序号的包，通过自适应重传算法（通过采样往返时间RTT不断调整）

但是，在TCP里面超时的采样存在不准确的问题。例如发送一个包，序号100，发现没有返回，于是在发送一个100，过一阵返回ACK101.客户端收到了，但是往返的时间是多少，没法计算。是ACK到达的时候减去第一还是第二。

QUIC也有个序列号，是递增的，任何宇哥序列号的包只发送一次，下次就要加1，那样就计算可以准确了

但是有一个问题，就是怎么知道包100和包101发送的是同样的内容呢？quic定义了一个offset概念。QUIC既然是面向连接的，也就像TCP一样，是一个数据流，发送的数据在这个数据流里面有个偏移量offset，可以通过offset查看数据发送到了那里，这样只有这个offset的包没有来，就要重发。如果来了，按照offset拼接，还是能够拼成一个流。

 
### 机制三： 无阻塞的多路复用
有了自定义的连接和重传机制，就可以解决上面HTTP2.0的多路复用问题

同HTTP2.0一样，同一条 QUIC连接上可以创建多个stream，来发送多个HTTP请求，但是，QUIC是基于UDP的，一个连接上的多个stream之间没有依赖。这样，假如stream2丢了一个UDP包，后面跟着stream3的一个UDP包，虽然stream2的那个包需要重新传，但是stream3的包无需等待，就可以发给用户。

### 机制四：自定义流量控制
TCP的流量控制是通过滑动窗口协议。QUIC的流量控制也是通过window_update，来告诉对端它可以接受的字节数。但是QUIC的窗口是适应自己的多路复用机制的，不但在一个连接上控制窗口，还在一个连接中的每个steam控制窗口。

在TCP协议中，接收端的窗口的起始点是下一个要接收并且ACK的包，即便后来的包都到了，放在缓存里面，窗口也不能右移，因为TCP的ACK机制是基于序列号的累计应答，一旦ACK了一个序列号，就说明前面的都到了，所以是要前面的没到，后面的到了也不能ACK,就会导致后面的到了，也有可能超时重传，浪费带宽

QUIC的ACK是基于offset的，每个offset的包来了，进了缓存，就可以应答，应答后就不会重发，中间的空档会等待到来或者重发，而窗口的起始位置为当前收到的最大offset，从这个offset到当前的stream所能容纳的最大缓存，是真正的窗口的大小，显然，那样更加准确。

# https
## 什么是https
HTTP+SSL/TLS，通过 SSL证书来验证服务器的身份，并为浏览器和服务器之间的通信进行加密。
## https的过程
* 首先客户端通过URL访问服务器建立SSL连接。
* 服务端收到客户端请求后，会将网站支持的证书信息（证书中包含公钥）传送一份给客户端。
* 客户端的服务器开始协商SSL连接的安全等级，也就是信息加密的等级。
* 客户端的浏览器根据双方同意的安全等级，建立会话密钥，然后利用网站的公钥将会话密钥加密，并传送给网站。
* 服务器利用自己的私钥解密出会话密钥。
* 服务器利用会话密钥加密与客户端之间的通信。

## https的缺点
* HTTPS协议多次握手，导致页面的加载时间延长近50%；
* HTTPS连接缓存不如HTTP高效，会增加数据开销和功耗；
* 申请SSL证书需要钱，功能越强大的证书费用越高。
* SSL涉及到的安全算法会消耗 CPU 资源，对服务器资源消耗较大。


# HTTPS和HTTP的区别

* HTTP协议运行在TCP之上，所有传输的内容都是明文，HTTPS运行在SSL/TLS之上，SSL/TLS运行在TCP之上，所有传输的内容都经过加密的。
* HTTP和HTTPS使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。
* HTTPS可以有效的防止运营商劫持，解决了防劫持的一个大问题。
* HTTP在OSI网络模型中是在应用层，而HTTPS的TLS是在传输层
* HTTP是无状态的，HTTPS是有状态的
* 连接方式不同，HTTP三次握手，HTTPS中TLS1.2版本7次，TLS1.3版本6次
