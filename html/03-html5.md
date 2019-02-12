	

# html5
## 概述
* hmtl：超文本标记语言
* hmtl5：w3c对html的第五次修改
## 目录
* [概述](#概述)
* [新特性](#新特性)
	* [语义化标签](#语义化标签)
	* [离线缓存](#离线缓存)
	* [表单控件](#表单控件)
	* [新增api](#新增api)
* [移除的标签](#移除的标签)
* [兼容](#兼容)
***

## 新特性：
### 语义化标签：
* 新增：`section`-文章、`nav`-导航、`aside`-侧边栏
* 作用：
	* 对SEO友好
	* 技术趋势, 更符合w3c标准
	* 没有样式时, 浏览器的默认样式也能让页面结构清晰
	* 对功能障碍用户(残障用户)友好
	* 对其他非主流终端设备友好, 移动端、机顶盒等
	![](/images/layout.png "html5经典页面设计")
* 注意：
    * 尽可能少的使用无语义的标签div和span；
    * 需要强调的文本，可以包含在strong或者em标签中，strong默认样式是加粗（不要用b），em是斜体（不用i）；
    * 使用表格时，标题要用caption，表头用thead，主体部分用tbody包围，尾部用tfoot包围。表头和一般单元格要区分开，表头用th，单元格用td；
    * 表单域要用fieldset标签包起来，并用legend标签说明表单的用途；
    * 每个input标签对应的说明文本都需要使用label标签，并且通过为input设置id属性，在lable标签中设置for=someld来让说明文本和相对应的input关联起来。
    ![](/images/html5-label.jpg "html5标签")
### 离线缓存
* localStorage：本地离线缓存, 长期储存数据, 浏览器关闭后数据不会丢失
* sessionStorage：浏览器关闭后数据自动删除
* 四种离线储存的比较：
	* `cookie`：服务器端生成, 储存在浏览器; 生命周期：服务器设置的时间
	* `httpsession`：纯服务器储存
	* `localStorage`：浏览器生成, 储存在浏览器; 生命周期：在页面关闭前
	* `sessionStorage`：浏览器生成, 储存在浏览器; 生命周期：永久, 直到用户主动删除
### 表单控件
* input的type属性更多样化, 如：`data`, `time`, `email`, `url`, `search`
* input的属性
	* `required`：必须填写的input
	* `autofocus`：页面加载后, 自动获取焦点
	* `pattern`：验证输入字段(可以直接使用正则表达式)
### 音频、视频api
* audio, video
### 画布api
* canvas
### 地理api
### 拖拽释放
### 新的技术
* webworker
* websocket
* geolocation
## 移除的标签
* 纯表现的元素：basefont, big, center, font, s, strike, tt, u；
* 对可用性产生负面影响的元素：frame, frameset, noframes
## 兼容
* IE8/IE7/IE6支持通过 `document.createElement` 方法产生的标签,          
	可以利用这一特性让这些浏览器支持 HTML5 新标签,         
	浏览器支持新标签后, 还需要添加标签默认的样式         
* 当然最好的方式是直接使用成熟的框架、使用最多的是`html5shim`框架：
````
	// CND引入html5shim框架
	<!--[if lt IE 9]>
		<script src="http://cdn.static.runoob.com/libs/html5shiv/3.7/html5shiv.min.js"></script>
	<![endif]-->
````



