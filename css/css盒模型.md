
# 盒模型
## 概述:
* 根据w3c标准，将页面中的每一个元素都设计为一个矩形的盒子。
## 目录
* [盒模型的组成](#盒模型的组成)
* [盒模型的理解](#盒模型的理解)
* [盒子模型分类](#盒子模型分类)
* [盒模型的层次关系](#盒模型的层次关系)
* [行内元素的盒模型](#行内元素的盒模型)
* [可见框](#可见框)
* [盒模型的样式](#盒模型的样式)
***

## 盒模型的组成
* 内容区(content)
  * 内容区用来装着子元素，所有的子元素都在父元素的内容区保存
  * width，height
* 内边距(padding)
  * 内容区与边框之间的距离
  * padding-top,padding-right,padding-bottom,padding-left
* 边框(border)
  * 盒子可见框最外面的部分
  * 属性
    * 宽度：border-width
    * 颜色：border-color
    * 样式：border-style
* 外边距(margin)
  * 当前盒子与其他盒子的距离
  * 负外边距(margin为负):   
    * 理解：为正，边界向内收；为负，边界向外扩    
      * 例如css绝对定位的元素定义的top、right、bottom、left等值是元素自身的边界到最近的已定位的祖先元素的距离，
      这个元素自身的边界指的就 是margin定义的边界，所以，如果margin为正的时候，那它的边界是向外扩的，
      如果margin为负的时候，则它的边界是向里收的
  ![](/images/负外边距.jpg "负外边距")      
  * IE6双外边距问题
    * 产生原因：margin与浮动元素的浮动方向、浮动边界的方向一致时          
    * 解决方案：         
      * 浮动元素添加css样式        
        * `display:inline-block`          
        * 去除float            
  * 外边距合并(叠加)     
    * 兄弟元素间：会把外边距进行计算，取大值         
    * 父与子元素间：也会计算，但影响较大        
    * 解决方案：     
      * 父元素加`border`         
      * 父元素加`padding`            
      * 父元素添加`overflow：hidden`            
      * 父元素加前置内容生成           
  ```
  parent:before {
    display:table;
    content:"";
  }
  ```  
## 盒模型的理解
1. 当css没有设置box-sizing属性的时候，
	* css中设置的width指的是content内容区的宽度
2. 设置box-sizing的时候：(总宽度:盒子所占位置大小)
	* box-sizing:content-box(标准模式-默认值)
	    * 总宽度 = margin + border + padding + width 
	* box-sizing:border-box (怪异模式)
	    * 总宽度 = margin + width；
	    * width = 内容区 + padding + border 
		* 为input设置样式时，常使用此方法
## 盒子模型分类
* w3c盒子模型：
	* 属性高（height）和属性宽（width）这两个值不包含 填充（padding）和边框（border）
![](/images/w3c盒模型.png "标准盒模型")
* IE盒子模型：
	* 属性高（height）和属性宽（width）这两个值包含 填充（padding）和边框（border）
![](/images/ie盒模型.png "IE盒模型")
## 盒模型的层次关系
* 第1层：盒子的边框(border)，
* 第2层：元素的内容(content)、内边距(padding)
* 第3层：背景图(background-image)
* 第4层：背景色(background-color)
* 第5层：盒子的外边距(margin)
* 所以当我们同时设置背景色和背景图片的时候，背景图片将在背景色上方显示
![](/images/盒子3D模型.jpg "盒模型的层次关系")
## 行内元素的盒模型
* 行内元素不支持width和height属性
* 行内元素支持水平方向的padding，垂直方向的padding会影响行内元素，但是不会影响到页面的布局
* 行内元素支持border
* 行内元素支持水平方向margin，不支持垂直方向的
## 可见框
* 可见框指的是元素的盒子模型可见的部分
* 可见框的大小由元素的内容区、内边距、边框共同决定
* 可见框的宽度 = border-left-width + padding-left + width + padding-right + border-right-width;
* 可见框的高度 = border-top-width + padding-top + height + padding-bottom + border-bottom-width;
## 盒模型的样式
* display
  * 用来设置盒子的显示的类型
  * 可选属性：
    * none
      * 元素将不会在页面中显示，同时也不会占用页面中的位置
    * block
      * 元素将会以块元素的形式显示
    * inline
      * 元素将会以内联元素的形式显示
    * inline-block
      * 元素将会以行内块元素的形式显示
* visibility	
  * 用来元素是否在页面中显示
  * 可选值：
    * visible：默认值，元素会正常在页面显示
    * hidden：元素会隐藏，不在页面中显示，但是它依然会占用位置
* overflow
  * 用来设置元素如何处理溢出的内容
  * 可选值：
    * auto：会自动根据需要生成滚动条
    * scroll：会默认在元素中添加水平和垂直两个方向的滚动
    * hidden：会将溢出的内容裁剪，不显示