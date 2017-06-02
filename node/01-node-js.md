# node.js
## 目录
* [url](#url)
* [fs](#fs)
* [路由](#路由)
* [express4.0](#express4.0)
  * [express的路由](#express的路由)
  * [ejs](#ejs)
* [get与post的区别](#get与post的区别)
***

## url
* 示例：http://www.atguigu.com:80/abc/efg?name1=value1&name2=value2#title
* DNS: 域名与IP地址之间的映射
* 端口号：1024-49151, web服务：80
* 请求报文
  * 两部分：
    * 请求头
      * 请求方法
      * url
      * 首部字段：cookie 
    * 空行
    * 请求体
  * 请求方法 (需要知道5种，重要的2种)
    * get --> 查询
    * post --> 增加
    * put --> 修改
    * delete --> 删除
    * head --> 索要响应头
* 响应报文
  * 两部分：
    * 响应头
      * 状态码
      * 状态原因
      * 首部字段
    * 空行分隔
    * 响应体
  * 状态码：5大类
   * 200 
   * 3XX
   * 404
   * 500 
## fs
* 定义：模块是文件操作的封装, 它提供了文件的读取、写入、更名、删除、遍历目录等操作
* 常用API
 * 读
   * `fs.readFile(filename,callback(err,data));`
   * `fs.readFileSync(filename, [encoding]);`
 * 写
   * `fs.writeFile(file, data, callback);`
   * `fs.writeFileSync(file, data[, options]);`
 *同步与异步
## 路由
* 定义：一个文件路径对应一个资源
* 路由分发：一个文件路径分配到他应该对应处理的过程
  //模拟一个正常网站的页面呈现过程
* 从查询字符串获取信息
## express4.0
### express的路由  
* 核心：3部分组成(重点)
 * 路由方法
 * 路由路径
 * 路由句柄(句柄、中间件、处理函数)
* 请求端点：路由方法 + 路由路径构成了请求端点
* 路由方法
 * get：只处理get请求
 * post：只处理post请求
 * all：处理所有路由方法
* 路由路径(重点)
 * 文件路径匹配
   * 字符串匹配, url中的文件路径
* 路由句柄
 * 一个请求端点可以有一个(最常用)或者多个路由句柄
 * 多个路由句柄我们主要使用两种形式
    * `app.get('/', func1, func2);`
    * `app.get('/', func1);`
    * `app.get('/', func2);`
 * 路由句柄接受3个参数
   * req --> 携带者分析好了之后的请求信息
   * res --> 处理响应信息
   * next --> 可以在执行完了之后向后继续执行
      * `next('route') //跳过本路由端点继续向后执行`
* 路由模块化
 * 原因
   * 代码管理维护方便
   * 团队合作
   * 可移植性与可扩展性
 * 代码
   * 文件 m.js
      `var myModule = require('express').Router();`
      `//商业逻辑`
      `moudule.exports = myModule;`
   * 文件 call.js
      `var mm = require('./m.js');`
      `app.use('/student/xueji',  mm);	//中间件`
     * use('path', func);
     * use(func);	// '/'
     * use('/', func);
### ejs
* 模板引擎就是把数据整合到html文件中
 * ejs的模板形式：HTML = 模板 + 数据
 * ejs语法：
   * `<% code %>：JavaScript代码`
   * `<%= code %>：显示替换过 HTML 特殊字符的内容`
   * `<%- code %>：显示原始 HTML 内容`
   * `<%- include('header') -%>`
* 在express中使用ejs
 * 安装ejs 
    * `npm install ejs -save`
      * 其中：`-save` 就是把在package.json中的依赖列表中写入 ejs 
 * 使用ejs
   * 设置
     * `app.set('views', path.join(__dirname, 'views'));`
     * `app.set('view engine', 'ejs');`
 * 生成页面
   * `res.render('index', { title:'奥运', number: number, names: ['A', 'B', 'C', 'D'] });`
## get与post的区别
* 区别与联系
  * 联系：提交数据
  * 区别：  
    * 数据存在位置不同		
      * get：url的查询字符串：`name1=value&name2=value`
      * post：请求体中
    * 访问次数
      * get：1次请求 
      * post：2次请求: 请求头, 请求体
    * 是否可被浏览器缓存
      * get：可以被缓存
      * post：不能被缓存
    * 安全性(相对安全性)
      * get：相对不安全一些
      * post：相对安全