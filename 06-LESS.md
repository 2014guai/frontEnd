# LESS
## 概述
* CSS 预处理器
  * CSS 预处理器是一种语言用来为 CSS 增加一些编程的的特性
## 目录
* [变量](#变量)
* [嵌套](#嵌套)
* [混入](#混入)
* [嵌套](#嵌套)
* [导入](#导入)
* [兼容性](#兼容性)
***

## 变量
* LESS-->	@
* SASS--> $
## 嵌套
* 在父级元素下，直接写选择器及css样式
```less
section {
  margin: 10px;
  nav {
    height: 25px;
    a {
      color: #0982C1;
      :hover {
        text-decoration: underline;
      }
    }
  }
}
```
## 混入
* 
```less
.error(@borderWidth: 2px) {
  border: @borderWidth solid #F00;
  color: #F00;
}
```
* 直接在内部调用.error()即可
  ```less
  .generic-error {
    padding: 20px;
    margin: 4px;
    .error(); 
  }
  ```
## 继承
* 同混入类似，定义个相同的类，在内部调用即可
* 但要考虑CSS优先级的问题
## 导入
* @import
## 函数
* 了解即可
## 操作符	
* 编译时可以进行样式计算
  *
  ```less
  body {
    margin: (14px/2);
    top: 50px + 100px;
    right: 100px - 50px;
    left: 10 * 10;
  }
  ```
## 兼容性
  * 创建
    ```less
    .border-radius(@values) {
    -webkit-border-radius: @values;
       -moz-border-radius: @values;
            border-radius: @values;
    }
    ```
  * 应用
    ```less
    div {
      .border-radius(10px);
    }
    ```

