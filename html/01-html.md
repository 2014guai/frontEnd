# html
## 概述
* 超文本标记语言(Hypertext Markup Language)
* 用来定义网页的整体结构
* w3c标准：
  * web产业是条河流, 程序员是中游, 浏览器制造商是上游, 用户是下游
  * 我们位于接口的位置, 满足下游用户用不同浏览器看到同样的内容
## 目录
* [html页面的基本结构](#html页面的基本结构)
* [标签](#标签)
* [doctype](#doctype)
* [meta标签](#meta标签)
* [css、js引入](#css、js引入)
* [注释](#注释)
* [实体字符](#实体字符)
* [超链接](#超链接)
* [内联框架](#内联框架)
* [框架集](#框架集)
* [文本标签](#文本标签)
***

## html页面的基本结构
```
<!doctype html> <!-- 文档的声明, 声明当前网页的版本, 这个声明表示网页是html5的 -->
<html> <!-- 网页的根标签, 一个页面中只有一个根标签, 网页中所有的内容都需要写到根标签中 -->
  <head> <!-- head标签中的内容不会直接在网页中显示, 它用来告诉浏览器如何解析网页 -->
    <title></title> <!-- 网页的标题, 搜索引擎检索时最重要的内容, 搜索会根据他来判断页面的主要内容 -->
    <meta charset="utf-8" /> <!-- 用来设置网页的字符集 -->
  </head>
  <body> <!-- 网页的主体内容, 所有需要在页面中显示的内容, 都应该写在body标签中 -->
    <!-- 网页的主体内容 -->
  </body> 
</html>
```
![](/images/网页.png)
## 标签(元素)
* 语法：
  * <标签名></标签名>, 一般标签成对出现, 如:`<p></p>`
  * <标签名/>, 自结束标签, 如:`<input/>`
* 属性
  * 键值对结构
  * 设置在成对标签的开始标签或自结束标签
* 分类：
  * 内联元素：只占用自身内容的大小, 不会占用一整行
  * 块元素：单独占一整行
  * 注意：
    * 一般使用块级元素去包裹内敛元素, 而不会使用内联元素去包裹块元素
    * a标签可以包裹任何元素, 除了a本身
    * p标签不能嵌套任何的块级元素
* 元素间的关系：
  * 父元素
  * 子元素
  * 祖先元素
  * 后代元素
  * 兄弟元素
## doctype
* 文档声明, 告诉浏览器网页的版本
* html5：<!doctype html>
## meta标签
* 设置页面中字符集
  * `<meta charset="utf-8" />`
* 设置当前页面的关键字
  * `<meta name="keywords" content="关键字1,关键字2,关键字N" />`
* 设置当前页面的描述（简介）
  * `<meta name="description" content="网页的描述" />`
*  设置页面的重定向
  * `<meta http-equiv="refresh" content="秒数;url=目标地址" />`
*  通过meta来为网页设置关键字和描述, 会被搜索引擎检索
  * 并且会在搜索结果中显示出来, 但是并不会影响页面的排名
## css、js引入
* css: `<link rel="stylesheet" href="文件相对路径">`
* js: `<script type="text/javascript" src="文件相对路径"></script>`
## 注释
* 语法：`<!-- 注释 -->`
* 注释中的内容不会在网页中显示, 但是会在网页的源码中显示, 我们可以通过注释来对网页进行描述
* 一定要养成良好的编写注释的习惯
## 实体字符
* 又名转义字符
* 语法：`&实体名字;`
* 例如：
  * 大于号：`&gt;` &gt;
  * 小于号：`&lt;` &lt;
  * 空格： `&nbsp;` &nbsp;
  * 版权声明: `&copy;` &copy;
## 图片
* 语法
  * `<img src="文件相对路径" alt="文件描述"/>`
* web中常见的标签格式
  * jepg
    * 支持的颜色比较多, 可以显示照片等
    * 不支持透明
  * gif
    * 支持颜色较少, 显示单一图片
    * 支持全透明, 不支持半透明
  * png
    * 支持颜色比较多, 功能比较强大
    * 完全支持透明
* 图片使用的规则：
  * 效果一致, 用最小的
  * 效果不一致, 用效果最合适的
## 超链接
* 作用：页面间跳转
* 用法：`<a href="地址"></a>`
  * 跳转到一个外部的网页
    * `<a href="http://www.baidu.com">去Baidu</a>`<a href="http://www.baidu.com">去Baidu</a>
  * 跳转到内部页面
    * `<a href="相对路径">超链接</a>`<a href="相对路径">超链接</a>
  * 跳转到当前页面的指定位置
    * `<a href="#">回顶部</a>`<a href="#">回顶部</a>
    * `<a href="#id属性值">去指定位置</a>`<a href="#id属性值">去指定位置</a>
  * 发送邮件的超链接
    * `<a href="mailto:邮件地址">发送邮件</a>`<a href="mailto:邮件地址">发送邮件</a>
## 内联框架
* 作用：用于向页面中引入另一个页面
* 用法：`<iframe src="外部页面地址或相对路径" name="" frameborder="0"></iframe>`
* 弊端：内联框架中的内容不会被搜索引擎检索
## 框架集
* <frameset>
* 框架集和iframe(内联框架)的作用类似, 都可以向网页引入页面, 
  但是不同的是iframe只引入一个, frameset可以引入多个
* 例子：
  ```
  <frameset rows="20%,*,50%">
    <frame src="" />
    <frame src="" />
    <frameset rows="20%,*,50%">
      <frame src="" />
      <frame src="" />
      <frame src="" />
    </frameset>
  </frameset>
  ```
* 属性：
  * rows --> 内联框架中所有页面, 按照一行一行的排列, 可以在rows指定每个框架的高度
  * cols --> 内联框架中的所有页面, 按照一列一列的排列, 可以在属性中指定每个框架的宽度
* 在实际开发中并不推荐使用内联框架和框架集, 但是如果非得用, 建议使用框架集。
## 文本标签
* `<em>`
  * 表示强调的内容
  * em一般是斜体显示
* `<strong>`
  * 表示强调重要的内容(比em要更强烈一些)
  * strong中的文字以加粗显示
* `<i>`
  * 单纯表示斜体，没有任何语义
* `<b>`	
  * 单纯表示加粗, 没有任何语义
  * 有些时候, 我们也会使用i和b去表示一些页面中的小图标
* `<small>`
  * small中的文字会比其父元素中的文字要小一些
  * 使用small一般表示一些细则一类的东西, 比如网站的copyright版权声明
* `<cite>`
  * cite表示引用的文献、歌曲、电影, 这些需要加书名号的内容
* `<q>`
  * 表示引用的内容, 它是一个行内引用
* `<blockquote>`
  * 表示引用的内容, 它和q的区别是, 它是一个块元素, 引用会独占一行
* `<sup>`
  * 表示一个上标
* `<sub>`	
  * 表示一个下标
* `<del>`
  * 表示一个删除的内容, 默认会在文字上添加删除线
* `<ins>`
  * 表示一个插入的内容, 默认会在文字上添加下划线
* `<pre>`
  * 预格式标签, 它会保留代码中的空格换行等等
* `<code>`
  * 专门用来表示程序代码
  * 一般pre和code会结合使用, 来表示一段程序
  * 内写html代码时, 需把实体(符号)转义
* 无序列表
  * 无序列表使用符号作为项目符合
  ```
  // 无需列表
  <ul>
    <li>无序列表1</li>
    <li>无序列表2</li>
  </ul>
  ```
  * 页面呈现：
  <ul>
    <li>无序列表1</li>
    <li>无序列表2</li>
    </ul>
* 有序列表
  * 有序列表使用有序的序号作为项目符合
  ```
  // 有序列表
  <ol>
    <li>有序列表1</li>
    <li>有序列表2</li>
  </ol>
  ```
  * 页面呈现：
  <ol>
    <li>有序列表1</li>
    <li>有序列表2</li>
  </ol>
* 定义列表	
  ```
  // 定义列表
  <dl>
    <dt>定义项1</dt>
    <dd>定义描述1</dd>
    <dt>定义项2</dt>
    <dd>定义描述2</dd>
  </dl>
  ```
  * 页面呈现：
  <dl>
    <dt>定义项1</dt>
    <dd>定义描述1</dd>
    <dt>定义项2</dt>
    <dd>定义描述2</dd>
  </dl>
* 列表中的所有的标签都是块元素, 并且列表是可以互相嵌套
* 导航条, 一般用无序列表写, 且ul、ol、dl均为块元素
* 去除列表的项目符号：
  `ul{list-style:none}`
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    