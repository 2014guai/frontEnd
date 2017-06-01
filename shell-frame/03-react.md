1. React的基本认识
	* Facebook开源的一个js库
	    * https://facebook.github.io/react/index.html
	    * http://www.ruanyifeng.com/blog/2015/03/react.html
	* 它并不是一个MVC框架, 而仅仅是其中的V, 用来渲染视图页面
	* React关心
		* 显示/更新DOM
		* 响应事件
	* React高效的原因
		* 虚拟(virtual)DOM, 不总是直接操作DOM
		* 高效的DOM Diff算法, 最小化页面重绘
2. 使用React入门
	1). 导入js库文件(react.js, react-dom.js, browser.js)
	2). 在页面中引入
	3). 编码:
		<div id="container"></div>
		<script type=text/babel>
			var aa = 123
			ReactDOM.render(<h2>{aa}</h2>, containerDOM);
3. JSX
	* javascript XML
	* react的代码由js的代码和xml标签组件
	* js中可以直接嵌套标签, 但标签中嵌套js需要放在{}中
	* 标签必须有结束
	* 在解析显示js数组数据时, React会自动遍历显示
	* 把数据的数组转换为标签的数组: 
		var liArr = dataArr.map(function(item, index){
			return <li key={index}>{item}</li>
		})
4. React的虚拟DOM
    * React设计的最终会转换为原生HTML DOM(浏览器能解析显示)的对象
    * 在内存中创建虚拟DOM的2种方式:
        1). 使用JSX(标签+js) : 
            <div id='tt' name='div1'>{name}</div>
        2). 使用React提供的纯JS创建函数: 
            React.createElement('div', {id:'tt',name:'div1'}, name) 
    * React在显示/更新页面时, 总是先进行完虚拟DOM操作后才统一更新HTML DOM(页面)
    * React同时使用DOM Diff算法来确定哪些dom元素发生了变化, 只更新变化的部分
5. Component
	1. 基本理解和使用
		* 自定义的标签: 组件类==>标签
		* 创建组件类
		    //MyComp是组件的构造函数, render是组件对象的方法
			var MyComp = React.createClass({
				render (){
					this instanceof MyComp --->true 
					return (
						vDOM
					);
				}
			})
		* 渲染组件标签
			ReactDOM.render(<MyComp tt={aa}/>,  cotainerEle);
		* 渲染的内部流程: 
		    * 创建MyComp组件对象
		    * 调用render方法得到虚拟DOM
		    * 解析成原生DOM
		    * 插入到cotainerEle中
	2. props属性
		* 所有组件标签属性的集合对象
		* 作用: 从组件外部向组件内部传递数据
		* 给标签指定属性, 保存外部数据(可能是一个function)
		* 在组件内部读取属性: this.props.propertyName
		* 初始化默认props
		    getDefaultProps() {
		        return {
		            //n个prop
		            name : "mm"
		        };
		    }
	3. refs属性
		* 包含指定了ref属性的标签的原生DOM的集合对象
		* 给目标标签指定ref属性, 打一个标识 : <input ref='refName'/>
		* 在组件内部获得标签对象: this.refs.refName(只是得到了标签元素对象)
		* 作用: 操作组件内部的真实标签dom对象
    4. 事件处理
        * 绑定监听: 
            <button onClick={this.handleClick}/>
        * 定义处理函数: 
            handleClick(event) {
                event.target
            }
        * 传递自定义参数: 
            <button onClick={this.handleClick.bind(this, arg)}/>
            handleClick(arg, event) {   }
	5. state属性
		* 组件被称为"状态机", 页面的显示是根据组件的state属性的数据来显示
		* 初始化指定:
			getInitialState : function(){
				return {
					stateName1 : stateValue1,
					stateName2 : this.props.xxx
				};
			}
		* 读取显示(render): 
		    {this.state.stateName1}
		* 更新状态(页面) : 
		    this.setState({
		        stateName1 : newValue
		    })
	6. 实现一个双向绑定的组件
		React是单向数据流
		需要手动实现: onChange
	7. 组件的生命周期
		* mount : ReactDOM.render(<MyComponent/>, domEle)
		    创建组件对象
		    getDefaultProps()
		    getInitialState()
		    componentWillMount()
		    render()
		    componentDidMount() : 已经渲染(只执行一次)
		        //做一些监听的工作
                //比如: 启动定时器, 订阅事件
		update : this.setState({})
		    componentWillUpdate()
		    render()
		    componentDidUpdate()
		unmount : ReactDOM.unmountComponentAtNode()
		    componentWillUnmount()
5. ajax
	* React没有ajax模块, 需要使用其它ajax库
	* 一般是在componentDidMount中发送ajax请求, 得到数据后, 更新state
	* 可以使用promise的方式
		* promise.then

6. 应用:
	多个组件的设计
	数据的结构
	数据的传递和保存
	自定义事件处理: pubsub.js
		* 订阅 subscribe		在父组件中设置	PubSub.subscribe("消息名", function(msgName, data){})
		* 发布 publish		在子组件中设置	PubSub.publish("消息名", data)
	
	
添加组件属性，有一个地方需要注意，就是 class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。	
