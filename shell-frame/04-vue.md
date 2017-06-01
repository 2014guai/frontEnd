* Vue.js是什么?
	* 一位华裔前Google工程师开发的前端js库
    * 与angular.js类似的是声明式开发，但性能高于angular，体积小很多, 比较适合移动端开发
    * 它本身不是全能框架, 只关注UI, 如果需要router/ajax, 可以使用对应插件或使用别的库来实现
* 基本使用
	* 引入vue.js
	* 创建Vue对象, 指定选项对象
		* el : 指定dom标签容器的选择器
		* data : 指定初始化状态属性数据的对象
	* 页面中
		* 使用v-model: 实现双向数据绑定
		* 使用{{}} ; 显示数据
* Vue对象的选项
	* el
		* 指定dom标签容器的选择器
		* Vue就会管理对应的标签及其子标签
	* data
		* 指定初始化状态属性数据的对象
		* vue对象可以直接访问其属性
		* 页面中可以直接访问使用
	* methods
		* 包含多个方法的对象
		* 供页面中的事件指令来绑定回调
		* 回调函数默认有event参数, 但也可以指定自己的参数
		* 所有的方法由vue对象来调用, 访问data中的属性直接使用this.xxx
	* computed
		* 包含多个方法的对象
		* 对状态属性进行计算返回一个新的数据, 供页面获取显示
		* 一般情况下是相当于是一个只读的属性
		* 利用set/get方法来实现属性数据的计算读取, 同时监视属性数据的变化
	* watch
		* 包含多个属性监视的对象
		* 分为一般监视和深度监视
		* 'xxx' : {
			deep : true,
			handler : fun(vlaue)
		}

* 扩展数组
	* $remove(ele) : 删除数组中对应的元素
	* $set(index, ele) : 给数组中指定下标指定对应的元素 

* 页面指令
	* v-text/v-html: 指定标签体
		* v-text : 当作纯文本
		* v-html : 将value作为html标签来解析
	* v-if v-else v-show
		* v-if : 如果vlaue为true, 当前标签会输出在页面中
		* v-else : 与v-if一起使用, 如果value为false, 将当前标签输出到页面中
		* v-show: 就会在标签中添加display样式, 如果vlaue为true, display=block, 否则是none
	* v-for : 遍历
		* 遍历数组 : v-for="person in persons"   $index
		* 遍历对象 : v-for="value in person"   $key
	* v-on : 绑定事件监视
		* v-on:事件名, 可以缩写为: @事件名
		* 监视具体的按键: @keyup.keyCode   @keyup.enter
		* 阻止事件的冒泡和事件默认行为: @click.stop   @click.prevent
		* 隐含对象: $event
	* v-bind : 强制绑定解析表达式  
		* 很多属性值是不支持表达式的, 就可以使用v-bind
		* 可以缩写为:  :id='nanme'
		* :class
			* :class="{classA : isA, classB : isB}"
			* :class="[classA, classB]"
		* :style
			:style="{'color' : myColor}"
	* v-model
		* 双向数据绑定
	* v-el : 标识某个标签
		* v-el:xxx
		* 读取得到标签对象: this.$els.xxx
* todoList练习