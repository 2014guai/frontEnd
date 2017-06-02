

## MVC
* 基本组成
  * 视图(View)：用户界面
    * 控制器(Controller)：业务逻辑
  * 模型(Model)：数据保存
  * M: Model模型, scope
  * V: View视图, 页面(指令, 表达式, 过滤器)
  * C: Controller控制器, controller
* 通信的模式
  * View, 传送指令到 Controller
  * Controller, 完成业务逻辑后, 要求Model改变状态
  * Model, 将新的数据发送到View, 用户得到反馈
* 互动模式
  * 通过view接收指令, 传递给controller
  * 通过controller接收指令
* MVC的案例
  * node.js
* MVC的一般流程
  * View(界面)触发事件
  * Controller(业务)处理了业务
  * 触发了数据更新
  * 不知道谁更新了Model的数据
  * Model(带着数据)回到了View
  * View更新数据

## MVVM
* http://www.cnblogs.com/whitewolf/p/4581254.html	
* M: Model模型, scope中的数据
* V: View视图, 页面(指令,表达式, 过滤器)
* VM: ViewModel视图模型, scope
![](/images/MVVM.png)






