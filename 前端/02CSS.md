# CSS（**C**ascading **S**tyle **S**heets）

层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现[HTML](https://baike.baidu.com/item/HTML)（[标准通用标记语言](https://baike.baidu.com/item/标准通用标记语言/6805073)的一个应用）或[XML](https://baike.baidu.com/item/XML)（标准通用标记语言的一个子集）等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化。 

CSS 能够对网页中元素位置的排版进行像素级精确控制，支持几乎所有的字体字号样式，拥有对网页对象和模型样式编辑的能力。



CSS知识点：

* CSS美化（文字，阴影，超链接，列表，渐变）
* 盒子模型
* 浮动
* 定位
* 网页动画（特殊效果）

![image-20210806221940366](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806221940366.png)



## CSS的发展史

* CSS 1.0
* CSS 2.0：DIV（块）+ CSS，提出了HTML 与 CSS 结构分离的思想，网页变得简单
* CSS 2.1：浮动、定位
* CSS 3.0：圆角、阴影、动画、、、浏览器兼容性



## 简单入门

**简单的CSS内部样式**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        h1{
            color: red;
        }
    </style>
</head>
<body>

<h1>CSS简单入门语法</h1>

</body>
</html>
```



**简单的CSS外部样式（建议使用此种规范）**

![image-20210809081454312](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809081454312.png)



```bash
 # 简单的CSS语法
 CSS选择器{
 	声明1;
 	声明2;
 	...
 }
```



**CSS的优势**

* 内容和表现分离
* 网页结构表现统一，可以实现复用
* 样式十分的丰富
* 建议使用独立于html的CSS文件
* 使用SEO，容易被搜索引擎收录



**CSS的三种样式**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

<!--    内部样式-->
    <style>
        h1{
            color: green;
        }
    </style>

    <link rel="stylesheet" href="css/style.css">

</head>
<body>
<!--行内样式：标签元素中定义一个style属性，编写样式-->
<h1 style="color: red">CSS样式</h1>
</body>
</html>
```

样式优先级：

1. 就近原则，即离标签越近，优先级越高
2. 后面的样式覆盖前面的样式
3. 指定的高于继承的



**外部样式的两种写法：**

* 链接式：

  ```html
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <link rel="stylesheet" href="css/style.css">
  
  </head>
  ```

  

* 导入式

  ```html
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <style>
          @import url(css/style.css);;
      </style>
  </head>
  ```

导入式式CSS 2.1 特有的写法，而链接式则是html 有的写法，链接式式同时加载html骨架以及css样式，而导入式则是先加载骨架，后加载样式。



## CSS的选择器

### CSS的基本选择器

* 标签选择器
* 类 选择器
* Id 选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
<h1 class="style1">标题1</h1>
<h1 class="style1">标题2</h1>
<h1 id="h1">标题3</h1>
<h1 id="h2">标题4</h1>

<p class="style1">P标签</p>
</body>
</html>
```

```css
h1{
    color: red;
}

/*
类选择器的格式
.class名{
}
*/
.style1{
    color: blue;
}

/*
id选择器格式
#id名{
}
*/
#h1{
    color: #02ff00;
}

#h2{
    color: #ff00d9;
}
```

**CSS样式注意事项：**

1. 标签选择器会选中页面中所有的此类型的标签，选中对其修饰
2. class可以被复用，归为一个类或者样式修饰一样的可以使用同一个class名
3. id选择器是全局唯一的，不可以被复用，只能修饰一个标签、
4. **优先级：不遵循就近原则，id选择器>class选择器>标签选择器**



### CSS的层次选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
<p>p1</p>
<p>p2</p>
<p>p3</p>
<p>p4</p>
<ul>
    <li>
        <p>p5</p>
    </li>
    <li>
        <p>p6</p>
    </li>
    <li>
        <p>p7</p>
    </li>
    <li>
        <p>p8</p>
    </li>
</ul>
</body>
</html>
```



1. 后代选择器

   ```css
   /*
   后代选择器
   */
   body p{
       color: red;
   }
   ```

   代表body 后面的所有的 p 标签

2. 子选择器

   ```css
   /*
   子选择器
   */
   body>p{
       color: red;
   }
   ```

   代表父元素下的子元素（一代）

3. 相邻兄弟选择器

   ```css
   /*
   相邻兄弟选择器
   */
   .test+p{
       color: red;
   }
   ```

   某个元素并列元素的后面一个

4. 通用选择器

   ```css
   /*
   通用选择器
   */
   .test~p{
       color: red;
   }
   ```

   class选中的元素后面的所有的同代的同类型元素



### 结构伪类选择器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="css/style.css">
    <title>Title</title>
</head>
<body>
<p>p1</p>
<p>p2</p>
<p>p3</p>
<p>p4</p>
<ul>

    <li>
        li1
    </li>
    <li>
        li2
    </li>
    <li>
        li3
    </li>
    <li>
        li4
    </li>
</ul>
</body>
</html>
```

```css
/*
选择第一个列表标签
*/
ul li:first-child{
    color: red;
}

/*
选择最后一个列表标签
*/

ul li:last-child{
    color: green;
}
```

```css
/*
选择当前元素的父元素，选中父元素的
第一个子元素，并且类型相同生效
*/
p:nth-child(1){

}
```

```css
/*
选中当前元素的父元素，并且选中父元素下
第n个此类型的子元素
*/
p:nth-of-type(1){

}
```



### 属性选择器（常用）

id + class 类型的选择器



```css
/*在p标签属性中，选中id或者class为test的标签*/
p[test]{
    color: red;
}

/*在p标签属性中，选中id或者class为test的标签*/
p[class="test"]{
    color: red;
}

/*在p标签属性中，选中class含有test的标签*/
p[class*="test"]{
    color: red;
}

/*a标签中，href属性以http开头的*/
a[href ^= "http"]{
    
}

/*a标签中，href属性以pdf结尾的*/
a[href$="pdf"]{
    
}
```



## 美化页面元素



### span标签

作用：特别突出的字，约定俗成用span套起来



### 字体样式

```css
/*
	font-family: 楷体; 字体样式
    color: red;	字体颜色
    font-size: 16px;	字体大小
    font-weight: bolder;	字体粗细
*/
p{
    font-family: 楷体;
    color: red;
    font-size: 16px;
    font-weight: bolder;
}

/*
font:字体的风格（粗体斜体）字体的粗细 字体的大小 字体的格式
*/
a{
    font:oblique bolder 12px 楷体;
}
```



### 文本样式

文本颜色

```css
p{
    color: #00FF00;
}
```

RGB颜色：00 00 00，各个位置的取值均为 0~F，red，green，blue。

RGBA颜色：0，0，0，0，前三个位置的取值为0~255，最后一个为0~1，即透明度



文本居中

```css
/*
text-align: center; 文本居中
*/
h1{
    text-align: center;
}
```

文本居左：left

文本居右：right



文本缩进

```css
/*
首行缩进2em（两个字符长度）
*/
.p1{
    text-indent: 2em;
}
```



文本行高

```css
.p2{
    line-height: 50px;
}
```



上中下三个划线

```css
/*下划线*/
h1{
    text-decoration: underline;
}

/*中划线*/
h1{
    text-decoration: line-through;
}

/*上划线*/
h1{
    text-decoration: overline;
}
```



超链接去下划线

```css
/*超链接去下划线*/
a{
    text-decoration: none;
}
```



### 超链接伪类

```css
a{
    /*去除下划线*/
    text-decoration: none;
    /*默认颜色*/
    color: black;
}
/*鼠标悬浮，颜色，即鼠标指在字体上
 */
a:hover{
    color: red;
}
/*鼠标点击颜色*/
a:active{
    color: green;
}
```



### 字体阴影

```css
/* 文字阴影：阴影颜色 水平偏移
垂直偏移 阴影半径
 */
.c1{
    text-shadow: red 10px 10px 2px;
}
```



### 列表样式

![image-20210809201000973](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809201000973.png)



### 背景颜色、背景图片



**背景图片**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>

<div></div>
<div class="div1"></div>
<div class="div2"></div>
<div class="div3"></div>

</body>
</html>
```

```css
div{
    width: 1200px;
    height: 1200px;
    border: 1px solid red;
    background-image: url("../source/img/03.jpeg");
}
.div1{
    /*水平平铺*/
    background-repeat: repeat-x;
}

.div2{
    /*竖直平铺*/
    background-repeat: repeat-y;
}

.div3{
    /*无平铺*/
    background-repeat: no-repeat;
}
```



### 渐变

渐变的网站：http://color.oulu.me/

```css
background-image: linear-gradient(to top, #9795f0 0%, #fbc8d4 100%);
```



## 盒子模型

![image-20210812082116356](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210812082116356.png)

* margin：外边距

* padding：外边距

* border：边框

### 边框

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
<div id="box">
    <h2>会员登陆</h2>
    <div>
        <form action="#">
            <div>
                <span>账号：</span>
                <input type="text">
            </div>
            <div>
                <span>密码：</span>
                <input type="password">
            </div>
            <div>
                <span>邮箱：</span>
                <input type="email">
            </div>
        </form>
    </div>
</div>
</body>
</html>
```

```css
body{
    /*很多东西都存在默认边框需要提前初始化为0*/
    margin: 0px;
}
#box{
    width: 300px;
    height: 150px;
    border: 1px solid green;
}
h2{
    font-size: 16px;
    background-color: red;
    color: white;
}

form{
    background-color: red;
}
div:nth-of-type(1) input{
    border: 1px solid black;
}
div:nth-of-type(2) input{
    border: 1px dashed #3200a5;
}
div:nth-of-type(2) input{
    border: 1px solid #0098c6;
}
```



### 内外边距

**左右居中**

```css
#box{
    width: 300px;
    height: 150px;
    border: 1px solid green;
    margin:0 auto
}
```

![image-20210812084258525](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210812084258525.png)

**顺序：顺时针顺序：上右下左，一个元素代表四个方向，两个元素代表上下、左右，四个元素按照顺序 上右下左**



### 圆角边框

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        /*
        border-radius: 左上 右上 右下 左下
        border-radius: 50px 10px 10px 5px
        */
        div {
            width: 500px;
            height: 500px;
            border: 10px solid red;
            border-radius: 50px 10px 10px 5px;
        }
    </style>
</head>
<body>
<div></div>
</body>
</html>
```

**圆圈：**



### 阴影

