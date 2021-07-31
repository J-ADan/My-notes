# Java多线程

普通方法调用

![image-20210727205324914](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727205324914.png)

多线程调用

![image-20210727205350604](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727205350604.png)

**并发与并行：**





**线程与进程：**

一个进程可以有多个线程。程序跑起来是一个进程，进程里面包括多个线程，真正执行的不是进程，是线程。

1. 程序是指令和数据的有序集合，其本身没有任何运行的含义，是一个静态的概念。
2. 进程就是程序的一次执行过程，他是一个动态的概念，是系统资源分配的单位
3. 通常在一个进程中包含若干个线程，一个进程至少有一个线程，不然没有意义，线程是 CPU 调度和执行的单位。

ps：很多多线程都是模拟出来的，真正的多线程是指有多个 CPU，即多核的概念，如服务器。如果是模拟出来的多线程，即在一个 CPU 的情况下，因为切换的很快，所以就有同时执行的错觉。



**核心概念：**

1. 线程就是独立的执行路径。
2. 在程序运行时，即使没有自己创建线程，后台也会有多个线程，如主线程，gc线程。
3. main() 称之为主线程，是系统的入口，用于执行整个程序。
4. 在一个进程中，如果开辟了多个线程，线程的运行有调度器（CPU）安排调度，调度器是与操作系统紧密相关的，先后顺序是不能人为的干预的。
5. 对同一份资源操作时，会存在资源抢夺问题，需要加入并发控制（例如买票）
6. 线程将会带来额外的开销，如 CPU的调度时间，并发控制开销。
7. 每个线程都在自己的工作内存交互，内存控制不当会造成数据不一致。
8. 

## 线程的创建

线程的三种创建形式：

1. 继承 Thread 类
2. 实现 Runnable 接口
3. 实现 Callable 接口



### Thread类

	1. 自定义线程类，继承Thread 类
	2. 重写 run() 方法
	3. 创建线程对象，调用 start() 方法启动线程。

```java
package com.sdut.demo06;

//继承Thread类
public class ThreadTest01 extends Thread{
    //重写Thread方法
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("多线程" + i);
        }
    }

    public static void main(String[] args) {
        //创建线程对象
        ThreadTest01 threadTest01 = new ThreadTest01();
        //调用strat() 方法
        threadTest01.start();//启动执行子线程，执行run方法，立即返回start方法。

        for (int i = 0; i < 2000; i++) {
            System.out.println("主线程" + i);
        }
    }
}

```

![image-20210727215953717](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727215953717.png)

多线程交替执行

```java
package com.sdut.demo06;

//继承Thread类
public class ThreadTest01 extends Thread{
    //重写Thread方法
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("多线程" + i);
        }
    }

    public static void main(String[] args) {
        //创建线程对象
        ThreadTest01 threadTest01 = new ThreadTest01();
        //调用strat() 方法
        threadTest01.run();

        for (int i = 0; i < 2000; i++) {
            System.out.println("主线程" + i);
        }
    }
}

```

![image-20210727220106815](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727220106815.png)

单线程顺序执行



**线程开始不一定立即执行，由CPU调度执行**

小练习

```java
package com.sdut.demo06;

import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.URL;

public class ThreadTest02 extends Thread{

    private String url;
    private String name;

    @Override
    public void run() {
        DownLoadTest downLoadTest = new DownLoadTest();
        downLoadTest.downLoad(url,name);
        System.out.println("下载了" + name);
    }

    public ThreadTest02(String url,String name){
        this.url = url;
        this.name = name;
    }

    public static void main(String[] args) {
        ThreadTest02 t1 = new ThreadTest02("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","01.png");
        ThreadTest02 t2 = new ThreadTest02("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","02.png");
        ThreadTest02 t3 = new ThreadTest02("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","03.png");

        t1.start();
        t2.start();
        t3.start();
    }
}

class DownLoadTest{
    //下载方法
    public void downLoad(String url,String name){
        try {
            FileUtils.copyURLToFile(new URL(url),new File(name));
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("下载器异常");
        }
    }
}

```

![image-20210727222507111](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727222507111.png)



### Runnable接口（因为Java单继承特性，推荐使用Runnable）

```java
package com.sdut.demo06;

public class RunnableTest implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("多线程" + i);
        }
    }

    public static void main(String[] args) {
        //船舰Runnable接口实现类对象
        RunnableTest runnableTest = new RunnableTest();

        //丢入Runnable的对象
        Thread thread = new Thread(runnableTest);
        //通过start开启线程
        thread.start();

        for (int i = 0; i < 2000; i++) {
            System.out.println("主线程" + i);
        }

    }
}

```

![image-20210727223318181](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727223318181.png)



小练习改造

```java
package com.sdut.demo06;

import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.URL;

public class RunnableTest01 implements Runnable{

    private String url;
    private String name;

    @Override
    public void run() {
        DownLoadTest downLoadTest = new DownLoadTest();
        downLoadTest.downLoad(url,name);
        System.out.println("下载了" + name);
    }

    public RunnableTest01(String url,String name){
        this.url = url;
        this.name = name;
    }

    public static void main(String[] args) {
        ThreadTest02 t1 = new ThreadTest02("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","01.png");
        ThreadTest02 t2 = new ThreadTest02("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","02.png");
        ThreadTest02 t3 = new ThreadTest02("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","03.png");

        new Thread(t1).start();
        new Thread(t2).start();
        new Thread(t3).start();
    }
}

class DownLoadTest01{
    //下载方法
    public void downLoad(String url,String name){
        try {
            FileUtils.copyURLToFile(new URL(url),new File(name));
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("下载器异常");
        }
    }
}

```

![image-20210727223707216](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210727223707216.png)



### 小结

**继承Thread类**

1. 子类继承Thread具备多线程能力
2. 启动线程：子类对象.strat()
3. 不建议使用：避免OOP单继承局限性



**实现Runnable接口**

1. 实现Runnable接口具备多线程能力
2. 启动线程：Thread对象.strat(传入对象目标)；
3. 推荐使用，避免单继承局限性，灵活方便，方便同一个对象被多个线程使用



### 实现多线程

```java
package com.sdut.demo06;


//多线程同时操作一个对象
public class ThreadTest implements Runnable{

    private int ticketNums = 10;
    @Override
    public void run() {

        while (true){
            if (ticketNums == 0){
                break;
            }
            System.out.println(Thread.currentThread().getName() + "拿到了" + ticketNums-- + "张票");
        }

    }

    public static void main(String[] args) {
        ThreadTest threadTest = new ThreadTest();

        new Thread(threadTest,"小米").start();
        new Thread(threadTest,"小花").start();
        new Thread(threadTest,"小明").start();
    }
}

```

![image-20210729133832573](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210729133832573.png)



### 龟兔赛跑

```java
package com.sdut.threadtest;

//龟兔赛跑
public class ThreadTest03 implements Runnable{

    private static String winner;

    @Override
    public void run() {
        for (int i = 0; i <= 100; i++) {
            if (Thread.currentThread().getName().equals("兔子")){
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            if (gameOver(i)){
                break;
            }
            System.out.println(Thread.currentThread().getName() + "跑了" + i + "步");
        }
    }

    public boolean gameOver(int steps){
        if (winner != null){
            return true;
        }{
            if (steps >= 100){
                winner = Thread.currentThread().getName();
                System.out.println(winner + "赢了");
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        ThreadTest03 threadTest03 = new ThreadTest03();

        new Thread(threadTest03,"兔子").start();
        new Thread(threadTest03,"乌龟").start();
    }
}

```

### Callable 接口

1. 实现Callable接口
2. 重写 call 方法，并且需要抛出异常
3. 创建目标对象
4. 创建执行服务 ExecutorService ser = Executors.newFixedThreadPool(1)
5. 提交执行 Future<Boolean> result1 = ser.submit(t1);
6. 获取结果：boolean r1 = result.get()
7. 关闭服务：ser.shutdownNow();



```java
package com.sdut.threadtest;

import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.URL;
import java.util.concurrent.*;

public class CallanleTest implements Callable<Boolean> {
    private String url;
    private String name;
    @Override
    public Boolean call() throws Exception {
        DownLoadTest05 downLoadTest = new DownLoadTest05();
        downLoadTest.downLoad(url,name);
        System.out.println("下载了" + name);
        return true;
    }
    public CallanleTest(String url,String name){
        this.url = url;
        this.name = name;
    }

    public static void main(String[] args) throws ExecutionException,InterruptedException {
        CallanleTest t1 = new CallanleTest("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","01.png");
        CallanleTest t2 = new CallanleTest("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","02.png");
        CallanleTest t3 = new CallanleTest("https://img-blog.csdnimg.cn/img_convert/27ab07360d9fdff5877982c0c1dfd917.png","03.png");

        ExecutorService ser = Executors.newFixedThreadPool(3);

        Future<Boolean> result1 = ser.submit(t1);
        Future<Boolean> result2 = ser.submit(t2);
        Future<Boolean> result3 = ser.submit(t3);

        boolean r1 = result1.get();
        boolean r2 = result2.get();
        boolean r3 = result3.get();

        ser.shutdownNow();
    }
}
class DownLoadTest05 {
    //下载方法
    public void downLoad(String url, String name) {
        try {
            FileUtils.copyURLToFile(new URL(url), new File(name));
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("下载器异常");
        }
    }
}
```



## 静态代理模式



```java
package com.sdut.staticproxtest;


//静态代理模式
public class StaticProxTest01 {

    public static void main(String[] args) {
        WeddingCompany weddingCompany = new WeddingCompany(new Me());
        weddingCompany.happyMarry();
    }

}
interface Marry{
    void happyMarry();
}

class Me implements Marry{

    @Override
    public void happyMarry() {
        System.out.println("我结婚了");
    }
}

class WeddingCompany implements Marry{

    //代理的对象
    private Marry taget;

    public WeddingCompany(Marry taget) {
        this.taget = taget;
    }

    @Override
    public void happyMarry() {
        before();
        this.taget.happyMarry();
        after();
    }

    public void before(){
        System.out.println("婚前布置");
    }

    public void after(){
        System.out.println("婚后收钱");
    }
}
```

 

## 线程的状态

![image-20210730191505009](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210730191505009.png)

**状态：**

1. 创建状态：对象被实例化之后为创建状态
2. 当线程被 start() 唤醒启动之后，为就绪状态
3. 当线程被 CPU调动之后为运行状态
4. 运行完成，要么回到就绪状态继续执行，要么线程生命周期结束，进入死亡状态
5. 当线程被 sleep() 之后，为阻塞状态。
6. 再次被唤醒之后，为就绪状态

![image-20210730191915414](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210730191915414.png)



### 线程的方法

![image-20210730192005240](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210730192005240.png)



### 线程的停止

```java
package com.sdut.threadtest;


//不建议使用 stop方法，以及destroy方法
//自己设置标志位
public class ThreadTest05 implements Runnable {

    private boolean flag = true;

    @Override
    public void run() {
        while (flag){
            System.out.println("一直在跑");
        }
    }

    public void stop(boolean flag){
        this.flag = flag;
    }

    public static void main(String[] args) {
        ThreadTest05 threadTest05 = new ThreadTest05();

        new Thread(threadTest05).start();
        for (int i = 0; i < 500; i++) {
            System.out.println("主线程" + i);
            if (i == 456){
                threadTest05.stop(false);
                System.out.println("线程停止");
            }
        }
    }
}

```

### 线程的休眠

**sleep()**

1. sleep 指定当前的线程阻塞的毫秒数
2. sleep 存在异常 InterruptdException
3. sleep 时间到达之后线程就进入就绪状态
4. sleep 可以模拟网络延迟，倒计时等
5. 每一个对象都有一个锁，sleep 不会释放锁。



**模拟延迟**

```java
//模拟延迟，可以放大方法的可能性
package com.sdut.threadtest;

//模拟网络延迟
public class ThreadTest06 implements Runnable {
    private int num = 10;

    @Override
    public void run() {
        while (num <= 10) {
            if (num < 0){
                break;
            }
            System.out.println(Thread.currentThread().getName() + "拿到了第" + num-- + "张票");
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }

    public static void main(String[] args) {
        ThreadTest06 threadTest061 = new ThreadTest06();

        new Thread(threadTest061, "小明").start();
        new Thread(threadTest061, "老师").start();
        new Thread(threadTest061, "黄牛").start();
    }
}

```



**模拟倒计时**

```java
package com.sdut.threadtest;

//模拟倒计时
public class ThreadTest07 implements Runnable {
    private int num = 10;
    @Override
    public void run() {
        while (true){
            if (num <= 0){
                break;
            }
            System.out.println(num--);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        ThreadTest07 threadTest07 = new ThreadTest07();

        new Thread(threadTest07).start();
    }
}

```



获取当前系统时间，每一秒一次

```java
package com.sdut.threadtest;

import java.text.SimpleDateFormat;
import java.util.Date;

public class ThreadTest08 implements Runnable {
    @Override
    public void run() {
        while (true){
            Date datetime = new Date(System.currentTimeMillis());//获取系统当前时间
            System.out.println(new SimpleDateFormat("HH:mm:ss").format(datetime));
            try {
                Thread.sleep(1000);
                datetime = new Date(System.currentTimeMillis());//更新时间
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        ThreadTest08 threadTest08 = new ThreadTest08();

        new Thread(threadTest08).start();
    }
}

```



### 线程的礼让

线程礼让，当前线程暂停，让其他线程先执行

礼让不是进入阻塞状态，而是进入就绪状态。

礼让不一定成功，看 CPU 的调度。

```java
package com.sdut.threadtest;

//线程的礼让，但是礼让不一定成功
public class ThreadTest09 implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + "线程启动");
        Thread.yield();//线程的礼让
        System.out.println(Thread.currentThread().getName() + "线程结束");
    }

    public static void main(String[] args) {
        ThreadTest09 threadTest09 = new ThreadTest09();

        new Thread(threadTest09,"a").start();
        new Thread(threadTest09,"b").start();
    }
}

```

礼让成功：

![image-20210730195839293](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210730195839293.png)

礼让失败：

![image-20210730195857461](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210730195857461.png)

### 线程的强制执行

Join 合并线程，待到此线程执行完成之后，再执行其他的线程，其他的线程阻塞。

```java
package com.sdut.threadtest;

//线程的强制执行，可以理解为找关系插队
public class ThreadTest10 implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            System.out.println("线程VIP" + i);
        }
    }

    public static void main(String[] args) throws InterruptedException {
        ThreadTest10 threadTest10 = new ThreadTest10();
        Thread thread = new Thread(threadTest10);

        thread.start();
        //主线程，被插队
        for (int i = 0; i < 500; i++) {
            System.out.println("main" + i);
            if ( i == 200){
                thread.join();
            }
        }
    }
}

```

**线程插队不一定代表，插队之前，此线程不执行，只是插队之后，所有的CPU资源全归为此线程，此线程必须先执行完毕**



### 线程的状态检测

- 线程状态。线程可以处于以下状态之一：

  - [`NEW`]  
    尚未启动的线程处于此状态。 
  - [`RUNNABLE`]  
    在Java虚拟机中执行的线程处于此状态。 
  - [`BLOCKED`] 
    被阻塞等待监视器锁定的线程处于此状态。 
  - [`WAITING`]
    正在等待另一个线程执行特定动作的线程处于此状态。 
  - [`TIMED_WAITING`]
    正在等待另一个线程执行动作达到指定等待时间的线程处于此状态。 
  - [`TERMINATED`]  
    已退出的线程处于此状态。 

  一个线程可以在给定时间点处于一个状态。 这些状态是不反映任何操作系统线程状态的虚拟机状态。 



```java
package com.sdut.threadtest;

public class ThreadTest11 {

    public static void main(String[] args) throws InterruptedException {

        Thread thread = new Thread(()->{
            for (int i = 0; i < 5; i++) {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("线程结束");
        });

        Thread.State state = thread.getState();
        System.out.println(state); //NEW

        thread.start();
        state = thread.getState();
        System.out.println(state);//Runnable

        while (state != Thread.State.TERMINATED){//只要线程不停止，一直监听状态

            Thread.sleep(100);
            state = thread.getState();//更新状态
            System.out.println(state);

        }
    }
}

```



### 线程的优先级

Java中提供一个线程的调度器来监控程序中启动后进入就绪状态的所有线程，线程的调度器按照优先级决定应该调度哪个线程来执行。

**线程的优先级不能够直接决定线程的调度顺序，还是要看 CPU 的调度实情**

线程的优先级用数字表示，1~10；

* Thread.MIN_PRIORITY = 1;

* Thread.MAX_PRIORITY = 10;
* Thread.NORM_PRIORITY = 5; **默认优先级**

使用以下的方法来获取设置优先级

getPriority()	SetPriority(int xxx)



**先设置优先级再启动**

```java
package com.sdut.threadtest;

public class ThreadTest12 implements Runnable {
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() +
                "..." + Thread.currentThread().getPriority());
    }

    public static void main(String[] args) {
        //获取主线程优先级，默认为5，且不可更改
        System.out.println(Thread.currentThread().getName() +
                "..." + Thread.currentThread().getPriority());

        ThreadTest12 threadTest12 = new ThreadTest12();
        Thread thread1 = new Thread(threadTest12);
        Thread thread2 = new Thread(threadTest12);
        Thread thread3 = new Thread(threadTest12);
        Thread thread4 = new Thread(threadTest12);
        Thread thread5 = new Thread(threadTest12);
        Thread thread6 = new Thread(threadTest12);

        thread1.setPriority(6);
        thread1.start();
        thread2.setPriority(Thread.MIN_PRIORITY);
        thread2.start();
        thread3.setPriority(6);
        thread3.start();
        thread4.setPriority(Thread.NORM_PRIORITY);
        thread4.start();
        thread5.setPriority(Thread.MAX_PRIORITY);
        thread5.start();
        thread6.setPriority(6);
        thread6.start();

    }
}

```



![image-20210730203626893](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210730203626893.png)

**可以看到不一定式优先级高的先调度，这种情况为性能倒置**



### 守护线程

线程分为 **用户线程** 和 **守护线程**

* 用户线程：例如主线程，自己创建的线程
* 守护线程：例如GC线程，即垃圾回收机制线程

虚拟机必须等待用户线程执行完毕

虚拟机不必等待守护线程执行完毕

如：后台操作日志，监控内存，垃圾回收等待。



```java
package com.sdut.threadtest;

public class ThreadTest13 {
    public static void main(String[] args) {
        Person person = new Person();
        God god = new God();

        Thread thread = new Thread(god);
        thread.setDaemon(true);//默认值为false，如果不设置，即为用户线程
        thread.start();

        new Thread(person).start();

    }
}

class Person implements Runnable{

    @Override
    public void run() {
        for (int i = 0; i < 365; i++) {
            System.out.println("开心的活着!");
        }
        System.out.println("再见世界!");
    }
}

class God implements Runnable{

    @Override
    public void run() {
        while (true){
            System.out.println("上帝一直都在!");
        }
    }
}
```

![image-20210730204634473](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210730204634473.png)



## 线程的同步

 处理多线程问题式，多线程访问同一个对象（并发问题），并且这些线程要修改对象。这个时候需要线程同步。线程同步其实就是一种等待机制，多个需要同时访问此对象的线程进入这个 **对象的等待池** 等待前面的线程使用完毕，下一个线程继续使用。



**线程同步需要两个条件解决安全性：队列和锁**



* 由于同一个进程共享同一块的存储空间，带来方便的同时，也带来了访问冲突问题，为了保证数据在方法中被访问的正确性，在访问时加入 **锁机制 synchronized** ，当一个线程或的对象的排他锁，独占资源，其他的线程必须等待
* 一个线程持有锁会导致其他所有需要此锁的线程挂起
* 在多线程的竞争下，加锁，释放锁会导致比较多的上下文切换 和 调度延迟，引起性能问题。
* 如果一格人优先级高的线程等待一个优先级低的线程释放锁，会导致优先级倒置（性能倒置），引起性能问题。



## 三大线程不安全案例





买票案例

ps：可能会买到最后的同一张票，可能会买到 -1 张票。

```java
package com.sdut.case01;

public class BuyTicket implements Runnable{

    private int ticketNumbers = 10;
    boolean flag = true;//外部控制线程停止

    @Override
    public void run() {
        while (flag){
            try {
                buy();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public void buy() throws InterruptedException {
        if (ticketNumbers <= 0){
            this.flag = false;
            return;
        }
        Thread.sleep(100);
        System.out.println(Thread.currentThread().getName() +
                "拿到了" + ticketNumbers-- + "张票");
    }
}
```

```java
package com.sdut.case01;

public class Test01 {
    public static void main(String[] args) {
        BuyTicket buyTicket = new BuyTicket();

        new Thread(buyTicket,"我").start();
        new Thread(buyTicket,"你").start();
        new Thread(buyTicket,"他").start();
    }
}
```

输出结果1：

你拿到了10张票
他拿到了9张票
我拿到了8张票
我拿到了7张票
他拿到了6张票
你拿到了5张票
我拿到了4张票
他拿到了3张票
你拿到了2张票
你拿到了1张票
我拿到了0张票
他拿到了1张票

输出结果2：

你拿到了8张票
我拿到了10张票
他拿到了9张票
他拿到了7张票
我拿到了6张票
你拿到了5张票
我拿到了3张票
你拿到了4张票
他拿到了2张票
你拿到了1张票
他拿到了0张票
我拿到了-1张票



银行取钱案例：

```java
package com.sdut.case02;

public class Account {
    private int money;
    private String name;

    public void setMoney(int money) {
        this.money = money;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Account(int money, String name) {
        this.money = money;
        this.name = name;
    }

    public int getMoney() {
        return money;
    }

    public String getName() {
        return name;
    }
}
```

```java
package com.sdut.case02;

//模拟银行
public class WithdrawMoney extends Thread {
    Account account;
    //取了多少钱
    int drawmoney;
    //手里有多少钱
    int nowmoney;

    @Override
    public void run() {

        if (account.getMoney() - drawmoney < 0){
            System.out.println("超出余额" + this.getName());
            //this.getName() == Thread.currentThread().getName()
            return;
        }

        try {
            //模拟延迟，放大问题的发生性
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        account.setMoney(account.getMoney() - drawmoney);
        nowmoney = nowmoney + drawmoney;

        System.out.println(this.getName() + "手里的钱为：" + nowmoney);
        System.out.println(account.getName() + "余额为：" + account.getMoney());

    }

    public WithdrawMoney (Account account, int drawmoney,String name){
        super(name);
        this.account = account;
        this.drawmoney = drawmoney;
    }
}
```

```java
package com.sdut.case02;

public class Test02 {
    public static void main(String[] args) {
        Account account = new Account(100,"不义之财");

        WithdrawMoney withdrawMoney =
                new WithdrawMoney(account,50,"自己");
        WithdrawMoney withdrawMoney1 =
                new WithdrawMoney(account,100,"同伙");

        new Thread(withdrawMoney).start();
        new Thread(withdrawMoney1).start();
    }
}
```

输出结果：

自己手里的钱为：50
同伙手里的钱为：100
不义之财余额为：-50
不义之财余额为：-50



线程不安全

```java
package com.sdut.case03;

import java.util.ArrayList;
import java.util.List;

//集合不安全案例
public class UnsafeList {

    public static void main(String[] args) {
        ArrayList<String> objects = new ArrayList<>();

        for (int i = 0; i < 1000; i++) {
            new Thread(
                    ()->{
                        objects.add(Thread.currentThread().getName());
                    }
            ).start();
        }

        System.out.println(objects.size());
    }
}
```

输出结果：

340

模拟延迟

```java
package com.sdut.case03;

import java.util.ArrayList;
import java.util.List;

//集合不安全案例
public class UnsafeList {

    public static void main(String[] args) {
        ArrayList<String> objects = new ArrayList<>();

        for (int i = 0; i < 10000; i++) {
            new Thread(
                    ()->{
                        objects.add(Thread.currentThread().getName());
                    }
            ).start();
        }
        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println(objects.size());
    }
}
```

输出结果：

9939



## 同步方法和同步块

**同步方法**

1. 由于我们可以通过private 关键字来保证数据对象只能被方法访问，所以我们只需要针对方法提出一套机制，这套机制就是 synchronized 关键字，他包括两种用法

   * synchronized 方法
   * synchronized 块

   同步方法：public synchronized void method(int args){}

2. synchronized 方法控制对对象的访问，每一个对象对应一把锁，每一个 synchronized 方法都必须获得调用该方法的对象锁才能执行，否则线程就会阻塞，方法一旦执行，就会独占锁，直到该方法返回才释放锁，后面阻塞的线程才会获得锁，继续执行。

**锁机制的缺陷，若将一个大的方法申明为 synchronized 将会影响效率**



**同步块**

1. 同步块 synchronized (Obj){}
2. Obj称之为同步检测器
   * Obj可以是任何对象，但是推荐使用共享资源作为同步检测器（即共同要修改的对象）
   * 同步方法中无需指定同步检测器，因为同步方法的同步检测器就是 this 就是这个对象本身，或者是class
3. 同步监视器的执行过程
   * 第一个线程访问，锁定同步监视器，执行其中代码
   * 第二个线程访问，发现同步监视器被锁定，无法访问
   * 第一个线程访问完毕，解锁同步监视器
   * 第二个线程访问，发现同步监视器没有锁，然后锁定访问



买票机制修改（同步方法）

```java
package com.sdut.synchronizedtest;

public class SynchronizedTest01 implements Runnable{
    private int ticketNumbers = 10;
    boolean flag = true;//外部控制线程停止

    @Override
    public void run() {
        while (flag){
            try {
                buy();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public synchronized void buy() throws InterruptedException {
        if (ticketNumbers <= 0){
            this.flag = false;
            return;
        }
        Thread.sleep(100);
        System.out.println(Thread.currentThread().getName() +
                "拿到了" + ticketNumbers-- + "张票");
    }

    public static void main(String[] args) {
        SynchronizedTest01 synchronizedTest01 = new SynchronizedTest01();

        new Thread(synchronizedTest01,"我").start();
        new Thread(synchronizedTest01,"你").start();
        new Thread(synchronizedTest01,"他").start();
    }
}
```



银行取钱机制修改（同步块）

```java
package com.sdut.synchronizedtest;

public class SynshronizedTest02 extends Thread{
    Account account;
    //取了多少钱
    int drawmoney;
    //手里有多少钱
    int nowmoney;

    @Override
    public void run() {

        //synchronized 代码块，
        synchronized (account){
            if (account.getMoney() - drawmoney < 0){
                System.out.println("超出余额" + this.getName());
                //this.getName() == Thread.currentThread().getName()
                return;
            }

            try {
                //模拟延迟，放大问题的发生性
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            account.setMoney(account.getMoney() - drawmoney);
            nowmoney = nowmoney + drawmoney;

            System.out.println(this.getName() + "手里的钱为：" + nowmoney);
            System.out.println(account.getName() + "余额为：" + account.getMoney());
        }

    }

    public SynshronizedTest02 (Account account, int drawmoney,String name){
        super(name);
        this.account = account;
        this.drawmoney = drawmoney;
    }
}

class Test02 {
    public static void main(String[] args) {
        Account account = new Account(100,"不义之财");

        SynshronizedTest02 withdrawMoney =
                new SynshronizedTest02(account,50,"自己");
        SynshronizedTest02 withdrawMoney1 =
                new SynshronizedTest02(account,100,"同伙");

        new Thread(withdrawMoney).start();
        new Thread(withdrawMoney1).start();
    }
}

class Account {
    private int money;
    private String name;

    public void setMoney(int money) {
        this.money = money;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Account(int money, String name) {
        this.money = money;
        this.name = name;
    }

    public int getMoney() {
        return money;
    }

    public String getName() {
        return name;
    }
}
```



同步方法

```java
package com.sdut.synchronizedtest;

import java.util.ArrayList;

public class SynchronizedTest03 {
    public static void main(String[] args) {
        ArrayList<String> objects = new ArrayList<>();

        for (int i = 0; i < 10000; i++) {
            new Thread(
                    ()->{
                        synchronized (objects){
                            objects.add(Thread.currentThread().getName());
                        }
                    }
            ).start();
        }
        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println(objects.size());
    }
}
```



## 死锁

多个线程各自占有一些共享资源，并且互相等待其他线程占有的资源才能运行，而导致两个或者多个线程都在等待对方释放资源，都停止执行的情形，某个同步块同时拥有 **两个以上对象的锁** 时，就可能会发生 **死锁的问题**

```java
package com.sdut.synchronizedtest;

public class SynchronizedTest04 {
    public static void main(String[] args) {
        change change1 = new change(0,"我");
        change change2 = new change(1,"你");
        change1.start();
        change2.start();
    }
}
class Mirror{

}
class Lipstick{

}

class change extends Thread{
    static Mirror mirror = new Mirror();
    static Lipstick lipstick = new Lipstick();

    int choise;
    String name;
    public change(int choise, String name){
        this.choise = choise;
        this.name = name;
    }


    @Override
    public void run() {
        try {
            makeUp();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public void makeUp() throws InterruptedException {
        if (this.choise == 0){
            synchronized (mirror){
                System.out.println(this.name + "获得镜子");
                Thread.sleep(1000);
                synchronized (lipstick){
                    System.out.println(this.name + "获得口红");
                }
            }
        }else {
            synchronized (lipstick){
                System.out.println(this.name + "获得口红");
                synchronized (mirror){
                    System.out.println(this.name + "获得镜子");
                }
            }
        }
    }
}
```

### 死锁产生的四个必要条件

1. 互斥条件：一个资源每次只能被一个进程使用
2. 请求和保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
3. 不剥夺条件：进程已获得的资源，在未完成使用之前，不进行强行剥夺
4. 循环等待条件：若干进程之间形成一种头尾相接的循环等待资源关系

只需要想办法破其中任意一个或者多个条件就可以避免死锁的发生



## Lock锁

```java
package com.sdut.synchronizedtest;

import java.util.concurrent.locks.ReentrantLock;

public class LockTest implements Runnable {
    private int ticketNumbers = 10;
    boolean flag = true;//外部控制线程停止
    private final ReentrantLock lock = new ReentrantLock();

    @Override
    public void run() {
        while (flag) {
            try {
                lock.lock();//加锁
                try {
                    buy();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }finally {
                lock.unlock();//解锁
            }
        }
    }

    public void buy() throws InterruptedException {
        if (ticketNumbers <= 0) {
            this.flag = false;
            return;
        }
        Thread.sleep(100);
        System.out.println(Thread.currentThread().getName() +
                "拿到了" + ticketNumbers-- + "张票");
    }

    public static void main(String[] args) {
        LockTest buyTicket = new LockTest();

        new Thread(buyTicket,"我").start();
        new Thread(buyTicket,"你").start();
        new Thread(buyTicket,"他").start();
    }
}
```



### synchronized 与 lock 锁的对比

1. lock 锁是显示锁（手动开启和关闭锁，不要忘记关闭锁），synchronized 是隐式锁，除了作用域会自动释放锁
2. Lock 锁只有代码块锁，synchronized 有代码块锁和方法锁
3. 使用Lock锁，JVM 将花费较少的时间来调度线程，性能更好，并且具有更好的扩展性（提供更多的子类）
4. 优先使用顺序：Lock > 同步代码块（已经进入方法体，分配了相应的资源）>同步方法（在方法体之外）



## 线程协作

![image-20210731143102679](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210731143102679.png)

### 线程的通信

![image-20210731144817527](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210731144817527.png)

**解决线程通信问题的方法：**

| 方法名             | 作用                                                         |
| ------------------ | ------------------------------------------------------------ |
| wait()             | 表示线程一直等待，知道其他线程通知，与sleep不同，会释放锁    |
| wait(long timeout) | 指定等待的毫秒数                                             |
| notify()           | 唤醒一个处于等待状态的线程                                   |
| notifyAll()        | 唤醒同一个对象上所有调用wait()方法的线程，优先级别高的线程优先调度 |
| sleep()            | sleep不是object下的方法，他是Thread下面的方法，而且他是线程休眠的意思，不会释放对象锁 |



### 管程法

![image-20210731145700977](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210731145700977.png)



```java
package com.sdut.threadtest;

public class ThreadTest14{
    public static void main(String[] args) {
        Buffer buffer = new Buffer();

        new Producer(buffer).start();
        new Consumer(buffer).start();
    }
}
//缓冲区
class Buffer{
    //容器大小
    Product[] products = new Product[10];
    int count = 0;
    //生产者放入产品
    public synchronized void push(Product product){
        if (count == products.length){
            //如果容器满了，通知消费者消费，生产者等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        //如果没有满，生产
        products[count] = product;
        count++;

        this.notifyAll();
    }

    //消费者取出产
    public synchronized Product pop(){
        //判断能否消费
        if (count == 0){
            //消费者等待，通知生产者生产
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        count--;
        Product product = products[count];


        this.notifyAll();
        return product;
    }

}
//消费者
class Consumer extends Thread{
    Buffer buffer;
    public Consumer(Buffer buffer){
        this.buffer = buffer;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("消费了" + buffer.pop().id);
        }
    }
}
//生产者
class Producer extends Thread{
    Buffer buffer;
    public Producer(Buffer buffer){
        this.buffer = buffer;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("生产第" + i);
            buffer.push(new Product(i));
        }
    }
}

class Product{
    int id;

    public Product(int id) {
        this.id = id;
    }
}
```

### 信号灯法

```java
package com.sdut.threadtest;

public class ThreadTest15 {
    public static void main(String[] args) {
        Tv tv = new Tv();
        new Actor(tv).start();
        new Audience(tv).start();
    }
}

//表演者--生产者
class Actor extends Thread{
    Tv tv;

    public Actor(Tv tv) {
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            if(i %2 ==0){
                this.tv.show("钢管舞");
            }else{
                this.tv.show("皮皮虾广告（正片）");
            }
        }
    }
}

//观众--消费者
class Audience extends Thread{
    Tv tv;

    public Audience(Tv tv) {
        this.tv = tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            this.tv.watch();
        }
    }
}

class Tv{
    String name;//节目名字
    //信号灯
    boolean flag = true;

    public synchronized void show(String name){
        if (!flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("表演了" + name);
        //通知观众观看
        this.notifyAll();
        this.name = name;
        this.flag = !this.flag;
    }

    public synchronized void watch(){
        if (this.flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("观看了" + name);
        //通知演员表演
        this.notifyAll();
        this.flag = !this.flag;
    }
}
```



## 线程池

为什么使用线程池

经常的创建、销毁、使用特别大的资源，比如并发情况下的线程，对性能的影响很大。

**线程池的思路：**

1. 提前创建好多个线程，放入线程池
2. 使用时直接获取没使用完毕放回

这样可以避免频繁的创建销毁、实现重复利用

**线程池的好处：**

1. 提高响应速度（减少了创建新线程的时间）
2. 降低资源消耗（重复利用线程池的线程，不需要次次创建）
3. 便于线程的管理

**线程池的关键字：**

1. corePoolSize：线程池的大小
2. maximumPoolSize：最大的线程数
3. keepAliveTime：线程没有任务最多保持的时间，超过时间自动终止。



**线程池的简单代码**

```java
package com.sdut.threadtest;


import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadTest16 implements Runnable{
    @Override
    public void run() {
        System.out.println("线程池中的第" + Thread.currentThread().getName() + "个线程");
    }

    public static void main(String[] args) {
        ThreadTest16 threadTest16 = new ThreadTest16();
        ExecutorService service = Executors.newFixedThreadPool(10);

        service.execute(threadTest16);
        service.execute(threadTest16);
        service.execute(threadTest16);
        service.execute(threadTest16);
        service.execute(threadTest16);
        //关闭连接
        service.shutdown();
    }
}
```



JDK 5.0 之后提供了线程池的相关 API ExecutorService 和 Executors

**ExecutorService** ：真正的线程池接口。常见子类 ThreadPoolExecutor

* void execute(Runnable command)：执行任务/命令，没有返回值，一般用来执行Runnable
* <T>Future<T>submit(Callable <T> task)：执行任务，有返回值，一般用来执行Callable
* void shutdown()：关闭线程池



Executors：工具类、线程池的工厂类，用于创建并返回不同类型的线程池
