# HTML基础

## SEO

1. 定义：Search Engine Optimization，**搜索引擎优化**。了解搜索引擎自然排名机制的基础上，对网站进行内部及外部的调整优化，改进网站在搜索引擎中的关键词自然排名，获得更多流量，从而达到网站销售及品牌建设的目标。简单来说，就是网站排名技术。
2. 合理的title、description、keywords：搜索对着三项的权重逐个减小，title值强调重点即可，重要关键词出现不要超过2次，而且要靠前，不同页面title要有所不同；description把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面description有所不同；keywords列举出重要关键词即可。
3. **语义化**的HTML代码，符合W3C规范：语义化代码让搜索引擎容易理解网页
4. 重要内容HTML代码放在最前：搜索引擎抓取HTML顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取
5. 重要内容不要用js输出：爬虫不会执行js获取内容
6. 少用**iframe**：搜索引擎不会抓取iframe中的内容
7. 非装饰性图片必须**加alt**
8. 提高网站速度：网站速度是搜索引擎排序的一个重要指标



## 会话跟踪

1. 会话跟踪技术用来**跟踪用户的整个会话**。常用的是Cookie和Session。还有url重写xml，隐藏input，ip地址。
2. Cookie：在HTTP协议下，服务器或脚本可以维护客户工作站上信息的一种方式。是由web服务器保存在用户浏览器上的小文本文件，可以包含有关用户的信息。当用户访问服务器时，服务器可以设置和访问Cookie的信息。Cookie利用了网页代码中的HTTP头信息进行传递的，浏览器的每一次网页请求，都可以伴随Cookie传递。
3. Cookie机制：一个用户的所有请求操作都应该属于同一个会话。因为HTTP协议是无状态协议，一旦数据交换完成，连接就会关闭，再次交换需要建立新的连接，因此无法跟踪会话。。

​                           Cookie实际上是一小段的文本信息。客户端请求服务器，如果服务器需要记录该用户状态，就使用response向客户端浏览器颁发一个Cookie。客户端浏览器会把Cookie保存起来。当浏览器再请求该网站时，浏览器把请求的网址连同该Cookie一同提交给服务器。服务器检查该Cookie，以此来辨认用户状态。服务器还可以根据需要修改Cookie的内容。

[参考](https://zhuanlan.zhihu.com/p/32836762)

1. Session：session是一种保存上下文信息的机制，保存在服务器端的标示，通过SessionID来区分不同的客户，以cookie或URL重写为基础的，默认使用cookie来实现。系统会创造一个名为JSESSIONID的输出cookie，我们叫做session cookie,注意session cookie是存储于浏览器内存中的，并不是写到硬盘上的，我们通常情况是看不到JSESSIONID的，但是把浏览器的cookie禁止后，web服务器会采用URL重写的方式传递Sessionid，就可以在地址栏看到 sessionid=KWJHUG6JJM65HS2K6之类的字符串。session cookie针对某一次会话而言，会话结束session cookie也就随着消失了，而persistent cookie（cookie）只是存在于客户端硬盘上的一段文本（通常是加密的），而且可能会遭到cookie欺骗以及针对cookie的跨站脚本攻击，自然不如 session cookie安全了。

[参考](http://www.cnblogs.com/xulb597/archive/2012/07/02/2573252.html)



## `<img>`的title和alt的区别

1. title：鼠标滑过元素时显示信息，加强用户体验
2. alt：当图片无法正确显示的时候起到文本代替的功能，除了纯装饰的图片都要设置有意义的值，**搜索引擎也会重点分析**



## doctype

1. `<!doctype>`声明必须处于HTML文档的头部，在`<html>`标签之前，HTML5中不区分大小写
2. `<!doctype>`声明不是一个HTML标签，是一个用于告诉浏览器当前HTMl版本的指令
3. 现代浏览器的html布局引擎通过检查doctype决定使用兼容模式还是标准模式对文档进行渲染，一些浏览器有一个接近标准模型



## web语义化，有什么好处

1. 定义：web语义化是指用恰当语义的html标签，css命名表示页面包含的信息，让页面具有更好的结构和含义，从而让人和机器都能**快速理解**网页内容。

​                HTML标签的语义化：通过使用包含语义的标签（如h1-h6）恰当地表示文档结构。css命名的语义化：为HTML标签添加有意义的class，id补充。

1. 好处：1. 有利于SEO，使搜索引擎能更好的理解页面

   ​            2. 页面结构清晰，可读性，可维护性高



## 从浏览器地址栏输入url到显示页面的步骤

1. 在浏览器地址栏输入URL
2. 浏览器查看**缓存**，如果请求资源在缓存中且新鲜直接提供给客户端，否则与服务器进行验证。
   - 检验是否新鲜通常由两个HTTP头控制，Expires和Cache-Control：
     - Expires为一个绝对事件表示缓存有效日期
     - Cache-Control: max-age=,值为以秒为单位的最大有效时间
3. 浏览器**解析**URL获取协议，主机，端口，path
4. 浏览器**组装一个HTTP（GET）请求报文**
5. 浏览器获取主机ip地址，过程：
   - 浏览器缓存
   - 本机缓存
   - hosts文件
   - 路由器缓存
   - ISP DNS缓存
   - DNS递归查询（可能存在负载均衡导致每次IP不一样）
6. **打开一个soctket与目标IP地址，建立TCP链接**，三次握手：
   - 客户端发送一个TCP的**SYN=1，Seq=X**的包到服务器端口
   - 服务器发回**SYN=1， ACK=X+1， Seq=Y**的响应包
   - 客户端发送**ACK=Y+1， Seq=Z**
7. TCP链接建立后**发送HTTP请求**
8. 服务器接受请求并解析，将请求转发到服务程序
9. 服务器检查**HTTP请求头是否包含缓存验证信息**如果验证缓存新鲜，返回304对应状态码
10. 处理程序读取完整请求并准备HTTP响应，可能需要查询数据库等操作
11. 服务器将**响应报文通过TCP连接发送回浏览器**
12. 浏览器接收HTTP响应，然后根据情况选择关闭TCP连接或者保留重用，关闭TCP四次握手如下：
    - 主动方发送**Fin=1， Ack=Z， Seq= X**报文
    - 被动方发送**ACK=X+1， Seq=Z**报文
    - 被动方发送**Fin=1， ACK=X， Seq=Y**报文
    - 主动方发送**ACK=Y， Seq=X**报文
13. 浏览器检查响应状态吗：是否为1XX，3XX， 4XX， 5XX，这些情况处理与2XX不同
14. 如果资源可缓存，进行缓存
15. 对响应进行解码（例如gzip压缩）
16. 根据资源类型决定如何处理（假设资源为HTML文档）
17. **解析HTML文档，构件DOM树，下载资源，构造CSSOM树，执行js脚本**，这些操作没有严格的先后顺序，以下分别解释
18. 构建DOM树：
    - 根据HTML规范将字符流解析为标记
    - 词法分析将标记转换为对象并定义属性和规则
    - 根据HTML标记关系将对象组成DOM树
19. 解析过程中遇到图片、样式表、js文件，启动下载
20. 构建CSSOM树：
    - 字符流转换为标记流
    - 根据标记创建节点
    - 节点创建CSSOM树
21. 根据DOM树和CSSOM树构建渲染树:
    - 从DOM树的根节点遍历所有**可见节点**，不可见节点包括：1）`script`,`meta`这样本身不可见的标签。2)被css隐藏的节点，如`display: none`
    - 对每一个可见节点，找到恰当的CSSOM规则并应用
    - 发布可视节点的内容和计算样式
22. JS解析过程：
    - 浏览器创建Document对象并解析HTML，将解析到的元素和文本节点添加到文档中，此时**document.readystate为loading**
    - HTML解析器遇到**没有async和defer的script时**，将他们添加到文档中，然后执行行内或外部脚本。这些脚本会同步执行，并且在脚本下载和执行时解析器会暂停。这样就可以用document.write()把文本插入到输入流中。**同步脚本经常简单定义函数和注册事件处理程序，他们可以遍历和操作script和他们之前的文档内容**
    - 当解析器遇到设置了**async**属性的script时，开始下载脚本并继续解析文档。脚本会在它**下载完成后尽快执行**，但是**解析器不会停下来等它下载**。异步脚本**禁止使用document.write()**，它们可以访问自己script和之前的文档元素
    - 当文档完成解析，document.readState变成interactive
    - 所有**defer**脚本会**按照在文档出现的顺序执行**，延迟脚本**能访问完整文档树**，禁止使用document.write()
    - 浏览器**在Document对象上触发DOMContentLoaded事件**
    - 此时文档完全解析完成，浏览器可能还在等待如图片等内容加载，等这些**内容完成载入并且所有异步脚本完成载入和执行**，document.readState变为complete,window触发load事件
23. 显示页面



## HTTP报文结构

1. repuest请求报文：首行是**Request-Line**包括：**请求方法**，**请求URI**，**协议版本**，**CRLF**。首行之后是若干行**请求头**，包括**general-header**，**request-header**或者**entity-header**，每个一行以CRLF结束。请求头和消息实体之间有一个**CRLF分隔**。根据实际请求需要可能包含一个**消息实体**

方法：

- GET -- 从服务器获取一份文档 
- HEAD -- 只从服务器获取文档的首部 
- POST -- 向服务器发送所需处理的数据 
- PUT -- 将请求的主体存储在服务器上 
- DELETE -- 从服务器上删除一份文档 
- OPTIONS -- 决定可以在服务器上执行的哪些方法

1. response响应报文：首行是状态行包括：**HTTP版本，状态码，状态描述**，后面跟一个CRLF。首行之后是**若干行响应头**，包括：**通用头部，响应头部，实体头部**。响应头部和响应实体之间用**一个CRLF空行**分隔。最后是一个可能的**消息实体**。

状态码分类： 

- 1XX：信息状态码
  - **100 Continue**：客户端应当继续发送请求。这个临时相应是用来通知客户端它的部分请求已经被服务器接收，且仍未被拒绝。客户端应当继续发送请求的剩余部分，或者如果请求已经完成，忽略这个响应。服务器必须在请求万仇向客户端发送一个最终响应
  - **101 Switching Protocols**：服务器已经理解力客户端的请求，并将通过Upgrade消息头通知客户端采用不同的协议来完成这个请求。在发送完这个响应最后的空行后，服务器将会切换到Upgrade消息头中定义的那些协议。
- 2XX：成功状态码
  - **200 OK**：请求成功，请求所希望的响应头或数据体将随此响应返回
  - **201 Created**：
  - **202 Accepted**：
  - **203 Non-Authoritative Information**：
  - **204 No Content**：
  - **205 Reset Content**：
  - **206 Partial Content**：
- 3XX：重定向
  - **300 Multiple Choices**：
  - **301 Moved Permanently**：
  - **302 Found**：
  - **303 See Other**：
  - **304 Not Modified**：
  - **305 Use Proxy**：
  - **306 （unused）**：
  - **307 Temporary Redirect**：
- 4XX：客户端错误
  - **400 Bad Request**:
  - **401 Unauthorized**:
  - **402 Payment Required**:
  - **403 Forbidden**:
  - **404 Not Found**:
  - **405 Method Not Allowed**:
  - **406 Not Acceptable**:
  - **407 Proxy Authentication Required**:
  - **408 Request Timeout**:
  - **409 Conflict**:
  - **410 Gone**:
  - **411 Length Required**:
  - **412 Precondition Failed**:
  - **413 Request Entity Too Large**:
  - **414 Request-URI Too Long**:
  - **415 Unsupported Media Type**:
  - **416 Requested Range Not Satisfiable**:
  - **417 Expectation Failed**:
- 5XX: 服务器错误
  - **500 Internal Server Error**:
  - **501 Not Implemented**:
  - **502 Bad Gateway**:
  - **503 Service Unavailable**:
  - **504 Gateway Timeout**:
  - **505 HTTP Version Not Supported**:



## 渐进增强

1. 渐进增强：保证所有人都能访问页面的基本内容和功能同时为高级浏览器和高带宽用户提供更好的用户体验。核心原则如下: 

- 所有浏览器都必须能访问基本内容
- 所有浏览器都必须能使用基本功能
- 所有内容都包含在语义化标签中
- 通过外部CSS提供增强的布局
- 通过非侵入式、外部javascript提供增强功能



## 网站性能优化

1. 目的：

- 从用户角度而言，优化能够让页面加载得更快、对用户的操作响应得更及时，能够给用户提供更为友好的体验。
- 从服务商角度而言，优化能够减少页面请求数、或者减小请求所占带宽，能够节省可观的资源。

1. 方法：

-  content方面
  1. 减少HTTP请求：合并文件、CSS精灵、inline Image、合理设置 HTTP缓存
  2. 减少DNS查询：DNS查询完成之前浏览器不能从这个主机下载任何任何文件。方法：DNS缓存、将资源分布到恰当数量的主机名，平衡并行下载和DNS查询
  3. 避免重定向：多余的中间访问
  4. 使Ajax可缓存
  5. 非必须组件延迟加载
  6. 未来所需组件预加载
  7. 减少DOM元素数量
  8. 将资源放到不同的域下：浏览器同时从一个域下载资源的数目有限，增加域可以提高并行下载量
  9. 减少iframe数量
  10. 不要404
- Server方面
  1. 使用CDN
  2. 添加Expires或者Cache-Control响应头
  3. 对组件使用Gzip压缩
  4. 配置ETag
  5. Flush Buffer Early
  6. Ajax使用GET进行请求
  7. 避免空src的img标签
- Cookie方面
  1. 减小cookie大小
  2. 引入资源的域名不要包含cookie
- css方面
  1. 将样式表放到页面顶部
  2. 不使用CSS表达式
  3. 使用不使用[*@*import](https://lark.alipay.com/import)
  4. 不使用IE的Filter
- Javascript方面
  1. 将脚本放到页面底部
  2. 将javascript和css从外部引入
  3. 压缩javascript和css
  4. 删除不需要的脚本
  5. 减少DOM访问
  6. 合理设计事件监听器
- 图片方面
  1. 优化图片：根据实际颜色需要选择色深、压缩
  2. 优化css精灵
  3. 不要在HTML中拉伸图片
  4. 保证favicon.ico小并且可缓存
- 移动方面
  1. 保证组件小于25k
  2. Pack Components into a Multipart Document

 

 





