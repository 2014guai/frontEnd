# 表格
* 表格用来表示一些格式化的数据, 表格之间可以互相嵌套
* 比如：账单、课程表、人名单
  * table
    * 使用table来创建表格
  * tr
    * 使用tr来创建表格中的一行
  * td
    * 使用td来创建表格中的单元格
  * th
    * 表示表格的表头
* 长表格：
  * 创建长表格时我们往往需要将一个表格分成几部分：
   * <caption>
        * 设置表格的标题
    * <thead>
      * 表示表格的头部
    * <tbody>
      * 表示表格的主体内容
      * 浏览器在渲染一个表格时，如果没有设置tbody，浏览器会自动在所有的tr外边添加一个tbody
      * 最好创建表格式，就将tbody加上
    * <tfoot>
      * 表示表格的底部信息
* 合并单元格：
  * colspan:横向的合并单元格
  * rowspan:纵向的合并单元格
* 表格的样式
  * color：设置文本颜色
  * padding: 设置内容与表格边框的距离
  * text-algin：设置文本水平对齐
  * vertical-algin：设置文本垂直对齐
    * 可选值：top、baseline、middle、bottom
  * border-spacing：设置边框间距
  * border-collapse：合并边框
    * collapse：合并边框
    * separate：不合并边框
	