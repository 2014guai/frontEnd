# 函数
## 概述
* 函数也是对象
* 除了可以封装属性外, 还可以封装可执行的代码
* 函数调用时, 内部代码才会执行
## 目录
* [函数](#函数)
* [函数的创建](#函数的创建)
* [arguments](#arguments)
* [this](#this)
* [改变this](#改变this)
* [IIFE](#IIFE)
***

## 函数
* 多条可执行语句的封装体-->函数是一个可执行的东西
* 函数也是对象
  * 从语法上判断: `instanceof()`
  * 可以通过"."操作内部属性/方法: `fn.prototype/fn.call()/apply()`
* 函数的3种不同角色
  * 一般函数: 直接调用
  * 构造函数: 通过new调用
  * 对象: 通过"."调用内部的属性/方法
## 函数的创建
* 构造函数
  * `var obj = new Object()`
  * 其实构造函数就是一个普通的函数, 但是我们的构造函数习惯首字母大写
  * 构造函数通过new关键字来调用
  * 定义一个构造函数：
    * ```
      function CreatPerson(name , age){
        this.name = name;
        this.age = age;
        this.sayHello = function(){};
      }
       var jc = new CreatPerson();
      ```
  * 构造函数的执行的过程：
    * 创建一个新的对象
    * 以这个新对象作为this, 然后调用函数
    * 将新建的对象作为返回值返回
  * 每一个对象都有一个隐含的属性constructor, 用来保存它自己的构造函数
  * 可以通过`instanceof()`来判断一个对象是否属于某个构造函数的实例
  * 语法：`对象 instanceof(构造函数)`, 如果是则返回true, 否则返回false
    由于Object是所有对象的祖先, 所以任何对象和Object进行instanceof运算都会返回true
* 函数声明表达式
  * ```
    function fn (){
      语句...
    }
    ```
* 匿名函数
  * ``` 
    var fn = function(){
      语句..
    }
    ```
* 工厂方法
  * 例:
    * ```
      //工厂函数
      function createPerson(name, age){
        //新创建一个对象
        var obj = new Object();
        //向对象中添加属性和方法
        obj.name = name;
        obj.age = age;
        obj.sayHello = function(){};
        //将对象返回
        return obj;
      }
      //创建实例
      var per = createPerson("swk", 18);
      ```
    * 使用工厂方法创建的对象全都是Object类型的对象, 我们无法识别不同的对象的类型
    * 我们希望创建一个人的对象, 使用`Person()` 创建一个狗的对象, 使用`Dog()`
## arguments
* 每个函数在执行时, 浏览器都会默认传递两个隐藏的参数
  * 一个是执行的上下文对象：this
  * 一个是封装实参的对象：arguments
* arguments是类数组的对象, 我们调用函数时所有的实参都会在arguments中保存
  * 我们可以通过arguments[索引]来获取实参
* arguments中还封装了一个属性callee, 这个属性指向的是当前函数本身
## this
 * 浏览器在调用一个函数时, 它会默认传递进一个参数, 这个参数叫this, 代表的是执行函数的上下文对象
* 函数中的this
  * 显式指定谁: `obj.xxx()`
  * 通过call/apply指定谁调用: `xxx.call(obj)     `                                               
  * 不指定谁调用, `xxx()` : window
  * 回调函数: 看背后是通过谁来调用的: window/其它
* this的指向：
  * 全局环境：this始终指向的是window对象
  * 局部环境：
    * 直接调用函数：this指向 window
    * 对象函数调用：哪个对象调用就指向哪个对象
    * 使用 new 实例化对象，在构造函数中的this指向实例化对象。
* 使用场景：
  * 用于区分全局变量和局部变量，需要使用this
  * 返回函数当前的对象： 比如jQuery源码
  * 将当前的对象传递到下一个函数： 好吧--->还是jQuery 
## 改变this
* 使用call()或apply()、bind()改变this的指向
  * apply 、 call 、bind 三者都是用来改变函数的this对象的指向的；
  * apply 、 call 、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文；
  * apply 、 call 、bind 三者都可以利用后续参数传参；
  * bind 是返回对应函数，便于稍后调用；apply 、call 则是立即调用 
  ```
  call: fn.call(target, 1, 2)
  apply: fn.apply(target, [1, 2])
  bind: fn.bind(target)(1,2)
  ```
## IIFE
* 为什么会有IIFE
  * 在javascript中, 每一个函数在被调用的时候都会创建一个执行上下文
  * 在该函数内部定义的变量和函数只能在该函数内部被使用
  * 而正是因为这个上下文, 使得我们在调用函数的时候能创建一些私有变量
* 执行的过程
  * 因为在javascript里, 括号内部不能包含语句, 当解析器对代码进行解释的时候, 先碰到了"()"
  * 然后碰到function关键字就会自动将()里面的代码识别为函数表达式而不是函数声明
* 两种常见写法
  * `(function(){}())`
  * `(function(){})()`
* 优点
  * 提升性能
    * 减少作用域的查找
    * 参数一般为window、document、jQuery
    * 将全局对象放在IIFE作用域内提升JS解析器的查找速度和性能
  * 有利于压缩
  * 避免冲突
  * 依赖加载
* 应用
  * jQuery
