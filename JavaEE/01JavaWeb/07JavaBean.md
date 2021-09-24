# JavaBean（实体类）

JavaBean有特定的写法：

* 必须要有一个无参构造
* 属性必须私有换
* 必须要有对应的get/set方法

一般来和数据库的字段做映射

ORM：对象关系映射

* 表-->类
* 字段-->属性
* 行记录-->对象



```java
package com.sdut.pojo;

public class People {
    private int id;
    private String name;
    private int age;
    private String address;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
}

```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

<jsp:useBean id="people" class="com.sdut.pojo.People" scope="page">
    <jsp:setProperty name="people" property="id" value="1"></jsp:setProperty>
    <jsp:setProperty name="people" property="name" value="姜富超"></jsp:setProperty>
    <jsp:setProperty name="people" property="age" value="18"></jsp:setProperty>
    <jsp:setProperty name="people" property="address" value="泰安"></jsp:setProperty>
</jsp:useBean>

id：
<jsp:getProperty name="people" property="id"/>
姓名：
<jsp:getProperty name="people" property="name"/>
年龄：
<jsp:getProperty name="people" property="age"/>
地址：
<jsp:getProperty name="people" property="address"/>

</body>
</html>
```



