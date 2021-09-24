# JDBC

Java数据库连接，（Java Database Connectivity，简称JDBC）是[Java语言](https://baike.baidu.com/item/Java语言)中用来规范客户端程序如何来访问数据库的[应用程序接口](https://baike.baidu.com/item/应用程序接口/10418844)，提供了诸如查询和更新数据库中数据的方法。JDBC也是Sun Microsystems的商标。我们通常说的JDBC是面向关系型数据库的。



## 数据库驱动

驱动：显卡驱动、声卡驱动

![image-20210814201234053](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210814201234053.png)



## JDBC

SUN公司为了简化开发人员的（对数据库的统一）操作，提供了一个规范，Java操作数据库的而规范，俗称**JDBC**，这些具体的规范由具体的厂商去做。

![image-20210814201616089](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210814201616089.png)



## 第一个JDBC程序

1. 创建一个普通的项目

   ![image-20210814202403446](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210814202403446.png)

2. 创建测试数据库

   ![image-20210814202524008](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210814202524008.png)

3. 导入数据库驱动

   ![image-20210814202757198](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210814202757198.png)

   将jar包导入lib目录下，然后add as library jar包出现了小箭头就算导入环境成功

4. 编写测试代码

   ```java
   package com.sdut.test;
   
   import java.sql.*;
   
   // 我的第一个JDBC程序
   public class MyUtil {
       public static void main(String[] args) throws ClassNotFoundException, SQLException {
           //加载驱动(固定写法)
           Class.forName("com.mysql.jdbc.Driver");
           //用户连接(用户信息和URL)
           String URL = "jdbc:mysql://localhost:3306/db_book?useUnicode=true&characterEncoding=utf8&useSSL=true";
           String USERNAME = "root";
           String PASSWORD = "8023";
           //连接成功，数据库对象
           Connection connection = DriverManager.getConnection(URL, USERNAME, PASSWORD);
           //connection 代表数据库
   
           //执行SQL对象
           Statement statement = connection.createStatement();
           // statement 执行SQL
   
           //去执行SQL,接收返回数据
           String sql = "SELECT * FROM user";
           ResultSet resultSet = statement.executeQuery(sql);
           // resultSet 返回的结果集（链表的形式）,封装了我们全部的查询出来的结果
           while (resultSet.next()){
               System.out.println(resultSet.getObject("id"));
               System.out.println(resultSet.getObject("username"));
               System.out.println(resultSet.getObject("userpassword"));
           }
           //断开连接
           resultSet.close();
           statement.close();
           connection.close();
       }
   }
   
   ```

   ```java
   // jdbc:mysql://localhost:3306/db_book?useUnicode=true&characterEncoding=utf8&useSSL=true
   // jdbc:mysql://localhost:3306 固定写法
   // db_book 要连接的数据库名
   // useUnicode=true 使用编码字符集
   // characterEncoding=utf8 设置字符集为utf8
   // useSSL=true 安全连接
   String URL = "jdbc:mysql://localhost:3306/db_book?useUnicode=true&characterEncoding=utf8&useSSL=true";
   ```

   

   输出结果：

   1
   jfc
   8023
   2
   jxx
   8023
   3
   姜富超
   6666

5. **通用的步骤**

   1. 加载驱动
   2. 用户连接，获取数据库驱动
   3. 执行SQL对象
   4. 执行SQL语句
   5. 获取返回值
   6. 操作输出返回值
   7. 断开连接



## JDBC外部配置文档

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/db_book?useUnicode=true&characterEncoding=utf8&useSSL=true
username=root
password=8023
```

**工具类**

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

**插入测试：**

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class InsertTest {
    public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();
            // 获得SQL的执行对象
            statement = connection.createStatement();

            String sql = "INSERT INTO `user` (id,`username`,`userpassword`)\n" +
                    "VALUES (5,'jfz','123456')";

            int i = statement.executeUpdate(sql);

            if (i > 0) {
                System.out.println("插入成功");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            JDBCUtil.release(connection,statement,resultSet);
        }
    }
}

```

**删除测试：**

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class DeleteTest {
    public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();
            // 获得SQL的执行对象
            statement = connection.createStatement();

            String sql = "DELETE FROM `user` WHERE id = 5";

            int i = statement.executeUpdate(sql);

            if (i > 0) {
                System.out.println("删除成功");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, statement, resultSet);
        }
    }

}

```

**更新成功：**

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class UpDateTest {
    public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();
            // 获得SQL的执行对象
            statement = connection.createStatement();

            String sql = "UPDATE `user` SET `username`='dxy' WHERE id=4";

            int i = statement.executeUpdate(sql);

            if (i > 0) {
                System.out.println("更新成功");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, statement, resultSet);
        }
    }
}

```

**查询测试：**

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class SelectTest {
    public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();
            // 获得SQL的执行对象
            statement = connection.createStatement();

            String sql = "SELECT * FROM user";

            resultSet = statement.executeQuery(sql);

            while (resultSet.next()){
                System.out.println(resultSet.getObject("id"));
                System.out.println(resultSet.getObject("username"));
                System.out.println(resultSet.getObject("userpassword"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, statement, resultSet);
        }
    }
}
```

**增删改都是使用 statement.executeUpdate，而查询则使用 statement.executeQuery**



## SQL注入问题

SQL注入即是指[web应用程序](https://baike.baidu.com/item/web应用程序/2498090)对用户输入数据的合法性没有判断或过滤不严，攻击者可以在web应用程序中事先定义好的查询语句的结尾上添加额外的[SQL语句](https://baike.baidu.com/item/SQL语句/5714895)，在管理员不知情的情况下实现非法操作，以此来实现欺骗[数据库服务器](https://baike.baidu.com/item/数据库服务器/613818)执行非授权的任意查询，从而进一步得到相应的数据信息。

**sql存在漏洞，会被攻击，导致数据泄露**

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class LoginTest {
    public static void main(String[] args) {
        login("jfc", "8023");
        System.out.println("========================");
        // SQL注入问题
        login("'or '1=1","'or '1=1");
    }

    public static void login(String username, String password) {
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();
            // 获得SQL的执行对象
            statement = connection.createStatement();
            //SELECT * FROM `user` WHERE username='jfc' AND userpassword='8023'
            String sql = "SELECT * FROM user WHERE username='" + username + "' AND userpassword='" + password + "'";

            resultSet = statement.executeQuery(sql);

            while (resultSet.next()) {
                System.out.println(resultSet.getObject("id"));
                System.out.println(resultSet.getObject("username"));
                System.out.println(resultSet.getObject("userpassword"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, statement, resultSet);
        }
    }
}

```

输出结果：

1
jfc

8023

==========================

1
jfc
8023
2
jxx
8023
3
姜富超
6666
4
dxy
123456



## PreparedStatement

PreparedStatement 可以防止SQL注入，并且效率更快

**插入：**

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.*;

public class InsertTest01 {
    public static void main(String[] args) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();
            // 先书写SQL语句
            String sql = "INSERT INTO `user` (id,`username`,`userpassword`) VALUES (?,?,?)";

            // 预处理SQL语句但是不执行
            preparedStatement = connection.prepareStatement(sql);

            preparedStatement.setInt(1,5);
            preparedStatement.setString(2,"jfz");
            preparedStatement.setString(3,"802399");

            // 执行SQL语句
            int i = preparedStatement.executeUpdate();

            if (i > 0) {
                System.out.println("插入成功");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            JDBCUtil.release(connection,preparedStatement,resultSet);
        }
    }
}

```

**删除：**

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.*;

public class DeleteTest01 {
    public static void main(String[] args) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();

            String sql = "DELETE FROM `user` WHERE id = 5";
            preparedStatement = connection.prepareStatement(sql);

            int i = preparedStatement.executeUpdate();

            if (i > 0) {
                System.out.println("删除成功");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, preparedStatement, resultSet);
        }
    }
}
```

**修改：**

```
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.*;

public class UpDateTest01 {
    public static void main(String[] args) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();

            String sql = "UPDATE `user` SET `username`=? WHERE id=?";

            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setString(1,"jfc");
            preparedStatement.setInt(2,3);

            int i = preparedStatement.executeUpdate();

            if (i > 0) {
                System.out.println("更新成功");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, preparedStatement, resultSet);
        }
    }
}
```

**查询：**

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.*;

public class SelectTest01 {
    public static void main(String[] args) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();

            String sql = "SELECT `username` FROM `user` WHERE id=?";

            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setInt(1,3);

            resultSet = preparedStatement.executeQuery();

            while (resultSet.next()) {
                System.out.println(resultSet.getObject("username"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, preparedStatement, resultSet);
        }
    }

}

```

关于SQL注入问题：

```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.*;

public class LoginTest01 {
    public static void main(String[] args) {
        login("jfc", "8023");
        System.out.println("========================");
        // SQL注入问题
        login("'' or 1=1 ","'' or 1=1");
    }

    public static void login(String username, String password) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = JDBCUtil.getConnection();
            //SELECT * FROM `user` WHERE username='jfc' AND userpassword='8023'
            String sql = "SELECT * FROM `user` WHERE username=? AND userpassword=?";

            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setString(1,username);
            preparedStatement.setString(2,password);

            resultSet = preparedStatement.executeQuery();



            while (resultSet.next()) {
                System.out.println(resultSet.getObject("id"));
                System.out.println(resultSet.getObject("username"));
                System.out.println(resultSet.getObject("userpassword"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, preparedStatement, resultSet);
        }
    }
}

```

输出结果：

1
jfc

8023

===============

**PreparedStatement防止SQL注入的本质：把传递进来的参数当作字符，假设当中存在转义字符，则直接被转义。**



## IDEA连接数据库

![image-20210817084008751](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210817084008751.png)

![image-20210817084102360](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210817084102360.png)

![image-20210817091130191](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210817091130191.png)

连接成功

![image-20210817091203101](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210817091203101.png)

可以选择操作的数据库

![image-20210817091348304](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210817091348304.png)

要点击提交才会修改成功

![image-20210817091742982](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210817091742982.png)



## JDBC操作事务

事务：要么都成功，要么都失败

> ACID 原则

* 原子性：要么全部完成，要么都不完成
* 一致性：总数不变
* 隔离性：多个进程互不干扰
* 持久性：一旦提交不可逆，持久化到数据库



**隔离性的问题：**

脏读：一个事务读取了里一个没有提交的事务

不可重复读：在同一个事务内，重复读取表中的数据，表的数据发生了改变

脏读（幻读）：在一个事务内，读取到了别人插入的数据，导致前后读取的结果不一致



```java
package com.sdut.test;

import com.sdut.util.JDBCUtil;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class AffairsTest {

    public static void main(String[] args) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {

            connection = JDBCUtil.getConnection();

            // 关闭自动提交，即为开启事务
            connection.setAutoCommit(false);

            // 模拟事务的转账
            String sql1 = "UPDATE book SET count = count + 1 WHERE id = 1";
            preparedStatement = connection.prepareStatement(sql1);
            preparedStatement.executeUpdate();

            // 模拟中途失败
            int x = 1/0;

            String sql2 = "UPDATE book SET count = count - 1 WHERE id = 3";
            preparedStatement = connection.prepareStatement(sql2);
            preparedStatement.executeUpdate();

            // 提交事务
            connection.commit();
            System.out.println("成功！");
        } catch (SQLException e) {
            // 如果失败回滚事务,但是失败Java会自动回滚事务，所以可以自己书写事务的回滚，也可以不写
//            try {
//                connection.rollback();
//            } catch (SQLException ex) {
//                ex.printStackTrace();
//            }
            e.printStackTrace();
        }finally {
            JDBCUtil.release(connection,preparedStatement,resultSet);
        }
    }
}

```



## 数据库连接池

**数据库的连接 --- 执行完毕 --- 释放连接** 这一系列的操作流程是十分浪费系统资源



**池化技术：准备一些预先的资源，放在一个 ”池“ 中，等链接操作，然后连接准备好的资源**



编写连接池，实现一个接口：**DataSource**



> 开源数据源的实现

* DBCP
* C3P0
* Druid：阿里巴巴

使用了这些数据库连接池之后，我们在开源的项目开发中就不用书写编写连接数据库的代码



### DBCP

需要用到的jar包

![image-20210818191638372](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210818191638372.png)

DBCP 的数据库连接配置文件

```properties
#连接设置
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/db_book?useUnicode=true&characterEncoding=utf8&useSSL=true
username=root
password=123456

#<!-- 初始化连接 -->
initialSize=10

#最大连接数量
maxActive=50

#<!-- 最大空闲连接 -->
maxIdle=20

#<!-- 最小空闲连接 -->
minIdle=5

#<!-- 超时等待时间以毫秒为单位 6000毫秒/1000等于60秒 -->
maxWait=60000
#JDBC驱动建立连接时附带的连接属性属性的格式必须为这样：【属性名=property;】
#注意：user 与 password 两个属性会被明确地传递，因此这里不需要包含他们。
connectionProperties=useUnicode=true;characterEncoding=UTF8

#指定由连接池所创建的连接的自动提交（auto-commit）状态。
defaultAutoCommit=true

#driver default 指定由连接池所创建的连接的只读（read-only）状态。
#如果没有设置该值，则“setReadOnly”方法将不被调用。（某些驱动并不支持只读模式，如：Informix）
defaultReadOnly=

#driver default 指定由连接池所创建的连接的事务级别（TransactionIsolation）。
#可用值为下列之一：（详情可见javadoc。）NONE,READ_UNCOMMITTED, READ_COMMITTED, REPEATABLE_READ, SERIALIZABLE
defaultTransactionIsolation=READ_UNCOMMITTED
```



**DBCP 获取连接**

```java
package com.sdut.util;

import org.apache.commons.dbcp.BasicDataSource;
import org.apache.commons.dbcp.BasicDataSourceFactory;

import javax.sql.DataSource;
import java.io.IOException;
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

public class DBCPUtil {
    public static void main(String[] args) {
        try {
            getConnection();
            System.out.println("连接成功");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    private static DataSource dataSource = null;
    static {
        try {
            // 通过反射获取类加载器获取资源
            InputStream resourceAsStream =
                    DBCPUtil.class.getClassLoader().getResourceAsStream("dbcpconfig.properties");
            //读取流的内容
            Properties properties = new Properties();
            properties.load(resourceAsStream);

            // 工厂模式 获取数据源
            dataSource = BasicDataSourceFactory.createDataSource(properties);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // 获取数据库连接,返回一个数据库连接对象
    public static Connection getConnection() throws SQLException {
        // 从数据源直接获取连接
        return dataSource.getConnection();
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



**测试DBCP：**

```java
package com.sdut.test01;

import com.sdut.util.DBCPUtil;
import com.sdut.util.JDBCUtil;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class DBCPTest01 {
    public static void main(String[] args) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = DBCPUtil.getConnection();

            String sql = "SELECT `username` FROM `user` WHERE id=?";

            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setInt(1,3);

            resultSet = preparedStatement.executeQuery();

            while (resultSet.next()) {
                System.out.println(resultSet.getObject("username"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, preparedStatement, resultSet);
        }
    }
}

```



### C3P0（配置文件必须为 c3p0-config.xml）

需要导入的jar包：

![image-20210818194817480](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210818194817480.png)



```xml
<?xml version="1.0" encoding="UTF-8"?>

<c3p0-config>
    <!--
    c3p0的缺省（默认）配置
    如果在代码中ComboPooledDataSource comboPooledDataSource=new ComboPooledDataSource();这样写就表示使用的是c3p0的缺省（默认）
    -->
<default-config>
<property name="driverClass">com.mysql.jdbc.Driver</property>
<property name="jdbcUrl">jdbc:mysql://localhost:3306/db_book?useUnicode=true&amp;characterEncoding=utf8&amp;useSSL=true</property>
<property name="user">root</property>
<property name="password">8023</property>
<property name="acquiredIncrement">5</property>
<property name="initialPoolSize">10</property>
<property name="minPoolSize">5</property>
<property name="maxPoolSize">20</property>
</default-config>
    <!--
    c3p0的缺省（默认）配置
    如果在代码中ComboPooledDataSource comboPooledDataSource=new ComboPooledDataSource("MySQL");这样写就表示使用的是c3p0的缺省（默认）
    -->
<named-config name="MySQL">
<property name="driverClass">com.mysql.jdbc.Driver</property>
<property name="jdbcUrl">jdbc:mysql://localhost:3306/db_book?useUnicode=true&amp;characterEncoding=utf8&amp;useSSL=true</property>
<property name="user">root</property>
<property name="password">8023</property>
<property name="acquiredIncrement">5</property>
<property name="initialPoolSize">10</property>
<property name="minPoolSize">5</property>
<property name="maxPoolSize">20</property>
</named-config>

</c3p0-config>
```

**可以配置多套数据源**

```java
package com.sdut.util;

import com.mchange.v2.c3p0.ComboPooledDataSource;
import org.apache.commons.dbcp.BasicDataSourceFactory;

import javax.sql.DataSource;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

public class C3P0Util {
    public static void main(String[] args) {
        try {
            getConnection();
            System.out.println("连接成功");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    private static ComboPooledDataSource comboPooledDataSource = null;

    static {
        try {
//            // 通过代码配置
//            comboPooledDataSource.setDriverClass("com.mysql.jdbc.Driver");
//            comboPooledDataSource.setUser("root");
//            comboPooledDataSource.setPassword("8023");
//            comboPooledDataSource.setJdbcUrl
//                    ("jdbc:mysql://localhost:3306/jdbcstudy?" +
//                            "useUnicode=true&amp;" +
//                            "characterEncoding=utf8&amp;useSSL=true");
//
//            comboPooledDataSource.setMaxPoolSize(20);
//            comboPooledDataSource.setMaxPoolSize(5);

            // 配置文件
            comboPooledDataSource = new ComboPooledDataSource("MySQL");


        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // 获取数据库连接,返回一个数据库连接对象
    public static Connection getConnection() throws SQLException {
        // 直接获取连接
        return comboPooledDataSource.getConnection();
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

**测试：**

```java
package com.sdut.test01;

import com.sdut.util.C3P0Util;
import com.sdut.util.DBCPUtil;
import com.sdut.util.JDBCUtil;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class C3P0Test {

    public static void main(String[] args) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            // 获取连接
            connection = C3P0Util.getConnection();

            String sql = "SELECT `username` FROM `user` WHERE id=?";

            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setInt(1, 3);

            resultSet = preparedStatement.executeQuery();

            while (resultSet.next()) {
                System.out.println(resultSet.getObject("username"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtil.release(connection, preparedStatement, resultSet);
        }
    }
}

```

