# JavaWeb

基本概念

在Java中，动态Web资源开发的技术统称为JavaWeb，它包括HTML5，Css3，JavaScript，MySQL，JDBC连接池，Servlet，JSP，AJAX，JQuery，Bootstrap等

**网页的区别：**

* 静态网页

提供的，用户看到的信息不会发生变化

* 动态网页

提供信息数据，每一个用户，每一个时间段都是不同的。

## Web应用程序

Web应用程序就是可以提供浏览器访问的程序

* 多个Web资源，这些Web资源可以被外界访问，对外界提供服务。
* 利用URL访问
* 这些统一的Web资源会被放同一文件夹下
* Web应用程序利用服务器提供服务 **服务器 ：Tomcat**
* 一个Web应该由多个部分组成 例如：HTML、CSS、JavaScript、JSP、Servlet、Java程序、Jar包、配置文件等文件组成。

Web应用程序编写完成后，若想提供给外界访问，需要一个服务器统一的管理



## 静态 Web

![image-20210811222252167](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811222252167.png)

*.html 如果服务器上一直存在静态的html文件，就可以直接读取



**静态网页的缺点：**

* Web页面无法动态更新，所有的用户看到的都是一个页面
* 无法与数据库交互，数据无法持久化，用户无法交互



## 动态Web

网页的页面因人而异

![image-20210811222927836](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811222927836.png)

缺点：

* 服务器的动态资源出现错误，需要重新编写后台程序，重新发布（停机维护）

优点：

* Web页面可以动态更新，所有的用户看到的页面都是不一样的
* 可以数据库交互，数据可以持久化，用户可以交互

