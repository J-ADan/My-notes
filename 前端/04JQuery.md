# JQuery

JavaScript 与 JQuery ：

jQuery是一个封装了大量的JavaScript的库，里面存在了大量的JavaScript的函数



## jQuery公式

```js
// $(选择器).函数名(变量)
$(selector).action()
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="js/jquery-3.6.0.js"></script>
</head>
<body>
<a href="" id="test">点我</a>

<script>
    $('#test').click(function () {
        alert("hello JQuery");
    })
</script>
</body>
</html>
```

![image-20210811212046876](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811212046876.png)



## JQuery 选择器

```js
document.getElementById();
document.getElementsByClassName();
document.getElementsByTagName();
```

JavaScript原生选择器，选择器少，麻烦不好记

```js
$('p').click(); // 标签选择器
$('#p').click(); //id选择器
$('.p').click(); // 类选择器
```

jQuery工具站：https://jquery.cuishifeng.cn/



## JQuery事件

![image-20210811212651754](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210811212651754.png)

```js
$('a').mousedown();//鼠标的按下操作
    $('a').mouseleave();//鼠标的离开操作
    $('a').mousemove();//鼠标的移动操作
    $('a').mouseover();//鼠标的点击结束操作
```



**获取鼠标的坐标：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #rear{
            width: 600px;
            height: 600px;
            border: 1px solid green;
        }
    </style>
    <script src="js/jquery-3.6.0.js"></script>
</head>
<body>
mouse: <span id="mousexy"></span>
<div id="rear">

</div>

<script>
    // 当前页面加载完毕的响应事件
    // $(document).ready(function () {
    //
    // })

    $(function () {
        $('#rear').mousemove(function (e) {
            $('#mousexy').text('X: ' + e.pageX + 'Y: ' + e.pageY)
        })
    })
</script>
</body>
</html>
```

## 操作DOM元素

```js
$('.uul li[name=python]').text()//获取值
$('.uul li[name=python]').text('123')//设置值
    
$('#lli').html()//获取值
$('#lli').html('<strong>123</strong>')//设置值
```

操作css

```js
$('.uul li[name=python]').css('color','red')
// 元素的显示与隐藏
$('.uul li[name=python]').show()
$('.uul li[name=python]').hide()
```



娱乐测试：

```js
$(window).height()
$(window).width()
```

