
# DOM事件	
## 目录
[事件](#事件)
[绑定事件的方法](#绑定事件的方法)
[事件解绑](#事件解绑)
[清除浏览器的默认行为](#清除浏览器的默认行为)
[事件对象(event)](#事件对象(event))
[事件的传播(事件流)](#事件的传播(事件流))
[事件委托](#事件委托)
[常见事件](#常见事件)
## 事件
  * 在JS中的事件是基于观察者模式		
  * 事件有这么几个要素：
    * 事件源: 被监听的对象
    * 事  件：监听的内容
    * 监听器：监听事件源, 当事件触发时, 调用回调函数
      * 回调函数：你定义的;但是你没有被调用;事件发生后, 它执行了
## 绑定事件的方法
* 两种方法：
  * 第一种(DOM0)：
    * obj.onclick = callback;
     * 这种方式只能为一个元素的一个事件绑定一个处理函数, 不能绑定多个, 一旦绑定多个则后边的会把前边的覆盖
  * 第二种(DOM2)：
    * 标准浏览器(IE9以上及Chrome、Firefox)：
      * obj.addEventListener(事件名称, 回调函数, 是否捕获);
        * 有捕获
        * 事件名称没有on
        * 事件执行的顺序是正序
        * this触发该事件的对象
      *注意：是否捕获, 默认是false;false: 冒泡, true：捕获*
    * IE浏览器(IE11不支持此方法)：
      obj.attachEvent("事件名", 回调函数);
        * 没有捕获(非标准的IE, 标准的IE有捕获)					//非标准IE6/7/8
        * 事件名称有on
        * 事件函数执行的顺序：标准ie->正序, 非标准ie->倒序
        * this指向window
    *注意：addEventListener()绑定的回调函数中的this就是当前的元素, 
        而attachEvent()绑定的回调函数中的this永远都是window*
* 两种方法的区别：
  * DOM0：  
    * 默认冒泡:
      * 取消冒泡的方法: event.cancelBubble = true;
    * 一个元素只能绑定一个同类事件, 如果继续绑定, 第二个事件函数的会覆盖第一个
  * DOM2:	
    * attachEvent默认冒泡
    * addEventListener第三个参数是否捕获, 默认为false冒泡, true捕获
    * 一个元素上可以绑定度过同类事件, 它们都会执行
## 事件解绑
  * DOM0: 只需要再注册一次事件, 把值设成null
    * 原理: 最后注册的事件要覆盖之前的, 最后一次注册事件设置成null, 
        也就解除了事件绑定
  * DOM0事件模型还涉及到直接写在html中的事件:
    * 因此不会传入event对象, 同时, this指向的是window, 不再是触发事件的dom对象
  * DOM2: removeEventListener
     * 解除事件语法：btn.removeEventListener("事件名称", "事件回调", "捕获/冒泡");
     * detachEvent(ie)
## 清除浏览器的默认行为
  * DOM0: return false
  * DOM2: dom2  event.preventDefault()
## 事件对象(event)
  * 在事件的响应函数被触发时, 浏览器每次都会传递进一个事件对象(Event), 
    在这个事件对象中封装了当前事件相关的一切信息, 鼠标的坐标、键盘的那个按键被按下
  * 但是注意在IE8以下的浏览器中, 它不会传递事件对象, 而是将事件对象作为window对象的属性保存 
    * 解决IE8以下event兼容问题：
    * ```
      元素.事件 = function(event){				或		元素.事件 = function(ev){
            event = event || window.event;						ev = ev || event
          }													}
      ```
## 事件的传播(事件流)
* 当触发了一个页面中某一个事件时, 它实际上经过了三个阶段：
  *捕获阶段
    * 指从最外层的元素开始向目标元素捕获事件（由外向内）
  *目标阶段
    * 事件传播到了触发事件的对象
  *冒泡阶段
    * 冒泡阶段指的是事件由目标元素, 向他的祖先元素传导(由内向外)
* 一般来说我们的事件都是在冒泡阶段执行的, 在IE8以下的浏览器中没有捕获阶段
* 全局捕获：
      * 只在IE下有效果;firefox有此属性, 但没有效果;chrome则不支持此属性
      * 全局捕获触发后只执行一次
        * 元素.setCapture激活全局捕获
        * 元素.releaseCapture释放全局捕获
* 冒泡：
  * 冒泡简单来说就是事件的向上传导
  * 后代元素上的事件被触发也会导致祖先元素上的相同事件被触发
  * 开发中很多情况我们可以去利用冒泡, 但是有些情况我们不希望事件冒泡
* 阻止冒泡：
  * event.cancelBubble = true;
  * event.stopPropagation();
## 事件委托
  * 过程:
    * 将多个子元素(li)的事件监听委托给父辈元素(ul)处理
    * 监听回调是加在了父辈元素上
    * 当操作任何一个子元素(li)时, 事件会冒泡到父辈元素(ul)
    * 父辈元素不会直接处理事件, 而是根据event.target得到发生事件的子元素(li), 通过这个子元素调用事件回调函数
  * 好处:
    * 减少事件监听的数量: n--->1
    * 添加新的子元素, 自动有事件响应处理
## 具体事件    
* 拖拽
  * 拖拽相关的三个事件：
    * onmousedown：当鼠标按下时触发
    * onmousemove: 当鼠标移动时触发
    * onmouseup：当鼠标松开时触发
  * 注意：
    * onmousedown给被拖拽的对象绑定
    * onmousemove和onmouseup需要给document绑定
    * onmousemove和onmouseup这两个事件需要在onmousedown响应函数内绑定
    * onmouseup时需要清除两个事件：onmousemove和onmousedown = null
* 区别四种鼠标事件
  * mouseover, mouseout: 当xxx = mouseover时：把鼠标放在outer容器里面来回移动, 就会发现控制台不断地输出, 说明mouseover是可以冒泡的;
  * mouseenter, mouseleave: 当xxx = mouseenter时：把鼠标放在outer容器里面来回移动, 就会发现控制台没有输出, 说明mouseenter是不冒泡的;
* 鼠标滚动事件
  * document.documentElement.scrollTop;
  * document.body.scrollTop;	
  * window.pageYOffset;	//safari
* 滚轮滚动事件
  * 其他浏览器：
    * onmousewheel
  * 火狐：
    * DOMMouseScroll
  *注意火狐中的事件必须通过addEventListener()来绑定*
  * 滚轮方向的判断：
    * 其他浏览器中：使用：event.wheelDelta
      * 当值大于0时, 向上滚动, 当值小于0是, 向下滚动
    * 火狐浏览器：使用：event.detail
      * 当值大于0时, 向下滚动, 当值小于0是, 向上滚动
* 键盘事件：
  * 一般情况键盘事件都会绑定给输入框或者是document
    * onkeydown --> 当按键按下时触发
    * onkeyup --> 当按键被松开时触发	
  * 键盘相关的事件属性：
    * keyCode：按键的编码（可以获取到哪个按键被按下）
      * altKey
      * ctrlKey
      * shiftKey
        * 这三个用来检查alt、ctrl、shift是否被按下, 如果按下则返回true, 否则返回false
    
      

  
		