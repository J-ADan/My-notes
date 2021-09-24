# Servlet

## Servlet简介

Servlet（Server Applet）是[Java](https://baike.baidu.com/item/Java/85979) Servlet的简称，称为小服务程序或服务连接器，用Java编写的[服务器](https://baike.baidu.com/item/服务器/100571)端程序，具有独立于平台和[协议](https://baike.baidu.com/item/协议/13020269)的特性，主要功能在于交互式地浏览和生成数据，生成动态[Web](https://baike.baidu.com/item/Web/150564)内容。

狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。Servlet运行于支持Java的应用服务器中。从原理上讲，Servlet可以响应任何类型的请求，但绝大多数情况下Servlet只用来扩展基于[HTTP协议](https://baike.baidu.com/item/HTTP协议/1276942)的Web服务器。

最早支持Servlet标准的是JavaSoft的Java [Web Server](https://baike.baidu.com/item/Web Server/9306055)，此后，一些其它的基于Java的Web服务器开始支持标准的Servlet。



开发Servlet的两个简单的步骤：

1. 编写一个类，实现Servlet接口
2. 把开发好的Java类部署到Web服务器中

**把实现了Servlet接口的Java程序叫做Servlet**



## HelloServlet

1. 导入依赖

   ![image-20210816093131288](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816093131288.png)

   ```xml
   <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
   <dependency>
       <groupId>javax.servlet</groupId>
       <artifactId>javax.servlet-api</artifactId>
       <version>3.0.1</version>
       <scope>provided</scope>
   </dependency>
   ```

   ```xml
   <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
   <dependency>
       <groupId>javax.servlet</groupId>
       <artifactId>javax.servlet-api</artifactId>
       <version>4.0.1</version>
       <scope>provided</scope>
   </dependency>
   ```

2. 书写代码

   ```java
   package com.sdut;
   
   import javax.servlet.ServletException;
   import javax.servlet.http.HttpServlet;
   import javax.servlet.http.HttpServletRequest;
   import javax.servlet.http.HttpServletResponse;
   import java.io.IOException;
   import java.io.PrintWriter;
   
   public class HelloServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse response) throws ServletException, IOException {
           // 响应的类型 html
           response.setContentType("text/html");
           // 设置编码格式
           response.setCharacterEncoding("utf-8");
           // 获得响应的输出流
           PrintWriter out = response.getWriter();
           out.println("<html>");
           out.println("<head>");
           out.println("<title>Hello World!</title>");
           out.println("</head>");
           out.println("<body>");
           out.println("<h1>Hello World!</h1>");
           out.println("</body>");
           out.println("</html>");
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           super.doPost(req, resp);
       }
   }
   
   ```

3. 修改web.xml文件

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0"
            metadata-complete="true">
   <!--  web.xml 是配置web的核心应用-->
   <!--  注册servlet-->
     <servlet>
       <servlet-name>HelloServlet</servlet-name>
       <servlet-class>com.sdut.HelloServlet</servlet-class>
     </servlet>
   <!--  一个servlet对应一个servlet-mapping 映射-->
     <servlet-mapping>
       <servlet-name>HelloServlet</servlet-name>
   <!--    映射的请求路径-->
       <url-pattern>/index</url-pattern>
     </servlet-mapping>
   
   </web-app>
   ```

4. 设置项目的Tomcat，之前有过赘述

5. 跑项目



## 正式开始

### 关于Servlet源码的解读

![image-20210813201928345](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813201928345.png)

```java
public interface Servlet {
    //初始化
    void init(ServletConfig var1) throws ServletException;

    //获取servlet配置
    ServletConfig getServletConfig();

    // 服务
    void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;

    // 获取servlet信息
    String getServletInfo();

    //销毁
    void destroy();
}

```

**GenericServlet并没有对service做任何动作**

![image-20210813201212543](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813201212543.png)

**HttpServlet 实现了service 但是仅仅是判断了使用的是doGet 还是 doPost 方法，并没有做其他的方法**

```java
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String method = req.getMethod();
        long lastModified;
        if (method.equals("GET")) {
            lastModified = this.getLastModified(req);
            if (lastModified == -1L) {
                this.doGet(req, resp);
            } else {
                long ifModifiedSince = req.getDateHeader("If-Modified-Since");
                if (ifModifiedSince < lastModified) {
                    this.maybeSetLastModified(resp, lastModified);
                    this.doGet(req, resp);
                } else {
                    resp.setStatus(304);
                }
            }
        } else if (method.equals("HEAD")) {
            lastModified = this.getLastModified(req);
            this.maybeSetLastModified(resp, lastModified);
            this.doHead(req, resp);
        } else if (method.equals("POST")) {
            this.doPost(req, resp);
        } else if (method.equals("PUT")) {
            this.doPut(req, resp);
        } else if (method.equals("DELETE")) {
            this.doDelete(req, resp);
        } else if (method.equals("OPTIONS")) {
            this.doOptions(req, resp);
        } else if (method.equals("TRACE")) {
            this.doTrace(req, resp);
        } else {
            String errMsg = lStrings.getString("http.method_not_implemented");
            Object[] errArgs = new Object[]{method};
            errMsg = MessageFormat.format(errMsg, errArgs);
            resp.sendError(501, errMsg);
        }

    }
```

**HttpServlet的doGet与doPost方法也并没有做任何的操作，所以我们的主要任务即为重写doGet与doPost方法**

```java
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String protocol = req.getProtocol();
        String msg = lStrings.getString("http.method_post_not_supported");
        if (protocol.endsWith("1.1")) {
            resp.sendError(405, msg);
        } else {
            resp.sendError(400, msg);
        }

    }
```

```java
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String protocol = req.getProtocol();
        String msg = lStrings.getString("http.method_get_not_supported");
        if (protocol.endsWith("1.1")) {
            resp.sendError(405, msg);
        } else {
            resp.sendError(400, msg);
        }

    }
```





### 项目的构建流程

1. 构建一个普通的Maven项目，删除目录下的src文件夹，以后的项目在里面建Module 子项目

   ![image-20210813195121808](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813195121808.png)

2. 导入需要的依赖

   ```xml
   <dependency>
               <groupId>javax.servlet</groupId>
               <artifactId>javax.servlet-api</artifactId>
               <version>3.0.1</version>
               <scope>provided</scope>
           </dependency>
   
           <!-- https://mvnrepository.com/artifact/javax.servlet.jsp/jsp-api -->
           <dependency>
               <groupId>javax.servlet.jsp</groupId>
               <artifactId>jsp-api</artifactId>
               <version>2.1</version>
               <scope>provided</scope>
           </dependency>
   ```

3. 创建子模块

   ![image-20210813195332648](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813195332648.png)

   ![image-20210813195436780](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813195436780.png)

   ![image-20210813195453143](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813195453143.png)

   ![image-20210813195507689](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813195507689.png)



**关于Maven父子工程的理解**

1. 子项目

   ```xml
   <parent>
       <artifactId>JavaWeb-01-Servlet</artifactId>
       <groupId>com.sdut</groupId>
       <version>1.0-SNAPSHOT</version>
     </parent>
   ```

2. 父项目

   ```xml
   <modules>
       <module>servlet-01</module>
   </modules>
   ```

3. 父项目的Java子项目可以使用



**修改webapp版本**

修改为与使用的Tomcat版本一致的webapp版本

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
  
</web-app>
```

**子项目可以使用父项目的jar包**



重写doGet与doPost方法

```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PipedWriter;
import java.io.PrintWriter;

public class HelloServlet extends HttpServlet {
    // 由于get或者post只是请求实现的不同方式，可以相互调用，业务逻辑都一样
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 响应流
        PrintWriter printWriter = resp.getWriter();
        printWriter.print("Hello Servlet!");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

**编写webapp文档，映射**

因为我们编写的是Java文件，但是我们需要通过浏览器访问，浏览器需要连接web服务器，所以我们需要在web服务器中注册Servlet

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">

<!--    注册servlet-->
    <servlet>
        <servlet-name>HelloServlet</servlet-name>
<!--        需要注册的类-->
        <servlet-class>com.sdut.servlet.HelloServlet</servlet-class>
    </servlet>

<!--    注册的访问路径-->
    <servlet-mapping>
        <servlet-name>HelloServlet</servlet-name>
        <url-pattern>/mian</url-pattern>
    </servlet-mapping>
</web-app>

```



**配置Tomcat**

![image-20210813203433872](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813203433872.png)

![image-20210813203510121](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813203510121.png)

![image-20210813203600928](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813203600928.png)

![image-20210813203612764](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813203612764.png)

![image-20210813203624060](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813203624060.png)

![image-20210813203658711](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813203658711.png)

![image-20210813203753600](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813203753600.png)

![image-20210813203821190](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210813203821190.png)



## Servlet 原理

![image-20210814092641103](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210814092641103.png)

Servlet是由Web服务器调用，Web服务器在收到浏览器请求后，进行以上步骤



## Mapping的问题

1. 一个Servlet对应一个映射路径

   ```xml
   <servlet-mapping>
       <servlet-name>HelloServlet</servlet-name>
       <url-pattern>/mian</url-pattern>
   </servlet-mapping>
   ```

2. 一个Servlet的对应多个映射路径

   ```xml
   <servlet-mapping>
       <servlet-name>HelloServlet</servlet-name>
       <url-pattern>/mian</url-pattern>
   </servlet-mapping>
   
   <servlet-mapping>
       <servlet-name>HelloServlet</servlet-name>
       <url-pattern>/hello</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
       <servlet-name>HelloServlet</servlet-name>
       <url-pattern>/hello1</url-pattern>
   </servlet-mapping>
   ```

3. 通配符路径

   ```xml
   <servlet-mapping>
       <servlet-name>HelloServlet</servlet-name>
       <url-pattern>/*</url-pattern>
   </servlet-mapping>
   ```

   这样会把默认的访问JSP文件覆盖

   ```xml
   <servlet-mapping>
           <servlet-name>HelloServlet</servlet-name>
           <url-pattern>/hello/*</url-pattern>
       </servlet-mapping>
   ```

4. 指定后缀或者前缀

   ```xml
   <servlet-mapping>
       <servlet-name>HelloServlet</servlet-name>
       <url-pattern>*.jfc</url-pattern>
   </servlet-mapping>
   ```



**优先级问题：**

指定了固有映射路径优先级最高，如果找不到就按默认请求处理

```xml
<servlet>
        <servlet-name>HelloServlet</servlet-name>
<!--        需要注册的类-->
        <servlet-class>com.sdut.servlet.HelloServlet</servlet-class>
    </servlet>
    <servlet>
        <servlet-name>ErrorServlet</servlet-name>
        <servlet-class>com.sdut.servlet.ErrorServlet</servlet-class>
    </servlet>

<!--    注册的访问路径-->
    <servlet-mapping>
        <servlet-name>HelloServlet</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>

    <servlet-mapping>
        <servlet-name>ErrorServlet</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
```



## ServletContext

**Web容器在启动的时候，他会为每一个Web程序创建一个对应的ServletContext对象，它代表了当前的Web应用**

* 共享数据

  当前Servlet中保存的数据，可以在另外一个Servlet中拿到

  ![image-20210814112321007](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210814112321007.png)

  

  **传入设置数据：**

  ```java
  package com.sdut.servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  
  public class Servlet01 extends HttpServlet {
  
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          ServletContext servletContext = this.getServletContext();
          String username = "jfc";
          //键值对存取一个对象
          servletContext.setAttribute("username",username);
      }
  
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          doGet(req, resp);
      }
  }
  
  ```

  

  **读取数据：**

  ```java
  package com.sdut.servlet;
  
  import javax.servlet.ServletContext;
  import javax.servlet.ServletException;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.IOException;
  import java.io.PrintWriter;
  
  public class Servlet02 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          ServletContext servletContext = this.getServletContext();
  
          String username = (String) servletContext.getAttribute("username");
  
          PrintWriter printWriter = resp.getWriter();
  
          printWriter.print(username);
      }
  
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          doGet(req, resp);
      }
  }
  
  ```

  

  **webapp.xml**

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                        http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
           version="4.0"
           metadata-complete="true">
  
    <servlet>
      <servlet-name>ServletContext</servlet-name>
      <servlet-class>com.sdut.servlet.Servlet01</servlet-class>
    </servlet>
    
    <servlet-mapping>
      <servlet-name>ServletContext</servlet-name>
      <url-pattern>/context</url-pattern>
    </servlet-mapping>
    
    <servlet>
      <servlet-name>getname</servlet-name>
      <servlet-class>com.sdut.servlet.Servlet02</servlet-class>
    </servlet>
    
    <servlet-mapping>
      <servlet-name>getname</servlet-name>
      <url-pattern>/getname</url-pattern>
    </servlet-mapping>
  </web-app>
  ```

  

  ![image-20210814113249686](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210814113249686.png)

## ServletContext 应用

### 获取初始化参数

```java
package com.sdut.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class Servlet04 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = this.getServletContext();

        //获取初始化参数
        String namespace = servletContext.getInitParameter("namespace");

        PrintWriter writer = resp.getWriter();

        writer.print(namespace);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

```xml
<!--  初始化参数-->
  <context-param>
    <param-name>namespace</param-name>
    <param-value>jdbc:mysql://127.0.0.1:3306/user</param-value>
  </context-param>
```



![image-20210816083456346](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816083456346.png)

### 请求转发（request、dispatcher）

```java
package com.sdut.servlet;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Servlet05 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = this.getServletContext();
        // 转发的路径请求
        RequestDispatcher requestDispatcher = servletContext.getRequestDispatcher("/parm");
        // 调用forword实现请求转发
        requestDispatcher.forward(req,resp);
        System.out.println("请求转发成功");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

```xml
<servlet>
    <servlet-name>patcher</servlet-name>
    <servlet-class>com.sdut.servlet.Servlet05</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>patcher</servlet-name>
    <url-pattern>/patcher</url-pattern>
  </servlet-mapping>
```

![image-20210816084933314](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816084933314.png)

![image-20210816084943874](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816084943874.png)

![image-20210816084957459](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816084957459.png)

**请求转发的路径不会发生改变，只是接收到了请求转发页面的内容**

1. 请求与转发原理
2. 重定向原理

![image-20210816085058149](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816085058149.png)

### 读取资源文件

**Properties**

JDBC复习

```java
package com.sdut.util;

import java.io.IOException;
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

public class JDBCUtil {
    private static String driver = null;
    private static String url = null;
    private static String username = null;
    private static String password = null;

    static {
        try {
            // 通过反射获取类加载器获取资源
            InputStream resourceAsStream =
                    JDBCUtil.class.getClassLoader().getResourceAsStream("db.properties");
            //读取流的内容
            Properties properties = new Properties();
            properties.load(resourceAsStream);
            //获取文档内容
            driver = properties.getProperty("driver");
            url = properties.getProperty("url");
            username = properties.getProperty("username");
            password = properties.getProperty("password");

            // 驱动器只需要加载一次
            Class.forName(driver);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    // 获取数据库连接,返回一个数据库连接对象
    public static Connection getConnection() throws SQLException {
            return DriverManager.getConnection(url, username, password);
    }


    // 关闭数据库连接
    public static void release(Connection connection, Statement statement, ResultSet resultSet){
        if (connection != null){
            try {
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (statement != null){
            try {
                statement.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (resultSet != null){
            try {
                resultSet.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}

```

![image-20210816191449794](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816191449794.png)

Maven会出现导出资源错误的问题

解决方案：

```xml
<build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```

![image-20210816191905721](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816191905721.png)

读取文档信息：

```java
package com.sdut.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.InputStream;
import java.io.PrintWriter;
import java.util.Properties;

public class Servlet06 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext servletContext = this.getServletContext();
        InputStream resourceAsStream =
                servletContext.getResourceAsStream("/WEB-INF/classes/db.properties");
        Properties properties = new Properties();
        properties.load(resourceAsStream);
        String username = properties.getProperty("username");
        String password = properties.getProperty("password");

        PrintWriter writer = resp.getWriter();
        writer.print(username + ":" + password);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

![image-20210816192733805](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210816192733805.png)

## HttpServletResponse（响应）

Web服务器接收到客户端的http请求，准对这个请求，分别创建一个代表请求的HttpServletRequest对象，和一个代表响应的HttpServletResponse请求。

* 获取客户端请求的参数，HttpServletRequest
* 给客户端响应信息，HttpServletResponse



**负责向浏览器发送数据的方法**

```java
ServletOutputStream getOutputStream() throws IOException;

PrintWriter getWriter() throws IOException;
```

**负责向浏览器发送响应头的消息：**

```java
void setCharacterEncoding(String var1);

void setContentLength(int var1);

void setContentLengthLong(long var1);

void setContentType(String var1);

void setBufferSize(int var1);

void sendError(int var1, String var2) throws IOException;

void sendError(int var1) throws IOException;

void sendRedirect(String var1) throws IOException;

void setDateHeader(String var1, long var2);

void addDateHeader(String var1, long var2);

void setHeader(String var1, String var2);

void addHeader(String var1, String var2);

void setIntHeader(String var1, int var2);

void addIntHeader(String var1, int var2);

void setStatus(int var1);
```

**状态码：**

```java
int SC_CONTINUE = 100;
    int SC_SWITCHING_PROTOCOLS = 101;
    int SC_OK = 200;
    int SC_CREATED = 201;
    int SC_ACCEPTED = 202;
    int SC_NON_AUTHORITATIVE_INFORMATION = 203;
    int SC_NO_CONTENT = 204;
    int SC_RESET_CONTENT = 205;
    int SC_PARTIAL_CONTENT = 206;
    int SC_MULTIPLE_CHOICES = 300;
    int SC_MOVED_PERMANENTLY = 301;
    int SC_MOVED_TEMPORARILY = 302;
    int SC_FOUND = 302;
    int SC_SEE_OTHER = 303;
    int SC_NOT_MODIFIED = 304;
    int SC_USE_PROXY = 305;
    int SC_TEMPORARY_REDIRECT = 307;
    int SC_BAD_REQUEST = 400;
    int SC_UNAUTHORIZED = 401;
    int SC_PAYMENT_REQUIRED = 402;
    int SC_FORBIDDEN = 403;
    int SC_NOT_FOUND = 404;
    int SC_METHOD_NOT_ALLOWED = 405;
    int SC_NOT_ACCEPTABLE = 406;
    int SC_PROXY_AUTHENTICATION_REQUIRED = 407;
    int SC_REQUEST_TIMEOUT = 408;
    int SC_CONFLICT = 409;
    int SC_GONE = 410;
    int SC_LENGTH_REQUIRED = 411;
    int SC_PRECONDITION_FAILED = 412;
    int SC_REQUEST_ENTITY_TOO_LARGE = 413;
    int SC_REQUEST_URI_TOO_LONG = 414;
    int SC_UNSUPPORTED_MEDIA_TYPE = 415;
    int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;
    int SC_EXPECTATION_FAILED = 417;
    int SC_INTERNAL_SERVER_ERROR = 500;
    int SC_NOT_IMPLEMENTED = 501;
    int SC_BAD_GATEWAY = 502;
    int SC_SERVICE_UNAVAILABLE = 503;
    int SC_GATEWAY_TIMEOUT = 504;
    int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```

### 常见应用

* 向浏览器输出消息

* 下载一个文件

  ```java
  package com.sdut.servlet;
  
  import javax.servlet.ServletException;
  import javax.servlet.ServletOutputStream;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.FileInputStream;
  import java.io.IOException;
  import java.net.URLEncoder;
  
  public class ServletFile01 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          // 1. 获取文件的路径
          String realPath = this.getServletContext().getRealPath("/02.jpg");
          System.out.println("下载的路径为:" + realPath);
          // 获取下载的文件名
          // 记住这个方法，以后常用，最后一个/后面的名字即为文件名
          String substring = realPath.substring(realPath.lastIndexOf("\\") + 1);
  
          // 设置浏览器支持下载,并且设置一下编码转换，防止下载文件名出现中文的乱码问题
          resp.setHeader("Content-Disposition","attachment;filename="
                  + URLEncoder.encode(substring,"UTF-8"));
  
          // 获取文件下载的流
          FileInputStream fileInputStream = new FileInputStream(realPath);
          // 创建缓冲区
          int len = 0;
          byte[] buffer = new byte[1024];
          // 创建输出流
          ServletOutputStream outputStream = resp.getOutputStream();
          while ((len = fileInputStream.read(buffer)) != 0){
              // 写出
              outputStream.write(buffer);
          }
  
          // 关闭流
          outputStream.close();
          fileInputStream.close();
  
      }
  
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          doGet(req, resp);
      }
  }
  
  ```

  下载的路径为:G:\Java\Tomcat\apache-tomcat-9.0.21\webapps\response_war\02.jpg

  下载的路径是从Tomcat服务器下的资源文件夹下获取。但是我们的文件是在项目目录之下

  ```java
  package com.sdut.servlet;
  
  import javax.servlet.ServletException;
  import javax.servlet.ServletOutputStream;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import java.io.FileInputStream;
  import java.io.IOException;
  import java.net.URLEncoder;
  
  public class ServletFile01 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          // 1. 获取文件的路径
          String realPath = "G:\\Java\\IDEA\\WorkSpace\\JavaWeb-01-Servlet\\response\\target\\classes\\02.jpg";
          System.out.println("下载的路径为:" + realPath);
          // 获取下载的文件名
          // 记住这个方法，以后常用，最后一个/后面的名字即为文件名
          String substring = realPath.substring(realPath.lastIndexOf("\\") + 1);
  
          // 设置浏览器支持下载,并且设置一下编码转换，防止下载文件名出现中文的乱码问题
          resp.setHeader("Content-Disposition","attachment;filename="
                  + URLEncoder.encode(substring,"UTF-8"));
  
          // 获取文件下载的流
          FileInputStream fileInputStream = new FileInputStream(realPath);
          // 创建缓冲区
          int len = 0;
          byte[] buffer = new byte[1024];
          // 创建输出流
          ServletOutputStream outputStream = resp.getOutputStream();
          while ((len = fileInputStream.read(buffer)) > 0){
              // 写出
              outputStream.write(buffer);
          }
  
          // 关闭流
          outputStream.close();
          fileInputStream.close();
  
      }
  
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          doGet(req, resp);
      }
  }
  
  ```

  ![image-20210818090634982](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210818090634982.png)

* 上传一个文件



### 验证码的实现

```java
package com.sdut.servlet;

import javax.imageio.ImageIO;
import javax.servlet.GenericFilter;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.BufferedReader;
import java.io.IOException;
import java.util.Random;

public class ServletTest02 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        // 浏览器定时刷新
        resp.setHeader("refresh","3");

        // 内存中创建一个图片
        BufferedImage bufferedImage =
                new BufferedImage(80,20, BufferedImage.TYPE_INT_RGB);

        // 得到图片，创建一个笔
        Graphics2D graphics2D = (Graphics2D)bufferedImage.getGraphics();

        // 设置背景颜色
        graphics2D.setColor(Color.white);
        graphics2D.fillRect(0,0,80,80);

        // 给图片写入数据
        graphics2D.setColor(Color.BLUE);
        graphics2D.setFont(new Font(null,Font.BOLD,20));
        graphics2D.drawString(reradom(),0,20);

        // 告知浏览器，请求打开方式为图片
        resp.setContentType("image/jpeg");
        // 网站存在缓存，去掉网站的缓存
        resp.setDateHeader("expires",-1);
        resp.setHeader("Cache-Control","no-cache");
        resp.setHeader("Pragma","no-cache");

        // 通过流，把图片给浏览器
        ImageIO.write(bufferedImage,"jpg",resp.getOutputStream());

    }

    // 生成随机数
    public static String reradom(){
        Random random = new Random();
        String num = random.nextInt(9999999) + "";
        StringBuffer stringBuffer = new StringBuffer();

        // 不足七位数，补零
        for (int i = 0; i < 7 - num.length(); i++) {
            stringBuffer.append("0");
        }
        num = stringBuffer.toString() + num;
        return num;
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```



### 重定向

![image-20210818221412119](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210818221412119.png)

B一个Web资源收到客户端A的请求后，B会通知A去访问另一个Web资源C，这个过程叫做重定向

```java
void sendRedirect(String var1) throws IOException;
```

```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ServletTest03 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.sendRedirect("/response_war/img");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```



![image-20210818222446391](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210818222446391.png)

![image-20210818222529949](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210818222529949.png)



相当于做了以下操作

```java
package com.sdut.servlet;

import com.sun.net.httpserver.HttpsServer;
import com.sun.prism.shape.ShapeRep;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ServletTest03 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setHeader("Location","/response_war/img");
        resp.setStatus(HttpServletResponse.SC_MOVED_TEMPORARILY);
//        resp.setStatus(302);
//        resp.sendRedirect("/response_war/img");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```



**请求转发与重定向的区别：**

* 相同点
  * 页面都能实现跳转
* 不同点
  * 请求转发的时候URL不会发生变化
  * 重定向，URL会发生变化



## HttpServletRequest（请求）

**HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，Http请求中的所有的信息都会被封装到HttpServletRequest**

```jsp
<html>
<body>
<form action="${pageContext.request.contextPath}/login" method="get">
    账号：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    <input type="submit">
</form>
</body>
</html>
```

```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ServletTest04 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username = req.getParameter("username");
        String password = req.getParameter("password");

        System.out.println(username + ":" + password);

        resp.sendRedirect("/response_war/success.jsp");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: J-ADan
  Date: 2021/8/18
  Time: 22:50
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>success</h1>
</body>
</html>
```

简单的request处理前端请求并且重定向



### HttpServletRequest的简单的方法

![image-20210819085322856](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210819085322856.png)

```jsp
<%--
  Created by IntelliJ IDEA.
  User: J-ADan
  Date: 2021/8/19
  Time: 8:48
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Login</title>
</head>
<body>
<h1>登录</h1>
<div>
    <form action="${pageContext.request.contextPath}/login" method="post">
        账号：<input type="text" name="username"><br>
        密码：<input type="password" name="password"><br>

        <input type="checkbox" name="hobbys" value="女人">女人
        <input type="checkbox" name="hobbys" value="男人">男人
        <input type="checkbox" name="hobbys" value="代码">代码
        <input type="checkbox" name="hobbys" value="电脑">电脑

        <br>
        <input type="submit">
    </form>
</div>
</body>
</html>

```

```java
package com.sdut.request;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;

public class RequestTest01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 设置请求与响应的格式均为utf8
        req.setCharacterEncoding("utf8");
        resp.setCharacterEncoding("utf8");

        // 获取前端的数据
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] hobbys = req.getParameterValues("hobbys");

        // 输出前端的数据
        System.out.println(username);
        System.out.println(password);
        System.out.println(Arrays.toString(hobbys));
        req.getRequestDispatcher("/success.jsp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: J-ADan
  Date: 2021/8/19
  Time: 8:58
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Success</title>
</head>
<body>
<h1>成功</h1>
</body>
</html>

```

