# Gulp
## Gulp介绍
  * 中文主页: http://www.gulpjs.com.cn/
  * gulp是前端开发过程中对代码进行构建的工具, 是自动化项目的构建利器
  * gulp是基于Nodejs的自动任务运行器
  * 能自动化地完成 javascript/coffee/sass/less/html/image/css 等文件的
    测试、检查、合并、压缩、格式化、监听文件变化、浏览器自动刷新、部署文件生成等任务
  * gulp和grunt非常类似, 但相比于grunt的频繁IO操作, gulp的流操作能更快地更便捷地完成构建工作
* 安装nodejs, 查看版本: `node -v`
* 创建一个简单的应用gulp_test
  ```
  |- dist
    |- src
      |- js
      |- css
      |- less
    |- index.html    //页面文件
    |- gulpfile.js  //Gulp配置文件
    |- package.json  //项目的配置文件
      {
        "name": "gulp_test",
        "version": "1.0.0",
        "devDependencies": {
          
        }
      }
  ``` 
## 安装gulp:
* 全局安装gulp : `npm install gulp -g`
* 局部安装gulp : `npm install gulp --save-dev`
* 配置编码: gulpfile.js
  ```
  //引入gulp模块
  var gulp = require('gulp');
  //定义默认任务
  gulp.task('default', function() {
    // 将你的默认的任务代码放在这
  });
  ```
* 命令: gulp
## 使用gulp插件
* 相关插件:
  * gulp-concat: 合并文件(js/css)
  * gulp-uglify: 压缩js文件
  * gulp-rename: 文件重命名
  * gulp-less: 编译less
  * gulp-clean-css: 压缩css
  * gulp-livereload: 实时自动编译刷新
### 处理js
* 创建js文件
  * src/js/test1.js
    ```
    (function () {
      function add(num1, num2) {
        var num3 = 0;
        num1 = num2 + num3;
        return num1 + num2;
      }
      console.log(add(10, 30));
    })();
    ```
  * src/js/test2.js
    ```
    (function () {
      var arr = [2,3,4].map(function (item, index) {
        return item+1;
      });
      console.log(arr);
    })();
    ```
* 下载插件:
  * `npm install --save-dev gulp-concat gulp-uglify gulp-rename`
* 配置编码
  ```javascript
  var concat = require('gulp-concat');
  var uglify = require('gulp-uglify');
  var rename = require('gulp-rename');
  gulp.task('minifyjs', function() {
    gulp.src('src/js/*.js') //操作的源文件
      .pipe(concat('built.js')) //合并到临时文件     
      .pipe(gulp.dest('dist/js')) //生成到目标文件夹
      .pipe(rename({suffix: '.min'})) //重命名  
      .pipe(uglify())    //压缩
      .pipe(gulp.dest('dist/js'));
  });
  gulp.task('default', ['minifyjs']);
  ```
* 页面引入js浏览测试 : index.html
  `<script type="text/javascript" src="dist/js/built.min.js"></script>`
* 打包测试: gulp
### 处理css
* 创建less/css文件
  * src/css/test1.js
    ```
    #div1 {
      width: 100px;
      height: 100px;
      background: green;
    }
    ```
  * src/css/test2.js
    ```
    #div2 {
      width: 200px;
      height: 200px;
      background: blue;
    }
    ```
  * src/less/test3.less
    ```
    @base: red;
    .index1 { color: @base; }
    .index2 { color: black; }
    ```
* 下载插件:
  * `npm install --save-dev gulp-less gulp-clean-css` 
* 配置编码
  ```javascript
  var less = require('gulp-less');
  var cleanCSS = require('gulp-clean-css');
  gulp.task('cssTask', function () {
    gulp.src('src/less/*.less')
      .pipe(less())
      .pipe(gulp.dest('src/css'));
    gulp.src('src/css/*.css')
      .pipe(concat('built.css'))
      .pipe(gulp.dest('dist/css'))
      .pipe(rename({suffix: '.min'}))   
      .pipe(cleanCSS({compatibility: 'ie8'}))
      .pipe(gulp.dest('dist/css'));
  });
  gulp.task('default', ['minifyjs', 'cssTask']);
  ```
* 页面引入css浏览测试 : index.html
  `<link rel="stylesheet" href="dist/css/built.min.css">`
  `<div id="div1" class="index1">div1111111</div>`
  `<div id="div2" class="index2">div2222222</div>`
* 打包测试: gulp
### 自动编译刷新
* 下载插件
  * `npm install --save-dev gulp-livereload`
* 配置编码:
  ```javascript
  var livereload = require('gulp-livereload')
  //所有的pipe
  .pipe(livereload());
  gulp.task('watch', ['minifyjs', 'cssTask'], function () {    
    var server = livereload();
    gulp.task('watch', function() {
      livereload.listen();
      gulp.watch(['src/css/*.css', 'src/less/*.less'], ['cssTask']);
      gulp.watch('src/js/*.js', ['minifyjs'])
    });
  });
  ```
* 下载安装chrome插件: LiveReload_v2.1.0.crx
* 命令: gulp watch
* 测试访问: 通过虚拟地址访问页面, 并点插件图标启动, 修改js/css/less页面会自动编译并刷新浏览器