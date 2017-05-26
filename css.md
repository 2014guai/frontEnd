
## CSS
* 盒模型
	* 对盒模型的理解：
            1. 当CSS没有设置box-sizing属性的时候，
                * CSS中设置的width指的是content内容区的宽度
            2. 设置box-sizing的时候：(总宽度:盒子所占位置大小)
                * box-sizing:content-box(默认值)(标准模式)
	                * 总宽度 = margin + border + padding + width 
                * box-sizing:border-box (怪异模式)
	                * 总宽度 = margin + width；
	                * width = 内容区 + padding + border 
					* 为input设置样式时，常使用此方法
    * 盒子模型分为两类：W3C标准盒子模型和IE盒子模型 
		* W3C盒子模型——属性高（height）和属性宽（width）这两个值不包含 填充（padding）和边框（border）
		* IE盒子模型——属性高（height）和属性宽（width）这两个值包含 填充（padding）和边框（border）
	* 盒模型的层次关系：
        * 第1层：盒子的边框(border)，
        * 第2层：元素的内容(content)、内边距(padding)
        * 第3层：背景图(background-image)
        * 第4层：背景色(background-color)
        * 第5层：盒子的外边距(margin)
        * 所以当我们同时设置背景色和背景图片的时候，背景图片将在背景色上方显示
* margin
	* 为负:
		为正，边界向内收；为负，边界向外扩
			例如css绝对定位的元素定义的top、right、bottom、left等值是元素自身的边界到最近的已定位的祖先元素的距离，
			这个元素自身的边界指的就 是margin定义的边界，所以，如果margin为正的时候，那它的边界是向外扩的，
			如果margin为负的时候，则它的边界是向里收的
	* IE6双外边距问题
		产生原因：margin与浮动元素的浮动方向、浮动边界的方向一致时
		解决方案：
			浮动元素添加css样式
				* display:inline-block
				* 去除float
	
	* 外边距合并(叠加)
		兄弟元素间：会把外边距进行计算，取大值
		父与子元素间：也会计算，但影响较大
			解决方案：
				* 给父元素加border
				* 给父元素加padding
				* 父元素添加overflow：hidden
				* 父元素加前置内容生成
					* 通常添加为元素 parent:before {display:table,content:""}


* 清除浮动总结
	1、给父级设置高度 (扩展性不好)
	2、给父级加浮动 (页面中所有元素都加浮动，margin左右自动失效（floats bad ！）)
	3、空标签清除浮动 (IE6 最小高度 19px；（设置font-size：0后，下还有2px偏差）)
	4、.br清浮动	(不符合工作中：结构、样式、行为，三者分离的要求  IE6、IE7不支持)
	5、overflow（IE6不支持）
	6、伪元素after
		.clearfix:before,.clearfix:after{
			display:table,
			content:"",
			clear:both
		}
		.clearfix{
			zoom:1
		}

* CSS选择器的优先级
	* !important	优先级最高
	* 内联			1000
	* id			100
	* 类、伪类		10
	* *				1
	* 元素			0
	* 继承样式		没有优先级

* link与@import的区别
	* 区别1：link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。
	* 区别2：link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。
	* 区别3：link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。
	* 区别4：link支持使用Javascript控制DOM去改变样式；而@import不支持。
* 经典布局
	* 圣杯布局
``
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>双飞翼布局</title>
		<!--
			优点：
				内容部分(中间列)优先加载，且实现响应宽
				结构上仅仅添加了一个父级容器
				任何一列都可以作为最高列
			缺点：
				多写了一成html结构
				
			**********************************************
			
			两组实现的对比:
				1.俩种布局方式都是把主列放在文档流最前面，使主列优先加载。
				2.两种布局方式在实现上也有相同之处，都是让三列浮动，然后通过负外边距形成三列布局。
				3.两种布局方式的不同之处在于如何处理中间主列的位置：
						圣杯布局是利用父容器的左、右内边距定位；
						双飞翼布局是把主列嵌套在div后利用主列的左、右外边距定位
		-->
		<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}
			body{
				min-width: 600px;
			}
			.header,.footer{
				border: 1px solid #000;
				background: gray;
				text-align: center;
			}
			.container{
				overflow: hidden;
			}
			.container:after{
				content: "";
				display:block ;
				clear: both;
			}
			.left,.right,.middle{
				float: left;
				padding-bottom: 10000px;
				margin-bottom: -10000px;
			}
			.left{
				width: 200px;
				background: pink;
				margin-left: -100%;
			}
			.right{
				width: 200px;
				background: pink;
				margin-left: -200px;
			}
			.middle{
				width: 100%;
				background: yellow;
			}
			.middle-inner{
				padding: 0 200px;
			}
		</style>
	</head>
	<body>
		<div class="header">
			<h4>header</h4>
		</div>
		<div class="container">
			<div class="middle">
				<div class="middle-inner">
					middle
				</div>
			</div>
			<div class="left">
				left<br />
				left<br />
				left<br />
				left<br />
				left<br />
				left<br />
				left<br />
				left<br />
				left<br />
				left<br />
				left<br />
				left<br />
			</div>
			<div class="right">right</div>
		</div>
		<div class="footer">
			<h4>footer</h4>
		</div>
	</body>
</html>	
``
* 圣杯布局
``
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>圣杯布局</title>
		<!--
			优点：
				内容部分(中间列)优先加载，且实现响应宽
				结构上仅仅添加了一个父级容器
				任何一列都可以作为最高列
			缺点：
				使用了相对定位与负外边距，过于复杂
		-->
		<!--
		总结：
			middle写最上方，优先加载
			wrap区域，清除浮动
			三个模块开启相对定位，向左浮动
			left设置margin-left：100%，left：-200px
			right设置margitn-left：-200px，left：-200px
			middle设置width：100%
		-->
		<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}
			.header,.footer{
				border: 1px solid #000;
				background: gray;
				text-align: center;
			}
			.container{
				overflow: hidden;
				padding: 0 200px;
			}
			.left,.right,.middle{
				position: relative;
				float: left;
				/*padding-bottom: 100000px;
				margin-bottom: -100000px;*/
			}
			.left{
				width: 200px;
				background: pink;
				margin-left: -100%;
				left: -200px;
			}
			.right{
				width: 200px;
				background: pink;
				margin-left: -200px;
				right: -200px;
			}
			.middle{
				width: 100%;
				background: yellow;
				height: 200px;
			}
			
		</style>
	</head>
	<body>
		<div class="header">
			<h4>header</h4>
		</div>
		<div class="container">
			<div class="middle">middle</div>
			<div class="left">left</div>
			<div class="right">right</div>
		</div>
		<div class="footer">
			<h4>footer</h4>
		</div>
	</body>
</html>

``
