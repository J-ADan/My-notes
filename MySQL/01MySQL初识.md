# 初识MySQL

在JavaEE的企业级开发中一共分为三个模块。

* 前端：页面，展示数据以及其他的界面信息
* 后端：中间起到连接的作用，连接数据库，操作数据库，连接前端，操作前端（控制视图的跳转，和给前端传递数据）
* 后台：数据库，存储数据。



**数据库是所有的软件体系中最核心的存在。**



## 什么是数据库

数据库（DateBase，DB）

概念：

数据库是“按照数据结构来组织、存储和管理数据的仓库”。是一个长期存储在[计算机](https://baike.baidu.com/item/计算机/140338)内的、有组织的、可共享的、统一管理的大量数据的集合。

是一个数据仓库，软件，安装在操作系统之上的。（Windows，Linux，MacOS）



数据库的作用：

存储数据，管理数据



## 数据库管理系统

**数据库的分类：**

1. 关系型数据库（SQL）：通过表和表之间的关系，行和列之间的关系进行数据的存储
   * MySQL
   * Oracle
   * Sql Server
   * DB2
   * SQLlite
2. 非关系型数据库（NoSQL（Not Only SQL））：通过对象存储，通过对象自身的属性来决定
   * Redis
   * MongDB



**DBMS（数据库管理系统）**

实质：数据库的管理软件，科学有效的管理我们的数据，维护和获取数据。



## 认识MySQL

MySQL是一个**[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511)****，**由瑞典[MySQL AB](https://baike.baidu.com/item/MySQL AB/2620844) 公司开发，属于 [Oracle](https://baike.baidu.com/item/Oracle) 旗下产品。MySQL 是最流行的[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511)之一，在 [WEB](https://baike.baidu.com/item/WEB/150564) 应用方面，MySQL是最好的 [RDBMS](https://baike.baidu.com/item/RDBMS/1048260) (Relational Database Management System，关系数据库管理系统) 应用软件之一。

MySQL是一种关系型数据库管理系统，关系数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。

MySQL所使用的 SQL 语言是用于访问[数据库](https://baike.baidu.com/item/数据库/103728)的最常用标准化语言。MySQL 软件采用了双授权政策，分为社区版和商业版，由于其体积小、速度快、总体拥有成本低，尤其是[开放源码](https://baike.baidu.com/item/开放源码/7176422)这一特点，一般中小型网站的开发都选择 MySQL 作为网站数据库。



## MySQL的安装

