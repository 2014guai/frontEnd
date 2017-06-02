## ajax
##目录
* [基本认识](#基本认识)
* [ajax的应用](#ajax的应用)
* [比较传统web请求与ajax请求](#比较传统web请求与ajax请求)
* [ajax请求的过程](#ajax请求的过程)
* [readyState](#readyState)
* [后台路由](#后台路由)
* [ajax请求的过程](#ajax请求的过程)
* [ajax跨域请求](#ajax跨域请求)
***

## 基本认识
  * AJAX（Asynchronous JavaScript and XML）
  * 是一种浏览器端不用刷新整个页面就可以与服务器端通信的技术
  * 它不是新技术, 而是一种由多种技术组合的技术
  * 包括Javascript、HTML和CSS、DOM、XML和JSON、XMLHttpRequest
## ajax的应用
  * 检查用户是否可用
  * 三级联动
  * 地图
  * 搜索列表提示
## 比较传统web请求与ajax请求
  * 传统web请求
    * 同步请求: 发2个请求, 只完全完全处理完第1个后, 才能发第2个请求
    * 响应数据: 带数据的页面
    * 谁来发送的请求: 一般的http请求模块
  * ajax请求 :
    * 异步请求: 发2个请求, 可以瞬间将2个请求都发送出去(此时并没有得到响应), 通过监听回调函数来接收响应数据
    * 响应数据: json/xml/html标签数据
    * 谁来发送的请求: ajax引擎模块
## ajax请求的过程
  * 创建xmlhttprequest对象, 并设置用于接收响应数据的监听回调, 并在回调中读取响应数据, 更新局部页面
  * xmlhttprequest.send()发送异步请求
  * ajax接收到这个命令后, 就会发送一个http请求
  * 服务器接收到请求, 对请求进行处理, 并返回一个响应数据(json/xml/html标签)
  * ajax引擎接收到响应数据后的处理:
    * 将响应数据保存到request对象上(responseXML/responseText)
    * 调用request对象的onreadystatechange()
  * ![](/images/ajax请求过程.png)
## readyState
* 0-->UNSENT(初始状态, 未打开), 此时xhr对象被成功构造, open()方法还未被调用 //初始化
* 1-->OPENED(已打开，未发送)open()方法已被成功调用, send()方法还未被调用 //已打开
  * 注意：只有xhr处于OPENED状态, 才能调用`xhr.setRequestHeader()`和`xhr.send()`,
    否则会报错
* 2-->HEADERS_RECEIVED(已获取响应头)send()方法已经被调用, 响应头和响应状态已经返回 //获取响应头
* 3-->LOADING(正在下载响应体)响应体(response entity body)正在下载中 //获取响应体
  * 此状态下通过xhr.response可能已经有了响应数据
* 4-->DONE(整个数据传输过程结束)整个数据传输过程结束, 不管本次请求是成功还是失败 //数据传输完成
## 后台路由
  ```javascript
  router.get/post('path', function(req, res, next){
    //1. 获取请求参数数据
    var xxx = req.query.xxx
    var xxx = req.body.yyy
    //2. 处理数据
        //逻辑处理
    //3. 返回响应数据
    res.end/send/json(result);
  })
  ```
## ajax跨域请求
* 问题说明: 浏览器基于同源策略(安全策略)，不允许跨域请求(ajax)
* 跨域: 协议、域名、端口号, 只要有一个不同就是跨域
* 解决办法
  * jsonp
    * 基本原理:
      * 本质不是ajax请求
      * 动态创建一个<script>, 指定src属性为请求的url, 浏览器会自动发送对url的get类型的一般HTTP请求
      * 服务器接收到请求, 处理请求, 返回是一个函数调用的字符串, 并将数据(json格式)作为实参传入
      * 浏览器接收到响应数据, 解析它, 就会去执行函数调用(之前就已经定义好的一个回调函数)
      * 在回调函数中, 得到返回的json数据, 读取内部数据进行处理
  * cors
    * 服务端, 向响应中添加一个特别的响应头: `'Access-Controll-Allow-Origin':'*'`
    * 存在浏览器兼容的问题
## 前端js模板
  * 作用: 将ajax请求得到数据渲染到提前定义好的标签模板生成html标签结构, 插入到页面的指定标签中
  * 场景: ajax请求返回数据比较大时
  * 优点: 编码简洁, 支行效率高
  * 基本语法: 使用特殊结构({{}})来实现标签与js的嵌套
  * 基本原理: 使用正则表达式匹配: 看到<> 就是标签, 一旦看到{{}}就当作js解析
## 原生ajax
  ```javascript
  var request = new XmlHttpRequest();
  request.onreadystateChange = function(){
      if(request.readyState==4&&request.status==200) {
          var result = request.responeText/XML;
          //更新局部页面
      }
  }
  request.open('POST/GET', url, true/false)
  request.setRequestHeader('Content-Type', '......'); //标识对请求体数据进行编码处理
  request.send(body);
  ```
## jQuery-ajax
```javascript
$.ajax({
  type : 'POST/GET',
  url : 'url',
  data : {}/string,
  success : function(msg){},
  error : function(){},
  dataType : 'json/xml/html'  //响应数据
});
$.get(url, data, function(msg){}, 'json');
$.post(url, data, function(msg){}, 'json');
$.getJSON(url, data, function(msg){});
```
* 跨域请求
  * 编码(jQuery):
    * 浏览器端
        * `$.getJSON('url?callback=?', function(obj/arr){})`
    * 服务器端
        * `var callback = req.query.callback`
        * `var resultJson = '{}/[]';`
        * `res.send(callback+'('+resultJson+')');`
## angular-ajax
* 通过$http服务来实现ajax请求
* 提交get/post请求
```javascript
$http({
  method : 'GET/POST',
  url : '/test',
  params : '参数键值对字符串、对象',
  data : '参数键值对字符串、对象'
})
.success(function(data){
  //将数据保存到scope中
})
.error(function(data){
  //提示错误
})
```
```javascript
$http.get('/get?参数')
.success(function(data){
  //将数据保存到scope中
})
.error(function(data){
  //提示错误
})
``` 
```javascript
$http.post('/get', data)
.success(function(data){
  //将数据保存到scope中
})
.error(function(data){
  //提示错误
})
```
* 跨域请求
  * jsonp解决get请求
    ```javascript
    $http.jsonp('/jsonp?callback=JSON_CALLBACK&name=tom')
    .success(function(data){
      //将数据保存到scope中
    })
    .error(function(data){
      //提示错误
    })
    ```
  * CORS解决post请求
    * 服务端：`res.set('Access-Control-Allow-Origin', '*')`
## react-ajax
* React没有ajax模块, 需要使用其它ajax库
* 一般是在componentDidMount中发送ajax请求, 得到数据后, 更新state
* 可以使用promise的方式
  * promise.then
## vue-ajax
* vue-resource //现在vue停止更新
* vue-axios //推荐使用 