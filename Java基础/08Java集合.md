# Java集合

![image-20210723185425947](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210723185425947.png)

Collection集合主要有List和Set两大接口

- List：有序(元素存入集合的顺序和取出的顺序一致)，元素都有索引。元素可以重复。
- Set：无序(存入和取出顺序有可能不一致)，不可以存储重复元素。必须保证元素唯一性

## List集合

List是元素有序并且可以重复的集合。

List的主要实现：ArrayList， LinkedList， Vector。

![image-20210723185503458](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210723185503458.png)

### ArrayList、LinkedList、Vector 的区别

|              | ArrayList                                                    | LinkedList                 | Vector                 |
| ------------ | ------------------------------------------------------------ | -------------------------- | ---------------------- |
| 底层实现     | 数组                                                         | 双向链表                   | 数组                   |
| 同步性及效率 | 不同步、非线性安全、效率高、支持随机访问                     | 不同步、非线性安全、效率高 | 同步、线性安全、效率低 |
| 特点         | 查询快、增删慢                                               | 查询慢，增删块             | 查询快、增删慢         |
| 默认扩容     | 10                                                           | /                          | 10                     |
| 扩容机制     | int newCapacity = oldCapacity + (oldCapacity >> 1)；//1.5 倍 | /                          | 2倍                    |

**总结**：

- ArrayList 和 Vector 基于数组实现，对于随机访问get和set，ArrayList优于LinkedList，因为LinkedList要移动指针。
- LinkedList 不会出现扩容的问题，所以比较适合随机位置增、删。但是其基于链表实现，所以在定位时需要线性扫描，效率比较低。
- 当操作是在一列数据的后面添加数据而不是在前面或中间，并且需要随机地访问其中的元素时，使用ArrayList会提供比较好的性能；
- 当你的操作是在一列数据的前面或中间添加或删除数据，并且按照顺序访问其中的元素时，就应该使用LinkedList了



## 常用的简单的数组集合ArrayList

**跟数组相似的，存储数据的集合**

```java
package com.sdut.Demo01;

import java.util.ArrayList;

public class Demo11 {
	public static void main(String[] args) {
		
		ArrayList<String> arrayList  = new ArrayList<>();
		
	}
}

```

**集合的元素必须是引用类型，集合的长度是不给固定的，是可变的**

数组的元素的存储是依靠下标的形式，**集合的元素的存储是依靠方法的使用**

ArrayList的简单操作

```java
package com.sdut.Demo01;

import java.util.ArrayList;

public class Demo11 {
	public static void main(String[] args) {
		// 集合--基于方法的调用的方式，实现增删改查
		ArrayList<String> arrayList = new ArrayList<>();
		// 增加数据
		arrayList.add("a1");
		System.out.println(arrayList);
		arrayList.add(0, "a2");
		System.out.println(arrayList);

		// 删除数据
		arrayList.remove(0);
		System.out.println(arrayList);
		arrayList.remove("a1");	//向上转型
		System.out.println(arrayList);

		// 增加数据
		arrayList.add("a1");
		arrayList.add(0, "a2");
		System.out.println(arrayList);
		
		//修改数据
		arrayList.set(0, "a0");
		System.out.println(arrayList);
		
		//数据的查询
		String s = arrayList.get(0);
		System.out.println(s);
		
		//集合的遍历
		for (int i = 0; i < arrayList.size(); i ++) {
			String s1 = arrayList.get(i);
			System.out.print(s1 + " ");
		}
		System.out.println();
		for (String k : arrayList) {//数据类型与集合泛型数据类型一致
			System.out.print(k + " ");
		}
	}
}

```

输出结果：

[a1]
[a2, a1]
[a1]
[]
[a2, a1]
[a0, a1]
a0
a0 a1 
a0 a1 



## C语言链表相仿的集合，LinkedList

```java
package com.sdut.Demo01;

import java.util.LinkedList;

public class Demo12 {
	public static void main(String[] args) {
		LinkedList<String> linked = new LinkedList<>();
	}
}

```

**LinkedList集合的操作与ArrayList大致一致，ArrayList的大多方法LinkedList集合同样适用**

```java
package com.sdut.Demo01;

import java.util.LinkedList;

public class Demo12 {
	public static void main(String[] args) {
		LinkedList<String> linkedList = new LinkedList<>();
		
		linkedList.add("a1");
		linkedList.add("a2");
		linkedList.add("a3");
		linkedList.add("a4");
		
		System.out.println(linkedList.get(2));
		System.out.println(linkedList.getFirst());
		System.out.println(linkedList.getLast());
		System.out.println(linkedList.peek());
		System.out.println(linkedList.peekFirst());
		System.out.println(linkedList.peekLast());
		System.out.println(linkedList.pop());
		System.out.println(linkedList.poll());
		System.out.println(linkedList);
		System.out.println(linkedList.pollFirst());
		System.out.println(linkedList);
		System.out.println(linkedList.pollLast());
		System.out.println(linkedList);
	}
}

```

输出结果：

a3
a1
a4
a1
a1
a4
a1
a2
[a3, a4]
a3
[a4]
a4
[]



**ArrayList与LinkedList的区别：**

1. ArrayList 基于动态数组的数据结构，而LinkedList是基于双向链表的数据结构
2. 随机访问-ArrayList优于LinkedList，因为ArrayList跟数组相仿，会带有下标，所以访问比较快速，LinkedList是以移动索引的方式来访问元素
3. 增加删除操作，LinkedList优于ArrayList，



### 链表遍历的错误

```java
package com.sdut.Demo01;
import java.util.ArrayList;
public class Demo13 {
	public static void main(String[] args) {
		ArrayList<String> arrayList = new ArrayList<>();
		arrayList.add("a1");
		arrayList.add("a2");
		arrayList.add("a3");
		arrayList.add("a4");
		
		for (String s : arrayList) {
			System.out.println(s);
			if ("a2".equals(s)) {
				arrayList.remove(s);
			}
		}
	}
}

```

输出结果：

a1
a2
Exception in thread "main" java.util.ConcurrentModificationException
	at java.util.ArrayList$Itr.checkForComodification(ArrayList.java:901)
	at java.util.ArrayList$Itr.next(ArrayList.java:851)
	at com.sdut.Demo01.Demo13.main(Demo13.java:11)

在列表遍历过程中，不要删除元素，**删除倒数第二个元素不会报错，结果也正常，但是依旧是错误的**

```java
package com.sdut.Demo01;
import java.util.ArrayList;
public class Demo13 {
	public static void main(String[] args) {
		ArrayList<String> arrayList = new ArrayList<>();
		arrayList.add("a1");
		arrayList.add("a2");
		arrayList.add("a3");
		arrayList.add("a4");
		
		for (int i = 0; i <arrayList.size(); i++) {
			String s = arrayList.get(i);
			System.out.println(s);
			if ("a2".equals(s)) {
				arrayList.remove(s);
			}
			System.out.println(arrayList);
		}
	}
}
```

输出结果：

a1
[a1, a2, a3, a4]
a2
[a1, a3, a4]
a4
[a1, a3, a4]

**虽然这种情况不会报错，但是，不会遍历到删除元素的下一个元素，遍历次数也会变少**

索引正向遍历删除数据，必须注意错位问题，避免漏元素和错位问题

**正确方法1**

```java
package com.sdut.Demo01;
import java.util.ArrayList;
public class Demo13 {
	public static void main(String[] args) {
		ArrayList<String> arrayList = new ArrayList<>();
		arrayList.add("a1");
		arrayList.add("a2");
		arrayList.add("a3");
		arrayList.add("a4");
		
		for (int i = 0; i <arrayList.size(); i++) {
			String s = arrayList.get(i);
			System.out.println(s);
			if ("a2".equals(s)) {
				arrayList.remove(s);
				i--;
			}
			System.out.println(arrayList);
		}
	}
}

```

索引逆向遍历，正确运行

**正确方法2：可以从后往前遍历**

```java
package com.sdut.Demo01;
import java.util.ArrayList;
public class Demo13 {
	public static void main(String[] args) {
		ArrayList<String> arrayList = new ArrayList<>();
		arrayList.add("a1");
		arrayList.add("a2");
		arrayList.add("a3");
		arrayList.add("a4");
		
		for (int i = arrayList.size() - 1; i >= 0; i--) {
			String s = arrayList.get(i);
			System.out.println(s);
			if ("a2".equals(s)) {
				arrayList.remove(s);
			}
			System.out.println(arrayList);
		}
	}
}

```

输出结果：

a4
[a1, a2, a3, a4]
a3
[a1, a2, a3, a4]
a2
[a1, a3, a4]
a1
[a1, a3, a4]

**正确的方法3：迭代器方式**

```java
package com.sdut.Demo01;
import java.util.ArrayList;
import java.util.Iterator;
public class Demo13 {
	public static void main(String[] args) {
		ArrayList<String> arrayList = new ArrayList<>();
		arrayList.add("a1");
		arrayList.add("a2");
		arrayList.add("a3");
		arrayList.add("a4");
		
		Iterator<String> ite = arrayList.iterator();
		while (ite.hasNext()) {
			String s = ite.next();
			ite.remove();
			System.out.println(s);
		}
	}
}

```



## Set集合

Set集合元素无序(存入和取出的顺序不一定一致)，并且没有重复对象。
Set的主要实现类：HashSet， TreeSet。

### Set常用方法

![image-20210723191325111](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210723191325111.png)

### HashSet一些简单的代码

**HashSet的两种遍历方式：**

```java
package com.sdut.Demo01;

import java.util.HashSet;
import java.util.Iterator;

public class Demo15 {
	public static void main(String[] args) {
		HashSet<String> hasSet = new HashSet<>();
		
		hasSet.add("a1");
		hasSet.add("a2");
		hasSet.add("a3");
		hasSet.add("a4");
		hasSet.add("a5");
		//for循环增强型遍历
		for (String s : hasSet) {
			System.out.print(s + " ");
		}
		System.out.println();
		//迭代器遍历
		Iterator<String> ite = hasSet.iterator();
		while (ite.hasNext()) {
			String s = ite.next();
			System.out.print(s + " ");
		}
	}
}

```

**HashSet的特点（相比于ArrayList）**

```java
package com.sdut.Demo01;

import java.util.ArrayList;
import java.util.HashSet;
import java.util.Iterator;

public class Demo14 {
	public static void main(String[] args) {
		HashSet<String> hashSet = new HashSet<>(); 
		
		hashSet.add("a1");
		hashSet.add("a1");
        hashSet.add("a2");
        hashSet.add("a3");
		
		ArrayList<String> arrayList = new ArrayList<>();
		arrayList.add("a1");
		arrayList.add("a1");
        arrayList.add("a2");
        arrayList.add("a3");
		
		System.out.println(hashSet);
		System.out.println(arrayList);
		
		Iterator<String> ite1 = arrayList.iterator();
		Iterator<String> ite2 = hashSet.iterator();
		
		while (ite1.hasNext()) {
			String s1 = ite1.next();
			System.out.print(s1 + " ");
		}
		System.out.println();
		while (ite2.hasNext()) {
			String s2 = ite2.next();
			System.out.print(s2 + " ");
		}
	}
}
```

输出结果：

[a1, a2, a3]
[a1, a1, a2, a3]
a1 a1 a2 a3 
a1 a2 a3 

**这里可以看出HashSet，以及Set集合都是无序的，无需主要体现在默认遍历结果与添加顺序不一致**

### TreeSet的简单代码

```java
package com.sdut.Demo01;

import java.util.TreeSet;

public class Demo16 {
	public static void main(String[] args) {
		TreeSet<String> treeSet = new TreeSet<>();
		
		treeSet.add("d");
		treeSet.add("a");
		treeSet.add("e");
		treeSet.add("b");
		treeSet.add("c");
		treeSet.add("f");
		
		TreeSet<Integer> treeSet1 = new TreeSet<Integer>();
		treeSet1.add(1);
		treeSet1.add(3);
		treeSet1.add(5);
		treeSet1.add(2);
		treeSet1.add(4);
		
		System.out.println(treeSet);
		System.out.println(treeSet1);
	}
}

```

输出结果：

[a, b, c, d, e, f]
[1, 2, 3, 4, 5]

**TreeSet是一个无索引无重复的集合，他虽然大局上也是无序的，但是他对于里面的元素，自带两种顺序，一个是默认的（也就是自然顺序），另一个就是自定义的顺序**



#### HashSet、TreeSet、LinkedHashSet的区别

|            | HashSet                                           | TreeSet                                                      | LinkedHashSet                                                |
| ---------- | ------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 底层实现   | HashMap                                           | 红黑树                                                       | LinkedHashMap                                                |
| 重复性     | 不允许重复                                        | 不允许重复                                                   | 不允许重复                                                   |
| 有无序     | 无序                                              | 有序，支持两种排序方式，自然排序和定制排序，其中自然排序为默认的排序方式。 | 有序，以元素插入的顺序来维护集合的链接表                     |
| 时间复杂度 | add()，remove()，contains()方法的时间复杂度是O(1) | add()，remove()，contains()方法的时间复杂度是O(logn)         | LinkedHashSet在迭代访问Set中的全部元素时，性能比HashSet好，但是插入时性能稍微逊色于HashSet，时间复杂度是 O(1)。 |
| 同步性     | 不同步，线程不安全                                | 不同步，线程不安全                                           | 不同步，线程不安全                                           |
| null值     | 允许null值                                        | 不支持null值，会抛出 java.lang.NullPointerException 异常。因为TreeSet应用 compareTo() 方法于各个元素来比较他们，当比较null值时会抛出 NullPointerException异常。 | 允许null值                                                   |
| 比较       | equals()                                          | compareTo()                                                  | equals()                                                     |

#### HashSet如何检查重复

当你把对象加入HashSet时，HashSet会先计算对象的hashcode值来判断对象加入的位置，同时也会与其他加入的对象的hashcode值作比较，如果没有相符的hashcode，HashSet会假设对象没有重复出现。但是如果发现有相同hashcode值的对象，这时会调用equals()方法来检查hashcode相等的对象是否真的相同。如果两者相同，HashSet就不会让加入操作成功。
hashCode()与equals()的相关规定：

* 如果两个对象相等，则hashcode一定也是相同的
* 两个对象相等，equals方法返回true
* 两个对象有相同的hashcode值，它们也不一定是相等的
* 综上，equals方法被覆盖过，则hashCode方法也必须被覆盖
  hashCode()的默认行为是对堆上的对象产生独特值。如果没有重写hashCode()，则该class的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）。

总结：
HashSet是一个通用功能的Set，而LinkedHashSet 提供元素插入顺序保证，TreeSet是一个SortedSet实现，由Comparator 或者 Comparable指定的元素顺序存储元素。

## Map接口

Map 是一种把键对象和值对象映射的集合，它的每一个元素都包含一对键对象和值对象。 Map没有继承于Collection接口，从Map集合中检索元素时，只要给出键对象，就会返回对应的值对象。
Map 的常用实现类：HashMap、TreeMap、HashTable、LinkedHashMap、ConcurrentHashMap

### 双列集合继承关系

![image-20210723191018146](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210723191018146.png)

![image-20210723191046419](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210723191046419.png)

### HashMap的简单代码

* 双泛型参数，代表里面的数据是以键值对的形式存在

* HashMap<Key, Value>;

* 不允许key重复，但是value可以重复

  **HashSet 与 HashMap的底层是一模一样的**

```java
package com.sdut.Demo01;

import java.util.HashMap;

public class Demo17 {
	public static void main(String[] args) {
		//双泛型参数，代表里面的数据是以键值对的形式存在
		//HashMap<Key, Value>;
		//不允许key重复，但是value可以重复
		HashMap<String, String> hashMap = new HashMap<>();
		
		hashMap.put("mian", "int");
		hashMap.put("mian", "iii");
		String s = hashMap.get("mian");//获取值，通过key
		System.out.println(s);
        
        hashMap.remove("mian");//删除操作，键值对一块删除
        
	}
}

```

输出结果：

{mian=iii}
iii

**当put操作的key值相同时，put操作变为修改value值**

### HashMap的遍历操作

```java
package com.sdut.Demo01;

import java.util.HashMap;
import java.util.Map.Entry;
import java.util.Set;

public class Demo18 {
	public static void main(String[] args) {
		HashMap<String, String> hashMap = new HashMap<>();
		
		hashMap.put("a1", "a1");
		hashMap.put("a2", "a2");
		hashMap.put("a3", "a3");
		hashMap.put("a4", "a4");
		
		Set<Entry<String, String>> entrySet = hashMap.entrySet();
		
		for (Entry<String, String> entry : entrySet) {
			String key = entry.getKey();
			String val = entry.getValue();
			System.out.println(key + " " + val);
		}
		System.out.println();
		//单独遍历key
//		Set<String> keys = hashMap.keySet();
		for (String key : hashMap.keySet()) {
			System.out.print(key + " ");
		}
		System.out.println();
		//单独遍历value
		for (String val : hashMap.values()) {
			System.out.print(val + " ");
		}
	}
}
```

```java
package com.sdut.Demo01;

import java.util.HashMap;

public class Demo19 {
	public static void main(String[] args) {
		HashMap<String, String> hashMap = new HashMap<>();

		hashMap.put("a1", "a1");
		hashMap.put("a2", "a2");
		hashMap.put("a3", "a3");
		hashMap.put("a4", "a4");
		
		int a = hashMap.size();//获取map集合有多少键值对
		//查看map集合里是否存在某个key或者某个value
		boolean b1 = hashMap.containsKey("a1");
		boolean b2 = hashMap.containsValue("a1");
		
		System.out.println(a + " " + b1 + " " + b2);
	}
}

```

### LinkedHashMap



### HashMap、HashTable、TreeMap的区别

* TreeMap：基于红黑树实现。

* HashMap：基于哈希表实现。

* HashTable：和 HashMap 类似，但它是线程安全的，这意味着同一时刻多个线程可以同时写入 HashTable 并且不会导致数据不一致。它是遗留类，不应该去使用它。现在可以使用 ConcurrentHashMap 来支持线程安全，并且 ConcurrentHashMap 的效率会更高，因为 ConcurrentHashMap 引入了分段锁。

* LinkedHashMap：使用双向链表来维护元素的顺序，顺序为插入顺序或者最近最少使用（LRU）顺序。

  |          | HashMap                                                      | HashTable                                     | TreeMap                                                      |
  | -------- | ------------------------------------------------------------ | --------------------------------------------- | ------------------------------------------------------------ |
  | 底层实现 | 哈希表（数组+链表+红黑树）                                   | 哈希表（数组+链表）                           | 红黑树                                                       |
  | 同步性   | 线程不同步                                                   | 同步                                          | 线程不同步                                                   |
  | null值   | 允许 key 和 Vale 是 null，但是只允许一个 key 为 null，且这个元素存放在哈希表 0 角标位置 | 不允许key、value 是 null                      | value允许为null。当未实现 Comparator 接口时，key 不可以为null当实现 Comparator 接口时，若未对 null 情况进行判断，则可能抛 NullPointerException 异常。如果针对null情况实现了，可以存入，但是却不能正常使用get()访问，只能通过遍历去访问。 |
  | hash     | 使用hash(Object key)扰动函数对 key 的 hashCode 进行扰动后作为 hash 值 | 直接使用 key 的 hashCode() 返回值作为 hash 值 |                                                              |
  | 容量     | 容量为 2^4 且容量一定是 2^n                                  | 默认容量是11，不一定是 2^n                    |                                                              |
  | 扩容     | 两倍，且哈希桶的下标使用 &运算代替了取模                     | 2倍+1，取哈希桶下标是直接用模运算             |                                                              |

  ## 集合工具类 Collection

  Collections：集合工具类，方便对集合的操作。这个类不需要创建对象，内部提供的都是静态方法。

  **静态方法：**

  ```java
  Collections.sort(list);//list集合进行元素的自然顺序排序。
  Collections.sort(list,new ComparatorByLen());//按指定的比较器方法排序。
  class ComparatorByLen implements Comparator<String>{
    public int compare(String s1,String s2){
       int temp = s1.length()-s2.length();
       return temp==0?s1.compareTo(s2):temp;
    }
  }
  Collections.max(list);//返回list中字典顺序最大的元素。
  int index = Collections.binarySearch(list,"zz");//二分查找，返回角标。
  Collections.reverseOrder();//逆向反转排序。
  Collections.shuffle(list);//随机对list中的元素进行位置的置换。
  
  //将非同步集合转成同步集合的方法：Collections中的  XXX synchronizedXXX(XXX);  
  //原理：定义一个类，将集合所有的方法加同一把锁后返回。
  List synchronizedList(list);
  Map synchronizedMap(map);
  ```

  ### Collection 与 Collections的区别

  * Collections是个java.util下的类，是针对集合类的一个工具类,提供一系列静态方法,实现对集合的查找、排序、替换、线程安全化（将非同步的集合转换成同步的）等操作。
  * Collection是个java.util下的接口，它是各种集合结构的父接口，继承于它的接口主要有Set和List,提供了关于集合的一些操作,如插入、删除、判断一个元素是否其成员、遍历等。