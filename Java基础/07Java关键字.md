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



## static

**static 静态的**

static修饰的，可以直接使用静态成员，不可以直接使用实例成员

