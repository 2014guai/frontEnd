# DOM
## 性能影响：
1. DOM操作会导致最重要的,也是我们最需要的问题就是导致用户阻塞的重构(reflow)和重绘(repaint).
    * reflow意味着结构的改变,比如一堆元素堆叠,改变其中一个的宽高,那么相应的所有元素的位置都要改变
    * repaint意味着样式的改变比如div调整了背景色等,但是位置不变,只改变我们操作的元素
    * 所以通常来看repaint的代价要远小于reflow,速度也更快.
2. 原则：
    * 将DOM操作降低到尽量少
        - 能放到DOM操作之外的操作就放到外面 ---> 比如动态添加li，可以使用变量存储创建好的li，最后一次添加
    * 大范围操作先把容器隐藏,在其中操作完成后,再显示.
    * 样式操作不要注意修改属性,直接替换class
        - 逐一修改要访问很多次,而替换class就相当于批量操作了
    * 用变量保存DOM对象而不是多次获取,同时减少操作DOM属性的次数.
## 具体操作：(不怎么考虑兼容性..但求今后补充)
1. 创建元素
    * 创建节点：document.creatElement()
    * 创建文本节点：document.createTextNode()
2. 节点关系：
    * 父节点：parentNode
    * 子节点：childNodes ：返回包含指定节点的子节点集合
    * 兄弟节点：nextSibling返回某节点的下一个兄弟节点，previousSibling返回某节点的上一个兄弟节点；如果找不到将返回null
    * 第一个或最后一个子节点：firstChild、lastChild
3.节点元素关系(只算元素，不算文本节点)
    * children： 返回所有元素子节点（IE5+、ff3.5、opera3、chrome，但在IE8及以下会将注释节点看成一个元素节点）
    * nextElementSibling：返回元素的下一个兄弟元素节点
    * previousElementSibling: 返回元素的上一个兄弟元素节点
4. 节点操作：
    * appendChild()：用于向childNodes列表的末尾添加一个节点，并且返回这个新增的节点。
        - 如果传入到appendChild()里的节点已经是文档的一部分了，那结果就是将节点从原来的位置转移到新位置，任何一个节点不能同时出现在文档中的多个位置。
    * insetBefore()可以将节点插入到某个特定的位置。这个方法接受两个参数：要插入的节点和作为参照的节点。
    * replaceChild()接受两个参数：要插入的节点和要被替换的节点。被替换的节点将由这个方法返回并从文档中被移除，同时由要插入的节点占据其位置。
    * 删除节点：removeChild()
    * 克隆节点：cloneNode(true/false)
        - 参数表示是否采用深度克隆,如果为true,则该节点的所有后代节点也都会被克隆,如果为false,则只克隆该节点本身，文本或者换行、空格这些不会复制，因为他们都是一个textNode。
5. 元素选择：
    * querySelector、querySelectorAll(IE8及以上)
	    - 在页面重绘或者重排后不能获取样式
    * getElementById()
    * getElementsByTagName()
    * getElementsByName()
    * getElementsByClassName()
6. 属性操作:
    * setAttribute()
    * removeAttribute()
    * getAttribute()
    * 自定义属性data-*
        * `<div id="div1" data-aa="11">`
        * 利用div1.dataset可以获得一个DOMStringMap，包含了元素的所有data-*。
        * 使用div1.dataset.aa就可以获取11的值。
## DOM事件：
1. addEventListener()
2. removeEventListener()
4. attachEvent()、detachEvent() IE8及以下使用的事件绑定和解绑
5. 阻止默认事件和冒泡
    * IE事件
        *  e.returnValue = false; // 阻止默认事件
        *  e.cancelBubble = true; // 阻止冒泡
        * IE8及以下的event是绑定在window上的。
    * 标准事件
    * 
        * e.preventDefault(); // 阻止默认事件
        * e.stopPropagation(); // 阻止冒泡
6. 获取元素相关计算后的值
    * IE8及以下用currentStyle()
    * IE9+及其他标准浏览器用getComputedStyle()。

DOM操作节点
	1.访问/获取节点

document.getElementById(id);　　　　　　　　 　　//返回对拥有指定id的第一个对象进行访问

document.getElementsByName(name);　　　　　　//返回带有指定名称的节点集合　　 注意拼写:Elements

document.getElementsByTagName(tagname); 　　//返回带有指定标签名的对象集合　  注意拼写：Elements

document.getElementsByClassName(classname);  //返回带有指定class名称的对象集合 注意拼写：Elements

2.创建节点

document.createTextNode(text);　　　//创建文本节点

3.添加节点

document.insertBefore(newNode,referenceNode);　 //在某个节点前插入节点

parentNode.appendChild(newNode);　　　　　　　　//给某个节点添加子节点

4.复制节点

cloneNode(true | false);　　//复制某个节点  参数：是否复制原节点的所有属性

5.删除节点

parentNode.removeChild(node);　　//删除某个节点的子节点 node是要删除的节点



    - 

