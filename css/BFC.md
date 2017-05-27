### margin
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
### 清除浮动的方法
* 1. 给父级设置高度 (扩展性不好)
* 2. 给父级加浮动 (页面中所有元素都加浮动，margin左右自动失效（floats bad ！）)
* 3. 空标签清除浮动 (IE6 最小高度 19px；（设置font-size：0后，下还有2px偏差）)
* 4. br清浮动	(不符合工作中：结构、样式、行为，三者分离的要求  IE6、IE7不支持)
* 5. overflow（IE6不支持）
* 6. 伪元素after
```
.clearfix:before,.clearfix:after{
	display:table;
	content:"";
	clear:both;
}
.clearfix{
	zoom:1;
}
```



### link与@import的区别
* 区别1：link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。
* 区别2：link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。
* 区别3：link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。
* 区别4：link支持使用Javascript控制DOM去改变样式；而@import不支持。