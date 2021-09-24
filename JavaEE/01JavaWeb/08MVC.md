# MVC

MVC：Model	View	Controller	模型试图控制器

## 三层架构

早些年的三层架构

![image-20210821162405511](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210821162405511.png)

```java
用户直接访问控制层，控制层直接操作数据库
弊端：代码十分臃肿不利于维护
    Servlet代码中：处理请求、响应、视图的跳转、处理JDBC、处理业务代码、处理逻辑代码
    
在架构中没有什么是加一层解决不了的
```



新的MVC架构

![image-20210821162730657](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210821162730657.png)

Model：

* 业务处理：业务逻辑（Service）
* 数据持久层：CRUD（DAO）

View：

* 展示数据
* 提供链接发起Servlet请求

Controller（Servlet）：

* 接受用户的请求
* 交给业务层处理对应的代码
* 控制视图的跳转

```bash
登录-->接受用户的登陆请求-->处理用户的登录请求（获取登陆的参数）-->交给业务层处理业务（判断用户信息是否正确）-->Dao层查询用户名以及密码-->数据库
```

