# 块与静态块

```java
package com.sdut.codeblock;

public class CodeBlockTest01 {

    public static void main(String[] args) {
        Test test1 = new Test();
        Test test2 = new Test();
        Test test3 = new Test();
    }

}
class Test{
    static {
        System.out.println(200);
    }

    {
        System.out.println(100);
    }

    public Test() {
        System.out.println(50);
    }
}
```

输出结果：

200
100
50
100
50
100
50



**静态代码块在类第一次被使用的时候调用一次，而代码块实在每次类实例化对象之前调用一次**