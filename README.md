mongodb-lessons
=====
mongodb修炼记

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






