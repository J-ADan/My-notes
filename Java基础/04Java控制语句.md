# 控制语句

## 流程控制语句

### 顺序语句

```java
package com.sdut.Demo04;

public class Demo02 {
	public static void main(String[] args) {
		/*
		 * 顺序执行结构，即按照从上到下，从左到右的默认顺序执行语句
		 */
		
		int a = 2, b = 3;
		System.out.println(a + " " + b);
		
		int c = 4;
		System.out.println(c);
	}
}

```

输出结果：

2 3
4

### 选择语句

#### if……else结构

```java
package com.sdut.Demo04;

public class Demo03 {
	public static void main(String[] args) {
		
		/*
		 * 选择结构，即需要进行某些判断语句的判定来决定某些语句是否执行
		 * 结构1：if结构
		 * if (boolean){
		 *		执行语句
		 * }
		 * 
		 * 结构2：if……else结构
		 * if (boolean){
		 * 		执行语句
		 * }else{
		 * 		执行语句
		 * }
		 * 
		 * 结构3：if……else if……else结构，这里的else if是可以多个的
		 * if (boolean){
		 * 		执行语句
		 * }else if (boolean){
		 * 		执行语句
		 * }else{
		 * 		执行语句
		 * }
		 */
		//实例：
		
		int a = 2, b = 3;
		
		if (a < b) {
			System.out.println(a);
		}
		
		if (a > b) {
			System.out.println(a);
		}else {
			System.out.println(b);
		}
		
		if (a > b) {
			System.out.println(a);
		}else if (a == b) {
			System.err.println(a);
		}else {
			System.out.println(b);
		}
	}
}

```

**二分查找**

```java
package com.sdut.Demo05;

public class BinarySearch {
	public static void main(String[] args) {

		// 二分查找的数组一定是一个递增的数组，可以不连续，但是一定是递增的
		// 如果是无序的数组可以用其他的排序方式来进行数组的排序
		int arr[] = new int[] { 2, 6, 9, 12, 19, 26, 33, 59, 76 };

		int taget = 26;// 设置要查找的数值，可以手动输入

		int index = binarySearch(arr, taget, 0, arr.length);

		if (index == -1) {
			System.out.println("无此数字");
		} else {
			System.out.println("该数字所在位置为：" + index + 1);
		}

	}

	public static int binarySearch(int arr[], int taget, int start, int end) {
		if (end == start) {
			return -1;
		}

		int middle = (start + end) / 2;

		if (arr[middle] == taget) {
			return middle;
		} else if (arr[middle] < taget) {
			return binarySearch(arr, taget, middle, end);
		} else {
			return binarySearch(arr, taget, 0, middle);
		}
	}
}


```



**虽然if……else结构可以改变执行的顺序，但是从整体来看，还是按照默认顺序执行。当然if……else内部也是默认按照顺序结构执行。**

#### switch……case结构

```java
package com.sdut.Demo04;

public class Demo04 {
	public static void main(String[] args) {
		/*switch case选择结构
		 * 
		 * switch(key){
		 * case value:
		 * 		break;
		 * 
		 * default:
		 * 		break;
		 * }
		 * 
		 * 当key与value相等，则会执行当前case后的语句
		 * 可以有多个case
		 * 当没有向匹配的value时，则会执行default下面的语句。
		 */
		
		int a = 2;
		
		switch (a) {
		case 1:
			
			System.out.println("1111");;

		default:
			System.err.println("错误");;
		}
	}
}

```



输出结果：

错误

**switch……case执行顺序：从switch后面进入整个switch语句，然后逐句判断执行，知道最后一句或者default。当case某一语句有break时，直接在当前语句跳出switch，不去执行下面的语句**

### 循环语句

#### while循环（MySQL，Java JDBC中也是常用）



```java
package com.sdut.Demo05;

public class Demo02 {
	public static void main(String[] args) {
		/*
		 * while 循环
		 * 结构
		 * while (boolean){
		 * 		语句。
		 * }
		 * 
		 * 当while后面的boolean表达式为真时执行内部语句。
		 * 执行语句结束后，会再回去判断条件，为真则继续执行，知道为假。
		 * while循环，至少执行0次。
		 * 
		 */
		
		int i = 0;
		
		while (i < 5) {
			System.out.println(i);
			i++;
		}
		
		
		//死循环情况
		while (true) {
			System.out.println(1);
		}
		
	}
}

```

while 循环是可以不执行的，即可以执行零次，当他第一次条件就不符合时。**当然while循环时最常用的循环**

**最常用的while形式**

```java
package com.sdut.Demo05;

import java.util.Scanner;

public class Demo03 {
	public static void main(String[] args) {

		Scanner scanner = new Scanner(System.in);

		/*
		 * while (true)
		 * 利用控制台输入，来控制循环的次数
		 */

		while (true) {
			System.out.println("输入0结束输入");
			int x = scanner.nextInt();
			if (x == 0) {
				break;
			} else {
				System.out.println(x);
			}
		}
	}
}

```

```java
package com.sdut.Demo05;

import java.util.Scanner;

public class Demo04 {
	public static void main(String[] args) {
		
		Scanner scanner = new Scanner(System.in);
		
		/*
		 * while (.hasNext())
		 * 接收控制台输入，无输入不接收
		 */
		
		while (scanner.hasNext()) {
			int x = scanner.nextInt();
			System.out.println(x);
		}
	}
}

```

这就是两种很常用的while循环代码形式。

**第二种经常会在JDBC，接收ResultSet 集合返回值时使用，不过不是这种类型，是一种ResultSet.next()形式。**

#### do……while循环

```java
package com.sdut.Demo05;

public class Demo06 {
	public static void main(String[] args) {
		/*
		 * do……while ()循环 结构
		 *  do{
		 *   	语句. 
		 *   }while (boolean);
		 * 
		 * 在do……while循环中，因为条件是在循环语句后面，所以语句至少执行一遍
		 */

		int x = 5;

		do {
			System.out.println("循环语句");
			x++;
		} while (x < 5);

	}
}

```

输出结果：

循环语句

#### for循环（一个重要的循环，不仅仅是在Java基础）

```java
package com.sdut.Demo05;

public class Demo07 {
	public static void main(String[] args) {
		
		/*for 循环
		 * 结构：
		 * for (循环控制变量;循环界限;结束条件){
		 * 		循环语句。
		 * }
		 */
		
		for (int i = 0; i < 4; i ++) {
			System.out.println(i);
		}
		
	}
}

```

**循环最最经常用来遍历数组，排序，查找**	所以会有循环的嵌套，还一个for循环的增强型。\

**for循环的增强型**（用来遍历数组等类型）

```java
package com.sdut.Demo05;

public class Demo08 {
	public static void main(String[] args) {
		
		/*
		 * for循环增强型
		 * 结构：
		 * for (对应类型变量 : 数组等变量){
		 * 		循环语句
		 * }
		 * 当遍历完数组内部的元素即停止
		 */
		
		int [] arr = new int [] {1,2,3,4,5};
		
		for (int i : arr) {
			System.out.println(i);
		}
		
	}
}

```

#### 循环的嵌套

经常会用的嵌套对象一般会是	while循环	for循环

**冒泡排序**

```java
package com.sdut.Demo05;

public class BubbleSort {
	public static void main(String[] args) {

		int arr[] = new int[] { 15, 2, 14, 3, 8, 9 };
        
		//循环的嵌套
		for (int i = 0; i < arr.length - 1; i++) {
			for (int j = 0; j < arr.length - 1 - i; j++) {
					if (arr[j] > arr[j+1]) {//前后互换元素.
						int taget = arr[j+1];
						arr[j+1] = arr[j];
						arr[j] = taget;
					}
			}
		}

		for (int i : arr) {
			System.out.println(i);
		}
		
	}
}

```

# 递推和递归

**典型案例**：斐波那契序列



```java
package com.sdut.Demo05;

public class Fibonacci {
	public static void main(String[] args) {

		/*
		 * 斐波那契数列：已知f(1) = 1 , f(2) = 1 , 且满足关系式f(n) = f(n-1) + f(n-2)，则f(50)等于多少？
		 */

		// 递推代码实现

		long a[] = new long[51];// 递推50次后，数字会非常大，所以用long类型
		a[1] = 1;
		a[2] = 1;
		for (int i = 3; i <= 50; i++) {
			a[i] = a[i - 1] + a[i - 2];
		}

		System.out.println(a[50]);

		// 递归代码实现
		for (int i = 1; i < 51; i++) {
			if (i == 50) {
				System.out.println(Fibonacci(i));
			}
		}


	}

	private static long Fibonacci(int n) {
		// TODO Auto-generated method stub
		if (n == 1 || n == 2) {
			return 1;
		} else {
			return Fibonacci(n - 1) + Fibonacci(n - 2);
		}
	}
}

```

# 命令行传参

