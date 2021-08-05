# Java网络编程



## 计算机网络的概念

计算机网络是指将**[地理](https://baike.baidu.com/item/地理)位置不同**的具有独立功能的多台[计算机](https://baike.baidu.com/item/计算机/140338)及其外部设备，通过通信线路连接起来，在[网络操作系统](https://baike.baidu.com/item/网络操作系统/3997)，[网络管理软件](https://baike.baidu.com/item/网络管理软件/6579078)及[网络通信协议](https://baike.baidu.com/item/网络通信协议/4438611)的管理和协调下，实现[资源共享](https://baike.baidu.com/item/资源共享/233480)和信息传递的计算机系统。



**网络编程的目的：**

传播交流信息、数据交换、通信



**网络编程和网页编程：**

网页编程：JavaWeb技术，B/S技术

网络编程：TCP/IP技术，C/S技术



 ### 网络通信的要素

通信双方的地址：

* IP地址
* 端口号

网络规则：网络协议

![image-20210802191933629](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802191933629.png)

五层架构：应用层、传输层、网络层、数据链路层、物理层



**网络编程中的要素：**

* IP和端口号
* 网络通信协议



### IP

IP地址是网络上唯一定位一台网络计算机

1. 127.0.0.1：代表本机，localhost
2. IP地址的分类
   * IPV4和IPV6
     * IPV4：四个字节组成，最多有42亿，2011年用尽。
     * IPV6：fe80::4cca:24a3:476c:a7af%8，128位，8个无符号整数
   * 公网（互联网）-私网（局域网）
     * 192.168.xxx.xxx，给组织内部使用





```java
package com.inetaddresstest;

import java.net.InetAddress;
import java.net.UnknownHostException;

public class InetAddressTest01 {
    public static void main(String[] args) {
        //查询本机地址
        try {
            InetAddress inetAddress1 = InetAddress.getByName("127.0.0.1");
            System.out.println(inetAddress1);
            InetAddress inetAddress2 = InetAddress.getByName("localhost");
            System.out.println(inetAddress2);
            InetAddress inetAddress3 = InetAddress.getLocalHost();
            System.out.println(inetAddress3);

            //查询网站的IP地址
            InetAddress inetAddress4 = InetAddress.getByName("www.baidu.com");
            System.out.println(inetAddress4);

            //常用的方法
            byte[] address = inetAddress4.getAddress();
            System.out.println(address);

            //获取规范的名字
            String canonicalHostName = inetAddress4.getCanonicalHostName();
            System.out.println(canonicalHostName);

            //获取IP
            String hostAddress = inetAddress4.getHostAddress();
            System.out.println(hostAddress);

            //获取域名
            String hostName = inetAddress4.getHostName();
            System.out.println(hostName);

            //获取自己电脑名字
            System.out.println(inetAddress2.getHostName());


        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }
}
```

输出结果：

/127.0.0.1
localhost/127.0.0.1
J-ADan02/192.168.76.1
www.baidu.com/39.156.66.14
[B@1540e19d
39.156.66.14
39.156.66.14
www.baidu.com
localhost



## 端口

一个端口代表计算机上一个应用程序的进程。

* 不同的进程有不同的端口号，用来区分软件
* 端口号：0~65535
* TCP与UDP协议分别提供：65535，即总端口为 65535 * 2，单个协议下，端口号是不能冲突的，但是TCP、UDP共用80端口。
* 端口分类
  * 公有端口：0~1023，内置进程使用，不要占用这些端口
    * HTTP：80
    * HTTPS：443
    * FTP：21
    * Telent：23
  * 程序注册端口：1014~49151；分配用户进程或者程序
    * Tomcat：8080
    * MySQL：3306
    * Oracle：1521
  * 动态端口，私有端口：49152~65535



**一些常用的Dos命令：**

```bash
netstat -ano # 查看所有的端口
netstat -ano|findstr "1176" # 查看指定端口
tasklist|findstr "1176" # 查看指定端口进程
```



```java
package com.inetaddresstest;

import java.net.InetSocketAddress;
import java.sql.SQLOutput;

public class InetAddressTest02 {
    public static void main(String[] args) {
        InetSocketAddress inetSocketAddress =
                new InetSocketAddress("127.0.0.1",8080);
        InetSocketAddress inetSocketAddress2 =
                new InetSocketAddress("localhost",8080);
        System.out.println(inetSocketAddress);
        System.out.println(inetSocketAddress2);

        System.out.println(inetSocketAddress.getAddress());
        System.out.println(inetSocketAddress.getHostName());
        System.out.println(inetSocketAddress.getPort());
    }
}

```

输出结果：

/127.0.0.1:8080
localhost/127.0.0.1:8080
/127.0.0.1
activate.navicat.com
8080



## 通信协议

协议，网络协议的简称，网络协议是通信计算机双方必须共同遵从的一组约定。如怎么样建立连接、怎么样互相识别等。只有遵守这个约定，计算机之间才能相互通信交流。它的三要素是：[语法](https://baike.baidu.com/item/语法/2447258)、[语义](https://baike.baidu.com/item/语义/9716033)、[时序](https://baike.baidu.com/item/时序/4734345)。

为了使数据在网络上从源到达目的，网络通信的参与方必须遵循相同的规则，这套规则称为协议（protocol），它最终体现为在网络上传输的数据包的格式。

协议往往分成几个层次进行定义，分层定义是为了使某一层协议的改变不影响其他层次的协议。



**TCP/IP协议簇**

两个重要的协议：TCP、IP协议

* TCP：用户传输协议
* UDP：用户数据报协议

IP：网络互连协议



### TCP与UDP的对比

TCP：TCP协议是一个连接的，稳定的协议，他在双方通信前会进行双发的连接，然后才会进行通信。通信结束后，会释放掉双方的连接。是一个基于客户端、服务端的协议。

**三次握手，四次挥手**



UDP：UDP协议是一个不连接的协议，他不会在双方之间建立一个通道，会直接将信息包装好发送在通道。他的客户端、服务端没有一个明确的界限。是一个不稳定的传输协议，但是效率高，速度快。

DDOS：洪水攻击。（饱和攻击）



## TCP

**客户端**

```java
package com.inetaddresstest;

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;

public class ClientDemo {
    public static void main(String[] args) {
        InetAddress byName = null;
        Socket socket = null;
        OutputStream outputStream = null;
        try {
            //1.要知道服务器的地址
            byName = InetAddress.getByName("127.0.0.1");
            int port = 8023;//端口号
            //2.创建一个socket连接
            socket = new Socket(byName,port);
            //3.发送消息
            outputStream = socket.getOutputStream();
            outputStream.write("我爱你啊".getBytes());
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            if (outputStream != null){
                try {
                    outputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (socket != null){
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```



**服务器端**


```java
package com.inetaddresstest;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) {
        ServerSocket serverSocket = null;
        Socket accept = null;
        InputStream inputStream = null;
        ByteArrayOutputStream byteArrayOutputStream = null;

        try {
            //1.服务器得有一个地址
            serverSocket = new ServerSocket(8023);
            //2.等待客户端连接
            accept = serverSocket.accept();
            //3.读取客户端的消息
            inputStream = accept.getInputStream();

            //利用管道流接收信息
            byteArrayOutputStream = new ByteArrayOutputStream();
            byte[] aByte = new byte[1024];
            int len;
            while ((len = inputStream.read(aByte)) != -1){
                byteArrayOutputStream.write(aByte,0,len);
            }
            System.out.println(byteArrayOutputStream.toString());
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (byteArrayOutputStream != null){
                try {
                    byteArrayOutputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (inputStream != null){
                try {
                    inputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            if (accept != null){
                try {
                    accept.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            if (serverSocket != null){
                try {
                    serverSocket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }

}

```



### 文件上传

```java
package com.inetaddresstest;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;

public class ClientDemo {
    public static void main(String[] args) {
        InetAddress byName = null;
        Socket socket = null;
        OutputStream outputStream = null;
        FileInputStream fileInputStream = null;
        try {
            byName = InetAddress.getByName("127.0.0.1");
            int port = 8023;//端口号
            socket = new Socket(byName,port);
            fileInputStream = new FileInputStream(new File("jianbi.jpg"));
            outputStream = socket.getOutputStream();

            byte[] aByte = new byte[1024];
            int len;
            while ((len = fileInputStream.read(aByte)) != -1){
                outputStream.write(aByte,0,len);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            if (outputStream != null){
                try {
                    outputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (fileInputStream != null){
                try {
                    fileInputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (socket != null){
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```



```java
package com.inetaddresstest;

import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerDemo {
    public static void main(String[] args) {
        ServerSocket serverSocket = null;
        Socket accept = null;
        InputStream inputStream = null;
        FileOutputStream fileOutputStream = null;

        try {
            //1.服务器得有一个地址
            serverSocket = new ServerSocket(8023);
            //2.等待客户端连接
            accept = serverSocket.accept();
            inputStream = accept.getInputStream();

            //利用管道流接收信息
            fileOutputStream = new FileOutputStream(new File("02.jpg"));
            byte[] aByte = new byte[1024];
            int len;
            while ((len = inputStream.read(aByte)) != -1){
                fileOutputStream.write(aByte,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (fileOutputStream != null){
                try {
                    fileOutputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (inputStream != null){
                try {
                    inputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            if (accept != null){
                try {
                    accept.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            if (serverSocket != null){
                try {
                    serverSocket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }

}

```



## 初识Tomcat

服务端

* 自定义的服务端
* Tomcat：Java后台开发

客户端

* 自定义的客户端
* 浏览器



## UDP

不用链接的服务，但是需要知道对方的地址。

需要用到的两个类：DatagramPacket、DatagramSocket



发送端

```java
package com.inetaddresstest;

import java.io.IOException;
import java.net.*;
import java.nio.channels.DatagramChannel;

public class UDPClient {
    public static void main(String[] args) {
        DatagramSocket datagramSocket = null;
        try {
            //建立一个Socket
            datagramSocket = new DatagramSocket();
            //建个包
            String msg = "我爱你啊";
            InetAddress inetAddress =InetAddress.getByName("127.0.0.1");
            int port = 8023;

            //数据，数据的长度的起始，数据要发送给谁
            DatagramPacket datagramPacket =
                    new DatagramPacket
                            (msg.getBytes(),0,msg.getBytes().length,inetAddress,port);

            datagramSocket.send(datagramPacket);
        } catch (SocketException | UnknownHostException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (datagramSocket != null){
                datagramSocket.close();
            }
        }
    }
}

```

接收端

```java
package com.inetaddresstest;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketException;

public class UDPServer {
    public static void main(String[] args) {

        DatagramSocket datagramSocket = null;
        DatagramPacket datagramPacket = null;

        try {
            //开放端口
            datagramSocket = new DatagramSocket(8023);
            //接收数据包
            byte[] bytes = new byte[1024];
            datagramPacket =
                    new DatagramPacket(bytes,0,bytes.length);

            //阻塞接收
            datagramSocket.receive(datagramPacket);

            //输出发送主机的地址
            System.out.println(
                    datagramPacket.getAddress().getHostAddress());
            System.out.println(new java.lang.String(datagramPacket.getData(),0,datagramPacket.getLength()));
        } catch (SocketException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (datagramSocket != null){
                datagramSocket.close();
            }
        }
    }
}

```



**聊天初实现（持续输入持续接收）**

持续输入端

```java
package com.inetaddresstest;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.*;

public class UDPPerson01 {
    public static void main(String[] args) {
        DatagramSocket datagramSocket = null;
        try {
            datagramSocket = new DatagramSocket(8023);
            while (true){


                //准备数据，控制台读取
                BufferedReader bufferedReader =
                        new BufferedReader(new InputStreamReader(System.in));

                String data = bufferedReader.readLine();
                byte[] bytes = data.getBytes();
                DatagramPacket datagramPacket =
                        new DatagramPacket
                                (bytes,0,bytes.length,new InetSocketAddress("127.0.0.1",9999));

                datagramSocket.send(datagramPacket);

                if (data.equals("bye")){
                    break;
                }
            }
        } catch (SocketException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (datagramSocket != null){
                datagramSocket.close();
            }
        }
    }
}

```

持续输出端

```java
package com.inetaddresstest;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketException;

public class UDPPerson02 {
    public static void main(String[] args) {
        DatagramSocket datagramSocket = null;
        try {
            datagramSocket = new DatagramSocket(9999);
            while (true){

                //准备接收包裹
                byte[] bytes = new byte[1024];
                DatagramPacket datagramPacket = new DatagramPacket(bytes,0,bytes.length);
                datagramSocket.receive(datagramPacket);
                byte[] data = datagramPacket.getData();
                String datas = new String(data,0,data.length);
                System.out.println(datas);

                if (datas.equals("bye")){
                    break;
                }
            }

        } catch (SocketException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (datagramSocket != null){
                datagramSocket.close();
            }
        }
    }
}
```



**聊天程序**

发送端

```java
package com.inetaddresstest;

import jdk.internal.org.objectweb.asm.tree.TryCatchBlockNode;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetSocketAddress;
import java.net.SocketException;

public class Demo01 implements Runnable{
    DatagramSocket datagramSocket = null;
    BufferedReader bufferedReader = null;
    private int fromPort;
    private String toIP;
    private int toPort;

    public Demo01(int fromPort, String toIP, int toPort) {
        this.fromPort = fromPort;
        this.toIP = toIP;
        this.toPort = toPort;
        try {
            datagramSocket = new DatagramSocket(fromPort);
            bufferedReader =
                    new BufferedReader(new InputStreamReader(System.in));
        } catch (SocketException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void run() {
        try {
            while (true){
                String data = bufferedReader.readLine();
                byte[] bytes = data.getBytes();
                DatagramPacket datagramPacket =
                        new DatagramPacket
                                (bytes,0,bytes.length,new InetSocketAddress(this.toIP,this.toPort));

                datagramSocket.send(datagramPacket);

                if (data.equals("bye")){
                    break;
                }
            }
        } catch (SocketException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (datagramSocket != null){
                datagramSocket.close();
            }
        }
    }
}

```

接收端

```java
package com.inetaddresstest;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketException;

public class Demo02 implements Runnable{
    DatagramSocket datagramSocket = null;
    private int port;
    private String fromname;

    public Demo02(int port, String fromname) {
        this.port = port;
        this.fromname = fromname;
        try {
            datagramSocket = new DatagramSocket(port);
        } catch (SocketException e) {
            e.printStackTrace();
        }

    }

    @Override
    public void run() {

        try {

            while (true){

                //准备接收包裹
                byte[] bytes = new byte[1024];
                DatagramPacket datagramPacket = new DatagramPacket(bytes,0,bytes.length);
                datagramSocket.receive(datagramPacket);
                byte[] data = datagramPacket.getData();
                String datas = new String(data,0,data.length);
                System.out.println(fromname + ":" + datas);

                if (datas.equals("bye")){
                    break;
                }
            }

        } catch (SocketException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (datagramSocket != null){
                datagramSocket.close();
            }
        }
    }
}

```

学生端

```java 
package com.inetaddresstest;

public class Student {
    public static void main(String[] args) {
        new Thread(new Demo01(6666,"127.0.0.1",9999)).start();
        new Thread(new Demo02(7777,"老师")).start();
    }
}

```

教师端

```java
package com.inetaddresstest;

public class Teacher {
    public static void main(String[] args) {
        new Thread(new Demo01(8888,"127.0.0.1",7777)).start();
        new Thread(new Demo02(9999,"学生")).start();
    }
}

```



### URL

统一资源定位符-URL：定位互联网上的某一个资源



DNS域名解析：将一个域名网站解析为ip地址访问

```bash
# URL组成部分
协议://ip地址:端口/项目名/资源
```



``` 
package com.inetaddresstest;

import java.net.MalformedURLException;
import java.net.URL;

public class URLDemo {
    public static void main(String[] args) {
        try {
            URL url = new URL("http://localhost:8080//helloworld/index.html?username=jfc&password=123456");
            
            //获取协议
            System.out.println(url.getProtocol());
            //获取文件
            System.out.println(url.getPath());
            //获取端口
            System.out.println(url.getPort());
            //获取ip
            System.out.println(url.getHost());
            //获取文件的全路径
            System.out.println(url.getFile());
            //获取参数
            System.out.println(url.getQuery());
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
    }
}
```



**下载网络资源：**

```java
package com.inetaddresstest;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.HttpCookie;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;

public class URLDown {
    public static void main(String[] args) {
        try {
            URL url = new URL("http://rcode.zongheng.com/v2018/images/logo.png");
            //连接到资源
            HttpURLConnection httpURLConnection = (HttpURLConnection)url.openConnection();

            //流下载
            InputStream inputStream = httpURLConnection.getInputStream();

            //文件下载
            FileOutputStream fileOutputStream = new FileOutputStream("logo.png");
            byte[] bytes = new byte[1024];
            int len;
            while ((len = inputStream.read(bytes)) != -1){
                fileOutputStream.write(bytes,0,bytes.length);
            }

            fileOutputStream.close();
            inputStream.close();
            httpURLConnection.disconnect();
        } catch (MalformedURLException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```

