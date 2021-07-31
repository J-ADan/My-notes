# MyBatis

## 简介

MyBatis中文文档：https://mybatis.org/mybatis-3/zh/index.html

### 什么是MyBatis

* MyBatis 是一款优秀的**持久层框架**

* 它支持自定义 SQL、存储过程以及高级映射。

* MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。

* MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。



GitHub：https://github.com/mybatis/mybatis-3/releases

Maven仓库

```java
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.4.6</version>
</dependency>

```

###  持久化

数据持久化

* 持久化就是将程序的数据在持久状态和瞬时状态转化的过程

* 数据库（JDBC）、IO文件持久化



### 持久层

Dao层、Controller层、、、

 * 完成持久化工作的代码块



### 为什么需要MyBatis

* 方便
* 传统的JDBC太复杂
* MyBatis是一个框架，简化很多代码书写
* 帮助程序员将数据存入数据库



### MyBatis特点

- 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件易于学习，易于使用，通过文档和源代码，可以比较完全的掌握它的设计思路和实现。
- 灵活：mybatis不会对应用程序或者数据库的现有设计强加任何影响。 sql写在xml里，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
- 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql和代码的分离，提高了可维护性。
- 提供映射标签，支持对象与数据库的orm字段关系映射
- 提供对象关系映射标签，支持对象关系组建维护
- 提供xml标签，支持编写动态sql。



# 第一个MyBatis程序

思路：搭建环境-->导入MyBati-->编写代码-->测试

## 
