# jQuery
## 目录
* [jQuery](#jQuery)
* [整体结构](#整体结构)
* [理解](#理解)
* [特点](#特点)
* [window.onload与$(document).ready() 区别](#window.onload与$(document).ready() 区别)
* [插件兼容](#插件兼容)
* [插件扩展](#插件扩展)
* [jQuery核心函数用法](#jQuery核心函数用法)
* [常用函数](#常用函数)
* [引入jQuery](#引入jQuery)
* [attr&prop的区别](#attr&prop的区别)
***

## jQuery
* jQuery是函数库, 封装简化dom操作
* 优势：
  * 核心稳定、效率高、兼容性强
  * 插件多
* 主旨：
  * 以更少的代码, 实现更多的功能 (Write less,do more)
## 整体结构
* IIFE
```javaScript
(function (window) {
      var jquery = function () {
          return {
              xxxx: function () {
                  console.log('xxx');
                  return this;
              }
          };
      }
      window.jquery = window.$$ = jquery;
  })(window);
```
## 理解
* 关键概念：
  * 仅向外提供两个命名空间：即jQuery和它的简称$,
   一切对jQuery库内方法的调用, 都只能通过这两个命名空间
  * jQuery对象的生成方式：外部通过调用$(arg)方法可以得到jQuery对象
* jQuery框架的最外层是可自动执行的闭包方法, 
  该闭包方法执行结束后可以通过该闭包向外提供的接口(window命名空间内的变量)来继续调用闭包内的成员变量。
  该闭包只设定了jQuery和$它的简称作为window的变量, 
  故而, jQuery库仅向外提供了两个接口, 或者说是两个命名空间
* 从面向对象的角度来说, 对象都是经过类new出来的, 
  而jquery最直观的一点就是：jquery并没有经过new这个过程(当然js也可以使用特殊的手段不经由new关键字而生成一个对象，可是jquery也没有经过这个方式构建出来)。
  jQuery的对象并不是通过 new jQuery 创建的, 而是通过 new jQuery.fn.init 创建的, 
  叫做"init对象"还更贴切, 而且这个对象的原型是jquery的原型
## 特点 
* 选择器：通过JQuery的选择器选择出来的DOM元素存入JQuery的DOM数组中, 返回的是一个数组集合
* 链式调用：每个方法返回的都是调用者自己, JQuery中几乎都是方法, 属性很少, 方便实现链式编程。 
  每个JQuery对象的方法都是从 Jquery函数的 prototype属性中共享  
* 强大的功能函数(同一函数具有读、写的功能)
* 隐式迭代：JQuery的隐式迭代就是JQuery方法遍历内部DOM数组的过程(不用再像JS中循环遍历)
* 丰富插件
* 浏览器兼容
## window.onload与$(document).ready() 区别
* 执行时间
  * window.onload必须等到页面内包括图片的所有元素加载完毕后才能执行
  * $(document).ready()是DOM结构加载完毕后就执行, 不必等到图片加载完毕
* 编写个数不同
  * window.onload不能同时编写多个, 如果有多个window.onload方法, 只会执行一个
  * $(document).ready()可以同时编写多个, 并且都可以得到执行
* 简化写法
  * window.onload没有简化写法
  * $(document).ready(function(){})可以简写成$(function(){});
## 插件兼容
* 跟js引入顺序有关
* 如果有2个库都有$, 就存在冲突
  * 解决: jQuery库可以释放$的使用权, 让另一个库可以正常使用, 此时jQuery库只能使用jQuery了
* 自定义别名：
  * API : jQuery.noConflict() --> `<script>var $j = jQuery.noConflict();</script>`
## 插件扩展
* 扩展jQuery的工具方法
  * $.extend(object)
* 扩展jQuery对象的方法
  * $.fn.extend(object);
* $.extend的详细用法
  * `$.extend([deep], target, object, [objectN)`
    * 用一个或多个其他对象来扩展一个对象, 返回被扩展的对象
    * 如果不指定target, 则给jQuery命名空间本身进行扩展
    * 这有助于插件作者为jQuery增加新方法 
    * 如果第一个参数设置为true, 则jQuery返回一个深层次的副本, 递归地复制找到的任何对象
    * 否则的话, 副本会与原对象共享结构 
    * 未定义的属性将不会被复制, 然而从对象的原型继承的属性将会被复制
  * 扩展静态的方法
    * 
    ```javascript
    $.extend({
          test: function(){
            console.log("静态方法")
          }
        })
    ```
    * 合并多个对象
      * $.extend(css1, css2)
        * css2中有, css1中没有, 就会将css2的属性添加到css1中
        * css2中有, css1中有, 就会将css2的属性覆盖css1的属性
        * 返回css1, 破坏css1的结构
      * $.extend({}, css1, css2)
        * 返回{}新对象, 不破坏css1, css2结构
    * 深度嵌套对象
      * `$.extend(true, {}, css1, css2)`
        * 第一个参数为true时，就会进行深度嵌套
      * 例子：
      ```javascript
      var css1 = {name:"tom", location:{city: "cc"}};
      var css2 = {last:"jack", location:{country: "US"}};
      $.extend(true, {}, css1, css2)
      //结果：{name:"tom", last:"jack", location{city:"cc", country:"US"}
      $.extend({}, css1, css2)
      //结果：{name:"tom", last:"jack", location{country:"US"}
      ```
## jQuery核心函数用法
* 作为一般函数调用: $(params)
  * callback, function: 绑定文档加载完成的回调
  * 选择器字符串: 查找所有匹配的dom元素, 并包装为jQuery对象返回
  * 标签字符串: 生成dom元素对象, 并包装为jQuery对象返回
  * dom元素对象: 将指定的dom元素包装为jQuery对象返回(用得较多的是this)
* 作用对象使用(工具方法)
  * $.each(): 遍历数组/对象
## 常用函数
* $()选择器
* jQuery对象与dom对象的转换 
* 同一函数实现set和get 
  * $("#msg").click()
  * $("#msg").html()
  * $("input").val(")
* 集合处理
  * $("p").each
* 扩展
  * $.extend()
* 操作元素的样式 
  * $("#msg").css()
  * $("#msg").height()
  * $("#msg").addClass(); 
  * $("#msg").removeClass(); 
  * $("#msg").toggleClass();
* 事件处理
  * $("#msg").click() 
  * $("#msg").hover(fn1,fn2)
  * $(document).ready(fn): 当DOM载入就绪可以查询及操纵时绑定一个要执行的函数
  * $("p").toggle(fn,fn2): 每次点击时切换要调用的函数。
    如果点击了一个匹配的元素, 则触发指定的第一个函数, 当再次点击同一元素时, 则触发指定的第二个函数。
    随后的每次点击都重复对这两个函数的轮番调用。
## 引入jQuery
* 使用CDN加载jQuery库的主要优势是什么
	* 这是一个稍微高级点儿的jQuery问题。
	* 好吧, 除了报错节省服务器带宽以及更快的下载速度这许多的好处之外, 
	  最重要的是, 如果浏览器已经从同一个CDN下载类相同的jQuery 版本, 那么它就不会再去下载它一次。 
	  因此今时今日, 许多公共的网站都将jQuery用于用户交互和动画, 如果浏览器已经有了下载好的jQuery库, 网站就能有非常好的展示机会。
## attr&prop的区别
* 浏览器的读写操作, 只会关注property属性
* 当我们通过代码控制attributes属性来同步property属性时
  (由于布尔值转化的问题), 并不是每个属性都会同步。
  * 属性值为布尔值的属性, attriute和proterty会实时同步
    * 没有人为的干扰proterty时, 会同步
    * 干扰了proterty后, 就不会同步
  * 属性值不为布尔值的属性attriute和proterty会实时同步
* 那些我们可以通过浏览器端通过实际操作来改变的属性最好使用prop()
