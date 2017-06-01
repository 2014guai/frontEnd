angular如何操作dom	
	引入jQuery或者用angular自己的jQlite

* AngularJS是什么?
	* Google开源的前端JS结构化框架，动态显示数据
	* AngularJS特性和**优点**
		* 双向数据绑定**
		* 声明式依赖注入**
		* 解耦应用逻辑, 数据模型和视图
		* 完善的页面指令**
		* 定制表单验证
		* Ajax封装
		* 测试更方便
	* <--与jQuery的比较：
		* jQuery是函数库，封装简化dom操作
		* angular是JS结构化框架，主体不是DOM，而是页面中的动态数据
	  -->
* 编写Angular应用的基本步骤
	* 编写基本静态页面
	* 将angular.js引入工程中， 并在页面中引入
	* 在页面中指定ng-app, ng-controller
	* 在js中定义model和controller
	* 在controller中初始化数据（$scope）
	* 在页面中通过表达式或指令来显示数据
	* 在页面中使用ng-click添加点击监听，并定义对应的方法进行操作
* 双向数据绑定
	* View（视图）： 页面（标签、指令，表达式）
	* Model(模型) ：作用域对象（属性、方法）
	* 数据绑定： 数据从一个位置(通过框架)自动流向另一个位置
	* 单向数据绑定： 只支持一个方向
		* View-->Model    ： ng-init
		* Model-->View     : {{表达式}}
	* 双向数据绑定
		* Model<-->View    : ng-model		 ng-model='最好绑定为对象属性, 而不是对象本身'
	* angular是支持双向数据绑定的
* 作用域
	* 是一个js实例对象
	* 这个对象的属性、方法， 页面都可以直接引用、操作
	* ng-app指令： 内部创建一个根作用域（$rootScope）, 是所有其它作用域的父对象
* 控制器
	* 也是一个对象，是我们View与Model之间的桥梁
		* （用来控制AngularJS应用数据的实例对象）
	* 当我们使用了ng-controller指令， 内部就会创建控制器对象
	* 但我们同时得提供控制器的构造函数（必须定义一个$scope的形参）
	* 每定义一个ng-controller指令， 内部就会创建一个新的作用域对象（$scope）, 并输入构造函数中
* 模块
	* 也是一个对象
	* 创建模块对象： angular.module('模块名', [依赖的模块])
	* 通过模块添加控制器：
	    * module.controller('MyController', funnction($scope){//操作$scope的语句})
	* angular的整体设计也是多模块的
		* 核心模块： angular.js
		* 扩展模块： angular-router.js, angular-message.js, angular-animate.js
* 依赖注入
	* 依赖的对象被别人自动注入进入
	* 注入的方式;
		* 内部自建 ： 不动态 
		* 全局变量 ： 污染全局环境
		* 形参： 这种最好
	* angualr就是通过声明式依赖注入， 来得到作用域对象 
	* 形参名不能随便定义（只是针对当前这种写法）
* 表达式
	* {{js表达式}}
	* 从作用域对象中读取对应的属性(包括其原型属性)数据来显示数据
	* 不支持if/for/while,但支持**三目表达式**
	<-- angular表达式与JS表达式：
		* angular表达式写法与JS的表达式类同
		* 与JS表达式不同，angular表达式可以写在HTML中
		* 与JS表达式不同，angular表达式不支持条件判断，循环及异常
		* 与JS表达式不同，angular表达式支持过滤器
	-->
* 指令
	* 是什么？ 标签属性、标签，类，注释
	* 作用： 在页面进行数据绑定的操作
	* 内置指令：
		ng-app
		ng-model
		ng-controller
		ng-init			//初始化值
		ng-click
		ng-repeat
		ng-bind :		//相当于{{}}
		ng-show
	    ng-hide

		ng-class : 		//动态引用定义的样式				{aClass:true, bClass:false}
	    ng-style : 		//动态引用通过js指定的样式对象
	    ng-include ： 	//动态插入一个模板页面
	
	    ng-click
	    ng-blur
	    ng-keydown
	    ng-keyup
	    ng-mouseenter : 	//鼠标移入
	    ng-mouseleave ： //鼠标移出
	    ng-mousedown
	    ng-mouseup
	    $event
	* 自定义指令
		* 使用module对象来定义
		* module.directive('指令名', function(){		//工厂函数
			return {								//配置对象
				restrict : 'ECMA', 			//指令的类型，默认为EA
				template : '简单的html标签结构',
				templateUrl : '包含模板标签结构的页面',
				replace : true/false  		//默认false, 插入在指令标签中， 如果为true指令标签就会被替换
				priority : 10 				//优先级 （优先被解析）ng-repeat优先级最高
				terminal : true/false  		//是否终止优先级低的指令的解析
				scope ： false  				//直接使用外部作用域作为当前作用域
				scope ： true  				//新建一个作用域， 继承于外部作用域
				scope : {     				//隔离作用域： 新建一个作用域， 但不从外部外部作用域继承
							//隔离作用域的绑定策略：
						模板中需要显示： {{msg}}
					msg : '@'     <my-directive msg='tt'>    ---->将tt作为字符串显示
					msg ： '='    <my-directive msg='tt'>	 ---->将tt作为表达式， 从外部作用域中取对应的属性显示
						模板中需要显示： {{msg()}}
					msg : '&'     <my-directive msg='tt()'>  ---->将tt()作为表达式, 从外部作用域中取对应的方法调用来显示
 				},
				transclude : false/true 	 //用来解决指令默认会将指令所在的标签的标签体完全的替换， 但有时我们需要留下它们
				controller : function($scope, $element, $attrs, $transclude) {  //引用某个controller或者定义新的，在初始化时执行一次
                        //$scope.number = $scope.number + "controller--->"; 
						//this.xxx = function(){};
                    }
				link : function (scope, elements, attrs, controller) {   		 //指定链接期执行的函数，在初始化时执行一次
                        //scope.number = scope.number + "link--->";
						//elements[0]-->指令所在的标签对象
						//scope-->向scope中添加属性和方法
						//controller.xxx（）
                    },
				requrie:找哪个指令的controller对象，并注入到link中来
						 'xxx'		//在当前标签中查找指定的控制器，注入到当前指令的link函数中
						 '?xxx'		//在当前指令中查找控制器，如果没有为null
						 '^xxx'		//查找外部指令的控制器
			}
		})
	


* 过滤器
	* 在显示数据时可以对数据进行格式化或过滤
		* 单个--->格式化（将别的类型的数据转换为特定格式的字符串）
		* 多个--->过滤  （内部的个数变化， 但类型不变）
		* 不会真正改变被操作数据
	* 语法： *{{express | 过滤器名：补充说明}}
			*ng-bind='expression | 过滤器'
	* 常用内置：
		* currency 		//货币格式化(文本)
		* number		//数值格式化(文本)
		* date 			//将日期对象格式化(文本)
		* json:			//将js对象格式化为json(文本)
		* lowercase : 	//将字符串格式化为全小写(文本)
		* uppercase : 	//将字符串格式化全大写(文本)

		* limitTo 从一个数组或字符串中过滤出一个新的数组或字符串(根据下标)
			* limitTo : 3  limitTo : -3
		* orderBy : 根据指定作用域属性对数组进行排序**
			* {{[2,1,4,3] | orderBy}}  升序
			* {{[2,1,4,3] | orderBy：‘-’}}  降序
			* {{[{id:2,price:3}, {id:1, price:4}] | orderBy:'id'}  id升序
			* {{[{id:2,price:3}, {id:1, price:4}] | orderBy:'-price'} price降序
		* filter : 从数组中过滤返回一个新数组（根据数据）
			* {{[{id:22,price:35}, {id:23, price:45}] | filter:{id:'3'}} //根据id过滤
			* {{[{id:22,price:35}, {id:23, price:45}] | filter:{$:'3'}} //根据所有字段过滤
	* 自定义过滤器
		* 内置过滤器有限， 有时并不能满足页面显示数据的需求
		* 语法：
			module.filter('myLimitTo'， function(){
				return function(value, startIndex, endIndex){
					对vlaue进行过滤处理， 并return 处理的结果
					//不要修改value本身
				}
			});


* 服务
	* 是什么？ 具有特定功能的对象（object对象、函数，数组，基本类型）
	* 内置服务
		* 都以$开头
		* 引入内置服务： 声明式依赖注入（定义形参）
		* 常用的几个：
			* $rootScope
			* $scope
			* $filter：是一个函数，返回值也是个函数	$filter('过滤器名')(value, params)
			* $timeout
			* $interval
		* 脏数据检查：（是否是angular定义的函数）
		    * 当angular定义的函数执行完后, 会对scope内的属性进行检查, 如果发现有改变更新界面
		    * 在非angular定义的回调函数执行完后, 不会进行脏数据检查 --->即使更新了scope页面不会同步更新
		* 页面如何能自动更新的？
			* 在内置的一些函数执行完后， angular会进行脏数据检查的操作
			* controller, $timeout()中的回调函数,  $interval()中的回调函数
			* 如果我们在setTimeout()的回调函数中更新scope， 是不会进行脏数据检查的， 页面不可能更新 
	* 自定义服务
		* 使用module对象来定义服务
		* 定义的方法：
			* factory() : 可以定义任意类型的服务		**常用**
			* service() ： 只能定义object类型对象
			* value()：value
			* constant()：常亮
			* provider()：任意类型，但是太麻烦
		* factory()
			factory('服务名', function(){
				return 服务对象;		//可以式任意类型的
			})
		* 如何引入： 声明式依赖注入
* 过滤器
	* 在显示数据时可以对数据进行格式化或过滤
		* 单个--->格式化（将别的类型的数据转换为特定格式的字符串）
		* 多个----》过滤（内部的个数变化， 但类型不变）
		* 不会真正改变被操作数据
	* {{express | 过滤器名：补充说明}}
	* 常用内置：
		* currency 货币格式化(文本)
		* number数值格式化(文本)
		* date 将日期对象格式化(文本)
		* json: 将js对象格式化为json(文本)
		* lowercase : 将字符串格式化为全小写(文本)
		* uppercase : 将字符串格式化全大写(文本)

		* limitTo 从一个数组或字符串中过滤出一个新的数组或字符串
			* limitTo : 3  limitTo : -3
		* orderBy : 根据指定作用域属性对数组进行排序
			* {{[2,1,4,3] | orderBy}}  升序
			* {{[2,1,4,3] | orderBy：‘-’}}  降序
			* {{[{id:2,price:3}, {id:1, price:4}] | orderBy:'id'}  id升序
			* {{[{id:2,price:3}, {id:1, price:4}] | orderBy:'-price'} price降序
		* filter : 从数组中过滤返回一个新数组
			* {{[{id:22,price:35}, {id:23, price:45}] | filter:{id:'3'}} //根据id过滤
			* {{[{id:22,price:35}, {id:23, price:45}] | filter:{$:'3'}} //根据所有字段过滤
	* 自定义过滤器
		* 内置过滤器有限， 有时并不能满足页面显示数据的需求
		* 语法：
			module.filter('myLimitTo'， function(){
				return function(value, startIndex, endIndex){
					对vlaue进行过滤处理， 并return 处理的结果
					//不要修改value本身
				}
			});
* 编写Angular应用的基本步骤
	* 编写基本静态页面
	* 将angular.js引入工程中， 并在页面中引入
	* 在页面中指定ng-app, ng-controller
	* 在js中定义model和controller
	* 在controller中初始化数据（$scope）
	* 在页面中通过表达式或指令来显示数据
	* 在页面中使用ng-click添加点击监听, 并定义对应的方法进行操作

* 服务
	* 是什么？ 具有特定功能的对象（object对象、函数，数组，基本类型）
	* 内置服务
		* 都以$开头
		* 引入内置服务： 声明式依赖注入（定义形参）, 你不使用它就存在了
		* 常用的几个：
			* $rootScope
			* $scope
			* $filter  :  $filter('过滤器名')(value, params);
			* $timeout 
			* $interval
			* 脏数据检查: 
			    * 当angular定义的函数执行完后, 会对scope内的属性进行检查, 如果发现有改变更新界面
			    * 在非angular定义的回调函数执行完后, 不会进行脏数据检查 --->即使更新了scope页面不会同步更新
		* 页面如何能自动更新的？
			* 在内置的一些函数执行完后， angular会进行脏数据检查的操作
			* controller, $timeout()中的回调函数,  $interval()中的回调函数
			* 如果我们在setTimeout()的回调函数中更新scope， 是不会进行脏数据检查的， 页面不可能更新 
	* 自定义服务
		* 使用module对象来定义服务
		* 定义的方法：
			* factory() : 可以定义任意类型的服务
			* service() ： 只能定义object类型对象
			* value()
			* constant()
			* provider()
		* factory()
			factory('服务名', function(){
				return 服务对象;  //可以是任意类型
			})
		* 如何引入： 声明式依赖注入

* 视图与路由
	* angular中用来实现SPA的技术		//SPA单网页应用	single-page application
		* SPA应用的基本原理：向ng-view中塞入模板页面/发送ajax请求，加载得到模板页面内容，解析页面
	* 使用angular-route.js
		* 将angular-route.js复制到当前项目中
		* 在页面中引入
		* 在创建module时依赖'ngRoute'
	* 在主页中指定<ng-view>/<ng-view>, 它是用来包含显示不同页面内容的容器
	* 如何得到其它页面： ajax请求（局部刷新， 没有页面跳转）
	* 路由： $routeProvider服务
		module.config(function($routeProvider){
				$routeProvider.when('/xx/yy', {      //发请求：  #/xx/yy?name=Tom
						templateUrl : 'aa.html',
						controller : 'AController'
					})
					.when('/xx/yy/:name', {      	//发请求：  #/xx/yy/tom
						templateUrl : 'bb.html',
						controller : 'BController'
					})
					.otherwise()					//设置默认
		})
		.controller('AController', function($scope){
			//给$scope添加属性、方法  					---->给aa.html使用
		})
		.controller('AController', function($scope, $routeParams){
			$scope.name = $routeParams.name
					//给$scope添加属性、方法  			---->给bb.html使用
		})			
* MVC
	* MV*
	* MVVM	详解：http://www.cnblogs.com/whitewolf/p/4581254.html	



* $apply, $watch方法
	* 都是$scope的方法
	* $apply ： 
		* 强制进行脏数据检查， 如果scope中的数据有变化， 更新到页面
		* 如果在不是angular提供的回调函数中更新scope, angular不会进行脏数据检查， 页面不更新
		* 在不是angular提供的回调函数中调用$scope.$apply()
			$apply(function(){
				//更新scope的代码
			})
		* 另一种办法： 直接调用$scope.$digest() (不建议用)
	* $watch
		* 监视scope的属性数据的变化
		* $watch('属性名', function(newValue, oldValue){
			//做处理
		 }, isDeepWatch)  //isDeepWatch表示是否是深度监视，默认是false（只监视它本身， 不监视内部数据的变化）
		* $watch的返回值为函数，取消执行，在内部调用即可
		* 在项目中不要使用太多的watch
* 表单验证
	* 使用工具： AngularJS Batarang
	* 使用angular-messages.js
	* 表单<form>需要有name属性（name='myForm'）, 插件会自动在$scope添加一个属性myForm
		* $invalid：不合法的
		* 各个表单项的name属性
	* 表单项<input>需要有name属性(name='username'), 插件会自动在$scope的myForm添加属性username
		* $dirty ： 用户是否操作过
		* $invalid ： 是否非法
		* $error : 错误对象（非法时有值）
			* 某个验证规则名： true   -->不满足当前这个验证规则
	* 表单项中指令需要的验证规则
		* ng-required	
		* ng-minlength
		* ng-maxlength
		* ng-pattern
		* min
		* max
		* email
		* url
	* 提示：
		<div ng-class='"danger"' ng-messages='myfrom.username.$error' ng-show='myform.username.$dirty&&myform.username.$invalid'>
			<span ng-message='required' ng-bind='"用户名是必须的"'></span>
			<span ng-message='minlength' ng-bind='"用户名至少6位"'></span>

* 动画
	* angular通过操作css来实现动画效果
* ajax
	* 通过$http服务来实现ajax请求
	* 提交get/post请求
		$http({
			method : 'GET/POST",
			url : '/test',
			params : 参数键值对字符串、对象,
			data : 参数键值对字符串、对象
		})
		.success(function(data){
			//将数据保存到scope中
		})
		.error(function(data){
			//提示错误
		})

		$http.get('/get?参数')
			.success(function(data){
				//将数据保存到scope中
			})
			.error(function(data){
				//提示错误
			})

		$http.post('/get', data)
			.success(function(data){
				//将数据保存到scope中
			})
			.error(function(data){
				//提示错误
			})
	* 跨域请求
		* jsonp解决get请求
			$http.jsonp('/jsonp?callback=JSON_CALLBACK&name=tom')
				.success(function(data){
					//将数据保存到scope中
				})
				.error(function(data){
					//提示错误
				})
		* CORS解决post请求
			* 服务端： res.set('Access-Control-Allow-Origin', '*')