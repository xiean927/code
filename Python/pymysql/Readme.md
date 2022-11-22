
[如何打开mysql数据库？](https://blog.csdn.net/seanyang_/article/details/122221488)

[启动MySQL服务的两种方式（图解）](http://c.biancheng.net/view/7142.html)

[Python如何连接数据库，一文看懂](https://blog.csdn.net/laozhu_Python/article/details/107560672)


### 查询语句返回结果是多行的，如何实现

fetchall()获取所有数据
```
# 导入模块，固定写法
import pymysql
 
# 打开数据库连接     数据库地址
db = pymysql.connect("localhost", "root", "111223", "study_date")

# 使用 cursor() 方法创建一个游标对象 cursor
cursor = db.cursor()

# 使用 execute()  方法执行 SQL 查询
cursor.execute("select * from studys")

# 使用 fetchall() 方法获取所有数据.以元组形式返回
data = cursor.fetchall()
print(data)

# 关闭数据库连接
db.close()
```

### 5.数据库基本操作
增加数据：

语法：
```
insert 语句可以用来将一行或多行数据插到数据库表中, 使用的一般形式如下:

insert [into] 表名 [(列名1, 列名2, 列名3, ...)] values (值1, 值2, 值3, ...);

其中 [ ] 内的内容是可选的, 例如, 要给study_date数据库中的 studys 表插入一条记录, 执行语句:

insert into studys values(3, '骑着乌龟赶猪', 30);
```

```
import pymysql
# 打开数据库连接
db = pymysql.connect("localhost", "root", "111223", "study_date")
# 使用cursor()方法获取操作游标
cursor = db.cursor()
insert_sql = 
# 执行sql语句
cursor.execute("insert into studys(id, name, age) values(3, '骑着乌龟赶猪', 35)") 
# 提交到数据库执行 
db.commit() cursor.execute("select * from studys")
# 查看表里所有数据 
data = cursor.fetchall() 
print(data) # 关闭数据库连接 db.close()
```




