# Java的抽象类

用 abstract 修饰

抽象的概念：所有的对象都是通过类来描述的，但是不是所有的类都可以用来描述对象。如果一个类没有足够的信息来描述一个具体的对象，这个类就是抽象类。

主要修饰的位置：类与成员方法。

![image-20210728192559821](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210728192559821.png)

**抽象类不允许实例化对象，抽象类是用来继承的。**

抽象类的构造方法可以在子类实例化中被间接执行。

```Java
package com.sdut.demo07;

public class Demo01 {
    public static void main(String[] args) {
    }
}

abstract class Demo011{

}

class Demo012 extends Demo011{
    
}
```



## 抽象方法

```java
package com.sdut.demo07;

public abstract class Demo02 {
    //抽象方法,没有方法体的方法
    public abstract void test01();
}
```

抽象类中不一定包含抽象方法，但是有抽象方法的类一定是抽象方法。抽象类不能实例化对象，但是抽象类有构造方法。



```java
package com.sdut.abstracttest;

public abstract class Test01 {
    public abstract void test01();
}

```

```java
package com.sdut.abstracttest;

public class Test02 extends Test01 {
    @Override
    public void test01() {
        
    }
}
```

```java
package com.sdut.abstracttest;

public abstract class Test03 extends Test01{
    
}

```

```java
package com.sdut.abstracttest;

public class Test04 extends Test03 {
    @Override
    public void test01() {
        
    }
}

```

一个抽象类中如果含有一个抽象方法，那么他的普通子类必须重写这个抽象方法。抽象子类则不需要。但是，抽象子类的普通子类必须实现此方法。

### abstract 语法规则

1. 修饰类与方法
2. 使用规则
   1. 可以被继承，
   2. 继承的类不是抽象类，需要重写抽象方法
   3. 不可以实例化对象，大可以间接实例化。



# Java的接口

**面向对象的开发，面向接口的编程**

概念：接口是一系列的方法的声明，是一些方法特征的集合。

方法特征：只有方法声明，没有方法体的方法。

接口中的方法可以在不同的地方被重写，可以在不同的地方体现不同的功能。



**接口的目的：**

接口是Java解决无法多继承的方式。而在实际开发的过程中，更多的是，**制定标准和规范方法**

**跟抽象类不一样的是，接口里面只能定义常量，即必须赋一个初值。**

```java
package com.sdut.interfacetest;

//接口
public interface Test01 {
    int value = 10;   //public static final 修饰
    
    public void test01();
    
    public void test02();
}

```

```java
package com.sdut.interfacetest;

public class Test02 implements Test01 {
    @Override
    public void test01() {
        
    }

    @Override
    public void test02() {

    }
}
```

接口中主要能定义的东西：

1. 常量（即赋初值的变量）
2. 方法的特征



**接口当中不可以存在构造方法，普通方法，代码块，静态代码块**

JDK1.8之后，接口中是可以出现静态方法的。也可以出现默认方法（default）

```java
package com.sdut.interfacetest;

public interface Test03 {
    static void test01(){
        
    }
    
    default void test02(){
        
    }
}
```



**子类必须实现接口中的抽象类，除非子类是抽象类**



# 抽象类与接口的区别

1. 抽象类中可以有构造方法，接口中不可以有，但是抽象类的构造方法不可以实例化对象，即抽象类和接口都不可以实例化对象
2. 方法体：抽象类中可以有，接口中可以有（1.8之后的jdk版本接口可以存在静态方法和默认方法）
3. 代码块与静态代码块：抽象类可以有，接口不能有
4. 变量：接口中必须赋初值，成为常量，抽象类没有要求。



类/接口/继承/实现

继承：类+类，单继承

实现：类+接口，多实现

继承：接口 + 接口，多继承



**先继承，后实现**
