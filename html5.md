	

## html5
* 浅析
	* hmtl：超文本标记语言
	* hmtl5：w3c对html的第五次修改
* 新特性：
1. 语义化标签：
* 新增：section-文章、nav-导航、aside-侧边栏
* 作用：
	* 对SEO友好
	* 技术趋势，更符合w3c标准
	* 没有样式时，浏览器的默认样式也能让页面结构清晰
	* 对功能障碍用户(残障用户)友好
	* 对其他非主流终端设备友好，移动端、机顶盒等
* 实例：
	* 一个常见的html5，经典页面设计
	[![](/images/layout.png "html5经典页面设计")][layout]
2. 离线缓存
* localStorage：本地离线缓存，长期储存数据，浏览器关闭后数据不会丢失
* sessionStorage：浏览器关闭后数据自动删除
	* 四种离线储存
		* cookie：服务器端生成，储存在浏览器；生命周期：服务器设置的时间
		* httpsession：纯服务器储存
		* localStorage：浏览器生成，储存在浏览器；生命周期：在页面关闭前
		* sessionStorage：浏览器生成，储存在浏览器；生命周期：永久，直到用户主动删除
3. 表单控件
* input的type属性更多样化，如：data，time，email，url，search
* input的属性
	* required：必须填写的input
	* autofocus：页面加载后，自动获取焦点
	* pattern：验证输入字段(可以直接使用正则表达式)
4. 音频、视频api
* audio，video
5. 画布api
* canvas
6. 地理api
7. 拖拽释放
8. 新的技术：webworker、websocket、geolocation
* 移除的标签
* 纯表现的元素：basefont，big，center，font, s，strike，tt，u；
* 对可用性产生负面影响的元素：frame，frameset，noframes；
* 兼容
* IE8/IE7/IE6支持通过 document.createElement 方法产生的标签，
	可以利用这一特性让这些浏览器支持 HTML5 新标签，
	浏览器支持新标签后，还需要添加标签默认的样式
* 当然最好的方式是直接使用成熟的框架、使用最多的是html5shim框架：
````
	<!--[if lt IE 9]>
		<script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
	<![endif]-->
````
* hmtl页面加载和解析过程：
* 输入网址，浏览器向服务器发送请求，服务器返回一个html文件
* 浏览器加载html，发现<head>标签的内的link标签引入外部文件
* 浏览器又发出请求css文件请求，服务器返回css文件
* 浏览器继续加载html中<body>部分的代码，并且css文件已经拿到，开始渲染页面
* 浏览器在代码中发现img标签引入一张图片，向浏览器发送请求。
	浏览器不会等到图片下载完，而是继续渲染后面的代码
* 服务器返回图片文件，由于图片占用了位置，影响后面代码排布，因此浏览器需要回过头来重新渲染这部分代码
* 浏览器发现<script>标签，运行javascript代码
* 执行js代码过程中，它命令浏览器隐藏某个div，浏览器必须重新渲染这部分代码
* 最后运行到</html>，页面第一次加载全部完成
	用户交互等行为，将重新渲染页面


