# Java Lambda 表达式

使用λ表达式的作用：避免匿名内部类定义过多。

lambda表达式是属于**函数式编程**。

**函数式接口：**

定义：任何接口，如果只包含唯一一个抽象方法，那么它就是一个函数式接口。

对于这种函数式接口，就可以通过lambda表达式来创建该接口的对象。



多线程语句

```java
package com.sdut.lambdatrst;

public class LambdaTest01 extends Thread{
    public static void main(String[] args) {

        new Thread(
                ()-> System.out.println("多线程语句")
        ).start();

        System.out.println("主线程语句");
    }
}

```



**为什么使用lambda表达式**

1. 避免内部类定义过多
2. 代码整洁
3. 去掉没有意义的代码，只留下核心逻辑



**老式实现接口方法**

```java
package com.sdut.lambdatrst;

public interface LambdaTest02 {
    void test();
}

```

```java
package com.sdut.lambdatrst;

public class LambdaTest03 implements LambdaTest02{
    @Override
    public void test() {
        System.out.println("Lambda");
    }

    public static void main(String[] args) {
        LambdaTest03 lambdaTest03 = new LambdaTest03();
        lambdaTest03.test();
    }
}

```

**使用lambda表达式**

演化过程

```java
package com.sdut.lambdatrst;

public class LambdaTest04 {
    //2.内部类(静态内部类)
    static class Test02 implements LambdaTest02 {

        @Override
        public void test() {
            System.out.println("静态内部类");
        }
    }

    public static void main(String[] args) {
        //3.局部内部类
        class Test03 implements LambdaTest02 {

            @Override
            public void test() {
                System.out.println("局部内部类");
            }
        }

        //4.匿名内部类

        new LambdaTest02() {
            @Override
            public void test() {
                System.out.println("匿名内部类");
            }
        };

        //5.lambda表达式
        LambdaTest02 lambdaTest02 = new Test01();
        lambdaTest02 = () ->{
            System.out.println("lambda表达式");
        };
        lambdaTest02.test();
    }

}

//1.外部类
class Test01 implements LambdaTest02 {

    @Override
    public void test() {
        System.out.println("外部类");
    }
}
```



```java
package com.sdut.lambdatrst;

public class LambdaTest05 {
    public static void main(String[] args) {
        //标准写法
        Interface01 interface01 = (int a) ->{
            System.out.println("a :" + a);
        };
        interface01.test(520);

        //简化变量
        Interface01 interface02 = (a) ->{
            System.out.println("a :" + a);
        };
        interface02.test(521);

        //单是一个参数可以省略括号
        Interface01 interface03 =  a ->{
            System.out.println("a :" + a);
        };
        interface03.test(522);

        //单是一条语句可以省略代码块括号
        Interface01 interface04 = a -> System.out.println("a :" + a);;
        interface04.test(523);
    }
}

```

**注意：**

1. 如果是多个变量，不可以省略括号，但是如果省略变量类型，那么必须都省略
2. 如果是多条语句，必须加上代码块括号。



