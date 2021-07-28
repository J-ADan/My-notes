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

```java
package com.sdut;

import java.util.Arrays;

public class Test03 {
    public static void main(String[] args) {
        int[] arr01 = new int[10];
        
        //向一个数组填入某个值，所有的位置
        Arrays.fill(arr01, 2);
        printTest(arr01);

        //向一个数组的特定的区间填入特定的值，前闭后开
        int[] arr02 = new int[10];
        Arrays.fill(arr02, 0, 3, 2);
        printTest(arr02);
    
        //查找某个元素在数组的位置，返回下标值
        int[] arr03 = new int[]{1, 2, 3, 4, 5};
        int b = Arrays.binarySearch(arr03, 2);
        System.out.println(b);

        //对某个数组进行排序，系统自带的是快排
        int[] arr04 = new int[]{2, 8, 4, 3, 12, 6};
        Arrays.sort(arr04);
        printTest(arr04);
    }

    public static void printTest(int arr[]) {
        for (int k : arr) {
            System.out.print(k + " ");
        }
        System.out.println();
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



1. 随机生成十个数
2. 输出最大值
3. 数组倒置输出
4. 寻找某个特定的值

```java
package com.sdut;

import java.util.Random;
import java.util.Scanner;

public class Test {
    static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        int[] arr = new int[10];
        randomEnter(arr);

        int max = maxNumber(arr);
        System.out.println("最大值为：" + max);
        invert(arr);

        System.out.println("输入想要查找的数字");
        int key = Integer.parseInt(sc.nextLine());
        Boolean b = searchNumber(arr, key);

        if (b == true) {
            System.out.println("存在");
        } else {
            System.out.println("不存在");
        }
    }

    public static void randomEnter(int arr[]) {
        Random ra = new Random();
        for (int i = 0; i < arr.length; i++) {
            arr[i] = ra.nextInt(10);
        }
    }

    public static int maxNumber(int arr[]) {
        int max = Integer.MIN_VALUE;

        for (int k : arr) {
            if (k > max) {
                max = k;
            }
        }
        return max;
    }

    public static void invert(int arr[]) {
        for (int k : arr) {
            System.out.print(k + " ");
        }
        System.out.println();
        int taget = 0;
        for (int i = 0, j = arr.length - 1; i < j; i++, j--) {
            taget = arr[i];
            arr[i] = arr[j];
            arr[j] = taget;
        }

        for (int k : arr) {
            System.out.print(k + " ");
        }
        System.out.println();
    }

    public static Boolean searchNumber(int arr[], int key) {
        int i;
        for (i = 0; i < arr.length; i++) {
            if (arr[i] == key) {
                return true;
            }
        }
        return false;
    }
}
```



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

**数组的复制：**

```java
package com.sdut;

public class Test01 {
    public static void main(String[] args) {
        //数组的复制
        //System类中提供的特殊的方法
        int[] arr01 = new int[]{1, 2, 3, 4, 5, 6};
        int [] arr02 = new int [arr01.length];
        //
        System.arraycopy(arr01,0,arr02,0,arr01.length);
        /*
        第一个参数：来源数组的名称（即获取其地址）
        第二个参数：来源数组的起始位置，即从什么位置开始复制
        第三个参数：目的数组的名称（获取目的数组的地址）
        第四个参数：目的数组的起始位置，即复制的数值从什么地方插入
        第五个参数：来源数组中需要复制的元素的个数，也为需要复制的长度
         */

        for (int k : arr01){
            System.out.print(k + " ");
        }
        System.out.println();

        for (int k : arr02){
            System.out.print(k + " ");
        }
    }
}

```



```java
package com.sdut;

import java.util.Arrays;

public class Test02 {
    public static void main(String[] args) {
        int [] arr01 = new int [] {1,2,3,4,5,6};
        int [] arr02;

        arr02 = Arrays.copyOf(arr01,arr01.length - 2);
        /*
        第一个参数，原数组名称，即获取其地址
        第二个参数，复制的长度
        这个方法复制的起始点默认为0
         */
        for (int k : arr01){
            System.out.print(k + " ");
        }
        System.out.println();
        for (int k : arr02){
            System.out.print(k + " ");
        }
    }
}
```

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

