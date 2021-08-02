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



