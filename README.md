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

###更新


