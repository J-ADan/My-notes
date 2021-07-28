# Java--面向对象（Object-oriented、OO）

## 面向对象与面向过程

一个经典的问题，
把大象装进冰箱分几步。
对于面向过程思想来说。
三步走，

打开冰箱
装进去
关上冰箱
但是对于面向对象思想
在问题中涉及到两个对象
**大象 冰箱** 贯穿问题是始终的对象为 **冰箱**
所以冰箱的行为为

冰箱->开门
冰箱->装东西
冰箱->关门
然后确定了对象的行为我们把对象的行为组织好，就完成了整个问题。

以上不难看出，其实面向对象思想中包括面向过程思想。只是面向对象站在一个更高的层次来看待问题的解决的办法。

## OOA OOD OOP的概念以及区别

### OOA（Object-Oriented Analysis、面向对象分析方法）

OOA是在一个系统的开发过程中进行了系统业务调查以后，按照面向对象的思想来分析问题。OOA与结构化分析有较大的区别。OOA所强调的是在系统调查资料的基础上，针对OO方法所需要的素材进行的归类分析和整理，而不是对管理业务现状和方法的分析。

OOA（面向对象的分析）模型由5个层次（主题层、对象类层、结构层、属性层和服务层）和5个活动（标识对象类、标识结构、定义主题、定义属性和定义服务）组成。在这种方法中定义了两种对象类之间的结构，一种称为分类结构，一种称为组装结构。分类结构就是所谓的一般与特殊的关系。组装结构则反映了对象之间的整体与部分的关系。

OOA在定义属性的同时，要识别实例连接。实例连接是一个实例与另一个实例的映射关系。

OOA在定义服务的同时要识别消息连接。当一个对象需要向另一对象发送消息时，它们之间就存在消息连接。

OOA 中的5个层次和5个活动继续贯穿在OOD（画向对象的设计）过程中。OOD模型由4个部分组成。它们分别是设计问题域部分、设计人机交互部分、设计任务管理部分和设计数据管理部分。

### OOD（Object-Oriented Design、面向对象设计）

OOD方法是OO方法中一个中间过渡环节。其主要作用是对OOA分析的结果作进一步的规范化整理，以便能够被OOP直接接受。

面向对象设计（OOD）是一种软件设计方法，是一种工程化规范。这是毫无疑问的。按照Bjarne Stroustrup的说法，面向对象的编程范式（paradigm）是：

　　1. 决定你要的类；

　　2. 给每个类提供完整的一组操作；

　　3. 明确地使用继承来表现共同点。

由这个定义，我们可以看出：OOD就是“根据需求决定所需的类、类的操作以及类之间关联的过程”。

OOD的目标是管理程序内部各部分的相互依赖。为了达到这个目标，OOD要求将程序分成块，每个块的规模应该小到可以管理的程度，然后分别将各个块隐藏在接口（interface）的后面，让它们只通过接口相互交流。比如说，如果用OOD的方法来设计一个服务器-客户端（client-server）应用，那么服务器和客户端之间不应该有直接的依赖，而是应该让服务器的接口和客户端的接口相互依赖。

这种依赖关系的转换使得系统的各部分具有了可复用性。还是拿上面那个例子来说，客户端就不必依赖于特定的服务器，所以就可以复用到其他的环境下。如果要复用某一个程序块，只要实现必须的接口就行了。

OOD是一种解决软件问题的设计范式（paradigm），一种抽象的范式。使用OOD这种设计范式，我们可以用对象（object）来表现问题领域（problem domain）的实体，每个对象都有相应的状态和行为。我们刚才说到：OOD是一种抽象的范式。抽象可以分成很多层次，从非常概括的到非常特殊的都有，而对象可能处于任何一个抽象层次上。另外，彼此不同但又互有关联的对象可以共同构成抽象：只要这些对象之间有相似性，就可以把它们当成同一类的对象来处理。

### OOP（Object Oriented Programming、面向对象编程）

OOP是一种计算机编程架构。OOP 的一条基本原则是计算机程序是由单个能够起到子程序作用的单元或对象组合而成。OOP 达到了软件工程的三个主要目标：重用性、灵活性和扩展性。为了实现整体运算，每个对象都能够接收信息、处理数据和向其它对象发送信息。OOP 主要有以下的概念和组件：

　　组件 － 数据和功能一起在运行着的计算机程序中形成的单元，组件在 OOP 计算机程序中是模块和结构化的基础。

　　抽象性 － 程序有能力忽略正在处理中信息的某些方面，即对信息主要方面关注的能力。

　　封装 － 也叫做信息封装：确保组件不会以不可预期的方式改变其它组件的内部状态；只有在那些提供了内部状态改变方法的组件中，才可以访问其内部状态。每类组件都提供了一个与其它组件联系的接口，并规定了其它组件进行调用的方法。

　　多态性 － 组件的引用和类集会涉及到其它许多不同类型的组件，而且引用组件所产生的结果得依据实际调用的类型。

　　继承性 － 允许在现存的组件基础上创建子类组件，这统一并增强了多态性和封装性。典型地来说就是用类来对组件进行分组，而且还可以定义新类为现存的类的扩展，这样就可以将类组织成树形或网状结构，这体现了动作的通用性。

由于抽象性、封装性、重用性以及便于使用等方面的原因，以组件为基础的编程在脚本语言中已经变得特别流行。Python 和 Ruby 是最近才出现的语言，在开发时完全采用了 OOP 的思想，而流行的 Perl 脚本语言从版本5开始也慢慢地加入了新的面向对象的功能组件。用组件代替“现实”上的实体成为 JavaScript（ECMAScript） 得以流行的原因，有论证表明对组件进行适当的组合就可以在英特网上代替 HTML 和 XML 的文档对象模型（DOM）。

**OOA的结果可以作为OOD的模型，OOD的结果可以作为OOP的蓝图，OOP依据OOD提供的蓝图实现一个系统。**

[具体赘述](https://www.cnblogs.com/kdcaptain/archive/2012/05/24/2516198.html)

## 面向对象的三大特性

1. 封装
2. 继承
3. 多态

### 对象与类

**对象**，我们所说的对象是一种现实中具体存在的事物。
在代码中，对象就是在程序具体运行过程中的一块“内存”。

**类**，类是对现实中一类事物的抽象的描述，类是一种概念。
类主要存在两个点：一个是事物的共同的特征（状态），二是事物的共同的行为。**（状态与行为，属性与方法）**



**在Java中，类就是一段代码，它也是一种数据类型。**

**类是对象的抽象描述，对象是类的一种具体化，实例化。**



**构造方法**
每一个类中都会有一个与其名字一样的方法，（可以写出，也可以不写，也可以重写），他的作用是用来创建类的对象。

1. 类的构造方法是不能有返回值
2. 类的构造方法必须与类名一致
3. 如果没有定义构造方法，编译器会自动定义一个无参的构造方法。如果定义了构造方法，编译器将不会创建。
4. 构造方法可以重载
    当然有方法的重载，就应当有变量或者说是属性名字一致的情况
  1. 在构造方法中，this代表的是当前创建变量的属性。
  2. 在普通方法中，代表的是当前调用方法属性。



**实例化：**

```java
package com.sdut.demo;

public class Student {
	
	public static void main(String[] args) {
		Student student = new Student();
		//类->对象 ---即为实例化
	}
}

```





### 封装

1. 广义封装
    编写一个类的过程就是一个封装的过程
    封装要遵循**高内聚低耦合**
    高内聚：功能高度集中，一个类不应该有过多的功能。
    低耦合：各功能之间的联系越少越好

2. 狭义封装
    在Java中，类中的内部信息尽量隐藏起来。
    就是将类中的属性全部使用private修饰，让他变成私有的属性变量

  通过构造公有属性方法，即get，set方法

  构造方法--与类名重名的方法--方法的重载

  直接操作属性的方法

**封装的过程，就是对数据封装的过程，即对属性的封装，对数据的保护。即私有化属性变量，公有化属性方法**

属性的首字母必须小写，除id外，属性变量的长度不得小于三个字符。

```java
package com.sdut.demo;

public class Student {//实体类

	private String name;
	private int age;
	private String sex;

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

	public String getSex() {
		return sex;
	}

	public void setSex(String sex) {
		this.sex = sex;
	}

}

```

**通过get、set方法来获取、设置属性的值，这样可以避免别的类直接操作当前类的属性变量，即为保护数据**

封装的意义：（代码的复用）

1. 隐藏类中的实现细节
2. 只能通过已定义的方法来访问操作数据，方便加入控制，限制对属性的不合理操作
3. 便于维护修改，增加代码的可维护性

**简单的一个小练习：**

```java
//实体类
package com.sdut.demo01;

public class StudentModel {

	private int id;
	private String name;
	private String sex;
	private int age;
	private String major;

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

	public String getSex() {
		return sex;
	}

	public void setSex(String sex) {
		if (sex.equals("男") || sex.equals("女")) {
			this.sex = sex;
		}
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		if(age > 0) {
			this.age = age;
		}
	}

	public String getMajor() {
		return major;
	}

	public void setMajor(String major) {
		this.major = major;
	}

}

```

```java
//实现类
package com.sdut.demo01;

import java.util.ArrayList;
import java.util.Scanner;

import org.junit.Test;

public class Function {
	Scanner sc = new Scanner(System.in);
	ArrayList<StudentModel> arrl = new ArrayList<>();

	public void allFunction() {
		while(true) {
			System.out.println("------系统选项------");
			System.out.println("-----01录入信息-----");
			System.out.println("----02查询所有信息---");
			System.out.println("----03按照姓名查询---");
			System.out.println("-----04添加专业-----");
			System.out.println("---05按照专业查询---");
			System.out.println("-----输入e退出此次操作-----");
			String in = sc.nextLine();
			if (in.equals("e")) {
				return;
			}

			switch (in) {
			case "01":
				inputs();
				break;
			case "02":
				checkAll();
				break;
			case "03":
				nameCheck();
				break;
			case "04":
				addMajor();
				break;
			case "05":
				majorCheck();
				break;
			default:
				break;
			}
		}
	}

	@Test
	public void inputs() {
		while (true) {
			input();
			System.out.println("是否继续输入：(y/n)");
			if (sc.nextLine().equals("n")) {
				break;
			}
		}
	}

	@Test
	public void input() {
		StudentModel stu = new StudentModel();
		System.out.println("输入学号，例如：001");
		stu.setId(Integer.parseInt(sc.nextLine()));
		System.out.println("输入姓名，");
		stu.setName(sc.nextLine());
		System.out.println("输入性别，");
		stu.setSex(sc.nextLine());
		System.out.println("输入年龄，");
		stu.setAge(Integer.parseInt(sc.nextLine()));
		arrl.add(stu);
	}

	public void checkAll() {
		for (StudentModel s : arrl) {
			System.out.println("学号" + s.getId());
			System.out.println("姓名" + s.getName());
			System.out.println("性别" + s.getSex());
			System.out.println("年龄" + s.getAge());
			System.out.println("专业" + s.getMajor());
		}
	}

	public void majorCheck() {
		System.out.println("输入要查询的专业");
		String m = sc.nextLine();
		for (StudentModel s : arrl) {
			if (s.getMajor().equals(m)) {
				System.out.println("学号" + s.getId());
				System.out.println("姓名" + s.getName());
				System.out.println("性别" + s.getSex());
				System.out.println("年龄" + s.getAge());
			}
		}
	}

	public void nameCheck() {
		System.out.println("输入要查询的姓名");
		String m = sc.nextLine();
		for (StudentModel s : arrl) {
			if (s.getName().equals(m)) {
				System.out.println("学号" + s.getId());
				System.out.println("性别" + s.getSex());
				System.out.println("年龄" + s.getAge());
				System.out.println("专业" + s.getMajor());
			}
		}
	}

	public void addMajor() {
		for (StudentModel s : arrl) {
			if(s.getMajor() != null) {
				continue;
			}
			System.out.println("姓名" + s.getName());
			System.out.println("请输入专业：");
			s.setMajor(sc.nextLine());
		}
	}
}

```

```java
//控制类
package com.sdut.demo01;

import java.util.Scanner;

public class Control {
	static Scanner sc = new Scanner(System.in);
	public static void main(String[] args) {
		Function fuc = new Function();
		while (true) {
			fuc.allFunction();
			System.out.println("输入e结束系统");
			if ("e".equals(sc.nextLine())) {
				return; 
			}
		}
	}
}

```



### 继承

子类继承父类的特征和行为，使得子类的对象具有父类对象的特征和行为，使得子类具有父类的实例域和方法，或子类从父类继承的方法，使得子类具有父类相同的行为。

继承是Java面向对象编程的一块基石，因为他允许创建分等级层次的对象。

继承需要符合的关系：is-a，父类更通用，子类更具体。

在这种继承的关系下，
1. 字类会继承父类所有的属性和方法（非 private 私有的属性和方法）。
2. 字类还可以扩展自己的属性跟方法。
3. 子类可以重写父类的方法，即用自己的方式实现父类的方法。
4. 子类可以定义与父类一致的属性，但是不是同一个。
5. 一个类只能有一个直接的父类，（单继承）。
6. 继承是可以传递的（即字类可以继承父类继承的属性与方法）
7. 构造方法是不会被继承的（构造性）（构造方法不算是一个方法，所以它不会被继承），虽然他不会被继承但是在字类创建对象时，会先调用父类的构造方法，然后再调用子类的构造方法。
8. 提高了类之间的耦合性。

子类包含可以使用父类种可以访问的东西。

父类：基类，超类，上级类

子类：派生类



**简单的继承：**

```java
package com.sdut.demo05;

public class Demo01 {

    public int a = 0;
    public String b = "aaa";

    public static void test01(){
        System.out.println("继承");
    }

}

```

```java
package com.sdut.demo05;

public class Demo02 extends Demo01{
    public static void main(String[] args) {
        test01();
    }
}

```

**Java支持单继承，不支持多继承，但是支持多重继承。**（一个儿子只能有一个爹，一个爹但是有多个儿子）



#### Object

`Object 默认是所有类的超类（基类）`

当一个类没有父类时，会默认直接继承Object。

![image-20210726201141813](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210726201141813.png)

![image-20210726201335438](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210726201335438.png)

可以继承直接父类的方法以及属性，也可以继承间接父类的属性和方法。



**Overload 和 Override 的区别**

**answer：**

1. Overload 与 Override 都是Java多态的一种表现形式。
2. Overload 意为重载，是一个类中的多态的一种表现，即方法的名称相同，但是参数列表的不同，或者参数列表的顺序不同。
3. Override 意为重写（覆盖），是父类与子类多态的一种形式，即方法名称相同，参数列表相同，返回类型相同，但是在子类对象是使用这个方法时，会调用子类重写的方法。



**”==“ 与 equals 方法究竟有什么区别？**

**answer：**

1. ”==“ 是Java提供的等于的比较运算符，他在比较基本数据类型的时候，尽管数据类型不同，但是值相等，即返回 true ,在比较引用数据类型，并且两个引用变量类型相同或者具有父子关系时才能比较，判断的时地址是否相同。equals 是 Object 类中的方法，它返回的实际上就是 ”==“ 判断的结果，但是他比较的是地址，而且要尤为关注 equals 的重写问题

**例：**

```java
package com.sdut.demo;

public class Demo01 {
	public static void main(String[] args) {
		// -128 ~ +127 之间
		Integer a = 5;
		int b = 5;
		Integer c = new Integer(5);
		Integer d = 5;
		
		System.out.println("-128 ~ +127 之间");
		System.out.println(a.equals(b));
		System.out.println(a == b);
		System.out.println(a.equals(c));
		System.out.println(a == c);
		System.out.println(a == d);

		// -128 ~ +127 之外
		a = 128;
		b = 128;
		c = new Integer(128);
		d = 128;
		System.out.println("-128 ~ +127 之外");
		System.out.println(a.equals(b));
		System.out.println(a == b);
		System.out.println(a.equals(c));
		System.out.println(a == c);
		System.out.println(a == d);
	}

}

```

输出结果：

-128 ~ +127 之间
true
true
true
false
true
-128 ~ +127 之外
true
true
true
false
false



**重点关注 Integer 常量池之外的 ”==“ 与 equals 的差别，两个不一样的结果，因为 Integer 类会重写 equals 方法，使其判断的不再是地址，而是判断里面的值，不仅仅是 Integer，String 也会重写 equals 方法，也是使其判断里面的值是够相同**

1. `【强制】所有的相同类型的包装类对象之间值的比较，全部使用 equals 方法比较。`
2. `说明：对于 Integer var = ? 在-128 至 127 范围内的赋值，Integer 对象是在`
3. `IntegerCache.cache 产生，会复用已有对象，这个区间内的 Integer 值可以直接使用==进行`
4. `判断，但是这个区间之外的所有数据，都会在堆上产生，并不会复用已有对象，这是一个大坑，`
5. `推荐使用 equals 方法进行判断。`



**hashCode**

**哈希值** 本地方法



### 多态

**方法重写规则：**

1. 参数列表必须完全与被重写的方法相同
2. 返回类型必须完全与被重写方法相同
3. 访问权限不能比父类中被重写的方法访问权限更低，例如父类中的访问权限为 public 子类中不能用 protected
4. 父类的成员方法只能被他的子类重写。
5. 声明为 final 的方法不能被重写
6. 声明为 static 的方法不能被重写，但是能被再次声明
7. 子类和父类在同一个包内，那么子类可以重写父类中的所有的方法，除了 private 和 final 修饰的方法。
8. 子类和父类不在同一个包内，子类只能重写父类声明为 public protected 的非 final 方法。
9. 构造方法不能被重写
10. 如果不能继承一个方法，则不能重写这个方法。
11. 重写方法可以抛出任何非强制性的异常，无论重写的方法是否抛出异常，但是，重写的方法不能抛出新的强制性异常，或者，比被重写方法声明更广泛的异常，反之则可以。

**向上转型**

当产生对象向上转型时，调用规则，为调用变量类型所在类的成员，但是，若调用的时重写的方法，则调用的是子类中重写的方法。

**自动向上转型：**

子类对象赋值给父类对象。

**强制向下转型：**

不同于强制类型转换，只能由上级转为下级。



**instanceof：**

判断某个实例对象是不是某个类的实例。

