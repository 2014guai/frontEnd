# BOM
## 什么是BOM
* ECMAScript无疑是JavaScript的核心, 但是要想在浏览器中使用JavaScript, 那么BOM(浏览器对象模型)才是真正的核心
* 对象：Window document location screen history navigator
* 方法：Alert() confirm() prompt() open() close()
## window
* window对象是BOM的核心, 它表示一个浏览器的实例
* 在浏览器中我们可以通过window对象来访问操作浏览器, 同时window也是作为全局对象存在的
* 全局作用域：
  * window对象是浏览器中的全局对象, 因此所有在全局作用域中声明的变量、对象、函数都会变成window对象的属性和方法
* window的方法
  * window.open('url') 要新的窗口打开链接
    * 需要加载的url地址
    * 窗口的目标
    * 一个特性的字符串
    * 是否创建新的历史记录
  * window.onload()	预先加载
  * window.onresize()	当窗口大小发生变化的时候触发
  * window.onscroll()	当滚动条滚动的时候触发
  * window.location = 'url'	跳转后有后退功能
  * window.location.replace("url") 跳转后没有后退功能
  * window.location.search() 返回url中?后面的内容
  * window.location.reload() 刷新当前页面
  * window.screen.width 窗口宽度大小
  * window.navigator.userAgent 获取浏览器的版本
  * window.print() 打印当前页
## location对象
* location对象提供了与当前窗口中加载的文档有关的信息, 还提供了一些导航功能
* href属性：
  * href属性可以获取或修改当前页面的完整的URL地址, 使浏览器跳转到指定页面
* assign()方法
  * 所用和href一样, 使浏览器跳转页面, 新地址错误参数传递到assign()方法中
* replace()方法
  * 功能一样, 只不过使用replace方法跳转地址不会体现到历史记录中
* reload() 方法
 * 用于强制刷新当前页面
## navigator对象
* navigator对象包含了浏览器的版本、浏览器所支持的插件、浏览器所使用的语言等各种与浏览器相关的信息
* 我们有时会使用navigator的userAgent属性来检查用户浏览器的版本
## screen对象
* screen对象基本上只用来表明客户端的能力, 其中包括浏览器窗口外部的显示器的信息, 如像素宽度和高度等
* 一般不太用
## history对象
* history对象保存着用户上网的历史记录, 从窗口被打开的那一刻算起
* go()
  * 使用 go()方法可以在用户的历史记录中任意跳转, 可以向后也可以向前
* back()
  * 向后跳转
* forward()
  * 向前跳转
## document
* document对象也是window的一个属性, 这个对象代表的是整个网页的文档对象
* 我们对网页的大部分操作都需要以document对象作为起点
* document.write()方法使用	
  * 页面载入过程中, 用脚本加入新的页面内容
  * 用延时脚本创建本窗口或新窗口的内容
    * 脚本向窗口(不管是本窗口或其他窗口)写完内容后, 必须关闭输出流。
    在延时脚本的最后一个document.write()方法后面, 必须确保含有document.close()方法, 
    不这样做就不能显示图像和表单。
## 定时器
  * setTimeout()：超时调用
    * 参数
      * 要执行的内容
      * 超过的时间
    * 取消超时调用
      * clearTimeout()
    * 超时调用都是在全局作用域中执行的
  * setInterval(): 间歇调用
    * 需要两个参数：
      * 要执行的代码
      * 间隔的时间
    * 取消间隔调用：
      * clearInterval()
## 系统对话框
* alert
  * alert()接收一个字符串并显示给用户, 用alert()方法会向用户显示一个包含一个确认按钮的对话框
* confirm
  * confirm和alert类似, 只不过confirm弹出的对话框有一个确认和取消按钮, 用户可以通过按钮来确认是否执行操作
  * 这个函数的执行会返回一个布尔值, 如果选择确定则返回true, 如果点击取消则返回false
* prompt
  * prompt会弹出一个带输入框的提示框, 并可以将用户输入的内容返回
  * 需要两个值作为参数：
    * 显示的提示文字
    * 文本框中的默认值
* 移动端获取机器类型
   * ```
      //获取访问的user-agent
      var ua = navigator.userAgent.toLowerCase() || window.navigator.userAgent.toLowerCase();
      //判断user-agent
      var isWX = /MicroMessenger/i.test(ua), //微信端
        isIOS = /(iPhone|iPad|iPod|iOS)/i.test(ua), //苹果家族
        isAndroid = /(android|nexus)/i.test(ua), //安卓家族
        isWindows = /(Windows Phone|windows[\s+]phone)/i.test(ua), //微软家族
        isBlackBerry = /BlackBerry/i.test(ua); //黑莓家族
     ```
  * 得到结果都是true或者false, i是忽略大小写
  * user-agent不是万能的, 有些访问设备或者浏览器可以强制改变, 客户端校验只是多一重标准
  * 至于服务器端的判断还有IP判断








