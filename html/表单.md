# 表单
* 表单用来向服务器提交信息
* 表单相关的标签：
  * <form> 
    * 我们使用form标签来创建一个表单
    * 属性：
      * action：需要一个服务器的地址，指定地址以后，表单将会提交给相应的地址
      * method: 指定请求的类型
        * 可选值：
          * get:默认值, 发送get请求
          * post:发送post请求
  * 表单项
    * `<input type="" name="" value="" />`
      * 根据type的不同，input的显示方式也不同。
      * `type="text"` 文本框
      * `type="password"` 密码框
      * `type="radio"` 单选按钮
        * 这种单选按钮和多选框，都是通过name属性进行分组, 
          相同的name属性，浏览器会认为是一组
        * 这种选择框，不需要用户填写内容，必须指定value属性
      * `type="checkbox"` 多选框
        * 可以通过在多选框或单选按钮中添加一个`checked="checked"`，来将选项设置为默认选中
      * `type="submit"` 提交按钮
        * 可以通过value属性值来指定提交按钮上的文字
      * `type="reset"` 重置按钮
        * 重置按钮，可以将表单中的内容重置到默认值
    * 下拉列表：
      ```
      <select name=""> --> 用来创建一个下拉列表
        <optgroup label=""> --> 指定选项的分组，label用来指定分组的名字
          <option value=""></option> ---> 用来创建下拉列表中的选项
        </optgroup>
      </select>
      ```
      * 可以通过在option中添加`selected="selected"`来设置选项为默认选中
    * 多行文本域
      `<textarea name="" rows="" cols=""></textarea>`
      * rows:指定行数，可以使用css中height代替
      * cols:指定列数，可以使用css中width来代替
    * 按钮
      `<button type="">按钮上的文字</button>`
        * type的可选值：
          * submit : 提交按钮
          * reset : 重置按钮
          * button ：普通按钮
    * fieldset
      * 为表单项进行分组
    * legend
      * 指定分组的名字
    * label
      * 指定表单项的提示文字
      * 属性：for，可以指定一个表单项的id, 
        这样当点击label时，指定的表单项将会获取焦点