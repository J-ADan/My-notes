# 数组

## 数组的基本的定义

数组的定义：**数组是最为常见的一种数据结构，同时也是将一些相同类型的数据按照线性顺序连续存储的序列**

数组同时也是效率最高的存储和访问元素的方式（利用下标来访问数组内的元素）。

**数组在初始化之后长度固定不变，数组内部元素遵循定义的数组类型**

```java
package com.sdut.Demo06;

public class Demo01 {
	public static void main(String[] args) {

		/*数组的定义：
		 * 元素类型 [] 数组名;
		 * 元素类型 数组名 [];
		 * 
		 * 数组的初始化：
		 * 元素类型 [] 数组名 = new 元素类型 [数组长度];
		 * 元素类型 数组名 [] = new 元素类型 [数组长度];
		 */

		int arr0[];// 这种定义方法更符合使用习惯
		int[] arr00;// 这种的定义方法更符合原理

		int[] arr = new int[10];
		int arr01[] = new int[10];

		char arr02[] = new char[10];

		String arr03[] = new String[10];
		/*
		 * 基本数据类型和引用数据类型都可以作为数组的元素类型
		 */
	}
}


```

数组元素的初始值的定义

```java
package com.sdut.Demo06;

public class Demo02 {
	public static void main(String[] args) {

		/*
		 * 数组元素的初始化定义
		 */

		int arr01[] = new int[] { 1, 2, 3, 4, 5 };

		int arr02[] = new int[5];

		int arr03[] = { 1, 2, 3, 4, 5 };
		
		String str [] = new String [] {};
		
		
	}
}

```



## 数组的默认值

```java
package com.sdut.Demo06;

public class Demo03 {
	public static void main(String[] args) {
		
		int arr01 [] = null;
		int arr02 [] = new int [5];
		int arr03 [] = new int [] {};
		
		String [] arr04 = null;
		String arr05 [] = new String [] {};
		
		Integer arr06 [] = null;
		Integer arr07 [] = new Integer[] {};
		
		System.out.println(arr01);
		System.out.println(arr02);
		System.out.println(arr03);
		System.out.println(arr04);
		System.out.println(arr05);
		System.out.println(arr06);
		System.out.println(arr07);
	}
}

```

输出结果

null
[I@15db9742
[I@6d06d69c
null
[Ljava.lang.String;@7852e922
null
[Ljava.lang.Integer;@4e25154f

数组在没有进行内存空间的分配时，他是null空的，但是当数组进行new即空间分配后，他里面存的是一个地址。



## 数组的基本操作以及方法

数组元素的获取，长度的获取，以及遍历数组

```java
package com.sdut.Demo06;

public class Demo04 {
	public static void main(String[] args) {
		/*
		 * 数组元素的获取
		 * 数组长度的获取
		 * 数组内部元素的遍历(利用数组长度获取，利用加强for循环获取)
		 */

		int arr[] = new int[] { 1, 2, 3, 4, 5 };

		// 获取某个数组元素
		System.out.println(arr[3]);// 因为数组下标是从0开始，所以这是获取第四个元素
		// 数组的下标是从0开始，最大的下标为数组长度length - 1

		// 获取数组的长度，利用数组的方法，length方法，这个方法以后还会出现在其他的组成数据中
		System.out.println(arr.length);

		// 遍历数组
		// 1.利用数组长度遍历
		for (int i = 0; i < arr.length; i++) {
			System.out.println(arr[i]);
		}

		// 2.利用加强for循环
		for (int k : arr) {
			System.out.println(k);
		}

	}
}

```

数组的倒置

```java
package com.sdut.Demo04;

import java.util.Scanner;

public class Demo01 {

	static Scanner scanner = new Scanner(System.in);

	public static void main(String[] args) {
		int arr[] = new int[5];
		arr = enter();
		invert(arr);
	}

	public static int[] enter() {
		int arr[] = new int[5];

		for (int i = 0; i < arr.length; i++) {
			arr[i] = Integer.parseInt(scanner.nextLine());
		}
		return arr;
	}

	public static void invert(int arr[]) {
		for (int i = 0, j = arr.length - 1; i < j; i++, j--) {
				int taget = arr[i];
				arr[i] = arr[j];
				arr[j] = taget;
		}
		
		for (int i : arr) {
			System.out.print(i + " ");
		}
	}
}

```

next（）与nextLIne（）的区别

next()方法在读取内容时，会过滤掉有效字符前面的无效字符，对输入有效字符之前遇到的空格键、Tab键或Enter键等结束符，next()方法会自动将其过滤掉；只有在读取到有效字符之后，next()方法才将其后的空格键、Tab键或Enter键等视为结束符；所以next()方法不能得到带空格的字符串。
nextLine()方法字面上有扫描一整行的意思，它的结束符只能是Enter键，即nextLine()方法返回的是Enter键之前没有被读取的所有字符，它是可以得到带空格的字符串的。

```java
package com.sdut.Demo04;

public class Demo02 {
	public static void main(String[] args) {

		int a1[] = new int[] { 1, 2, 3, 4 };
		int a2[] = new int[] { 1, 2, 3, 4 };
		int a3[] = a1;
		
		for (int i = 0; i < a1.length; i ++) {
			a3[i]++;
			System.out.println(a1[i] + " " + a2[i] + " " + a3[i]);
		}
	}
}

```

输出

2 1 2
3 2 3
4 3 4
5 4 5

因为数组为引用类型，所以a3存放的是一个引用地址，所以改变a3，a1也会随之发生改变。

# 引用传递，值传递

```java
package com.sdut.Demo04;

public class Demo03 {
	public static void main(String[] args) {
		
		int arr[] = new int[] {1,2,3,4};
		int k = 2;
		
		for (int i : arr) {
			System.out.print(i + " ");
		}
		System.out.println();
		System.out.println(k);
		
		f(arr,k);//引用传递，值传递。
		
		for (int i : arr) {
			System.out.print(i + " ");
		}
		System.out.println();
		System.out.println(k);
		
	}
	
	public static void f(int arr[],int k) {
		for (int i = 0; i < arr.length; i ++) {
			arr[i]++;
		}
		k += 5;
	}
}

```

输出

1 2 3 4 
2
2 3 4 5 
2



# 二维数组

数组可以分为一维数组，二维数组，多维数组。

二维数组其实就是excel的表结构，一种行列式结构，二维数组第一个数字代表行，第二个数字代表列。

在Java中，二维数组可以被看作是一个特殊的数组，即一个一维数组，数组的元素又是数组。

```java
package com.sdut.Demo04;

public class Demo04 {
	public static void main(String[] args) {

		// 二维数组的定义
		int[][] arr01;
		int arr02[][];

		// 二维数组的初始化
		int[][] arr03 = new int[2][3];
		int[][] arr04 = new int[][] { { 1, 2, 3 }, { 1, 2, 3 } };
		int[][] arr05 = { { 1, 2, 3 }, { 1, 2, 3 } };

		// 特殊情况的二维数组初始化
		int[][] arr06 = new int[2][];// 不指定每个元素的长度，可以在后面进行赋值
		int[] a1 = arr05[0];// 一个二维数组的元素是一个一维数组
		int[][] arr07 = new int[][] {};// 定义一个空的二维数组，长度为0;

		arr06[0] = new int[] { 1, 2, 3, 4, 5, 6 };
		
		

	}
}

```

二维数组的遍历，利用循环的嵌套。

```java
package com.sdut.Demo04;

public class Demo05 {
	public static void main(String[] args) {

		int[][] arr = new int[][] { { 1, 2, 3 }, { 1, 2, 3 } };

		for (int i = 0; i < arr.length; i++) {//简单的for循环嵌套遍历数组元素
			for (int j = 0; j < arr[i].length; j++) {
					System.out.print(arr[i][j] + " ");
			}
		}
		System.out.println();
		for (int a[] : arr) {//for循环加强型遍历数组元素
			for (int i : a) {
				System.out.print(i + " ");
			}
		}
		
	}
}

```

