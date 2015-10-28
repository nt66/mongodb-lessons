
##CRUD
###插入
####单条插入
>db.person.insert("name":"hlf","age":30)
####批量插入
> for(var i=0;i<1000;i++){
> db.person.insert("name":"guest"+i,"age":i)
> }




