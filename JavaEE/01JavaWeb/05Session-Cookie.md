**保存会话的两种技术：**

* Cookie

  客户端技术（请求,响应）

* Session

  服务器技术，利用这个技术，可以保存用户的会话信息，可以把信息或者数据放在

# Cookie

Cookie，有时也用其复数形式 [Cookies](https://baike.baidu.com/item/Cookies/187064)。类型为“**小型文本文件**”，是某些网站为了辨别用户身份，进行[Session](https://baike.baidu.com/item/Session/479100)跟踪而储存在用户本地终端上的数据（通常经过加密），由用户[客户端](https://baike.baidu.com/item/客户端/101081)计算机暂时或永久保存的信息

Cookie：一般会保存在本地的 用户目录下 appdata;

**小细节：**

* 一个Cookie只能保存一个信息
* 一个Web站点可以给浏览器发送多个Cookie，一个站点最多存放20个Cookie
* Cookie的大小有限制，4kb
* 一个浏览器的Cookie上限为300个

```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

public class CookieTest01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 保存用户上一次登录时间

        // 解决中文乱码
        req.setCharacterEncoding("utf8");
        resp.setCharacterEncoding("utf8");

        // 从客户端获取Cookie
        PrintWriter writer = resp.getWriter();
        // Cookie可能存在多个
        Cookie[] cookies = req.getCookies();

        // 判断Cookie是否存在
        if (cookies != null) {
            // 如果存在
            writer.print("上次访问时间:");
            for (Cookie cookie : cookies) {
                if ("LastLoginTime".equals(cookie.getName())){
                    long lastLoginTime = Long.parseLong(cookie.getValue());
                    Date date = new Date(lastLoginTime);
                    writer.print(String.valueOf(date));
                }
            }
        } else {
            writer.print("第一次访问本站");
        }

        // 服务器给客户端的本次访问相应一个Cookie
        Cookie lastLoginTime = new Cookie("LastLoginTime", System.currentTimeMillis() + "");

//        // 设置Cookie的生命周期，因为一次开关浏览器即为一个会话，Cookie只在本次会话有效
//        lastLoginTime.setMaxAge(24*60*60);//一天的寿命
        // 返回客户端Cookie
        resp.addCookie(lastLoginTime);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



**删除Cookie：**

* 不设置有效期，关闭浏览器，自动失效
* 设置有效期为 0 即可

```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class CookieTest02 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Cookie的键唯一，所以设置一个重名的Cookie覆盖
        Cookie lastLoginTime = new Cookie
                ("LastLoginTime", System.currentTimeMillis() + "");
        
        lastLoginTime.setMaxAge(0);
        resp.addCookie(lastLoginTime);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```



```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.net.URLDecoder;
import java.net.URLEncoder;
import java.util.Date;

public class CookieTest03 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 关于一个简单的数据编码、解码的问题

        req.setCharacterEncoding("utf8");
        resp.setCharacterEncoding("utf8");
        // 从客户端获取Cookie
        PrintWriter writer = resp.getWriter();
        // Cookie可能存在多个
        Cookie[] cookies = req.getCookies();

        // 判断Cookie是否存在
        if (cookies != null) {
            // 如果存在
            writer.print("***");
            for (Cookie cookie : cookies) {
                if ("name".equals(cookie.getName())){
                    writer.print(URLDecoder.decode(cookie.getValue(),"utf8"));
                }
            }
        } else {
            writer.print("第一次访问本站");
        }
        Cookie name = new Cookie("name", URLEncoder.encode("姜富超","utf8"));
        resp.addCookie(name);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



# Session（重点）

Session：在计算机中，尤其是在网络应用中，称为“会话控制”。[Session对象](https://baike.baidu.com/item/Session对象/5250998)存储特定用户会话所需的属性及配置信息。这样，当用户在应用程序的Web页之间跳转时，存储在Session对象中的变量将不会丢失，而是在整个用户会话中一直存在下去。当用户请求来自应用程序的 Web页时，如果该用户还没有会话，则Web服务器将自动创建一个 Session对象。当会话过期或被放弃后，服务器将终止该会话。Session 对象最常见的一个用法就是存储用户的首选项。例如，如果用户指明不喜欢查看图形，就可以将该信息存储在Session对象中。有关使用Session 对象的详细信息，请参阅“ASP应用程序”部分的“管理会话”。注意会话状态仅在支持cookie的浏览器中保留。

## 会话

会话：用户代开浏览器，并具有操作，最后关闭浏览器即为会话

**有状态会话bean**   ：每个用户有自己特有的一个实例，在用户的生存期内，bean保持了用户的信息，即“有状态”；一旦用户灭亡（调用结束或实例结束），bean的生命期也告结束。即每个用户最初都会得到一个初始的bean。 

**无状态会话bean**   ：bean一旦实例化就被加进会话池中，各个用户都可以共用。即使用户已经消亡，bean   的生命期也不一定结束，它可能依然存在于会话池中，供其他用户调用。由于没有特定的用户，那么也就不能保持某一用户的状态，所以叫无状态bean。但无状态会话bean   并非没有状态，如果它有自己的属性（变量），那么这些变量就会受到所有调用它的用户的影响，这是在实际应用中必须注意的



**什么是Session**

* 服务器会给每一个浏览器（用户）创建一个Session对象
* 一个Session独占一个浏览器，只要浏览器没有关闭，Session一直存在
* 用户登录之后，通过Session，任何一个页面都能访问



```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

public class SessionTest01 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        // 解决编码问题
        req.setCharacterEncoding("utf8");
        resp.setCharacterEncoding("utf8");
        resp.setContentType("text/html;charset=utf8");

        // 得到一个Session对象
        HttpSession session = req.getSession();
        // Session中存入
        session.setAttribute("name","jfc");

        // 获取SessionID
        String id = session.getId();

        // 判断Session是否为新建
        if (session.isNew()) {
            resp.getWriter().write("新建");
        } else {
            resp.getWriter().write("不是新建");
        }


    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

```java
// Session 的实质操作  
Cookie cookie = new Cookie("name", "jfc");
resp.addCookie(cookie);
```



```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

public class SessionTest02 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 解决编码问题
        req.setCharacterEncoding("utf8");
        resp.setCharacterEncoding("utf8");
        resp.setContentType("text/html;charset=utf8");

        // 得到一个Session对象
        HttpSession session = req.getSession();

        String name = (String)session.getAttribute("name");

        resp.getWriter().write(name);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```



![image-20210819202534184](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210819202534184.png)

**注销Session：**

```java
package com.sdut.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

public class SessionTest03 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        HttpSession session = req.getSession();
        // 移除设置的键值对
        session.removeAttribute("name");
        // 注销Session
        session.invalidate();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

```xml
<!--    关于Session的设置-->
    <session-config>
<!--        设置十五分钟后失效，分钟计时-->
        <session-timeout>15</session-timeout>
    </session-config>
</web-app>
```



Session和Cookie的区别：

* Cookie是把用户的数据写给用户的浏览器，浏览器保存（可以保存多个）
* Session是把用户的数据写到用户独占的Session中，服务器端保存（保存重要信息、减少服务器资源的浪费）
* Session是由服务器创建



**使用场景：**

* 保存一个用户的登录信息
* 购物车信息
* 在整个网站中经常使用的数据



