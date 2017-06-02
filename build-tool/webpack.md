# webpack

## 了解Webpack相关
* 什么是webpack
  * Webpack是一个模块打包器
  * 它将根据模块的依赖关系进行静态分析, 然后将这些模块按照指定的规则生成对应的静态资源
* Webpack 的特点
  * 代码拆分
    * Webpack有两种组织模块依赖的方式, 同步和异步, 每一个异步区块都作为一个文件被打包
  * 理解Loader
    * Webpack本身只能处理原生的js模块, 但是loader转换器可以将各种类型的资源转换成js模块
  * 智能解析
    * 几乎可以处理任何第三方库, 包括普通的js
  * 插件系统
    * Webpack还有一个功能丰富的插件系统
    * 大多数内容功能都是基于这个插件系统运行的
  * 快速运行
    * Webpack使用异步I/O和多级缓存提高运行效率, 这使得Webpack能够以令人难以置信的速度快速增量编译
* 理解Loader
  * Webpack本身只能处理JavaScript模块, 如果要处理其他类型的文件, 就需要使用 loader 进行转换
  * Loader本身也是运行在node.js环境中的JavaScript模块
  * 它本身是一个函数, 接受源文件作为参数, 返回转换的结果
  * loader一般以xxx-loader的方式命名, xxx代表了这个loader要做的转换功能, 比如 json-loader
* 配置文件
  * 项目根目录下配置文件webpack.config.js: 这个文件是一个 node.js 模块, 返回一个 json 格式的配置信息对象
* 插件
  * 插件件可以完成更多loader不能完成的功能。
  * 插件的使用一般是在webpack的配置信息plugins选项中指定。
  * Webpack本身内置了一些常用的插件, 还可以通过 npm 安装第三方插件
## 学习文档 : 
* webpack官方入门: http://webpack.github.io/docs/tutorials/getting-started/
* Webpack中文指南: http://zhaoda.net/webpack-handbook/index.html
## 你将学到:
* How to install webpack
* How to use webpack
* How to use loaders
* How to use the development server
* How to use image
## 创建一个简单的应用webpack_test
  ```
  |- dist
    |- src
      |- js
      |- css
      |- img
    |- index.html    
    |- package.json 
      {
        "name": "webpack_test",
        "version": "1.0.0",
        "devDependencies": {
          
        }
      } 
  ```
## 安装webpack
* `npm install webpack -g`, 全局安装
* `npm install webpack --save-dev`, 局部安装
## 开始编译
* 创建入口js : src/js/entry.js
  * `document.write("It works.");`
* 创建主页面 : index.html
  * `<script type="text/javascript" src="dist/bundle.js"></script>`
* 编译js
  * webpack src/js/entry.js dist/bundle.js
* 查看页面效果
## 第二个js
* 创建第二个js: src/js/content.js
  * `module.exports = " <br> It works from content.js.";`
* 更新入口js : src/js/entry.js
  * `document.write("It works.");`
  * `document.write(require("./content.js"));`
* 编译js:
  * `webpack src/js/entry.js dist/bundle.js`
* 查看页面效果
## 第一个加载器(loader)
* 安装样式的loader
  * npm install css-loader style-loader --save-dev
* 创建样式文件: src/css/test.css
  ```
  body {
    background: yellow;
  }
  ```
* 更新入口js : src/js/entry.js
  * `require(""!style!css!../css/test.css");`
  * `document.write("It works.");`
  + `document.write(require("./content.js"));`
* 编译js, 并查看页面效果
  * webpack src/js/entry.js dist/bundle.js
## 绑定加载器
* 更新入口js : src/js/entry.js
  - require("!style!css!../css/test.css");
  + require("../css/test.css");
* 编译:
  * webpack src/js/entry.js dist/bundle.js --module-bind "css=style\!css"
* 查看页面效果
## 使用webpack配置文件
* 创建webpack.config.js
  ```
  module.exports = {
    entry: "./src/js/entry.js",
    output: {
      publicPath : './dist/'
      path: './dist/',
      filename: "bundle.js"
    },
    module: {
      loaders: [
        { test: /\.css$/, loader: "style!css" }
      ]
    }
  };
  ```
* 编译
  * webpack
  * webpack --progress --colors   //编译显示进度带颜色
  * webpack --watch  //编译并启动监视(自动编译但需要刷新浏览器)
* 使用开发服务器(自动编译并刷新浏览器)
  * `npm install webpack-dev-server -g`
  * `webpack-dev-server`
  * `http://localhost:8080/webpack-dev-server/bundle`
## 加载图片
* 安装依赖的loader
  * `npm install url-loader file-loader --save-dev`
* 添加config中loader的配置
  `{ test: /\.(png|jpg)$/, loader: "url-loader?limit=8192" }  //如果图片小于limit就会进行Base64编码`
* 拷入2张图片: 
  * 小图: src/img/logo.png
  * 大图: src/img/big.jpg
* 定义引用图片的样式: src/css/test.css
  ```
  #div1{
    background-image: url(./src/img/logo.jpg);
    height: 200px;
    width: 200px;
  }
  #div2{
    background-image: url(./src/img/big.jpg);
    height: 200px;
    width: 200px;
  }
  ```
* 在页面引用样式或图片: index.html
  ```
  <img src="src/img/logo.jpg">
  <div id="div1"></div>
  <div id="div2"></div>
  ```
* 编译并浏览
  * webpack-dev-server
------------------------------------------------------------------------------------------
* chcp 65001 就是换成UTF-8代码页
