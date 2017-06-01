## Mongoose

难点1：mongoose的内存数据与数据库数据相互映射的思想
    schema 定义数据骨架
    model 定义数据模型：映射数据库中的集合(collection)
    entity 数据实体：映射数据库中的文档(document)
    
  
  难点2：异步执行的乱序问题
    异步执行的函数，一定会执行，
    但是，执行的次序不可控。
    执行次序该怎么控制呢？
    异步IO执行代码，在回调函数执行的时候，一定已经完成操作，
    那么，在回调函数里面写后续操作就一定按照次序执行了
  
  
  难点3：查询代码与功能逻辑代码相分离
    把业务逻辑进行封装
    把查询过程进行封装
    “实参”是一个函数
  

  难点4：模块化

* Mongoose是什么?
	* Mongoose是MongoDB nodejs驱动，可以在异步的环境下执行
* 安装Mongoose
	* npm install mongoose
* 使用Mongoose
	//引入mongoose
	var mongoose = require('mongoose');

	//连接数据库
	mongoose.connect('mongodb://localhost/atguigu_o2o');
	
	
//Schema
var Schema  = mongoose.Schema;
var userSchema = new Schema({
	phone : String
});
//Model
var UserModel = mongoose.model('user', userSchema);

//使用model构造函数进行查询/更新/删除
UserModel.find({name:value}, function(error, userArr){}) : 查找多个: 数组
UserModel.findOne({name:value}, function(error, user){}) : 查找一个 : 对象
UserModel.update({_id:user._id}, user, function(err, result){); : 更新
UserModel.remove({_id:'xxxxx'}, function(err, result){}); : 删除
//使用model实例对象进行添加
var userModel = new UserModel(user);
userModel.save(function(error, user){});



//创建Schema的实例对象
var Schema = mongoose.Schema;
var userSchema = new Schema({ //指定所有字段
  phone : String
});
//根据userSchema生成模型
var UserModel = mongoose.model('user', userSchema);

//查询得到所有数据
UserModel.find(function(err, users){
  
});
//查询得到一个文档(记录)
UserModel.findOne({_id: 'xxx'}, function(err, user)) {
  
}
//保存一个文档(记录)
var userModel = new UserModel({phone : '13712341234'});
userModel.save(function(err, user){

});
//更新一个文档(记录)
UserModel.update({_id:user._id}, user, function(err, result){
  
});
//删除一个文档(记录)
UserModel.remove({_id:'xxxxx'}, function(err, result){
  
});



//得到连接对象
var conn = mongoose.connection;

//监听打开连接
db.on('open', function() {
    console.log('we are connected!');
});

//监听打开连接
db.on('close', function() {
    console.log('we are connected!');
});

//设置连接错误的监听
  db.on('error', console.error.bind(console, 'connection error:'));