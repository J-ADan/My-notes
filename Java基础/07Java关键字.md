# 关键字

具有特定功能的标识符

```java
package com.sdut.Demo01;
//包 当前文件所在的全包名

import java.util.Scanner;
//import 在当前文件中使用其他包的文件时，java.lang除外
//import 全文件名 （全报名.文件名）

public class Demo02 {
	static Scanner scanner = new Scanner(System.in); 
	
	//访问修饰符 public -公共的/共有的，可以在当前工程中的任意位置使用
	public static void main(String[] args) {
		
	}
}

```



## static详解

**static 静态的**

static修饰的，可以直接使用静态成员，不可以直接使用实例成员，**即static修饰的，可以使用static修饰的，但不能使用未被staticiu是的方法或者变量，而未被修饰的可以使用static修饰的**



```java
package com.sdut.demo;

public class Student {
	
	private static int age;
	private String name;
	
	public static void main(String[] args) {
		Student st = new Student();
		
		System.out.println(Student.age);
		System.out.println(st.name);
		System.out.println(st.age);//会出现警告，黄线
	}
}

```



**这里我们可以看到，静态的变量，可以利用类名直接调用，也可以通过对象调用，但是通过对象调用会出现警告，所以我们的静态变量，Java推荐我们使用类名直接调用，而非静态变量，我们只能通过对象调用，使用类名会报错，静态方法与非静态方法同样如此**

`这是因为类的加载顺序的问题 静态成员快于实例成员`

### 块与静态块（简单一提）

```java
package com.sdut.demo;

public class Demo02 {
	
	{
		//块(匿名代码块)
		System.out.println("匿名代码块");
	}
	
	static {
		//静态块(静态代码块)
		System.out.println("静态代码块");
	}
	
	public Demo02() {//构造方法
		System.out.println("构造方法");
	}
	
	public static void main(String[] args) {
		Demo02 de1 = new Demo02();
		Demo02 de2 = new Demo02();
	}
}

```

**执行顺序：** `静态代码块>代码块>构造方法`

**并且，静态块只执行一次**

### 静态导入包

**不导入类使用方法：**

![image-20210723222441756](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210723222441756.png)

**静态导入：**

![image-20210723222629836](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210723222629836.png)

# 关键字的详细整理

关键字和保留字的区别

正确识别java语言的关键字（keyword）和保留字（reserved word）是十分重要的。Java的关键字对java的编译器有特殊的意义，他们用来表示一种数据类型，或者表示程序的结构等。保留字是为java预留的关键字，他们虽然现在没有作为关键字，但在以后的升级版本中有可能作为关键字。

识别java语言的关键字，不要和其他语言如c/c++的关键字混淆。 

标志符包含关键字而关键字里面又包含两个保留字，根据java文档true、false、null不属于关键字但是属于标志符，规定的关键字只有50个包含两个保留字，但是这53个都属于标志符。

1.保留字（reserved words）：是语言已经定义过的字，一些保留字可能没有相对应的语法，考虑到扩展性，为了向后兼容不能再将其作为变量名。const和goto是java的保留字。 所有的关键字都是小写 

2.50个关键字（keywards）：在语言中有特殊的含义成为语法的一部分。

| abstract   | assert       | boolean   | break      | byte   |
| ---------- | ------------ | --------- | ---------- | ------ |
| case       | catch        | char      | class      | const  |
| continue   | default      | do        | double     | else   |
| enum       | extends      | final     | finally    | float  |
| for        | goto         | if        | implements | import |
| instanceof | int          | interface | long       | native |
| new        | package      | private   | protected  | public |
| return     | strictfp     | short     | static     | super  |
| switch     | synchronized | this      | throw      | throws |
| transient  | try          | void      | volatile   | while  |

关键字的分类

关键字分为：访问控制、类方法和变量修饰符、程序控制语句、错误处理、包相关、基本类型、变量引用。

访问控制 修饰符的关键字（共3个）：

| 关键字    | 意思     | 备注，常用             |
| --------- | -------- | ---------------------- |
| public    | 公有的   | 可跨包，（默认选择）   |
| protected | 受保护的 | 当前包内可用，子类可见 |
| private   | 私有的   | 当前类可用             |

（1）private：可以应用于类、方法或字段（类中声明的变量），只能在声明的类内部中引用这些类、方法或字段，在外部或者对于子类而言是不可见的，类的默认访问范围是package访问，除非存在特殊的访问控制修饰符。可以从一个包中的任何类访问类成员 。只能修饰内部类。

（2）protected：应用于类、方法或字段（类中声明的变量），可以在声明 protected 类、方法或字段的类、同一个包中的其他任何类以及任何子类（无论子类是在哪个包中声明的）中引用这些类、方法或字段。所有类成员的默认访问范围都是 package 访问，也就是说，除非存在特定的访问控制修饰符，否则可以从同一个包中的任何类访问类成员。 当前类、同包、非同包的子类。不能修饰外部类。

子类与父类在同一个包内，被protected修饰的成员可以被同包的其他文件访问，子类与父类在不同包下，子类可以访问从父类继承的protected成员，父类不能访问protected成员。

（3）public：应用于类、方法或字段（在类中声明的变量）的访问控制修饰符。 可能只会在其他任何类或包中引用 public 类、方法或字段。所有类成员的默认访问范围都是 package 访问，也就是说，除非存在特定的访问控制修饰符，否则，可以从同一个包中的任何类访问类成员。 所有类均可访问。一个文件中，只有一个public修饰的外部类

默认修饰符：friendly，有好的，默认的，在同包下可见，修饰成员变量，成员方法，类。



类、方法和变量修饰符：

定义类、接口、抽象类和实现接口、继承类的关键字、实例化对象（共6个）

| 关键字     | 意思       | 备注，常用                                                   |
| ---------- | ---------- | ------------------------------------------------------------ |
| class      | 类         | public class A(){} 花括号里有已实现方法体，类名需要与文件名相同 |
| interface  | 接口       | public interface B(){} 花括号里有方法体，但没有实现，方法体句子后面是英文分号“;”结尾 |
| abstract   | 声明抽象   | public abstract class C(){} 介于类与接口中间，可以有也可以没有已经实现的方法体 |
| implements | 实现       | 用于类或接口实现接口public class A interface B(){}           |
| extends    | 继承       | 用于类继承类 public class A extends D(){}                    |
| new        | 创建新对象 | A a=new A(); A表示一个类                                     |

（1）class：用来声明新的 Java类，该类是相关变量和/或方法的集合。类是面向对象的程序设计方法的基本构造单位。类通常代表某种实际实体，如几何形状或人。类是对象的模板。每个对象都是类的一个实例。要使用类，通常使用 new 操作符将类的对象实例化，然后调用类的方法来访问类的功能。

（2） interface ：用来声明新的 [Java](http://lib.csdn.net/base/java) 接口，接口是方法的集合。接口是 Java 语言的一项强大功能。任何类都可声明它实现一个或多个接口，这意味着它实现了在这些接口中所定义的所有方法。 实现了接口的任何类都必须提供在该接口中的所有方法的实现。一个类可以实现多个接口。

（3）abstract：可以修改类或方法。abstract类可以扩展（增加子类），但不能直接实例化。abstract方法不在声明它的类中实现，但必须在某个子类中重写。采用 abstract方法的类本来就是抽象类，并且必须声明为abstract。

（4）implements：在 class 声明中使用，以指示所声明的类提供了在 implements 关键字后面的名称所指定的接口中所声明的所有方法的实现。类必须提供在接口中所声明的所有方法的实现。一个类可以实现多个接口。

（5）extends：用在 class 或 interface 声明中，用于指示所声明的类或接口是其名称后跟有 extends 关键字的类或接口的子类。子类继承父类的所有 public 和 protected 变量和方法。 子类可以重写父类的任何非 final 方法。一个类只能扩展一个其他类。

（6） new：用于创建类的新实例。 new 关键字后面的参数必须是类名，并且类名的后面必须是一组构造方法参数（必须带括号）。 参数集合必须与类的构造方法的签名匹配。 = 左侧的变量的类型必须与要实例化的类或接口具有赋值兼容关系。

修饰方法、类、属性和变量（共9个）

| 关键字       | 意思               | 备注，常用                                                   |
| ------------ | ------------------ | ------------------------------------------------------------ |
| static       | 静态的             | 属性和方法都可以用static修饰，直接使用类名.属性和方法名。 只有内部类可以使用static关键字修饰，调用直接使用类名.内部类类名进行调用。 static可以独立存在。静态块 |
| final        | 最终的不可被改变的 | 方法和类都可以用final来修饰 final修饰的类是不能被继承的 修饰的方法是不能被子类重写。 常量的定义：final修饰的属性就是常量。 |
| super        | 调用父类的方法     | 常见public void paint(Graphics g){ super.paint(g); ··· }     |
| this         | 当前类的父类的对象 | 调用当前类中的方法（表示调用这个方法的对象） this.addActionListener(al):等等 |
| native       | 本地               |                                                              |
| strictfp     | 严格,精准          |                                                              |
| synchronized | 线程,同步          |                                                              |
| transient    | 短暂               |                                                              |
| volatile     | 易失               |                                                              |

  

（1） static：static 关键字可以应用于内部类（在另一个类中定义的类）、方法或字段（类的成员变量）。 通常，static 关键字意味着应用它的实体在声明该实体的类的任何特定实例外部可用。static（内部）类可以被其他类实例化和引用（即使它是顶级类）。在上面的示例中，另一个类中的代码可以实例化 MyStaticClass 类，方法是用包含它的类名来限定其名称，如 MyClass.MyStaticClass。 static 字段（类的成员变量）在类的所有实例中只存在一次。 可以从类的外部调用 static 方法，而不用首先实例化该类。这样的引用始终包括类名作为方法调用的限定符。模式：public final static <type> varName = <value>; 通常用于声明可以在类的外部使用的类常量。在引用这样的类常量时需要用类名加以限定。在上面的示例中，另一个类可以用 MyClass.MAX_OBJECTS 形式来引用 MAX_OBJECTS 常量。

（2）final：应用于类，以指示不能扩展该类（不能有子类）。final 关键字可以应用于方法，以指示在子类中不能重写此方法。一个类不能同时是 abstract 又是 final。abstract 意味着必须扩展类，final 意味着不能扩展类。一个方法不能同时是 abstract 又是 final。abstract 意味着必须重写方法，final 意味着不能重写方法

（3）super ：用于引用使用该关键字的类的超类。 作为独立语句出现的 super 表示调用超类的构造方法。 super.<methodName>() 表示调用超类的方法。只有在如下情况中才需要采用这种用法：要调用在该类中被重写的方法，以便指定应当调用在超类中的该方法。

（4） this ：用于引用当前实例。 当引用可能不明确时，可以使用 this 关键字来引用当前的实例。

（5）native ：以指示该方法是用 Java 以外的语言实现的。Java的不足除了体现在运行速度上要比传统的C++慢许多之外，Java无法直接访问到 [操作系统](http://lib.csdn.net/base/operatingsystem)底层（如系统硬件等)，为此Java使用native方法来扩展Java程序的功能。 

　　可以将native方法比作Java程序同Ｃ程序的接口，其实现步骤： 

　　１、在Java中声明native()方法，然后编译； 

　　２、用javah产生一个.h文件； 

　　３、写一个.cpp文件实现native导出方法，其中需要包含第二步产生的.h文件（注意其中又包含了JDK带的jni.h文件）； 

　　４、将第三步的.cpp文件编译成动态链接库文件； 

　　５、在Java中用System.loadLibrary()方法加载第四步产生的动态链接库文件，这个native()方法就可以在Java中被访问了。

（6） strictfp：strictfp的意思是FP-strict，也就是说精确浮点的意思。在Java虚拟机进行浮点运算时，如果没有指定strictfp关键字时，Java的编译器以及运行环境在对浮点运算的表达式是采取一种近似于我行我素的行为来完成这些操作，以致于得到的结果往往无法令人满意。而一旦使用了strictfp来声明一个类、接口或者方法时，那么所声明的范围内Java的编译器以及运行环境会完全依照浮点规范IEEE-754来执行。因此如果想让浮点运算更加精确，而且不会因为不同的硬件平台所执行的结果不一致的话，那就请用关键字strictfp。可以将一个类、接口以及方法声明为strictfp，但是不允许对接口中的方法以及构造函数声明strictfp关键字。

（7） synchronized：可以应用于方法或语句块，并为一次只应由一个线程执行的关键代码段提供保护。 可防止代码的关键代码段一次被多个线程执行。 如果应用于静态方法，那么，当该方法一次由一个线程执行时，整个类将被锁定。 如果应用于实例方法，那么，当该方法一次由一个线程访问时，该实例将被锁定。 如果应用于对象或数组，当关联的代码块一次由一个线程执行时，对象或数组将被锁定。

（8） transient ：可以应用于类的成员变量，以便指出该成员变量不应在包含它的类实例已序列化时被序列化。当一个对象被串行化的时候，transient型变量的值不包括在串行化的表示中，然而非transient型的变量是被包括进去的。Java的serialization提供了一种持久化对象实例的机制。当持久化对象时，可能有一个特殊的对象数据成员，我们不想用serialization机制来保存它。为了在一个特定对象的一个域上关闭serialization，可以在这个域前加上关键字transient。 transient是Java语言的关键字，用来表示一个域不是该对象串行化的一部分。当一个对象被串行化的时候，transient型变量的值不包括在串行化的表示中，然而非transient型的变量是被包括进去的。

（9） volatile  ：用于表示可以被多个线程异步修改的成员变量。 注意：volatile 关键字在许多 Java 虚拟机中都没有实现。 volatile 的目标用途是为了确保所有线程所看到的指定变量的值都是相同的。Java 语言中的 volatile 变量可以被看作是一种 “程度较轻的 synchronized”；与 synchronized 块相比，volatile 变量所需的编码较少，并且运行时开销也较少，但是它所能实现的功能也仅是 synchronized 的一部分。

 程序控制语句

条件循环（流程控制）（共12个）

| 关键字     | 意思             | 备注，常用                                                   |      |      |      |
| ---------- | ---------------- | ------------------------------------------------------------ | ---- | ---- | ---- |
| if         | 如果             | if(){} 如果小括号里面怎么怎么样 花括号就怎么怎么样           |      |      |      |
| else       | 否则，或者       | 常与if连用，用法相同                                         |      |      |      |
| while      | 当什么的时候     | while 怎么样就do什么 while(){}                               |      |      |      |
| for        | 满足三个条件时   | for ( ; ; ){}                                                |      |      |      |
| switch     | 开关             | switch(表达式) { case 常量表达式1:语句1; .... case 常量表达式2:语句2; default:语句; } default就是如果没有符合的case就执行它,default并不是必须的. case后的语句可以不用大括号. switch语句的判断条件可以接受int,byte,char,short,不能接受其他类型. |      |      |      |
| case       | 返回开关里的结果 |                                                              |      |      |      |
| default    | 默认             |                                                              |      |      |      |
| do         | 运行             | 长与while连用                                                |      |      |      |
| break      | 跳出循环         |                                                              |      |      |      |
| continue   | 继续             | 中断本次循环，并并开始下一次                                 |      |      |      |
| return     | 返回             | return 一个返回值类型                                        |      |      |      |
| instanceof | 实例             | 一个二元操作符，和==，>，<是同一类的。测试它左边的对象是否是它右边的类的实例，返回boolean类型的数据 |      |      |      |

（1） if ：指示有条件地执行代码块。条件的计算结果必须是布尔值。 if 语句可以有可选的 else 子句，该子句包含条件为 false 时将执行的代码。 包含 boolean 操作数的表达式只能包含 boolean 操作数。

（2） else ：总是在 if-else 语句中与 if 关键字结合使用。else 子句是可选的，如果 if 条件为 false，则执行该子句。

（3） while ：用于指定一个只要条件为真就会重复的循环。

（4） for ：用于指定一个在每次迭代结束前检查其条件的循环。 for 语句的形式为 for(initialize; condition; increment) 控件流进入 for 语句时，将执行一次 initialize 语句。每次执行循环体之前将计算 condition 的结果。如果 condition 为 true，则执行循环体。 每次执行循环体之后，在计算下一个迭代的 condition 之前，将执行 increment 语句。

（5） switch ：用于基于某个表达式选择执行多个代码块中的某一个。 switch 条件的计算结果必须等于 byte、char、short 或 int。 case 块没有隐式结束点。break 语句通常在每个 case 块末尾使用，用于退出 switch 语句。 如果没有 break 语句，执行流将进入所有后面的 case 和/或 default 块。

（6）case ： 用来标记 switch 语句中的每个分支。 case 块没有隐式结束点。break 语句通常在每个 case 块末尾使用，用于退出 switch 语句。 如果没有 break 语句，执行流将进入所有后面的 case 和/或 default 块。

（7） default ：用来标记 switch 语句中的默认分支。 default 块没有隐式结束点。break 语句通常在每个 case 或 default 块的末尾使用，以便在完成块时退出 switch 语句。 如果没有 default 语句，其参数与任何 case 块都不匹配的 switch 语句将不执行任何操作。

（8） do：用于指定一个在每次迭代结束时检查其条件的循环。 do 循环体至少执行一次。 条件表达式后面必须有分号。

（9） break：用于提前退出 for、while 或 do 循环，或者在 switch 语句中用来结束 case 块。 break 总是退出最深层的 while、for、do 或 switch 语句。

（10）continue ：用来跳转到 for、while 或 do 循环的下一个迭代。 continue 总是跳到最深层 while、for 或 do 语句的下一个迭代。

（11）return ：会导致方法返回到调用它的方法，从而传递与返回方法的返回类型匹配的值。 如果方法具有非 void 的返回类型，return 语句必须具有相同或兼容类型的参数。 返回值两侧的括号是可选的。

（12）instanceof：用来确定对象所属的类。

 错误处理

错误处理（共5个）

| 关键字  | 意思                   | 备注，常用                                                   |      |      |      |
| ------- | ---------------------- | ------------------------------------------------------------ | ---- | ---- | ---- |
| catch   | 处理异常               | 1.try+catch 程序的流程是：运行到try块中，如果有异常抛出，则转到catch块去处理。然后执行catch块后面的语句 2.try+catch+finally 程序的流程是：运行到try块中，如果有异常抛出，则转到catch块,catch块执行完毕后，执行finally块的代码，再执行finally块后面的代码。 如果没有异常抛出，执行完try块，也要去执行finally块的代码。然后执行finally块后面的语句 3.try+finally 程序的流程是：运行到try块中,如果有异常抛出的话，程序转向执行finally块的代码。那末finally块后面的代码还会被执行吗？不会！因为你没有处理异常，所以遇到异常后，执行完finally后，方法就已抛出异常的方式退出了。 这种方式中要注意的是，由于你没有捕获异常，所以要在方法后面声明抛出异常 (来自网上的资料) |      |      |      |
| try     | 捕获异常               |                                                              |      |      |      |
| finally | 有没有异常都执行       |                                                              |      |      |      |
| throw   | 抛出一个异常对象       | 一些可以导致程序出问题的因素,比如书写错误,逻辑错误或者是api的应用错误等等. 为了防止程序的崩溃就要预先检测这些因素,所以java 使用了异常这个机制. 在java中异常是靠 "抛出" 也就是英语的"throw" 来使用的,意思是如果发现到什么异常的时候就把错误信息 "抛出" |      |      |      |
| throws  | 声明一个异常可能被抛出 | 把异常交给他的上级管理，自己不进行异常处理                   |      |      |      |

（1） catch ：用来在 try-catch 或 try-catch-finally 语句中定义异常处理块。 开始和结束标记 { 和 } 是 catch 子句语法的一部分，即使该子句只包含一个语句，也不能省略这两个标记。 每个 try 块都必须至少有一个 catch 或 finally 子句。 如果某个特定异常类未被任何 catch 子句处理，该异常将沿着调用栈递归地传播到下一个封闭 try 块。如果任何封闭 try 块都未捕获到异常，Java 解释器将退出，并显示错误消息和堆栈跟踪信息。

（2） try ：用于包含可能引发异常的语句块。 每个 try 块都必须至少有一个 catch 或 finally 子句。 如果某个特定异常类未被任何 catch 子句处理，该异常将沿着调用栈递归地传播到下一个封闭 try 块。如果任何封闭 try 块都未捕获到异常，Java 解释器将退出，并显示错误消息和堆栈跟踪信息。

（3）finally：用在异常处理的最后一个语句块，无论是否产生异常都要被执行。finally是对异常处理的最佳补充使代码总要被执行，使用finally可以维护对象的内部状态，并可以清理非内存资源。

（4） throw ：用于引发异常。 throw 语句将 java.lang.Throwable 作为参数。Throwable 在调用栈中向上传播，直到被适当的 catch 块捕获。 引发非 RuntimeException 异常的任何方法还必须在方法声明中使用 throws 修饰符来声明它引发的异常。

（5） throws ：可以应用于方法，以便指出方法引发了特定类型的异常。 throws 关键字将逗号分隔的 java.lang.Throwables 列表作为参数。 引发非 RuntimeException 异常的任何方法还必须在方法声明中使用 throws 修饰符来声明它引发的异常。 要在 try-catch 块中包含带 throws 子句的方法的调用，必须提供该方法的调用者。

  throw是你执行的动作。比如你觉得可能有异常，那么就抱出去 如：

​      String a; if(a == null),

​      throw new exception("a为null");

​      所以throw是一个抛出去的动作

  throws只用在一个方法的末端，表示这个方法体内部如果有异常，这抛给它的调用者。 如： public void add(int a, int b) throws Exception(); 这个方法表示，在执行这个方法的时候，可能产生一个异常，如果产生异常了，那么谁调用了这个方法，就抛给谁

 包相关

包的关键字（共2个）

| 关键字  | 意思           | 备注，常用                                                   |
| ------- | -------------- | ------------------------------------------------------------ |
| import  | 引入包的关键字 | 当使用某个包的一些类时，仅需类名 然后使用ctrl+shift+o或者选定类名（类或属性或方法）按住ctrl+单击 即可自动插入类所在的包。如：JFrame 快捷键之后自动加入 import javax.swing.JFrame; |
| package | 定义包的关键字 | 将所有有关的类放在一个包类以便查找修改等。如：package javake.flycat.draw002; |

\1) import：使一个包中的一个或所有类在当前 Java 源文件中可见。可以不使用完全限定的类名来引用导入的类。 当多个包包含同名的类时，许多 Java 程序员只使用特定的 import 语句（没有“*”）来避免不确定性。

\2) package：指定在 Java 源文件中声明的类所驻留的 Java 包。 package 语句（如果出现）必须是 Java 源文件中的第一个非注释性文本。 例:java.lang.Object。 如果 Java 源文件不包含 package 语句，在该文件中定义的类将位于“默认包”中。请注意，不能从非默认包中的类引用默认包中的类。

 基本类型

数据类型的关键字（共10个）

| 关键字  | 意思   | 备注，常用                                       |
| ------- | ------ | ------------------------------------------------ |
| byte    | 字节型 | 8bit                                             |
| char    | 字符型 | 16bit                                            |
| boolean | 布尔型 | --                                               |
| short   | 短整型 | 16bit                                            |
| int     | 整型   | 32bit                                            |
| float   | 浮点型 | 32bit                                            |
| long    | 长整型 | 64bit                                            |
| double  | 双精度 | 64bit                                            |
| void    | 无返回 | public void A(){} 其他需要返回的经常与return连用 |
| enum    | 枚举   |                                                  |

（1）byte： 是 Java 原始类型。byte 可存储在 [-128, 127] 范围以内的整数值。 Byte 类是 byte 原始类型的包装对象类。它定义代表此类型的值的范围的 MIN_VALUE 和 MAX_VALUE 常量。 Java 中的所有整数值都是 32 位的 int 值，除非值后面有 l 或 L（如 235L），这表示该值应解释为 long。

（2） char ：是 Java 原始类型。char 变量可以存储一个 Unicode 字符。 可以使用下列 char 常量：\b - 空格, \f - 换页, \n - 换行, \r - 回车, \t - 水平制表符, \' - 单引号, \" - 双引号, \\ - 反斜杠, \xxx - 采用 xxx 编码的 Latin-1 字符。\x 和 \xx 均为合法形式，但可能引起混淆。 \uxxxx - 采用十六进制编码 xxxx 的 Unicode 字符。 Character 类包含一些可用来处理 char 变量的 static 方法，这些方法包括 isDigit()、isLetter()、isWhitespace() 和 toUpperCase()。 char 值没有符号。

（3） boolean ：是 Java 原始类型。boolean 变量的值可以是 true 或 false。 boolean 变量只能以 true 或 false 作为值。boolean 不能与数字类型相互转换。 包含 boolean 操作数的表达式只能包含 boolean 操作数。 Boolean 类是 boolean 原始类型的包装对象类。

（4）short ：是 Java 原始类型。short 变量可以存储 16 位带符号的整数。 Short 类是 short 原始类型的包装对象类。它定义代表此类型的值的范围的 MIN_VALUE 和 MAX_VALUE 常量。 Java 中的所有整数值都是 32 位的 int 值，除非值后面有 l 或 L（如 235L），这表示该值应解释为 long。

（5）int： 是 Java 原始类型。int 变量可以存储 32 位的整数值。 Integer 类是 int 原始类型的包装对象类。它定义代表此类型的值的范围的 MIN_VALUE 和 MAX_VALUE 常量。 Java 中的所有整数值都是 32 位的 int 值，除非值后面有 l 或 L（如 235L），这表示该值应解释为 long。

（6） float ： 是 Java 原始类型。float 变量可以存储单精度浮点值。 使用此关键字时应遵循下列规则： Java 中的浮点文字始终默认为双精度。要指定单精度文字值，应在数值后加上 f 或 F，如 0.01f。 由于浮点数据类型是实际数值的近似值，因此，一般不要对浮点数值进行是否相等的比较。 Java 浮点数值可代表无穷大和 NaN（非数值）。Float 包装对象类用来定义常量 MIN_VALUE、MAX_VALUE、NEGATIVE_INFINITY、POSITIVE_INFINITY 和 NaN。

（7） long ： Java 原始类型。long 变量可以存储 64 位的带符号整数。 Long 类是 long 原始类型的包装对象类。它定义代表此类型的值的范围的 MIN_VALUE 和 MAX_VALUE 常量。 Java 中的所有整数值都是 32 位的 int 值，除非值后面有 l 或 L（如 235L），这表示该值应解释为 long。

（8）double ：是 Java 原始类型。double 变量可以存储双精度浮点值。 由于浮点数据类型是实际数值的近似值，因此，一般不要对浮点数值进行是否相等的比较。 Java 浮点数值可代表无穷大和 NaN（非数值）。Double 包装对象类用来定义常量 MIN_VALUE、MAX_VALUE、NEGATIVE_INFINITY、POSITIVE_INFINITY 和 NaN。

（9） void：表示 null 类型。 void 可以用作方法的返回类型，以指示该方法不返回值。

（10）enum：枚举类型，可以将一组具名的值的有限集合创建为一种新的类型，而这些具名的值可以作为常规的程序组件使用。

其他

包含（1个）

| 关键字 | 意思 | 备注，常用 |
| ------ | ---- | ---------- |
| assert | 断言 |            |

（1）assert：表示断言，在执行的时候默认不启动断言检查的（所有的断言语句都将忽略），如果要启动则需要用开关-enableassertions来开启，有两种方法：

1.assert：如果为true，则程序继续执行，如果为false，则程序抛出AssertionError并终止运行。

2.assert:<错误信息表达式> ：如果为true，则程序继续执行，如果为false则程序抛出java.lang.AssertionError，并输入<错误信息表达式>

保留字

保留字共包含（两个）

（1）goto ：但无任何作用。结构化程序设计完全不需要 goto 语句即可完成各种流程，而 goto 语句的使用往往会使程序的可读性降低，所以 Java 不允许 goto 跳转。

（2） const：是一个类型修饰符，使用const声明的对象不能更新。与final某些类似。

标志符

（1） null ：表示无值。 将 null 赋给非原始变量相当于释放该变量先前所引用的对象。 不能将 null 赋给原始类型（byte、short、int、long、char、float、double、boolean）变量。

（2） true ：表示 boolean 变量的两个合法值中的一个。

（3） false ：代表 boolean 变量的两个合法值之一。
