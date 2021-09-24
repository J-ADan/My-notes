# Filter (过滤器)

用来过滤网站的数据。

* 处理中文乱码
* 登陆验证

![image-20210823093529913](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210823093529913.png)



**开发步骤：**

1. 导入开发所需的包文件

```xml
<!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
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
        <!-- https://mvnrepository.com/artifact/javax.servlet.jsp.jstl/jstl-api -->
        <dependency>
            <groupId>javax.servlet.jsp.jstl</groupId>
            <artifactId>jstl-api</artifactId>
            <version>1.2</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/taglibs/standard -->
        <dependency>
            <groupId>taglibs</groupId>
            <artifactId>standard</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
```

2. 编写过滤器

   1. 导入servlet下的filter

      ![image-20210823095637779](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210823095637779.png)

   2. 重写方法

      ```java 
      package com.sdut.filter;
      
      import javax.servlet.*;
      import java.io.IOException;
      
      public class FilterTest01 implements Filter {
          // 初始化
          public void init(FilterConfig filterConfig) throws ServletException {
              System.out.println("过滤器启动");
          }
      
          public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
              /* 链的作用
              1. 过滤中的所有的代码，在过滤特定请求的时候都会执行
              2. 必须要让过滤器继续同行
               */
              servletRequest.setCharacterEncoding("utf8");
              servletResponse.setCharacterEncoding("utf8");
              servletResponse.setContentType("text/html;charset=UTF-8");
      
              System.out.println("执行前");
              // 过滤链，让我们的请求继续走下去，如果不写，则会被拦截在此
              filterChain.doFilter(servletRequest,servletResponse);
              System.out.println("执行后");
          }
      
          //销毁
          public void destroy() {
              System.out.println("过滤器销毁");
          }
      }
      
      ```

   3. xml

      ```xml
      <servlet>
              <servlet-name>ServletTest01</servlet-name>
              <servlet-class>com.sdut.servlet.ServletTest01</servlet-class>
          </servlet>
          <servlet-mapping>
              <servlet-name>ServletTest01</servlet-name>
              <url-pattern>/servlet/s01</url-pattern>
          </servlet-mapping>
          <servlet-mapping>
              <servlet-name>ServletTest01</servlet-name>
              <url-pattern>/s01</url-pattern>
          </servlet-mapping>
      
          <filter>
              <filter-name>FilterTest01</filter-name>
              <filter-class>com.sdut.filter.FilterTest01</filter-class>
          </filter>
      <!--    代表servlet下的请求响应都会走过滤器-->
          <filter-mapping>
              <filter-name>FilterTest01</filter-name>
              <url-pattern>/servlet/*</url-pattern>
          </filter-mapping>
      ```

   4. 注意事项

      1. 过滤器会在Web服务器启动的时候启动，随时等待请求的传入

         ![image-20210823103208145](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210823103208145.png)

      2. 每一次请求都会启动过滤器

         ![image-20210823103306478](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210823103306478.png)

      3. 在服务器停止后销毁

         ![image-20210823103356350](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210823103356350.png)

# 监听器

监听器存在很多种

![image-20210823143839996](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210823143839996.png)

```java
package com.sdut.listener;

import javax.servlet.ServletContext;
import javax.servlet.http.HttpSessionEvent;
import javax.servlet.http.HttpSessionListener;

public class ListenerTest01 implements HttpSessionListener {
    // 创建监听
    public void sessionCreated(HttpSessionEvent httpSessionEvent) {
        // 获取Session的信息
        ServletContext servletContext =
                httpSessionEvent.getSession().getServletContext();

        // 获取设置的Session的信息
        Integer count = (Integer) servletContext.getAttribute("Count");

        if (count == null){
            count = new Integer(1);
        } else {
            int count1 = count.intValue();
            count = new Integer(count1 + 1);
        }

//        Session设置某个值
        servletContext.setAttribute("count",count);
    }

    public void sessionDestroyed(HttpSessionEvent httpSessionEvent) {
        // 获取Session的信息
        ServletContext servletContext =
                httpSessionEvent.getSession().getServletContext();

        // 获取设置的Session的信息
        Integer count = (Integer) servletContext.getAttribute("Count");

        if (count == null){
            count = new Integer(1);
        } else {
            int count1 = count.intValue();
            count = new Integer(count1 - 1);
        }

        servletContext.setAttribute("count",count);
    }
}


```



```xml
<!--    注册监听器-->
    <listener>
        <listener-class>com.sdut.listener.ListenerTest01</listener-class>
    </listener>
```



```jsp
<h1>当前有<span><%=this.getServletConfig().getServletContext().getAttribute("count")%></span></h1>
```



# 过滤器、监听器的简单应用

监听器：GUI编程中经常使用

```java
package com.sdut.gui;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class GUITest01 {
    public static void main(String[] args) {
        Frame frame = new Frame("简单的测试");
        Panel panel = new Panel();

        frame.setLayout(null);

        frame.setBounds(500,500,500,500);
        frame.setBackground(Color.red);
        panel.setBounds(20,20,200,200);
        panel.setBackground(Color.blue);

        frame.add(panel);

        frame.setVisible(true);

        // 设置关闭监听
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
            }
        });

    }
}

```



# Filter 实现权限拦截

```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ServletTest02 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username = req.getParameter("username");
        System.out.println("222");
        if ("admin".equals(username)) {
            req.getSession().setAttribute("USER_SESSION", req.getSession().getId());
            System.out.println("111");
            resp.sendRedirect("/sys/success.jsp");
        } else {
            resp.sendRedirect("/sys/error.jsp");
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

```xml
<servlet>
        <servlet-name>ServletTest02</servlet-name>
        <servlet-class>com.sdut.servlet.ServletTest02</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>ServletTest02</servlet-name>
        <url-pattern>/servlet/login</url-pattern>
    </servlet-mapping>
```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: J-ADan
  Date: 2021/8/23
  Time: 20:23
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<form action="/servlet/login" method="post">
    用户名：<input type="text" name="username">
    <input type="submit">
</form>
</body>
</html>

```





**登录实现拦截，必须登录才能访问主页：**

```java
package com.sdut.constant;

public class Session {
    public final static String SESSION_USERNAME = "SESSION_USERNAME";
}
```

```java
package com.sdut.filter;

import javax.servlet.*;
import java.io.IOException;

public class CharsetFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("utf8");
        servletResponse.setCharacterEncoding("utf8");
        servletResponse.setContentType("text/html;charset=UTF-8");

        filterChain.doFilter(servletRequest,servletResponse);
    }

    @Override
    public void destroy() {

    }
}
```

```java
package com.sdut.filter;

import com.sdut.constant.Session;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.net.ResponseCache;

public class LoginFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
        HttpServletResponse httpServletResponse = (HttpServletResponse) servletResponse;

        String parameter = httpServletRequest.getParameter(Session.SESSION_USERNAME);

        if (parameter == null){
            httpServletResponse.sendRedirect("/sys/error.jsp");
        }
    }

    @Override
    public void destroy() {

    }
}
```

```java
package com.sdut.servlet;

import com.sdut.constant.Session;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Login extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username = req.getParameter("username");

        if ("admin".equals(username)) {
            req.getSession().setAttribute
                    (Session.SESSION_USERNAME, req.getSession().getId());
            resp.sendRedirect("/sys/success.jsp");
        } else {
            resp.sendRedirect("/sys/error.jsp");
        }

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

```java
package com.sdut.servlet;

import com.sdut.constant.Session;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class LoginOut extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Object attribute = req.getSession().getAttribute(Session.SESSION_USERNAME);

        if (attribute == null){
            req.getSession().removeAttribute(Session.SESSION_USERNAME);
            resp.sendRedirect("/Login.jsp");
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

```jsp
<body>
<form action="/servlet/login" method="post">
    用户名：<input type="text" name="username">
    <input type="submit">
</form>
</body>
```

```jsp
<body>
<h1>欢迎管理员</h1>
<p><a href="/servlet/loginout"></a></p>
</body>
```

```jsp
<body>
<h1>你没有权限</h1>
<a href="../Login.jsp">返回登录界面</a>
</body>
```
