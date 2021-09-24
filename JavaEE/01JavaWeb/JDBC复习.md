# JDBC

**Java数据库连接 Java Database Connect**

Java数据库连接，（Java Database Connectivity，简称JDBC）是[Java语言](https://baike.baidu.com/item/Java语言)中用来规范客户端程序如何来访问数据库的[应用程序接口](https://baike.baidu.com/item/应用程序接口/10418844)，提供了诸如查询和更新数据库中数据的方法。JDBC也是Sun Microsystems的商标。我们通常说的JDBC是面向关系型数据库的。

![image-20210826145413869](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210826145413869.png)

需要的jar包支持





创建数据库并插入数据

![image-20210826151021865](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210826151021865.png)

![image-20210826152445265](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210826152445265.png)

JDBC固定步骤：

* 加载驱动
* 连接数据库，代表数据库
* 向数据库发送SQL对象Statement对象：CRUD
* 编写SQL语句
* 执行SQL语句
* 关闭连接



**预编译**

![image-20210826154410366](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210826154410366.png)



**事务**

要么都成功要么都失败

![image-20210826154556349](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210826154556349.png)

![image-20210826160312403](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210826160312403.png)

