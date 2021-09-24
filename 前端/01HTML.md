# HTML（Hyper Text Markup Language）

超文本标记语言

超文本包括：文字、图片、音频、视频、动图等。

**世界知名的浏览器都支持HTML5，天然的跨平台的语言**。

![image-20210804212112215](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210804212112215.png)

**W3C：** World Wide Web Consorttium 万维网联盟。Web技术领域最权威和具有影响力的国际中立性标准机构。

W3C的标准包括

1. 结构化标准语言（HTML、XML）
2. 表现标准语言（CSS）
3. 行为标准（DOM（文档对象模型）、ECMAScript（JavaScript））

**HTML的重点是在表单的操作**



a标签的作用一般是链接标签，即跳转到别的页面或别的网址所用的标签。

```html
<!--!DOCTYPE html 设置使用的规范-->
<!DOCTYPE html>
<!-- 网页的总标签-->
<html lang="en">
<!--head标签代表网页的头部-->
<head>
<!--    meta 标签是一个描述性标签，用来描述网站的一些信息-->
    <meta charset="UTF-8">
<!--    网页的关键词-->
    <meta name = "keywords" content="第一个网页">
<!--    网页的描述-->
    <meta name="description" content="用来练习">
    <!--代表网页的标题-->
    <title>Demo01</title>
</head>
<!--网页的主体部分，网页的显示部分就是在此书写-->
<body>
Hello World!
</body>
</html>
```

![image-20210804215546364](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210804215546364.png)

只含有一个标签的称之为 **开放标签（自闭和标签）**，两个标签的 即 <></>的，被称之为 **闭合标签**



## 基本标签

**标题标签**

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo02</title>
</head>
<body>
<!--标题标签-->
<h1>一级标签</h1>
<h2>二级标签</h2>
<h3>三级标签</h3>
<h4>四级标签</h4>
<h5>五级标签</h5>
<h6>六级标签</h6>

</body>
</html>
```



![image-20210804220007596](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210804220007596.png)



**段落与换行标签**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo02</title>
</head>
<body>
<!--段落标签-->
<p>晚风中闪过 几帧从前啊</p>

<p>飞驰中旋转 已不见了吗</p>

<p>远光中走来 你一身晴朗</p>

<p>身旁那么多人 可世界不声 不响</p>
<!--换行标签-->
晚风中闪过 几帧从前啊 <br/>
飞驰中旋转 已不见了吗<br/>
远光中走来 你一身晴朗<br/>
身旁那么多人 可世界不声 不响<br/>
</body>
</html>
```

![image-20210805074924583](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210805074924583.png)

**水平线标签**

```html
<!--水平线标签-->
<hr/>
```

![image-20210805085238351](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210805085238351.png)

**水平线标签可以随着浏览器的缩放而缩放**



**字体样式标签**

粗体与斜体

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo02</title>
</head>
<body>
<!--粗体与斜体-->
<strong>晚风中闪过 几帧从前啊</strong>
<em>飞驰中旋转 已不见了吗</em>
</body>
</html>
```

![image-20210805085511294](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210805085511294.png)

![image-20210809110647576](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809110647576.png)



**特殊符号**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo02</title>
</head>
<body>
<!--html中的特殊符号-->
空      格：
空&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;格 <br/>

大于号：&gt; <br/>
小于号：&lt; <br/>
版权符号:&copy; <br/>
</body>
</html>
```

![image-20210805090031678](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210805090031678.png)

## 图像标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Demo02</title>
</head>
<body>
<!--
src(必填)：代表图片的路径
相对路径：与当前html文件的相对路径（推荐使用）
绝对路径：在盘符下的绝对路径
alt(必填)：图片名字，当图片啊不能加载时显示的文字
title：悬停文字，当鼠标悬停图片上方显示的文字
width：设置图片在网页中的宽度
height：设置图片在网页中的高度
-->
<img src="resource/image/01.jpg" alt="简笔少女" title="我的jpg" width="300" height="300">
</body>
</html>
```

![image-20210809104712581](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809104712581.png)



## 链接标签

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<!--锚链接，让点击时间直接跳转到本页面或者其他页面的某个位置-->
<a name="top"></a>
<!--链接标签-->
<!--
href:跳转到某个地址页面（必填）
target="_blank":代表新打开一个页面来跳转
target="_self":在自己的页面打开
-->
<a href="https://www.baidu.com" target="_self">点击我跳转到百度</a>
<a href="https://www.csdn.net/">
    <img src="resource/image/01.jpg" alt="简笔少女" title="我的jpg" width="300" height="300">
</a>
<!--锚点-->
<a href="#top"></a>
</body>
</html>
```

![image-20210809103017474](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809103017474.png)



### 功能型链接

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>

<!--邮件标签-->
<a href="mailto:18254874523@163.com">点击给我发邮件</a>

<!--QQ推广标签-->
<a target="_blank" href="http://wpa.qq.com/msgrd?v=3&uin=&site=qq&menu=yes">
    <img border="0" src="http://wpa.qq.com/pa?p=2::53" alt="点击加我好友" title="点击加我好友"/>
</a>

</body>
</html>
```



## 行内元素与块元素

* 块元素：无论内容的多少，该元素独占一行
* 行内元素：内容撑开宽度，左右都是行内元素的可以排在一行



## 列表

定义：列表就是信息资源的一种展示方式，它可以使信息结构化和条理化，并以列表的样式显示出来，以便浏览者能更快捷的获得相应的信息。

分类

* 无序列表
* 有序列表
* 定义列表



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!-有序列表
应用范围：试卷，问答，调查问卷....
-->
<ol>
    <li>java</li>
    <li>python</li>
    <li>C/C++</li>
    <li>前端</li>
    <li>运维</li>
</ol>

<!--无序列表
应用范围：导航，侧边栏
-->
<ul>
    <li>java</li>
    <li>python</li>
    <li>C/C++</li>
    <li>前端</li>
    <li>运维</li>
</ul>

<!--自定义列表
dt:列表名称
dd:列表内容
-->
<dl>
    <dt>学科</dt>

    <dd>java</dd>
    <dd>python</dd>
    <dd>C/C++</dd>
    <dd>前端</dd>

    <dt>位置</dt>
    <dd>山东</dd>
    <dd>泰安</dd>
    <dd>天宝</dd>
</dl>
</body>
</html>
```

![image-20210805222721857](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210805222721857.png)

## 表格标签

表格的作用：简单通用，结构稳定。

表格的基本结构

* 单元格
* 行
* 列
* 跨行
* 跨列

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--表格标签
table
tr:行
td:列
border="1px":代表行宽
-->

<table border="1px">
    <tr>
        <td>1-1</td>
        <td>1-2</td>
        <td>1-3</td>
        <td>1-4</td>
    </tr>
    <tr>
        <td>2-1</td>
        <td>2-2</td>
        <td>2-3</td>
        <td>2-4</td>
    </tr>
    <tr>
        <td>3-1</td>
        <td>3-2</td>
        <td>3-3</td>
        <td>3-4</td>
    </tr>
</table>
</body>
</html>
```

![image-20210806100224922](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806100224922.png)

**跨行跨列**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--表格标签
table
tr:行
td:列
border="1px":代表行宽
-->

<table border="1px">
    <tr>
<!--        跨列-->
        <td colspan="4">1-1</td>
    </tr>
    <tr>
<!--        跨行-->
        <td rowspan="2">2-1</td>
        <td>2-2</td>
        <td>2-3</td>
        <td>2-4</td>
    </tr>
    <tr>
        <td>3-1</td>
        <td>3-2</td>
        <td>3-3</td>
    </tr>
</table>
</body>
</html>
```

![image-20210806100406388](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806100406388.png)

## 视频和音频

* 视频元素：video
* 音频元素：audio



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--视频
src:文件路径（必填）
controls:进度条显示
autoplay:自动播放
-->
<video src="resource/video/白丝鹿乃.mp4" controls autoplay></video>

<!--音频
src:文件路径（必填）
controls:进度条显示
autoplay:自动播放
-->
<audio src="resource/audio/她的笑.mp3" controls autoplay></audio>
</body>
</html>
```



## 页面结构分析

![image-20210806101959083](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806101959083.png)

## iframe内联框架

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!--iframe标签，内联框架
src:地址
wigth:宽度
heigth:高度
-->
<iframe src="//player.bilibili.com/player.html?aid=55631961&bvid=BV1x4411V75C&cid=97257967&page=11"
        scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true">
</iframe>


<iframe src="https://www.csdn.net/" frameborder="0" width="800px" height="1000px"></iframe>

</body>
</html>
```

**通过a标签，iframe注入**

```html
<iframe src="" frameborder="0" name="ifa"></iframe>
<a href="https://www.csdn.net/" target="ifa">点击跳转</a>
```



## 表单语法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--表单语法
action:可以是提交到一个网站地址，也可以是一个请求处理的地址
method:请求提交的方法
get:可以在url中看到我们提交的表单数据，不安全，但是高效
post：安全，但是效率低，可以传输大文件
-->
<form action="Demo07.html" method="get">
    <p>账号：
        <input type="text" name="username">
    </p>
    <p>
        <!--autofocus 自动聚焦-->
        密码：<input type="password" name="psw" autofocus>
    </p>
    <p>
        <input type="submit">
        <input type="reset">
    </p>
</form>
</body>
</html>
```

**get与post区别**

get:可以在url中看到我们提交的表单数据，不安全，但是高效
post：安全，但是效率低，可以传输大文件

![image-20210809140128829](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809140128829.png)



![image-20210806195319129](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806195319129.png)

![image-20210809141546927](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210809141546927.png)



## 单选框

```html
    <p>
<!--        单选框
            type="radio"
            value="boy":单选框的值
            name:分组，在一个组内才可以只能选其一
-->
        <input type="radio" value="boy" name="sex">男
        <input type="radio" value="girl" name="sex">女
    </p>
```



## 按钮、多选框

```html
<!--    多选框
type="checkbox"
checked 默认选中
-->
    <p>
        <input type="checkbox" value="sleep" name="hobby">睡觉
        <input type="checkbox" value="eat" name="hobby" checked>吃饭
        <input type="checkbox" value="code" name="hobby">敲代码
        <input type="checkbox" value="chat" name="hobby">聊天
        <input type="checkbox" value="game" name="hobby">打游戏
    </p>

<!--    按钮标签
type="button" 按钮
type="image" 图像按钮
type="submit" 提交按钮
type="reset" 重置按钮
-->
    <p>
        <input type="button" name="but1" value="点击变长">
        <input type="image" src="resource/image/01.jpg">
    </p>
    <p>
        <input type="submit">
        <input type="reset">
    </p>
```



## 列表框、文本域

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>

<p>
<!--        select列表标签
name：列表名称，get，post提交时候用到的列表名称
selected:默认选择
-->
    <select name="列表名称">
        <option value="China">中国</option>
        <option value="US">美国</option>
        <option value="English">英国</option>
        <option value="Russia" selected>俄罗斯</option>
    </select>
</p>

<!--文本域
name：文本域名称
clos：列
rows：行
-->
<p>
    <textarea name="textarea" cols="30" rows="10"></textarea>
</p>

<!--文件域-->
<p>
    <input type="file" name="files">
</p>
</body>
</html>
```



## 一些其他的功能性标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--邮箱验证-->
<p>
    邮箱：
    <input type="email" name="email">
</p>

<!--URL验证-->
<p>
    URL：
    <input type="url" name="url">
</p>

<!--数字验证
step:步长
-->
<p>
    商品数量：
    <input type="number" name="number" step="1">
</p>

<!--滑块-->
<p>
    音量：
    <input type="range" name="range" step="2">
</p>

<!--搜索框-->
<p>
    请输入：
    <input type="search" name="search">
</p>
</body>
</html>
```

**这些功能性标签，会带有一些特殊的验证，但是只是初级的验证**



## 表单的应用

* 隐藏域
* 只读
* 禁用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--隐藏域 hidden-->
<p>
    密码：
    <input type="password" hidden>
</p>

<!--只读 readonly-->
<p>
    账号：
    <input type="text" readonly value="123456">
</p>

<!--禁用 disabled-->
<p>
    <input type="radio" value="boy" name="sex" disabled>男
    <input type="radio" value="girl" name="sex">女
</p>

<!--增强鼠标的可用性-->
<p>
    <label for="mark">你点我试试</label>
    输入：
    <input type="text" id="mark">
</p>
</body>
</html>
```

**隐藏域虽然将一些表单的输入框等隐藏，但是在提交请求时，仍会提交他的属性值，所以可以用来设置一些默认值，label标签的作用主要是当鼠标点击文字时，自动唤醒某个输入框的输入**



## 表单的初级验证

常用方式：

* placeholder：提示信息
* required：非空判断
* pattern：正则表达式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<form action="">
    <p>
        用户名<input type="text" required placeholder="请输入用户名">
    </p>
    <p>
        <input type="password" required>
    </p>
    <p>
        <input type="submit">
    </p>
</form>
</body>
</html>
```

![image-20210806210129098](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210806210129098.png)



## HTML的全局属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div id="d1" class="d2" style="" title="" name="">
    
</div>

</body>
</html>
```

id:元素的唯一标识，规定元素的唯一性

class：规定元素的一个或者多个类名

style：规定元素的CSS样式

title：规定元素的额外属性



## 块级元素标签

1. 总是独占一行，表现为另起一行开始，而且其后元素也必须另起一行显示
2. 宽度（width）、高度（height）、内边距（padding）、外边距（margin）都可控制
3. 块级元素即使设置了宽度，仍是独占一行的





## 内联元素标签

1. 和相邻的内联元素在同一行
2. 宽度，高度，无法改变，就是内部文字图片的大小
3. 水平方向padding，margin-left，margin-right都产生边距效果，但是竖直方向的margin-top，margin-bottom都不会产生边距效果
