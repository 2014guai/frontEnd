# grunt

## 安装
* 安装nodejs, 查看版本: `node -v`
* 创建一个简单的应用
  ```
  |- build              //构建生成的文件所在的文件夹
    |- src   
      |- js             //js源文件夹
      |- css            //css源文件夹
    |- index.html       //页面文件
    |- Gruntfile.js     //grunt配置文件
    |- package.json     //项目的配置文件
      {
        "name": "grunt_test",  //项目名称  
        "version": "1.0.0",    //版本
        "devDependencies": {   //编译期依赖模块
        }
      }  
  ```
* 全局安装grunt-CLI: 
  * `npm install -g grunt-cli`
* 安装grunt
    * 命令: `npm install grunt --save-dev`
    * 
    ```json
    // package.json:
    {
      "name": "grunt_test",
      "version": "1.0.0",
      "devDependencies": {
        "grunt": "^1.0.1"
      }
    }
    ```
    * 命令: `grunt`  //提示 Warning: Task "default" not found
## 配置Gruntfile.js
* 此配置文件本质就是一个node函数模块
* 配置编码包含3步:
  * 初始化插件配置
  * 加载插件任务
  * 注册默认任务
* 基本编码:
  ```
  module.exports = function(grunt){
    //1.初始化插件配置
    grunt.initConfig({
        
    });
    //2.加载插件任务
    //3.注册默认任务
    grunt.registerTask('default', []);
  };
  ``` 
* 命令: grunt  //提示成功, 但没有任何效果(还没有使用插件)
## Grunt插件介绍
* grunt官网的插件列表页面http://www.gruntjs.net/plugins 
* 插件分类:
  * grunt团队贡献的插件: 插件名都以contrib-开头
  * 第三方提供的插件: 不以contrib-开头
* 常用的插件:
    * Contrib-concat-->合并多个文件的代码到一个文件中
    * Contrib-uglify-->压缩js文件
    * Contrib-jshint-->javascript语法错误检查
    * Contrib-cssmin-->压缩/合并css文件
    * Contrib-watch-->实时监控文件变化、调用相应的任务重新执行
    * Contrib-clean-->清空文件、文件夹
    * Contrib-copy-->复制文件、文件夹
    * karma-->前端自动化测试工具
### 使用concat插件
* 命令: `npm install grunt-contrib-concat --save-dev`
* 编码:
  ```
  //src/js/test1.js
  (function () {
    function add(num1, num2) {
      return num1 + num2;
    }
    console.log(add(10, 20));
  })();
  
  //src/js/test2.js
  (function () {
    var arr = [2,3,4].map(function (item, index) {
      return item+1;
    });
    console.log(arr);
  })();
  ```
* 配置: Gruntfile.js
  * 配置任务:
    ```
    concat: {
      options: {
        separator: ';'   //使用;连接合并
      },
      build: {
        src: ["src/js/*.js"],  //合并哪些js文件
        dest: "build/js/built.js" //合并输出的js文件
      }
    }
    ```
  * 加载任务:
    `grunt.loadNpmTasks('grunt-contrib-concat');`
  * 注册任务:
    `grunt.registerTask('default', ['concat']);`
  * 命令: 
    `grunt   //会在build下生成一个built.js`
### 使用uglify插件
* 命令: `npm install grunt-contrib-uglify --save-dev`
* 配置: Gruntfile.js
  * 配置任务:
    ```
    pkg : grunt.file.readJSON('package.json'),
      uglify : {
        options: {
          banner: '/*! <%= pkg.name %> - v<%= pkg.version %> - ' +
          '<%= grunt.template.today("yyyy-mm-dd") %> */'
        },
        my_target: {
          files: {
            'build/built-<%=pkg.name%>-<%=pkg.version%>.min.js': ['build/js/built.js']
          }
        }
      }
    ```
    * 加载任务:
      `grunt.loadNpmTasks('grunt-contrib-uglify');`
    * 注册任务:
      `grunt.registerTask('default', ['concat', 'uglify']);`
    * 命令: 
      `grunt   //会在build下生成一个压缩的js文件`
### 使用jshint插件
* 命令: npm install grunt-contrib-jshint --save-dev
* 编码: .jshintrc
  ```
  {
    "boss": false,
    "curly": true, 
    "eqeqeq": true, 
    "eqnull": true,
    "expr" : true,
    "immed": true, 
    "newcap": true, 
    "noempty": true,
    "noarg": true, 
    "undef": true, 
    "regexp": true,
    "browser": true,
    "devel": true,
    "node": true
  }
  ```
* 修改src/js/test1.js
  ```
  (function () {
    function add(num1, num2) {
      num1 = num1 + num3
      return num1 + num2;
    }
    console.log(add(10, 20));
  })();
  ```
* 配置 : Gruntfile.js
  * 配置任务:
    ```
    jshint : {
      options: {
        jshintrc : '.jshintrc'
      },
      build : ['Gruntfile.js', 'src/js/*.js']
    }
    ```
  * 加载任务:
    `grunt.loadNpmTasks('grunt-contrib-jshint');`
  * 注册任务:
    `grunt.registerTask('default', ['concat', 'uglify', 'jshint']);`
  * 命令: 
    `grunt   //提示变量未定义和语句后未加分号 -->修改后重新编译`
### 使用cssmin插件
* 命令: `npm install grunt-contrib-cssmin --save-dev`
* 编码: 
  ```
  //test.css
    #div1 {
      width: 100px;
      height: 100px;
      background: red;
    }
    //test2.css
    #div2 {
      width: 200px;
      height: 200px;
      background: blue;
    }
    //index.html
    <link rel="stylesheet" href="build/css/output.min.css">
    <div id="div1">div11111</div>
    <div id="div2">div22222</div>
  ```
* 配置 : Gruntfile.js
  * 配置任务:
    ```
    cssmin:{
      options: {
        shorthandCompacting: false,
        roundingPrecision: -1
      },
      build: {
        files: {
          'build/css/output.min.css': ['src/css/*.css']
        }
      }
    }
    ``` 
  * 加载任务:
    `grunt.loadNpmTasks('grunt-contrib-cssmin');`
  * 注册任务:
    `grunt.registerTask('default', ['concat', 'uglify', 'jshint', 'cssmin']);`
  * 命令: 
    `grunt    //在build/css/下生成output.min.css`
* 使用watch插件（真正实现自动化）
  * 命令: npm install grunt-contrib-watch --save-dev
  * 配置 : Gruntfile.js
    * 配置任务:
      ```
      watch : {
        scripts : {
          files : ['src/js/*.js', 'src/css/*.css'],
          tasks : ['concat', 'jshint', 'uglify', 'cssmin'],
          options : {spawn : false}
        }
      }
      ```
    * 加载任务:
      `grunt.loadNpmTasks('grunt-contrib-watch');`
    * 注册任务:
      `grunt.registerTask('default', ['concat', 'uglify', 'jshint', 'watch']);`
    * 命令: 
      `grunt   //控制台提示watch已经开始监听, 修改保存后自动编译处理`
    