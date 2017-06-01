# BOM

* 对象：Window document location screen history navigator
* 方法：Alert() confirm() prompt() open() close() 

* window的方法
  * window.onload()					预先加载
  * window.onresize()					当窗口大小发生变化的时候触发
  * window.onscroll()					当滚动条滚动的时候触发
  * window.location = 'url'			跳转后有后退功能
  * window.location.replace("urll") 	跳转后没有后退功能
  * window.location.search()			返回url中?后面的内容
  * window.location.reload()			刷新当前页面
  * window.open('url')				要新的窗口打开链接
  * window.screen.width				窗口宽度大小
  * window.navigator.userAgent		获取浏览器的版本
  * window.print()					打印当前页


移动端获取机器类型
   //获取访问的user-agent
   var ua = navigator.userAgent.toLowerCase() || window.navigator.userAgent.toLowerCase();
   //判断user-agent
   var isWX = /MicroMessenger/i.test(ua), //微信端

     isIOS = /(iPhone|iPad|iPod|iOS)/i.test(ua), //苹果家族
     isAndroid = /(android|nexus)/i.test(ua), //安卓家族
     isWindows = /(Windows Phone|windows[\s+]phone)/i.test(ua), //微软家族
     isBlackBerry = /BlackBerry/i.test(ua); //黑莓家族


  /**
  * 得到结果都是一个true或者false , i 是忽略大小写...挺简单的一个小玩意..当做一个备忘录吧
  * user-agent不是万能的,有些访问设备或者浏览器可以强制改变,客户端校验只是多一重标准
  * 至于服务器端的判断还有IP判断,看需求了
  
document.write()方法使用	
  1.页面载入过程中，用脚本加入新的页面内容。
      2.用延时脚本创建本窗口或新窗口的内容。	
  
  脚本向窗口(不管是本窗口或其他窗口)写完内容后，必须关闭输出流。在延时脚本的最后一个document.write()方法后面，必须确保含有document.close()方法，不这样做就不能显示图像和表单。