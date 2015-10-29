mongodb-lessons
=====
mongodb修炼记

点击[全文][df1]

## CRUD
### 插入
单条插入:
```sh
db.person.insert({"name":"hualingfeng","age":"31"});
```
多条插入：
```sh
for(var i=0;i<1000;i++){ 
  db.person.insert("name":"guest"+i,"age":i) 
}
```

### 查找
```sh
db.person.find({"age":{$gt:22}})     //find age > 22
```
```sh
db.person.find({"age":{$lt:22}})     //find age < 22
```
```sh
db.person.find({"age":{$gte:22}})    //find age >= 22
```
```sh
db.person.find({"age":{$lte:22}})    //find age <= 22
```
```sh
db.person.find({"age":{$ne:22}})     //find age != 22
```
```sh
db.person.find({"age":22})           //find age = 22
```
```sh
db.person.find({"name":"hua","age":{$gt:22}})             //find name = hua AND age > 22
```
```sh
db.person.find({$or:[{"name":"hua"},{"age":{$gt:22}}]})   //find name = hua||age > 22
```
```sh
db.person.find({"name":{$in:["hua","hua1","hua2"]}})      //find name in ["hua","hua2","hua3"]
```
```sh
db.person.find({"name":{$nin:["hua","hua1","hua2"]}})     //find name not in ["hua","hua1","hua2"]
```

### 更新
##### 整体更新
用于文档结构变化较大的情况；按照update()值来更新;原先有的会被删除 
```sh
db.person.update({"name":"hua"},{"age":31})     
```

##### 局部更新
用于文档变化较小，局部字段改变
```sha
db.person.update({"name":"hua"},{$inc:{"age":30}})  //$inc 在原来的基础上增加 30
db.person.update({"name":"hua"},{$set:{"age":30}})  //$set 设置值，没有就新创建
db.person.update({},{},true,true)                   //第三个参数true若没找到就新增；第四个参数true，若有多条就批量更新
```

### 删除
```sha
db.person.remove({})               //删除全部
db.person.remove({"name":"hlf"})   //删除hlf
```
### 聚合
#### 统计&去重
```sha
db.person.count({"age":20}) //age=20的数量
db.person.distinct("age")   //age去重后的数组
```
#### group
#### mapreduce
#### 游标

### 索引
```sh
db.person.ensureIndex({"name":1})//name建立索引，1升序，-1降序
db.person.find({"name":"hxc"+100000}).explain() //explain 是分析工具

db.person.ensureIndex({"name":1},{"unique":true}) //重复的键不能插入
db.person.ensureIndex({"name":1},{"unique":true})
db.person.insert("name":"hlf","age":20)
db.person.insert("name":"hlf","age":32)
~~~error~~~

db.person.ensureIndex({"name":1,"birthday":1}); //组合索引

db.person.dropIndex("name_1"); //删除"name":1 索引
db.person.dropIndex("name_1_birthday_1"); //删除组合索引
```
### 主从复制
#### 集群
主从好处：数据备份、数据恢复、读写分离
```sh
主数据库 mongod --dbpath="mongodb1" --master
副数据库 mongod --dhpath="mongodb2" --port 2222 --slave --source="mongodb1"
```
连接之后，副数据库每10s会从主数据库中同步数据

#### 副本集
无特定的主数据库，如果主数据库宕掉，会选出从数据库顶上
```sh
mongod --dbpath="" --port 2222 --replSet test/127.0.0.1:2222    //--replSet 集群设置
mongod --dbpath="" --port 3333 --replSet test/127.0.0.1:3333
//另一个数据库服务
初始化副本集: mongo 127.0.0.1:2222/admin //随便选一台服务器进入admin
db.runCommand({"repSetInitiate":{
"_id":test
"members":[
 {
  "_id":1,
  "host":"127.0.0.1:2222"
 },
 {
  "_id":2,
  "host":"127.0.0.1:3333"
 }
]}})

mongo 127.0.0.1:2222/admin 
rs.addArb("...") //追加仲裁服务器

mongo 127.0.0.1:2222/admin 
rs.status() //察看服务器状态
```

[df1]: <http://blog.csdn.net/hechurui/article/category/5627917>






