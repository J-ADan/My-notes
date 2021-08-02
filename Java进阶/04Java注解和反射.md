# Java注解和反射

**Java框架的底层即为Java的注解和反射**



## 注解（开胃菜）

注释：给开发人员阅读，不算在程序之内

注解：可以给开发人员阅读，也可以给程序阅读，也可以被其他的程序阅读，也不算在程序之内。

Annotation：

1. 不是程序本身，可以对程序做出解释（这一点跟注释（comment）一样）
2. 可以被其他的程序读取，例如：编译器
3. 格式
   * 注解是以 @注释名 在代码中存在的，还可以添加一些参数值，例如：@SupperessWarnings(value = "unchecked")
4. Annotation使用的地方
   * 可以附加在package、class、method、field等上面，相当于给他们添加了额外的辅助信息，我们可以通过反射机制编程实现对这些元数据的访问。



```java
package com.sdut.annotationtest;


public class AnnotationTest01 extends Object {
    @Override
    public String toString() {
        return super.toString();
    }
}

```

重写注解

```java
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface <code>Runnable</code> is used
     * to create a thread, starting the thread causes the object's
     * <code>run</code> method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method <code>run</code> is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}
```

函数接口注解

```java
    @Deprecated
    public void destroy() {
        throw new NoSuchMethodError();
    }
```

弃用方法注解



**注解不仅仅是一种注释的作用，他还起到帮助检查的作用**

![image-20210801100744803](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210801100744803.png)



### 内置注解

1. @Override：定义在java.lang.Override 中，此注释只适用于修饰方法，表示一个方法声明打算重写超类中的另一个方法声明。
2. @Depeecated：定义在java.lang.Depeecated 中，此注释可以用于修饰方法，属性，类，表示不鼓励程序员使用这样的元素，通常因为他很危险，或者存在更好的选择。
3. @SuppressWarnings：定义在java.lang.SuppressWarnings 中，用来抑制编译时的警告信息。与上面两个注释不同，你需要提娜佳一个参数才能够正确使用，这些参数都是定义好的。
   * @SuppressWarnings("all")
   * @SuppressWarnings("unchecked")
   * @SuppressWarnings(value={"unchecked","deprecation})



![image-20210801101735028](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210801101735028.png)

```java
@SuppressWarnings("all")
    public void test(){
        
    }
```

消除黄色警告，但是尽量不要使用，除非不得已。



### 元注解

元注解的作用就是负责注解其他的注解，Java定义了四个标准的 meta-annotation 类型，它们被用来提供对其他 annotation 类型作说明。

这些类型和他们所支持的类可以在 java.lang.annotation 包中找到

**（@Target、@Retention、@Documented、@Inherited）**

1. @Target：用于描述注解的使用范围（即被描述的注解可以用在什么地方）
2. @Retention：表示需要在什么级别保存该注解信息，用于描述注解的生命周期（SOURCE<CLASS<RUNTIME）
3. @Document：表示该注解将被包含在 javadoc 中。
4. @Inherited：说明子类可以继承父类中的该注解。

```java
public class AnnotationTest01 extends Object {
    @MyAnnotation
    public void test(){
        
    }
}
@interface MyAnnotation{
    
}
```

简单的自定义注解

**元注解的使用**

```java
package com.sdut.annotationtest;

import java.lang.annotation.*;
//自定义注解
@MyAnnotation
public class AnnotationTest01 {
    @MyAnnotation
    public void test() {

    }
}


//表示注解可以使用的范围，即可以使用在类和方法
@Target(value = {ElementType.TYPE, ElementType.METHOD})

//表示注解存在的级别，即在什么地方可以存在
@Retention(RetentionPolicy.RUNTIME)

//表示注解可以存在与于javadoc中
@Documented

//表示注解可以被子类继承
@Inherited
@interface MyAnnotation {

}
```



### 自定义注解

1. 使用 @interface 自定义注解时，自动继承了 java.lang.annotation.Annotation 接口
2. @interface 用来声明一个注解，格式为 public @interface 注解名{定义的内容}
3. 其中的每一个方法实际上是声明了一个配置参数
4. 方法的名称就是参数的类型
5. 返回值类型就是参数的类型（返回值只能是基本类型，String、class、enum）
6. 可以通过 default 来声明参数的默认值
7. 如果只有一个参数成员，一般为 value
8. 注解元素不许要有值，我们定义注解元素是，经常使用空字符串，0作为默认值



```java
package com.sdut.annotationtest;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

public class AnnotationTest02 {
    
    //设置默认值的注解元素可以不写
    @Annotation1(age = 18)
    @Annotation2("姜富超")
    public void test(){
        
    }
    
}

@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@interface Annotation1{
    //可以设置默认值
    String name() default "姜富超";
    int id() default 001;
    int age();
    String[] school() default {"sdut","st"};
}
@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@interface Annotation2{
    //默认为value时，可以只写参数
    String value();
}
```



## 反射（重头戏）

**反射让Java语言有了动态的特性**



### 静态语言与动态语言

静态语言：

在运行时结构不可变的语言就是静态语言，例如Java、C、C++。

Java不是动态语言，但Java可以称之为 **准动态语言**，即Java有一定的动态性，我们可以利用反射机制获得类似动态语言的特征。Java的动态性可以让编程变得更加灵活。

动态语言：

是一类在运行时可以改变其结构的语言：例如新的函数，对象，甚至代码可以被引进，已有的函数可以被删除或是结构上的变化。通俗点说就是在运行时代码可以根据某些条件改变自身的结构。

主要的动态语言：Object-C、C#、JavaScript、PHP、Python等

```javascript
function f() {
    var x = "var a = 1; var b = 2; alert(a + b)"
    eval(x);
}
```





### Java的反射机制（Java Reflection）

Reflection（反射）是Java被视为动态语言的关键，反射机制允许程序在执行期间借助于 Reflection API 取得任何类的内部消息，并能直接操作任意对象的内部属性及方法。

Class c = Class.forName("java.lang.String")

加载完类之后在堆内存的方法区中就产生了一个Class类型的对象（一个类只能有一个Class类的对象），这个对象就包含了完整的类的结构信息，我们可以通过这个对象看到类的结构，这个对象就像是一面镜子，透过这个镜子看到类的结构，所以这个过程被称之为 **反射**

**正常的方式：引入需要的包类名称 -> 通过new实例化 -> 取得实例化对象**

**反射方式：实例化对象 -> getClass() 方法 -> 得到完整的包类名称**



**反射机制提供的功能**

1. 在运行时判断任意一个对象所属的类
2. 运行时构造任意一个类的对象
3. 在运行时判断任意一个类所具有的成员变量和方法
4. 在运行时获取泛型信息
5. 在运行时调用任意一个对象的成员变量和方法
6. 在运行时处理注解
7. 生成动态代理

**反射的优缺点**

优点：可以实现动态创建对象和编译，体现出很大的灵活性

缺点：性能有影响，使用反射基本上是一种解释操作，就像我们告诉JVM，我们希望他做什么，并且他满足我们的需求。这一类的操作总是比直接执行相同的操作要慢。



**反射的方法类**

1. java,lang.Calss：代表一个类
2. java.lang.reflect.Method：代表类的方法
3. java.lang.reflect.Field：代表类的成员变量
4. java.lang.reflect.Constructor：代表类的构造器



```java
package com.sdut.annotationtest;

import javax.print.attribute.standard.OrientationRequested;

public class ReflectTest01 {

    public static void main(String[] args) throws ClassNotFoundException {
        Class aClass = Class.forName("com.sdut.annotationtest.User");

        System.out.println(aClass);

        //一个类在内存中只有一个Class对象
        //一个类被加载后，类的整个结构都会被封装在Class对象中
        Class aClass1 = Class.forName("com.sdut.annotationtest.User");
        Class aClass2 = Class.forName("com.sdut.annotationtest.User");
        Class aClass3 = Class.forName("com.sdut.annotationtest.User");
        System.out.println(aClass1.hashCode());
        System.out.println(aClass2.hashCode());
        System.out.println(aClass3.hashCode());
    }

}

class User{
    private String name;
    private int id;

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", id=" + id +
                '}';
    }

    public User() {
    }

    public User(String name, int id) {
        this.name = name;
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}
```

输出结果：

class com.sdut.annotationtest.User
356573597
356573597
356573597



### Class 类

对象照镜子后可以得到的信息：某个类的属性、方法和构造器、某个类的到底实现了哪些接口。对于每个类而言，JRE 都为其保留一个不变的Class类型的对象。一个Class对象包含了某个特定的结构的有关信息（class/interface/enum/annotation/primitive type/vodi/[]）

1. Class本身也是一个类
2. Class对象只能由系统建立对象
3. 一个加载类在 JVM 中只会由一个Class实例
4. 一个Class对象对应的是一个加载到 JVM 中的一个 .class 文件
5. 每个类的实例都会记得自己是由哪个Class实例所生成的
6. 通过 Class 可以完整的得到一个类中的所有的被加载的结构
7. Class 类是 Reflection 的根源，针对任何你想的动态加载、运行的类，唯有先获得相应的Class对象



###  Class类中常用的方法

| 方法名                                 | 功能说明                                                    |
| -------------------------------------- | ----------------------------------------------------------- |
| static ClassforName(String name)       | 返回指定类名name的Class对象                                 |
| Object NewInstance()                   | 调用缺省构造函数，返回Class对象的一个实例                   |
| getName()                              | 返回此Class对象所表示的实体（类、接口、数组类或void）的名称 |
| Class getSuperClass()                  | 返回当前Class对象的父类的Class对象                          |
| Class[] getinterfaces()                | 获取当前Class对象的接口                                     |
| ClassLoader getClassLoader()           | 返回该类的类加载器                                          |
| Constructor[] getConstructors()        | 返回一个包含某些Constructor对象的数组                       |
| Method getMothed(String name,Class..T) | 返回一个Method对象，此对象的形参类型为paramType             |
| Field[] getDeclaredFields()            | 返回Field对象的一个数组                                     |

1. 若已知具体的类，通过类的class属性获取，该方法最为安全可靠，程序的性能最高

   Class clazz = Person.class;

2. 已知某个类的实例，调用该实例的getClass() 方法获取Class对象

   Class clazz = person.getClass();

3. 已知一个类的全类名，且该类在类的路径下，可通过Class类的静态方法forName() 获取，可能抛出ClassNotFoundException

   Class clazz = Class.forName("demo01.Student");

4. 内置基本数据类型可以直接使用类名.Type

5. 还可以利用ClassLoader



```java
package com.sdut.annotationtest;

import java.util.Scanner;

public class ReflectTest02 {
    public static void main(String[] args) throws ClassNotFoundException {
        Person person = new Student();
        System.out.println("这个人是" + person.name);

        //通过对象获得
        Class a1 = person.getClass();
        System.out.println(a1.hashCode());

        //通过forName全包名获得
        Class a2 = Class.forName("com.sdut.annotationtest.Student");
        System.out.println(a2.hashCode());

        //通过类名获得
        Class a3 = Student.class;
        System.out.println(a3.hashCode());

        //基本内置类型的包装类可以通过Type获得
        Class a4 = Integer.TYPE;
        System.out.println(a4);

        //获得父类类型
        Class a5 = a1.getSuperclass();
        System.out.println(a5);
    }
}

class Person{
    public String name;

    public Person() {
    }

    public Person(String name) {
        this.name = name;
    }
}

class Teacher extends Person{
    public Teacher() {
        this.name = "老师";
    }
}

class Student extends Person{
    public Student() {
        this.name = "学生";
    }
}
```



**那些类可以有Class对象**

1. class：外部类、成员（成员内部类、静态内部类）、局部内部类、匿名内部类
2. interface：接口
3. []：数组
4. enum：枚举
5. annotation：注解@interface
6. primitive type：基本数据类型
7. void

```java
package com.sdut.annotationtest;

import java.lang.annotation.ElementType;
import java.util.Objects;

public class ReflectTest03 {
    public static void main(String[] args) {
        Class c1 = Object.class;//类
        Class c2 = Comparable.class;//接口
        Class c3 = String[].class;//一维数组
        Class c4 = int[][].class;//二维数组
        Class c5 = Override.class;//注解
        Class c6 = ElementType.class;//枚举
        Class c7 = Integer.class;//基本数据类型
        Class c8 = void.class;//void
        Class c9 = Class.class;//Class

        System.out.println(c1);
        System.out.println(c2);
        System.out.println(c3);
        System.out.println(c4);
        System.out.println(c5);
        System.out.println(c6);
        System.out.println(c7);
        System.out.println(c8);
        System.out.println(c9);

        //只要元素类型与维度一致，就是同一个Class
        int [] a = new int [100];
        int [] b = new int [10];
        System.out.println(a.getClass().hashCode());
        System.out.println(b.getClass().hashCode());
    }
}

```

输出结果：

class java.lang.Object
interface java.lang.Comparable
class [Ljava.lang.String;
class [[I
interface java.lang.Override
class java.lang.annotation.ElementType
class java.lang.Integer
void
class java.lang.Class
356573597
356573597



### 类加载内存的分析

![image-20210802080346829](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802080346829.png)

**类的加载过程**

![image-20210802080506743](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802080506743.png)

1. 加载：将class文件的字节码内容加载到内存，并将这些静态数据转换成方法区运行时的数据结构，然后生成一个代表这个类的java.lang.Class对象
2. 链接：将Java类的二进制代码合并到JVM的运行状态之中的过程
   * 验证：确保加载的类的信息符合JVM规范，，没有安全方面问题
   * 准备：正式为类变量（static）分配内存并设置类变量的初始值阶段，这些内存都在方法区进行分配
   * 解析：虚拟机常量池内的符号引用（常量名）替换为直接引用（地址）的过程
3. 初始化：
   * 执行类构造器<clinit>() 方法的过程。类构造器<clinit>() 方法是由编译器自动收集类中所有类变量的赋值动作和静态代码块中的语句合并产生的。（类构造器是构造类信息的，不是构造该类对象的构造器）
   * 当初始化一个类的时候，如果发现其父类还没有进行初始化，则需要先触发其父类的初始化。
   * 虚拟机会保证一个类的<clinit>() 方法在多线程环境中被正确的加锁和同步。



```java
package com.sdut.annotationtest;

public class Test02 {
    public static void main(String[] args) {
        A a = new A();
        System.out.println(A.m);
        //1.加载到内存，会产生一个类对应的Class对象
        //2.链接，链接结束后 m = 0
        /*初始化
        <clinit>(){
         	System.out.println("类的静态块");
        	m = 300;
        	m = 100;
        }
        */
    }
}

class A{
    static {
        System.out.println("类的静态块");
        m = 300;
    }
    static int m = 100;

    public A() {
        System.out.println("类的无参构造方法");
    }
}
```

输出结果：

类的静态块
类的无参构造方法
100



![image-20210802082943066](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802082943066.png)

1. 加载到内存，会产生一个类对应的Class对象
2. 链接，链接结束后 m = 0
3. 初始化
           <clinit>(){
            	System.out.println("类的静态块");
           	m = 300;
           	m = 100;
           }



**什么时候会发生类的初始化（类的主动引用）：**

1. 当虚拟机启动，先初始化main方法所在的类
2. new一个类的对象
3. 调用类的静态成员（除final常量）和静态方法
4. 使用java.lang.reflect包的方法对垒进行反射调用
5. 当初始化一个类，如果其父类没有被初始化，则先会初始化父类

**什么时候不会发生类的初始化（类的被动引用）：**

1. 当访问一个静态域是，只有真正声明这个域的类才会被初始化。例如：通过子类引用父类的静态变量，不会导致子类初始化
2. 通过数组定义类的引用，不会触发此类的初始化
3. 引用常量不会触发此类的初始化



```java
package com.sdut.annotationtest;

public class Test03 {
    static {
        System.out.println("Main被加载");
    }
    public static void main(String[] args) throws ClassNotFoundException {
        //类的主动引用的情况
        System.out.println("1.");
        //1. new一个类的对象
        Son son = new Son();

        System.out.println("2.");
        //2.调用类的静态成员
        int n = Son.m;

        System.out.println("3.");
        //3. 反射调用
        Class aClass = Class.forName("com.sdut.annotationtest.Son");

        System.out.println("****************************");
        //类的被动引用
        System.out.println("1.");
        int n1 = Son.b;

        System.out.println("2.");
        //数组定义引用
        Son[] sons = new Son[10];

        System.out.println("3.");
        //引用常量
        int n3 = Son.a;
    }
}

class Father{
    static  int b = 1;
    static {
        System.out.println("父类被加载");
    }
}

class Son extends Father{
    static {
        System.out.println("子类被加载");
    }

    static int m = 100;
    static final int a = 1;
}
```



**类加载器的作用：**

![image-20210802085704615](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802085704615.png)

![image-20210802090141059](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802090141059.png)

```java
package com.sdut.annotationtest;

import javax.sound.midi.Soundbank;

public class Test04 {
    public static void main(String[] args) throws ClassNotFoundException {
        //获取系统的类加载器
        ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();
        System.out.println(systemClassLoader);

        //获取系统类加载器的父类加载器-->扩展类加载器
        ClassLoader parent = systemClassLoader.getParent();
        System.out.println(parent);

        //获取扩展类加载器的父类-->根加载器(C/C++)
        ClassLoader parent1 = parent.getParent();
        System.out.println(parent1);

        //获取某个类的加载器
        ClassLoader classLoader = Class.forName
                ("com.sdut.annotationtest.Test04").getClassLoader();
        System.out.println(classLoader);

        //测试JDK内置类是由谁加载的
        ClassLoader classLoader1 = Class.forName("java.lang.Object").getClassLoader();
        System.out.println(classLoader1);

        //获取系统类加载器可以加载的路径
        System.out.println(System.getProperty("java.class.path"));

        /*
        G:\Java\JDK\jdk1.8.0_131\jre\lib\charsets.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\deploy.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\access-bridge-64.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\cldrdata.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\dnsns.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\jaccess.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\jfxrt.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\localedata.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\nashorn.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\sunec.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\sunjce_provider.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\sunmscapi.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\sunpkcs11.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\ext\zipfs.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\javaws.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\jce.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\jfr.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\jfxswt.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\jsse.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\management-agent.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\plugin.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\resources.jar;
        G:\Java\JDK\jdk1.8.0_131\jre\lib\rt.jar;
        G:\Java\IDEA\WorkSpace\Demo02\out\production\Demo02;
        G:\Java\IDEA\IntelliJ IDEA 2019.3.5\lib\idea_rt.jar
         */
    }
}
```



**获取类中成员的方法**

```java
class User{
    private String name;
    private int id;

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", id=" + id +
                '}';
    }

    public User() {
    }

    public User(String name, int id) {
        this.name = name;
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }
}
```



```java
package com.sdut.annotationtest;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

public class Test05 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException, NoSuchMethodException {
        Class c1 = Class.forName("com.sdut.annotationtest.User");

        System.out.println("****************************");
        //获取类的名字
        System.out.println(c1.getName()); //获取全类名
        System.out.println(c1.getSimpleName()); //获取类名

        System.out.println("****************************");
        //获得类的属性
        Field [] field = c1.getFields(); //只能找到public属性
        for (Field field1 : field) {
            System.out.println(field1);
        }

        field = c1.getDeclaredFields();//找到全部属性
        for (Field field1 : field) {
            System.out.println(field1);
        }

        System.out.println("****************************");
        //获得指定属性的值
        Field name  = c1.getDeclaredField("name");
        System.out.println(name);

        System.out.println("****************************");
        //获得类的方法
        Method[] method = c1.getMethods();//获得本类及父类的全部public方法
        for (Method method1 : method) {
            System.out.println(method1);
        }

        method = c1.getDeclaredMethods();//获得本类的全部方法
        for (Method method1 : method) {
            System.out.println(method1);
        }

        System.out.println("****************************");
        //获得指定方法
        Method getName = c1.getMethod("getName",null);
        Method setName = c1.getMethod("setName", String.class);

        System.out.println(getName);
        System.out.println(setName);

        System.out.println("****************************");
        //获得构造器
        Constructor [] constructors = c1.getConstructors();
        for (Constructor constructor : constructors) {
            System.out.println(constructor);
        }
        constructors = c1.getDeclaredConstructors();
        for (Constructor constructor : constructors) {
            System.out.println(constructor);
        }

        System.out.println("****************************");
        //获得指定的构造器
        Constructor constructor = c1.getDeclaredConstructor(String.class,int.class);
        System.out.println("指定的" + constructor);
    }
}
```

输出结果

****************************
com.sdut.annotationtest.User
User
****************************
private java.lang.String com.sdut.annotationtest.User.name
private int com.sdut.annotationtest.User.id
****************************
private java.lang.String com.sdut.annotationtest.User.name
****************************
public java.lang.String com.sdut.annotationtest.User.toString()
public java.lang.String com.sdut.annotationtest.User.getName()
public int com.sdut.annotationtest.User.getId()
public void com.sdut.annotationtest.User.setName(java.lang.String)
public void com.sdut.annotationtest.User.setId(int)
public final void java.lang.Object.wait() throws java.lang.InterruptedException
public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
public boolean java.lang.Object.equals(java.lang.Object)
public native int java.lang.Object.hashCode()
public final native java.lang.Class java.lang.Object.getClass()
public final native void java.lang.Object.notify()
public final native void java.lang.Object.notifyAll()
public java.lang.String com.sdut.annotationtest.User.toString()
public java.lang.String com.sdut.annotationtest.User.getName()
public int com.sdut.annotationtest.User.getId()
public void com.sdut.annotationtest.User.setName(java.lang.String)
public void com.sdut.annotationtest.User.setId(int)
****************************
public java.lang.String com.sdut.annotationtest.User.getName()
public void com.sdut.annotationtest.User.setName(java.lang.String)
****************************
public com.sdut.annotationtest.User(java.lang.String,int)
public com.sdut.annotationtest.User()
public com.sdut.annotationtest.User(java.lang.String,int)
public com.sdut.annotationtest.User()
****************************
指定的public com.sdut.annotationtest.User(java.lang.String,int)

Process finished with exit code 0





### 获取对象，并操作方法以及属性

**步骤：**

1. 创建类的对象：调用Class对象的newInstance() 方法
   * 类必须有一个无参的构造器
   * 类的构造器的访问权限要足够
2. 有参构造器的使用方法
   * 通过Class类的getDeclaredConstructor(Class ... parameter Types) 取得本类的指定形参的构造器
   * 像构造器的形参中传递一个对象数组，里面包含了构造器中所需的各个参数
   * 通过Constructor实例化对象



```java
package com.sdut.annotationtest;

import javax.sound.midi.Soundbank;
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class ReflectTest04 {
    public static void main(String[] args) throws ClassNotFoundException, IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException, NoSuchFieldException {
        Class<?> c1 = Class.forName("com.sdut.annotationtest.User");

        //通过反射回来的c1构造一个对象
        //Object o = c1.newInstance();
        //因为我们确定这个对象是User的对象所以我们可以强转
        //这个方法实质上时调用了无参的构造方法
        User user1 = (User) c1.newInstance();
        System.out.println(user1);

        //通过构造器创建对象
        Constructor<?> constructor = c1.getDeclaredConstructor(String.class, int.class);
        User user2 = (User)constructor.newInstance("姜富超", 18);
        System.out.println(user2);
        System.out.println("******************");

        //通过反射调用普通方法
        User user3 = (User) c1.newInstance();
        Method setName = c1.getMethod("setName", String.class);

        //invoke激活的意思(对象,"方法的值")
        setName.invoke(user3,"姜富超");
        System.out.println(user3.getName());

        System.out.println("******************");
        //通过反射操作属性
        User user4 = (User) c1.newInstance();
        Field name = c1.getDeclaredField("name");

        //因为name属性为私有的属性，所以需要关闭安全检测
        name.setAccessible(true);
        name.set(user4,"姜富超");
        System.out.println(user4.getName());

    }
}

```

输出结果：

User{name='null', id=0}
User{name='姜富超', id=18}
******************
姜富超
******************
姜富超

![image-20210802185000030](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802185000030.png)



![image-20210802124808466](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802124808466.png)

![image-20210802124825689](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802124825689.png)

![image-20210802124831365](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802124831365.png)



### 分析性能问题



```java
package com.sdut.annotationtest;


import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

//性能测试
public class ReflectTest05 {
    //普通的调用方法
    public static void test01(){
        User user = new User();

        long satrtTime = System.currentTimeMillis();

        for (int i = 0; i < 1000000000; i++) {
            user.getName();
        }

        long endTime = System.currentTimeMillis();

        System.out.println("普通方式调用" + (endTime - satrtTime) + "ms");
    }

    public static void test02() throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        User user = new User();
        Class<? extends User> c1 = user.getClass();
        Method getName = c1.getMethod("getName", null);

        long satrtTime = System.currentTimeMillis();

        for (int i = 0; i < 1000000000; i++) {
            getName.invoke(user,null);
        }

        long endTime = System.currentTimeMillis();

        System.out.println("反射方式调用" + (endTime - satrtTime) + "ms");
    }

    public static void test03() throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        User user = new User();
        Class<? extends User> c1 = user.getClass();
        Method getName = c1.getMethod("getName", null);

        getName.setAccessible(true);
        long satrtTime = System.currentTimeMillis();

        for (int i = 0; i < 1000000000; i++) {
            getName.invoke(user,null);
        }

        long endTime = System.currentTimeMillis();

        System.out.println("关闭检测方式调用" + (endTime - satrtTime) + "ms");
    }

    public static void main(String[] args) throws NoSuchMethodException, IllegalAccessException, InvocationTargetException {
        test01();
        test02();
        test03();
    }
}

```

输出结果：

普通方式调用4ms
反射方式调用3128ms
关闭检测方式调用1754ms

**在使用反射方法的时候，尽量关闭检测**



### 反射操作泛型

1. Java中采用泛型擦除的机制来引入泛型，Java中的泛型仅仅是给编译器javac使用的，确保数据的安全性和免去强制类型转换的问题，但是，一旦编译完成，所有和泛型有关的类型全部擦除
2. 为了通过反射操作这些类型，Java中新增了 ParameterizedType，GenericArrayType，TypeVariable 和 WildcardType 几种类型来代表不能被归一到Class类中的类型但是有何原始类型齐名的类型。



* ParameterizedType：表示一种参数化类型，比如Collection<String>
* GenericArrayType：表示一种元素类型是参数化类型或者类型变量的数组类型
* TypeVariable ：是各种类型变量的公共父接口
* WildcardType ：代表一种通配符类型表达式



```java
package com.sdut.annotationtest;


import java.lang.reflect.Method;
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;
import java.util.List;
import java.util.Map;

public class ReflectTest06 {
    public void test01(Map<String,User> map, List<User> list){
        System.out.println("test01");
    }

    public Map<String,User> test02(){
        System.out.println("test02");
        return null;
    }

    public static void main(String[] args) throws NoSuchMethodException {
        Method method = ReflectTest06.class.getMethod("test01", Map.class, List.class);

        //获取泛型类型
        Type[] genericParameterTypes = method.getGenericParameterTypes();

        //打印泛型类型
        for (Type genericParameterType : genericParameterTypes) {
            //这里打印出来的只是获取到的集合
            System.out.println(genericParameterType);
            //判断是否是一个参数化类型，如果是就获得他的泛型
            if (genericParameterType instanceof ParameterizedType){
                Type[] actualTypeArguments =
                        ((ParameterizedType) genericParameterType).getActualTypeArguments();
                for (Type actualTypeArgument : actualTypeArguments) {
                    System.out.println("它的泛型为"+ actualTypeArgument);
                }
            }
        }

        method = ReflectTest06.class.getMethod("test02",null);

        //获取返回值泛型
        Type genericReturnType = method.getGenericReturnType();
        if (genericReturnType instanceof ParameterizedType){
            Type[] actualTypeArguments =
                    ((ParameterizedType) genericReturnType).getActualTypeArguments();
            for (Type actualTypeArgument : actualTypeArguments) {
                System.out.println("它的泛型为"+ actualTypeArgument);
            }
        }
    }
}

```

输出结果：

java.util.Map<java.lang.String, com.sdut.annotationtest.User>
它的泛型为class java.lang.String
它的泛型为class com.sdut.annotationtest.User
java.util.List<com.sdut.annotationtest.User>
它的泛型为class com.sdut.annotationtest.User
它的泛型为class java.lang.String
它的泛型为class com.sdut.annotationtest.User



### 反射操作注解

**OEM - Object relationship Mapping** 对象关系映射

![image-20210802132521589](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210802132521589.png)



**利用注解和反射完成类和表的映射关系**



```java
package com.sdut.annotationtest;

import java.lang.annotation.*;
import java.lang.reflect.Field;
import java.lang.reflect.Type;

public class ReflectTest07 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException {
        Class<?> aClass = Class.forName("com.sdut.annotationtest.Student01");

        //通过反射获得注解
        Annotation[] annotations = aClass.getAnnotations();
        for (Annotation annotation : annotations) {
            System.out.println(annotation);
        }

        System.out.println("********************");

        //获取注解的值
        classAnnotation annotation = aClass.getAnnotation(classAnnotation.class);
        String value = annotation.value();
        System.out.println(value);

        //获得属性的注解
        Field name = aClass.getDeclaredField("name");
        fieldAnnotation annotation1 = name.getAnnotation(fieldAnnotation.class);
        System.out.println(annotation1.length());
        System.out.println(annotation1.type());
        System.out.println(annotation1.name());
    }
}

@classAnnotation("db_student")
class Student01{
    @fieldAnnotation(type = "int",name = "db_id",length = "10")
    private int id;
    @fieldAnnotation(type = "varchar",name = "db_name",length = "3")
    private String name;
    @fieldAnnotation(type = "int",name = "db_age",length = "3")
    private int age;

    public Student01() {
    }

    public Student01(int id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

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
}

//类的注解
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@interface classAnnotation{
    String value();
}

@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
@interface fieldAnnotation{
    String type();
    String name();
    String length();
}
```

输出结果：

@com.sdut.annotationtest.classAnnotation(value=db_student)
********************
db_student
3
varchar
db_name



