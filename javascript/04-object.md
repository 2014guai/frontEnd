# 对象
## 概述
* Object是js中的引用数据类型, 它也称为复合数据类型, 除了基本数据类型, 都为Object类型
* 分类：
  * 内建对象: ES标准中的内置对象
  * 宿主对象：浏览器为我们提供的对象
  * 自定义对象: 开发人员自己定义的对象
## 目录
* [对象](#对象)
* [对象的属性](#对象的属性)
* [对象的实例方法](#对象的实例方法)
* [创建对象](#创建对象)
* [继承模式](#继承模式)
* [拷贝](#拷贝)
* [基本数据类型与引用数据类型](#基本数据类型与引用数据类型)
* [对象属性的增删改查](#对象属性的增删改查)
* [圾回收（GC）](#圾回收（GC）)
***

## 对象
* 多个数据(属性)的集合
* 属性组成:
  * 属性名: 字符串(标识)
  * 属性值: 任意类型
* 属性的分类:
  * 一般: 属性值不是function, 描述对象的状态
  * 方法: 属性值为function的属性, 描述对象的行为
* new一个对象背后做了些什么?
   * 创建一个空对象
   * 给对象设置`__proto__`, 值为构造函数对象的`prototype`属性值
   * 执行构造函数体(给对象添加属性/方法)
* 特别的对象
  * 数组
  * 函数
## 对象的属性
* JavaScript 提供了一个内部数据结构，用来描述对象的属性，控制它的行为
```
  {
    value: undefined,
    writable: true,
    enumerable: true,			// 是否可遍历
    configurable: true,		// 可配置性，控制了属性描述对象的可写性
    get: undefined,
    set: undefined
  }
```
* 属性的读取
```
  var obj = {
    foo: 1,
    bar: 2
  };
  
  obj.foo  // 1
  obj[foo] // 1
```
* 属性的赋值
```
  var obj = {};
  
  obj.foo = 'Hello';
  obj['bar'] = 'World';
```
* 属性的查看, Object.keys: 查看一个对象本身的所有属性
``` 
  var obj = {
    key1: 1,
    key2: 2
  };
  
  Object.keys(obj); // ['key1', 'key2']
```
* 属性的删除
```
  var obj = { p: 1 };
  delete obj.p // true
  obj.p // undefined
```
* 属性是否存在
```
  var obj = { p: 1 };
  'p' in obj // true
  'toString' in obj // true
```
## 对象的实例方法
* 即对象原型的方法
* `Object.prototype.valueOf()`：返回当前对象对应的值。
* `Object.prototype.toString()`：返回当前对象对应的字符串形式。
* `Object.prototype.toLocaleString()`：返回当前对象对应的本地字符串形式。
* `Object.prototype.hasOwnProperty()`：判断某个属性是否为当前对象自身的属性，还是继承自原型对象的属性。
* `Object.prototype.isPrototypeOf()`：判断当前对象是否为另一个对象的原型。
* `Object.prototype.propertyIsEnumerable()`：判断某个属性是否可枚举。
## 创建对象
* 分类
  * 工厂模式
  * 构造函数模式
  * 原型模式
  * 混合模式
  * 动态原型模式
* 对象的创建模式
	* 工厂函数创建对象
```
  function Person(){
    var obj = {}
    obj.name = 'Tom'
    obj.setAge = function(){
      this.age = 16
    }
    return obj
  }
```
  * Object构造函数模式
```
  var obj = {};
  obj.name = 'Tom';
  obj.setName = function(name){this.name=name;};
```
  * 对象字面量模式
```
  var obj = {
    name : 'Tom',
    setName : function(name){this.name = name;}
  };
```
  * 构造函数模式
```
  function Person(name, age) {
    this.name = name;
    this.age = age;
    this.setName = function(name){this.name=name;};
  }
  new Person('tom', 12);
```
  * 构造函数+原型的组合模式
```
  function Person(name, age) {
    this.name = name;
    this.age = age;
  }
  Person.prototype.setName = function(name){this.name=name;};
  new Person('tom', 12);
```
## 继承模式
* 原型链继承: 得到方法
```
  function Parent(){}
  Parent.prototype.test = function(){};
  function Child(){}
  Child.prototype = new Parent();
  var child = new Child(); //有test()
```
* 借用构造函数&&call(): 得到属性
```
  function Parent(xxx){this.xxx = xxx}
  Parent.prototype.test = function(){};
  function Child(xxx,yyy){
      Parent.call(this, xxx);//借用构造函数   this.Parent(xxx)
  }
  var child = new Child('a', 'b');  //child.xxx为'a', 但child没有test()
```
* 组合
* 组合继承, 有时候也叫做伪经典继承,指的是将原型链和借用构造函数的技术组合到一块,从而发挥两者之长的一种继承模式.
```
  function Father(name){
    this.name = name;
    this.colors = ["red","blue","green"];
  }
  Father.prototype.sayName = function(){
    alert(this.name);
  };
  function Son(name,age){
    Father.call(this,name);//继承实例属性，第一次调用Father()
    this.age = age;
  }
  Son.prototype = new Father();//继承父类方法,第二次调用Father()
  Son.prototype.sayAge = function(){
    alert(this.age);
  }
  
  var instance1 = new Son("louis",5);
  instance1.colors.push("black");
  console.log(instance1.colors);//"red,blue,green,black"
  instance1.sayName();//louis
  instance1.sayAge();//5
  
  var instance1 = new Son("zhai",10);
  console.log(instance1.colors);//"red,blue,green"
  instance1.sayName();//zhai
  instance1.sayAge();//10
  ```
## 拷贝
* 普通拷贝: 将obj对象赋值给了newObj对象
* 浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存
```
  var obj = {
      name: 'xiaoming',
      age: 23
  };
  var newObj = obj;
  newObj.name = 'xiaohua';
  console.log(obj.name); // 'xiaohua'
  console.log(newObj.name); // 'xiaohua'
```
* 深度拷贝: `Object.assign()`方法进行对象的深拷贝可以避免源对象被篡改的可能
* 深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象
```
  var obj2 = {
    name: 'xiaoming',
    age: 23
  };
  var newObj2 = Object.assign({}, obj2, {color: 'blue'});
  newObj2.name = 'xiaohua';
  console.log(obj2.name); // 'xiaoming'
  console.log(newObj2.name); // 'xiaohua'
  console.log(newObj2.color); // 'blue'
```
* 我们也可以使用`Object.create()`方法进行对象的拷贝, `Object.create()`方法可以创建一个具有指定原型对象和属性的新对象
```
  var obj3 = {
        name: 'xiaoming',
        age: 23
  };
  var newObj3 = Object.create(obj3);
  newObj3.name = 'xiaohua';
  console.log(obj3.name); // 'xiaoming'
  console.log(newObj3.name); // 'xiaohua'
```   
* 实例
```
  let a ={}
  //浅拷贝
  let b = a
  //深复制包含子对象
  let c = JSON.parse(JSON.stringify(a))
  //拷贝一层但不包含子对象
  let d = {...a}
``` 
## 基本数据类型与引用数据类型
* 内存
  * 内存分为两种结构：栈内存和堆内存
  * 栈内存用来保存变量, 堆内存用来保存对象
* 当创建一个基本数据类型的变量时, 变量会保存到栈内存中, 同时变量会直接保存基本数据类型的值, 
  当修改一个基本数据类型的值时, 由于每一个变量都是独立的, 不会影响其他的变量
* 当创建一个引用类型(对象)的变量时, 变量会保存到栈内存中, 对象会保存到堆内存, 
  而在栈内存的变量中保存的是堆内存的地址, 当我们对变量进行操作时, 实际上是在操作堆内存中的对象。
  可以有多个变量同时指向一个对象, 这样当我们修改一个变量时, 其他的变量也会受到影响
**当比较两个对象是否相等时, 比较的是对象的内存地址**
* ![](/images/栈和堆.png)
## 对象属性的增删改查
* 添加属性
  * 语法:
    * 对象.属性名 = 属性值;
    * 对象['属性名'] = 属性值;
      *必须加引号, 不然将会当成变量解析*
* 读取属性
  * 语法:
    * 对象.属性名
    * 对象['属性名]
* 修改属性
  * 语法: 
    * 对象.属性名 = 新属性值
    * 对象['属性名'] = 新属性值
* 删除属性
  * 语法:
    * delete 对象.属性名
## 圾回收（GC）
* 当一个对象没有任何的变量对其引用时, 这种对象我们就认为是垃圾, 需要清理出内存
* 在JS中拥有自动的垃圾处理的机制, 这些垃圾对象会自动被JS引擎所回收, 不需要我们手动处理
* 我们只需要将不再使用的对象和变量之间的引用断开即可	
