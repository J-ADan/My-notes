# Java的异常处理（Exception）

软件程序在运行过程中，非常可能会遇到异常情况，Exception。

软件因为各种语法错误，逻辑错误，会出现很严重的错误，Error。

**异常发生在程序运行期间，影像了程序正常的执行流程**

```java
package com.sdut.demo05;

public class Demo03 {
    public static void main(String[] args) {
        System.out.println(11/0);
    }
}
```

![image-20210727075820576](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727075820576.png)

简单的异常

```java
package com.sdut.demo05;

public class Demo03 {
    public static void main(String[] args) {
        new Demo03().a();
    }

    public void a(){
        b();
    }

    public void b(){
        a();
    }
}
```

![image-20210727075945611](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727075945611.png)

简单的错误



## 异常的分类

1. 检查性异常（非运行异常、明文异常、编译时异常）**RuntimeException**

   最具代表的检查性异常是用户错误或问题引起的，这是程序员无法预见的。**必须进行异常处理**

2. 运行时异常（非明文异常、非检查异常）**Exception**

   运行时异常时可能被程序员避免的异常，与检查性异常相反，运行时异常可以在编译时被忽略。**可以进行异常处理**

3. 错误

   错误不是异常，而是脱离程序员控制的问题，错误在代码中通常被忽略，例如栈溢出时，错误就发生了，但是在编译时检查不到。



## Java异常体系

![image-20210727080947252](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727080947252.png)

**Java把一场当作对象来处理，并且定义一个基类 java.lang.Throwable 作为所有异常的超类。**

**Exception 式所有异常类的超类。**

Java API 已经定义了许多的异常类，这些异常类分为两类，Error（错误）和 Exception（异常）。

**错误 Error：**

VirtualMachineError：虚拟机异常

AWTError：GUI异常

**异常 Exception：**

IOException：IO流异常

RuntinmeException：运行时异常。



### Error

Error 类对象有 Java 虚拟机生成并抛出，大多数的错误与代码编写者所执行的操作无关

Java 虚拟机运行错误（VirtualMachineError）：当 JVM 不再有继续执行操作所需要的内存资源时，将出现 OutOfMemoryError，这邪恶异常的发生，Java虚拟机一般会选择线程终止。

还有发生虚拟机试图执行应用时，如类定义的错误（NoClassDefFoundError）、链接错误（LinkageError）。这些错误时不可查的，因为他们在应用程序的控制和处理能力之外，而且绝大多数是程序运行时不允许

出现的状况。

### Exception

在 Exception 分支中有一个非常重要的子类 RuntimeException（运行时异常）

1. ArrayIndexOutOfBoundsException：数组下标越界
2. NullPointerException：空指针异常
3. ArithmeticException：算数异常
4. MissingResourceException：丢失资源
5. ClassNotFoundException：找不到类

这些异常是不检查异常，程序中可以选择捕获处理，也可以不处理。这些异常一般是由代码逻辑错误引起的，程序应该尽可能的便面这类异常的发生。



### Error 和 Exception 的区别

Error通常是灾难性的致命的错误，是程序无法控制和处理的，当出现这些异常时，Java 虚拟机（JVM）一般会选择终止线程；Exception 通常情况下是可以被程序处理的，并且在程序中应尽可能的去处理这些异常。



## 异常处理机制

异常处理的五个关键字：

**try、catch、finally、throw、throws。**



```java
package com.sdut.demo05;

public class Demo04 {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;

        System.out.println(a / b);
    }
}
```

![image-20210727090355513](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727090355513.png)

正常的异常抛出

设置监听并且捕获抛出异常

```java
package com.sdut.demo05;

public class Demo04 {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;


        try {//try的监控区域，此区域出现异常，则会被catch捕获
            System.out.println(a / b);
        } catch (ArithmeticException e) {//内部参数是想要捕获的异常类型，必须写try区域可能会出现的异常，可以是运行时异常，可以是能发生的编译时异常
            //catch捕获异常，并执行catch代码块代码
            System.out.println("出现异常，除数不能为0");
        } finally {
            //finally是一定会被执行的代码块，他代表异常处理结束后的善后工作
            b = 1;
            System.out.println(a / b);
        }
    }
}
```

![image-20210727090735721](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727090735721.png)

**finally 语句大部分情况是不写的，也可以说是不需要的，但是在IO流，调用资源，关闭文件，数据库链接等，是必须要做最后的关闭善后工作的**

**当然，一个程序中可以捕获多个异常但是要把最大的异常类型写在最后。**



```java
package com.sdut;

public class TestAll {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;
        try{
            if (b == 0){
                throw new ArithmeticException();//主动抛出异常
            }
        }catch (Exception e){
            System.out.println("异常处理");
        }

    }
}
```

**如果try区域不会出现异常，catch语句可以不存在。**



一般主动抛出异常都是在函数中，并且是使用throws

```java
package com.sdut;

public class TestAll {
    public static void main(String[] args) {
        try {
            new TestAll().AAA(1,0);
        }catch (ArithmeticException e){
            e.printStackTrace();//打印错误类型
        }

    }
    public void AAA(int a,int b) throws ArithmeticException{
        if (b == 0){
            throw new ArithmeticException();
        }
    }
}
```

**try/catch 的作用一般是捕获并且抛出异常，并且遇到异常时，不会暂停程序的运行**



## 自定义异常

使用Java内置的异常类可以描述在编程时出现的大部分的异常情况。除此之外，用户还可以自定义异常，用户自定义异常类，只需要继承**Exception** 类即可	

程序中，自定义异常类的步骤

1. 创建自定义异常类
2. 在方法中通过 throw 关键字抛出异常对象
3. 如果在当前抛出异常的方法中处理对象，可以使用try-catch语句捕获并处理，否则在方法的声明处通过 throws 关键字指明要抛出给方法调用者的异常，继续进行下一步操作。
4. 在出现异常方法的调用者中捕获并处理异常。

```java
package com.sdut.demo06;

public class MyException extends Exception {

    private int detail;

    public MyException(int a) {
        this.detail = a;
    }

    @Override
    public String toString() {
        return "MyException{" +
                "detail=" + detail +
                '}';
    }
}
```



```java
package com.sdut.demo06;

public class Test{
    public static void main(String[] args) {
        try {
            test(11);
        } catch (MyException e) {
            e.printStackTrace();
        }
    }
    static void test(int a) throws MyException{
        System.out.println("传递的参数为：" + a);

        if (a > 10){
            throw new MyException(a);
        }
        System.out.println("OK");
    }
}
```

![image-20210727162305005](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727162305005.png)

**抛出的自定义异常**



自定义异常：

1. 处理运行异常时，采用逻辑去河里规避异常的同时辅助 try/catch 处理
2. 在多重 catch 块后面，可以加上一个 catch（Exception）来处理可能会被遗漏的异常
3. 对于不确定的代码，也可以加上 try/catch，处理潜在的异常
4. 尽量去处理异常，切记只是简单的调用 printStackTrace（）去打印输出
5. 具体如何处理异常，要根据不同的业务需求和异常类型去决定
6. 精良添加finally语句块去释放占用的资源。