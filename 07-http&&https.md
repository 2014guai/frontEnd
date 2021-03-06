# http&&https

## http
* 什么是http
  * 超文本传输协议
* 用途
  * 计算机通过网络进行通信的规则, 是一种无状态的协议, 即不建立持久的连接
* 缺点
  * 明文发送内容, 无数据加密
  * 如果攻击者截取了web浏览器与服务器之间的传输报文, 就可以直接读懂其信息
* 不适用于传输敏感信息, 如: 信用卡号, 密码等支付信息
## https
* 什么是https
  * https是安全的http
  * s代表SSL/TLS协议
* 信息传输安全是什么意思
  * 客户端和服务器直接的通信只有自己能看懂, 即使第三方拿到数据也看不懂这些信息的真实含义
  * 第三方虽然看不懂数据, 但可以XJB改, 因此客户端和服务器必须有能力判断数据是否被修改过
  * 客户端必须避免中间人攻击, 即除了真正的服务器, 任何第三方都无法冒充服务器
    * 目前的http不能满足上述三条的一条
    * 第三个要求可以不用管
* 怎么加密信息
  * 使用对称加密技术
  * 对称加密后, https的握手流程又多了两步
    * 客户端：你好, 我需要发起一个HTTPS请求
    * 服务端：好的, 你的密匙是""
  * 使用对称加密一般要比非对称加密快得多, 对服务器的运算压力小得多
* 对称密匙如何传输
  * 服务器下发的内容不可能被伪造, 因为别人都没有私钥, 所以无法加密。强行加密的后果是客户端用公钥无法解开。
  * 任何人用公钥加密的内容都是绝对安全的, 因为私钥只有服务器有, 也就是只有真正的服务器可以看到被加密的原文。
## http与https的区别
  * https协议需要到ca申请证书, 一般免费证书较少, 因而需要一定费用
  * http是超文本传输协议, 信息是明文传输, https则是具有安全性的ssl加密传输协议
  * http和https使用的是完全不同的连接方式, 用的端口也不一样, 前者是80, 后者是443
  * http的连接很简单, 是无状态的; HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议, 比http协议安全
## URL到界面显示发生了什么
* DNS解析
  * 先本地缓存找，在一层层找
  * 将常见的地址解析成唯一对应的ip地址基本顺序为：
    * 本地域名服务器->根域名服务器->com顶级域名服务器依次类推下去,找到后记录并缓存下来
    * 如www.google.com为`. -> .com -> google.com. -> www.google.com.`
* TCP连接 三次握手，只要没收到确认消息就要重新发
  * 主机向服务器发送一个建立连接的请求（您好，我想认识您）；
  * 服务器接到请求后发送同意连接的信号（好的，很高兴认识您）；
  * 主机接到同意连接的信号后，再次向服务器发送了确认信号（我也很高兴认识您），自此，主机与服务器两者建立了连接。
* 发送HTTP请求
  * 浏览器会分析这个url，并设置好请求报文发出。
  * 请求报文中包括请求行、请求头、空行、请求主体。
  * https默认请求端口443， http默认80。
* 浏览器解析渲染页面
  * 通过HTML解析器解析HTML文档，构建一个DOM Tree，同时通过CSS解析器解析HTML中存在的CSS，构建Style Rules，两者结合形成一个Attachment。
  * 通过Attachment构造出一个呈现树（Render Tree）
  * Render Tree构建完毕，进入到布局阶段（layout/reflow），将会为每个阶段分配一个应出现在屏幕上的确切坐标。
  * 最后将全部的节点遍历绘制出来后，一个页面就展现出来了。遇到script会停下来执行，所以通常把script放在底部
* 连接结束
## 一个普通网站访问的过程
* 简单概括一下，对于我们普通的网站访问，涉及到的技术就是：
  * 用户操作浏览器访问, 浏览器向服务器发出一个HTTP请求
  * 服务器接收到HTTP请求, Web Server进行相应的初步处理, 使用服务器脚本生成页面
  * 服务器脚本(利用Web Framework)调用本地和客户端传来的数据, 生成页面
  * Web Server将生成的页面作为HTTP响应的body, 根据不同的处理结果生成HTTP header, 发回给客户端
  * 客户端(浏览器)接收到HTTP响应, 通常第一个请求得到的HTTP响应的body里是HTML代码, 于是对HTML代码开始解析
  * 解析过程中遇到引用的服务器上的资源(额外的CSS、JS代码、图片、音视频、附件等), 
    再向Web Server发送请求, Web Server找到对应的文件, 发送回来
  * 浏览器解析HTML包含的内容, 用得到的CSS代码进行外观上的进一步渲染, JS代码也可能会对外观进行一定的处理
  * 用户与页面交互（点击，悬停等等）时，JS 代码对此作出一定的反应，添加特效与动画
  * 交互的过程中可能需要向服务器索取或提交额外的数据(局部的刷新，类似微博的新消息通知), 
    一般不是跳转就是通过JS代码(响应某个动作或者定时)向Web Server发送请求, 
    Web Server再用服务器脚本进行处理(生成资源or写入数据之类的), 
    把资源返回给客户端, 客户端用得到的资源来实现动态效果或其他改变
