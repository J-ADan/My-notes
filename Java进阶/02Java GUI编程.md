# GUI编程

Java GUI 的大致组件

* 窗口
* 弹窗
* 面板
* 文本框
* 列表框
* 按钮
* 图片
* 监听事件
* 鼠标事件
* 键盘事件



## GUI简介

GUI 的核心开发技术

Swing、AWT。缺点：界面不美观，运行需要JRE环境。

**学习GUI编程，方便学习MVC架构、了解监听** ，也可以写出自己心中想要的一些小工具，工作的时候可能会维护到swing界面。



## AWT

可以理解为Swing的前身版。

**简介：** AWT(Abstract Window Toolkit)，中文译为抽象窗口工具包，该包提供了一套与本地图形界面进行交互的[接口](https://baike.baidu.com/item/接口/15422203)，是Java提供的用来建立和设置Java的[图形用户界面](https://baike.baidu.com/item/图形用户界面/3352324)的基本工具。

元素：窗口、按钮、文本框。

**java.awt包**



**Frame 窗口**

```java
package com.sdut.demo01;

import java.awt.*;

public class Frame01 {
    public static void main(String[] args) {
        Frame frame = new Frame("第一个界面");

        //设置可见性
        frame.setVisible(true);

        //设置大小
        frame.setSize(500,500);

        //设置背景颜色
        frame.setBackground(new Color(128, 127, 64));

        //设置显示位置
        frame.setLocation(200,200);

        //设置大小固定
        frame.setResizable(false);
    }


}

```

依靠封装弹出多个窗口

```java
package com.sdut.demo01;

import java.awt.*;

public class Frame02 {
    public static void main(String[] args) {
        MyFrame myFrame1 = new MyFrame(100, 100, 100, 100,Color.red);
        MyFrame myFrame2 = new MyFrame(200, 100, 100, 100,Color.blue);
        MyFrame myFrame3 = new MyFrame(100, 200, 100, 100,Color.yellow);
        MyFrame myFrame4 = new MyFrame(200, 200, 100, 100,Color.black);
    }

}
class MyFrame extends Frame {
    static int id = 0;//计数器

    //构造方法
    public MyFrame(int x, int y, int w, int h, Color color) {
        super("第" + "++id" + "个窗口");
        setBounds(x, y, w, h);
        setBackground(color);
        setVisible(true);
    }
}

```

**super 继承父类的构造方法，当子类继承父类时，父类的方法均可不用调用符**



**面板**

```java
package com.sdut.demo01;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class PanelTest {
    public static void main(String[] args) {
        Frame frame = new Frame();
        Panel panel = new Panel();

        //设置布局
        frame.setLayout(null);
        //窗口坐标及大小、背景颜色
        frame.setBounds(200,200,500,500);
        frame.setBackground(new Color(33, 153, 0));
        //设置容器
        panel.setBounds(100,100,200,200);
        panel.setBackground(new Color(37, 85, 150));
        //容器加入窗口
        frame.add(panel);
        //窗口可见性
        frame.setVisible(true);
        //设置关闭事件
        //监听事件，监听窗口关闭事件
        //适配器模式
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

```



**布局管理器**

* 流式布局（默认布局）

```java
package com.sdut.demo01;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class FlowLayutTest {
    public static void main(String[] args) {
        Frame frame = new Frame();

        //新建按钮对象
        Button button1= new Button("button1");
        Button button2 = new Button("button2");
        Button button3 = new Button("button3");

        //设置流式布局
        frame.setLayout(new FlowLayout());
        frame.setLayout(new FlowLayout(FlowLayout.LEFT));//靠左对齐
        frame.setLayout(new FlowLayout(FlowLayout.RIGHT));//靠右对齐

        //设置窗口大小
        frame.setSize(300,300);

        //添加按钮
        frame.add(button1);
        frame.add(button2);
        frame.add(button3);

        //设置可见性
        frame.setVisible(true);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });

    }
}
```



* 表格布局

```
package com.sdut.demo01;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class GridLayoutTest {
    public static void main(String[] args) {
        Frame frame = new Frame();

        Button button1 = new Button("button1");
        Button button2 = new Button("button2");
        Button button3 = new Button("button3");
        Button button4 = new Button("button4");
        Button button5 = new Button("button5");
        Button button6 = new Button("button6");

        frame.setLayout(new GridLayout(2,3));

        frame.add(button1);
        frame.add(button2);
        frame.add(button3);
        frame.add(button4);
        frame.add(button5);
        frame.add(button6);

        frame.pack();//自动填充，不需要设置大小
        frame.setVisible(true);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

```



* 东西南北中

```java
package com.sdut.demo01;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class BorderLayoutTest {
    public static void main(String[] args) {
        Frame frame = new Frame();

        Button east = new Button("East");
        Button west = new Button("West");
        Button south = new Button("South");
        Button north = new Button("North");
        Button center = new Button("Center");

        frame.add(east,BorderLayout.EAST);
        frame.add(west,BorderLayout.WEST);
        frame.add(south,BorderLayout.SOUTH);
        frame.add(north,BorderLayout.NORTH);
        frame.add(center,BorderLayout.CENTER);

        frame.setSize(500,500);
        frame.setVisible(true);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

```



**Test**

```java
package com.sdut.demo01;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class Test01 {
    public static void main(String[] args) {
        Frame frame = new Frame();

        Panel p1 = new Panel();
        Panel p2 = new Panel();
        Panel p3 = new Panel();
        Panel p4 = new Panel();
        frame.setSize(500,500);
        frame.setLayout(new GridLayout(2,1));
        p1.setLayout(new BorderLayout());
        p2.setLayout(new GridLayout(2,1));
        p3.setLayout(new BorderLayout());
        p4.setLayout(new GridLayout(2,2));

        p1.add(new Button("01"),BorderLayout.EAST);
        p1.add(new Button("02"),BorderLayout.WEST);
        p2.add(new Button("03"));
        p2.add(new Button("04"));

        p1.add(p2,BorderLayout.CENTER);

        p3.add(new Button("05"),BorderLayout.EAST);
        p3.add(new Button("06"),BorderLayout.WEST);

        for (int i = 0; i < 4; i ++){
            p4.add(new Button("0" + i +1));
        }

        p3.add(p4,BorderLayout.CENTER);

        frame.add(p1);
        frame.add(p3);

        frame.setVisible(true);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

```



**事件监听：**

当某个事件发生的时候，我们应该干什么。

```java
package com.sdut.demo01;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class ActionTest {
    public static void main(String[] args) {
        Frame frame = new Frame();

        Button button = new Button();
        frame.add(button);
        MyAction myAction = new MyAction();

        button.addActionListener(myAction);

        frame.setSize(200,200);
        frame.setVisible(true);

        myClosed(frame);

    }

    public static void myClosed(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

class MyAction implements ActionListener {

    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("事件监听");
    }
}
```

同一个监听事件

```java
package com.sdut.demo01;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class ActionTest02 {
    public static void main(String[] args) {

        Frame frame = new Frame();

        Button but1 = new Button("but1");
        Button but2 = new Button("but2");

        MyAction myAction = new MyAction();

        but1.setActionCommand("这是按钮一");

        but1.addActionListener(myAction);
        but2.addActionListener(myAction);

        frame.add(but1,BorderLayout.EAST);
        frame.add(but2,BorderLayout.WEST);

        frame.pack();
        frame.setVisible(true);
    }
}

class MyAction implements ActionListener {

    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("获得的点击对象" + e.getActionCommand());
    }
}
```



**输入框 TextFiled：**

```java
package com.sdut.demo02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TextFiledTest {
    public static void main(String[] args) {
        new MyFrame();

    }

}
class MyFrame extends Frame {
    public MyFrame() {
        TextField textField = new TextField();
        add(textField);

        MyActionListener myActionListener = new MyActionListener();
        //enter触发输入框事件
        textField.addActionListener(myActionListener);
        //设置替换编码
        textField.setEchoChar('*');
        setVisible(true);
        pack();
    }
}

class MyActionListener implements ActionListener{

    @Override
    public void actionPerformed(ActionEvent e) {
        TextField textField = (TextField) e.getSource();

        String s = textField.getText();
        System.out.println(s);
        //enter事件结束，设为空
        textField.setText("");
    }
}
```





**简易计算机：**

```java
package com.sdut.demo02;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class Demo01 {
    public static void main(String[] args) {
        MyCalculator myCalculator = new MyCalculator();
        myCalculator.loadFrame();
    }
}

class MyCalculator extends Frame {
    TextField textField1, textField2, textField3;

    public void loadFrame() {
        textField1 = new TextField();
        textField2 = new TextField();
        textField3 = new TextField();

        Button button = new Button("=");
        button.addActionListener(new MyCalculatorListener(this));

        Label label = new Label("+");

        setLayout(new FlowLayout());

        add(textField1);
        add(label);
        add(textField2);
        add(button);
        add(textField3);

        pack();
        setVisible(true);
        closeing(this);
    }

    public static void closeing(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

class MyCalculatorListener implements ActionListener {
    MyCalculator myCalculator = null;

    public MyCalculatorListener(MyCalculator myCalculator) {
        this.myCalculator = myCalculator;
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        int n1 = Integer.parseInt(myCalculator.textField1.getText());
        int n2 = Integer.parseInt(myCalculator.textField2.getText());

        myCalculator.textField3.setText("" + (n1+n2));

        myCalculator.textField1.setText("");
        myCalculator.textField2.setText("");
    }
}
```



**画笔**

```java
package com.sdut.demo02;

import java.awt.*;

public class PaintTest {
    public static void main(String[] args) {
        new MyPaint().loadFrame();
    }
}
class MyPaint extends Frame{
    public void loadFrame(){
        setBounds(200,200,400,400);
        setVisible(true);
    }

    @Override
    public void paint(Graphics g) {
        //获得颜色
        g.setColor(Color.red);
        g.drawOval(100,100,100,100);//空心圆
        g.fillOval(200,200,100,100);

        //养成习惯，画笔用完，还原最初颜色
        g.setColor(Color.black);

    }
}
```





## Swing

