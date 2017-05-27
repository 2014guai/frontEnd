
# CSS
## 目录
* 盒模型
* margin
* BFC
* 清除浮动的方法
* 选择器优先级
* link与@import的区别
* 经典布局
	* 圣杯布局
	* 双飞翼布局
* CSS3 transition transform animate
* background-* 系列属性，这个不要忽视了，还是很重要的
* position、z-index、display、float、margin
* less与sass
***

## 盒模型
### 对盒模型的理解：
1. 当css没有设置box-sizing属性的时候，
	* css中设置的width指的是content内容区的宽度
2. 设置box-sizing的时候：(总宽度:盒子所占位置大小)
	* box-sizing:content-box(标准模式-默认值)
	    * 总宽度 = margin + border + padding + width 
	* box-sizing:border-box (怪异模式)
	    * 总宽度 = margin + width；
	    * width = 内容区 + padding + border 
		* 为input设置样式时，常使用此方法
### 盒子模型分为两类：W3C标准盒子模型和IE盒子模型 
* w3c盒子模型：
	* 属性高（height）和属性宽（width）这两个值不包含 填充（padding）和边框（border）
![](/images/w3c.JPG "标准盒模型")
* IE盒子模型：
	* 属性高（height）和属性宽（width）这两个值包含 填充（padding）和边框（border）
![](/images/IE.JPG "IE盒模型")
### 盒模型的层次关系：
* 第1层：盒子的边框(border)，
* 第2层：元素的内容(content)、内边距(padding)
* 第3层：背景图(background-image)
* 第4层：背景色(background-color)
* 第5层：盒子的外边距(margin)
* 所以当我们同时设置背景色和背景图片的时候，背景图片将在背景色上方显示
![](/images/盒子3D模型.jpg "盒模型的层次关系")
