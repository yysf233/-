# WebAPI

<img src="_media\dom\dom_daohang.png" alt="DOM与js的关系" style="zoom:50%;" />



## DOM：文档对象模型

​	

DOM是W3C组织推荐的处理可扩展标记语言的标准编程接口。

W3C已经定义了一系列的DOM接口，通过这些接口可以改变王爷的内容、结构和样式。

### 1.DOM

#### 1.1 DOM树

<img src="_media/dom/dom01.png" alt="">

* 文档：一个页面就是一个文档，DOM中使用document表示
* 元素：页面中所有标签都是元素，DOM中使用element表示
* 节点：网页中所有内容都是节点（标签、属性、文本、注释等等），DOM中使用node表示。

#### 1.2 获取元素

##### 1.2.1 如何获取页面元素

* 根据ID获取
* 根据标签名获取
* 通过H5新增方法获取
* 特殊元素获取

##### 1.2.2 根据ID获取元素

​	使用getElementById()方法获取带有ID的元素对象。

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
    
    <div id="num">123456</div>
    <script>
        //1.因为文档页面从上往下加载，所以先得有标签，所有script写道标签下面
        //2.get 获得element元素by 通过驼峰命名法
        //3.参数：id是大小写敏感的字符串
        //4.饭会一个匹配到ID的额DOM element对象。如果没找到，则返回null。
        console.log(a);//<div id =num>123456</div>
        console.log(typeof a);//返回的是一个元素对象“object”
        console.dir(a);//打印返回的元素对象，更好的查看里面的属性和对象
    </script>
</body>
</html>
```

##### 1.2.3 根据标签名获取元素

通过getElementsByTagName()获取某些元素

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
    <ul>
        <li>111</li>
    <li>111</li>
    <li>111</li>
    <li>111</li>
    <li>111</li>
    </ul>
    <ol id="id">
        <li>113</li>
        <li>11123</li>
        <li>1112341</li>
        <li>111241</li>
        <li>11141</li>
    </ol>
    <script>
        //返回的是获取过来元素对象的集合，以伪数组的形式存储的
        var a = document.getElementsByTagName('li');
        console.log(a);
        console.log(a[0]);
        //2.我们想要一次打印里面的元素对象可以使用遍历的形式
        for(var b = 0;b<a.length;b++)
        {
            console.log(a[b]);
        }
        //3.如果页面中只有一个li 返回的还是伪数组的
        //4.如果页面中没有这个元素，返回的空的伪数组
        var ol = document.getElementById('id');
        console.log(ol.getElementsByTagName('li'));
        //5.element.getElementsByTagName('标签名')；父元素必须是指定的单个元素
    </script>
</body>
</html>
```

##### 1.2.4 H5新增方法获取（不兼容IE8以下）

1.getElementsByClassName根据类名获得某些元素的集合

2.querySelector 返回指定选择器的第一个元素对象(不考虑兼容时十分推荐)

3.querySeletorAll()返回指定选择器的所有元素对象集合

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
    <div class="box">我是个盒子</div>
    <div class="box">我是个盒子2</div>
    <div id="nav">
        <ul>
            <li>首页</li>
            <li>产品</li>
        </ul>
    </div>
    <script>
        //1.getElementsByClassName根据类名获得某些元素的集合
        var boxs = document.getElementsByClassName('box');
        console.log(boxs);
        //2.querySelector 返回指定选择器的第一个元素对象
        var firstbox = document.querySelector('.box');//根据Class选择器选择
        console.log(firstbox);
        var nav = document.querySelector('#nav');//根据ID选择器选择
        console.log(nav);
        var li= document.querySelector('li');
        console.log('li');
        //3.querySeletorAll()返回指定选择器的所有元素对象集合
        var allbox = document.querySelectorAll('.box');
        console.log(allbox);
        var li1 = document.querySelectorAll('li');
        console.log(li1);
    </script>
</body>
</html>
```

##### 1.2.5 获取特殊元素

* 获取HTML和body元素

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
        <script>
            //1.获取body元素
            var body = document.body;
            console.log(body);
            console.dir(body);//显示body元素中的属性
            //2.获取html元素
            var html = document.documentElement;
            console.log(html);
            console.dir(html);
        </script>
</body>
</html>
```

#### 1.3 事件基础

##### 1.3.1 事件概述

JS使我们有能力创建动态页面，而事件时可以被JS侦测到的行为

* 简单理解：所谓事件就是触发响应机制

网页中的每个元素都可以产生某些可以触发JS响应机制的事件。例如，我们可以在用户点击某按钮时产生一个时间，然后去执行某些操作。

##### 1.3.2 事件三要素

事件三要素：事件源，事件类型，事件处理程序

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
        
        <button id="btn">111</button>
        <script>
            var btn = document.getElementById('btn');
            //1.事件由三部分组成： 事件源，事件类型，事件处理程序
            //1.1事件源：事件被触发的对象
            //1.2事件类型：如何触发
            //1.2事件类型：如何触发，什么事件，比如鼠标点击（onclick）还是鼠标经过还是键盘按下
            //1.3事件处理程序：通过函数赋值的方法完成
            btn.onclick = function()
            {
                alert('23333');
            }
        </script>
</body>
</html>
```

##### 1.3.3 执行事件的步骤

1.获取事件源

2.注册事件（绑定事件）

3.添加事件处理程序（采取函数赋值形式）

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
    <div id="id">123123123</div>
    <script>
        var div = document.getElementById('id');
        div.onclick = function()
        {
            console.log('2333333333');
        }
    </script>
</body>
</html>
```

##### 1.3.4 常见的鼠标事件

* onclick 鼠标点击触发事件
* onmouseover 鼠标经过触发
* onmouseout 鼠标离开触发
* onfocus 获得鼠标焦点触发
* onblur 失去鼠标焦点触发
* onmousemove 鼠标移动触发
* onmousedown 鼠标按下触发
* onmouseup 鼠标弹起触发

##### 1.3.5 案例：分析事件三要素

先分析，后写事件

#### 1.4 操作元素

JavaScript的DOM操作可以改变网页内容、结构和样式，我们可以利用DOM操作来改变元素里面的内容属性等，注意以下都是属性。

##### 1.4.1 改变元素内容

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        div {
            width: 300px;
            height: 50px;
            background-color: cornflowerblue;
            line-height: 50px;
            text-align: center;
            font-size: 50px;
        }
    </style>
</head>
<body>
        <button id="btn">我是个按钮</button>
        <div id="time">时间</div>
        <script>
            //当点击按钮时，div里面的文字内容会发生变化
            var dianji = document.getElementById('btn');
            var shijian = document.getElementById('time');
            dianji.onclick = function()
            {
                shijian.innerText = '2021-1-25';
            }
        </script>
</body>
</html>
```

#####  1.4.2 innerText和innerHTML的区别

​	innerHTML 可以识别HTML标签，从起始位置到终止位置，但他去除HTML标签，同时空格和换行也会去除掉。

​	innerText 不能识别HTML标签，同时会保留起始位置到终止位置的全部内容，包括HTML标签以及空格和换行。

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        div {
            width: 900px;
            height: 50px;
            background-color: cornflowerblue;
            line-height: 50px;
            text-align: center;
            font-size: 50px;
            margin: auto;
        }
    </style>
</head>
<body>
        <div></div>
        <script>
            var neirong = document.querySelector('div');
            //neirong.innerText = '<strong>今天是</strong>2021';
            //innerText不识别HTML标签
            neirong.innerHTML = '<strong>今天是：</strong>2019';
            //innerHTML可以识别html标签
        </script>
</body>
</html>
```

##### 1.4.3 操作元素常用的属性

* #### innerText、innerHTML改变元素内容

* #### src、herf

* #### id、alt、title

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
        <button id="blue">点一下白色。点一下蓝色</button>
        <button id="black">黑色</button>
        <script>
            var blue_time = 1;
            var blue = document.getElementById('blue');
            var black = document.getElementById('black');
            blue.onclick = function()
            {
                blue_time++;
                if(blue_time%2==0)
                {
                    blue.style.backgroundColor = "white";
                }else
                {
                    blue.style.backgroundColor = "blue";
                }
                
            }
            black.onclick = function()
            {
                black.style.backgroundColor = "black";
            }
        </script>
</body>
</html>
```

##### 1.4.4 案例：分时间问候

​	根据不同的时间，显示不同的文字图画

​	未使用图片属性<img src = "">

```html
//根据系统的不同时间判断，需要日期时间判断
//利用多分枝语句来设置不同的图片
//需要一个图片，并且根据实际按修改图片，需要用到操作元素的src属性
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
        <div><strong>下午好！</strong></div>
        <script>
            var div = document.querySelector('div');
            var time = new Date();
            var hours = time.getHours();
            if(hours<=12)
            {
                div.innerHTML = '<strong>早上好！夜之城！</strong>';
            }else if(hours<18)
            {
                div.innerHTML = '<strong>下午好！夜之城！</strong>'
            }else
            {
                div.innerHTML = '<strong>晚上好！夜之城！</strong>'
            }
        </script>
</body>
</html>
```

##### 1.4.5 表单元素的属性操作

利用DOM可以操作如下表单元素的属性：

<type>：类型属性

<value>：内容属性

<checked>：选择属性

<selected>：选择属性

<disadled>：使用属性

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
        <button id="btn">我是个按钮</button>
        <input type="text" id="inputkuang" value="写点啥进去">
        <script>
            var btn1 = document.getElementById('btn');
            var input1 = document.getElementById('inputkuang');
            btn1.onclick = function()
            {
                //input1.innerHTML = '你点了按钮哦';
                //表单里面的值，是通过value属性进行修改的；
                
                input1.value = '你点了按钮哦';
                //如果想用某个表单被禁用，不能再点击disabled，想要这个按钮被禁用
                //btn1.disabled = true;
                this.disabled = true;
                //此处this指向的是函数调用者
            }
        </script>
</body>
</html>
```

##### 1.4.6 仿狗东隐藏密码显示密码案例

```html
	<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        .box
        {
            position: relative;
            width: 400px;
            border-bottom: 1px solid rgb(137, 137, 137);
            margin: 100px auto;
        }
        .box input
        {
            width: 370px;
            height: 30px;
            border: 0;
            outline: none;
        }
        .box img{
            position: absolute;
            top:5px;
            right: 5px;
            width:24px;
        }
    </style>
</head>
<body>
       <div class="box">
           <label for="">
               <img src="imgs/close.png" id="eye">
           </label>
           <input type="password" id="Pwd">
       </div>
       <script>
        console.log('ID获取成功');
        window.onload=function()
        {
        //1.获取元素
        var eye = document.getElementById('eye');
        console.log('ID获取成功');
        var pwd = document.getElementById('Pwd');
        console.log('ID获取成功');
        //2.注册事件 处理程序
        eye.onclick = function()
        {
            this.src = "imgs/open.png";
            pwd.type = 'text';
            console.log('被点击');
        }
        }
    </script>
</body>
</html>
```



##### 1.4.7 样式属性操作

我们可以通过JS修改元素的大小、颜色、位置等样式

* element.style 行内样式操作：用作少部分修改
* element.classname 类名样式操作：用作大量修改

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: salmon;
        }
    </style>
</head>
<body>
    <div>23333</div>
    <button id="btn">按钮</button>
    <script>
        var color = document.querySelector('div');
        var btn = document.getElementById('btn');
        btn.onclick = function()
        {
            color.style.backgroundColor = 'purple';
        }
    </script>
</body>
</html>
```

##### 1.4.8 仿淘宝关闭二维码案例

<核心思路>：利用样式里的显示和隐藏完成，display:none隐藏元素和display:block显示元素。

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        .box 
        {
            position: relative;
            width: 74px;
            height: 88px;
            border: 1px solid #ccc;
            margin: 100px auto;
            font-size: 12px;
            background-color: blueviolet;
        }
        .box img{
            width: 60px;
            margin-top: 5px;
        }
        .close_btn
        {
            position: absolute;
            top: -1px;
            left: -16px;
            width: 14px;
            height: 14px;
            border: 1px solid #ccc;
            line-height: 14px;
        }
    </style>
</head>
<body>
    <div class="box">淘宝二维码
        <img src="imgs/open.png" alt="">
        <i class="close_btn">x</i>
    </div>
    <script>
        window.onload = function()
        {
            //1.获取元素
            var btn = document.querySelector('.close_btn');
            var erweima = document.querySelector('.box');
            btn.onclick = function()
            {
                erweima.style.display = 'none';
            }
        }
    </script>
</body>
</html>
```

##### 1.4.10 显示隐藏文本框内容

​	首先表单需要两个新事件，获得焦点onfocus和失去焦点onblur。

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        input{
            color: #999999;
        }
    </style>
</head>
<body>
<div>
    <input type="text" value="手机">
    <script>
        var a = document.querySelector('input');
        a.onfocus = function()
        {
            console.log('得到焦点');
            this.value = '';
        }
        a.onblur = function()
        {
            console.log('失去焦点');
            this.value = '手机';
        }
    </script>
    </div>
</body>
</html>
```

##### 1.4.11 用className设置样式属性

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        input{
            color: #999999;
        }
        .change {
            background-color: purple;
            color: #fff;
            font-size: 25px;
            margin-top: 100px;
        }
    </style>
</head>
<body>
<div>
    <div>
        文本
    </div>
    <script>
        var a = document.querySelector('div');
        a.onclick = function()
        {
            //element.className属性可以修改元素的类名
            this.className = 'change';
            //element.style太低效
            // this.style.backgroundColor = 'purple';
            // this.style.color = '#fff';
            // this.style.fontSize = '25px';
            // this.style.marginTop = '100px';
        }
    </script>
    </div>
</body>
</html>
```

##### 1.4.12 密码框提示

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    
</head>
<body>
<div class="register">
    <input type="text" class="ipt">
    <p class="message">请输入6~16位密码</p>
</div>
    <script>
        var ipt = document.querySelector('input');
        var message = document.querySelector('p');
        //注册事件 失去焦点
        ipt.onblur = function()
        {
            //根据表单里面之的长度
            if(ipt.value.length>16||ipt.value.length<6)
            {
                //表单内容要使用this.value
                message.innerHTML = '密码长度不符合规范';
            }
        }
    </script>

</body>
</html>
```

##### 1.4.13 操作元素总结

<img src="_media/dom/dom02.png">


##### 1.4.14 百度换皮肤效果

<img src="_media/dom/dom03.png">

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        body {
            background:url(imgs/mercy.png0) no-repeat center top;
        }
        li {
            list-style: none;
        }
        .baidu {
            overflow: hidden;
            margin: 100px;
            background-color: #fff;
            width: 410px;
            padding-top: 3px;
        }
        .baidu li {
            float: left;
            margin: 0 1px;
            cursor: pointer;
        }
        .baidu img {
            width: 200px;
        }
    </style>
</head>
<body>
    <ul class="baidu">
        <li id="mercy"><img src="imgs/0.png" alt=""></li>
        <li id="yexiu"><img src="imgs/1.jpg" alt=""></li>
        <li id="guidao"><img src="imgs/2.jpg" alt=""></li>
        <li id="bilibili"><img src="imgs/3.png" alt=""></li>
    </ul>
    <script>
        var imgs = document.querySelector('.baidu').querySelectorAll('img');
        for(var i = 0;i<imgs.length;i++)
        {
            imgs[i].onclick = function()
            {
                document.body.style.backgroundImage = 'url('+this.src+')';
            } 
        }
    </script>
</body>
</html>
```

##### 1.4.15 获取自定义属性值

* element.属性  获取属性值；
* element.getAttribute('属性')；

**区别**：

第一种：获取内置属性值（元素本身自带的属性）eg:class、id等.....

第二种：主要获得自定义的属性（标准），程序员自定义的属性；

可以添加自定义属性的值，通过添加自定义属性到元素中去像id class等等；

````html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    
</head>
<body>
    <div id="demo"></div>
    <script>
        var div = document.querySelector('div');
        //1.获取元素的属性值
        //（1）element属性
        console.log(div.id);
        //2.element.getATTRIBUTE('属性')；
        console.log(div.getAttribute('id'));
        //程序员自定义的属性叫自定属性
    </script>
</body>
</html>
````

**2.设置属性值：**

* `element.属性 = "值"；`
* `<element.setAttribute('属性','值')>`

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    
</head>
<body>
    <div id="demo"></div>
    <script>
        var div = document.querySelector('div');
        div.id = 'test';
        div.setAttribute('class','demo233');
        div.setAttribute('index',2);
        console.log(div.getAttribute('index'));//2
        console.log(div.id);//demo
        console.log(div.getAttribute('class'));//demo233
    </script>
</body>
</html>
```



**3.移除属性值**

* `elment.removeAttribute('属性')`

```javascript
        div.removeAttribute('index');
        console.log(div.getAttribute('index'));
```

##### 1.4.16 Tab栏切换案例（自定义属性的应用）

<img src = "_media/dom/dom04.png">

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        li {
            list-style-type: none;
        }
        
        .tab {
            width: 978px;
            margin: 100px auto;
        }
        
        .tab_list {
            height: 39px;
            border: 1px solid #ccc;
            background-color: #f1f1f1;
        }
        
        .tab_list li {
            float: left;
            height: 39px;
            line-height: 39px;
            padding: 0 20px;
            text-align: center;
            cursor: pointer;
        }
        
        .tab_list .current {
            background-color: #c81623;
            color: #fff;
        }
        
        .item_info {
            padding: 20px 0 0 20px;
        }
        
        .item {
            display: none;
        }
        
    </style>
</head>
<body>
    <div class="tab">
        <div class="tab_list">
            <ul>
                <li class="current">商品介绍</li>
                <li>规格与包装</li>
                <li>售后保障</li>
                <li>商品评价（50000）</li>
                <li>手机社区</li>
            </ul>
        </div>
        <div class="tab_con">
            <div class="item" style="display: block;">
                商品介绍模块内容
            </div>
            <div class="item">
                规格与包装模块内容
            </div>
            <div class="item">
                售后保障模块内容
            </div>
            <div class="item">
                商品评价（50000）模块内容
            </div>
            <div class="item">
                手机社区模块内容
            </div>

        </div>
    </div>
    <script>
        //1.模块选项卡点以一个一个遍恒红色，其余的不变
        //。获取元素
        var tab_list = document.querySelector('.tab_list');
        var list = tab_list.querySelectorAll('li');
        var items = document.querySelectorAll('.item');
        for(var i = 0;i<list.length;i++)
        {
            //开始给5个li设置索引号
            list[i].setAttribute('index',i);
            list[i].onclick = function()
            {
                //干掉所有人:其余的li清除掉class这个类
                for(var i = 0;i<list.length;i++)
                {
                    list[i].className = '';
                    items[i].style.display = 'none';
                    //清除所有人
                }
                //留下我自己
                this.className = 'current';
                //下面的模块内容，会跟随上面的选项卡变化。所以下面模块的变化写到点击选项卡里面
                //2.下面的显示内容模块
                var index = this.getAttribute('index');//显示刚才添加的index属性
                console.log(index);
                //当我们点击tab_list里面的某个小li，让tab_con里面对应序号的内容显示出来（核心思想）
                items[index].style.display = 'block';
            }
        }
    </script>
</body>
</html>
```

##### 1.4.17 H5自定义属性

​		**自定义属性的目的：是为了保存并使用数据。有些数据可以保存到页面中而不用保存到数据库中**

​		自定义属性的获取是通过：`elment.getAttribute('属性')`获取

​		但是有些自定义属性很容易引起歧义，不容易判断是元素的内置属性还是自定义属性。

#### 1.5 节点操作

##### 1.5.1 为什么学习节点操作

**获取元素常用方式：**

**1.**利用DOM提供的方法获取元素

<img src = "_media/dom/dom05.png">

**2.**即将学习：**利用节点的层次关系获取元素**

* 利用父子兄关系获取元素
* 逻辑性强，但是兼容性稍差

**两种方法都能获取元素，但是节点更简单**

##### 1.5.2 节点概述

​		网页中的***所有内容***都是节点，在DOM中节点使用node表示。

​		HTML、DOM树中的所有节点均可以通过JavaScript进行访问，所有HTML元素（节点）均可被修改，也可以被删除。

​		一般的，节点至少拥有`nodeType:节点类型`、`nodeName:节点名称`、`nodeValue：节点值`这三个基本属性。

* 元素节点`nodeType`为 1 
* 属性节点`nodeType`为 2 
* 文本节点``nodeType`为 3（文本包含文字、空格、换行等等）

***在实际开发中：节点的操作主要都是针对元素节点***

##### 1.5.3 节点层级

利用DOM树可以把节点划分为不同的岑寂关系，常见的是**父子兄层级关系**。

<img src = "_media/dom/dom_daohang.png">

**1.父级节点**

`node.parentNode`

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
    <div class="aaa">
        <span class="bbb"></span>
    </div>
    <script>
        var bbb = document.querySelector('.bbb');
        var aaa = document.querySelector('.aaa');
        console.log(aaa);
        console.log(bbb.parentNode);//parent.nodeNode只能找到距离bbb最近的父节点，找不到返回null
    </script>
</body>
</html>
```

**2.子节点**

`parentNode.childNode(标准)`

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        var lis = ul.querySelectorAll('li');
        //1.子节点
        //childNode 柏寒的所有的节点包含元素节点、文本节点等等
        //文本节点的节点类型是3
        //元素节点的节点类型是1
        //如果想要只获得里面的元素节点，则需要专门处理，所以我们一般不提倡使用
        for(var i = 0;i<ul.childNodes.length;i++)
        {
            if(ul.childNodes[i].nodeType==1)
            console.log(ul.childNodes[i]);
        }
    </script>
</body>
</html>
```

`parentNode.children(非标准)`

这是一个只读属性，返回所有子元素节点。他**只返回元素节点**，**其余节点不返回**（重点掌握）。

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
</head>
<body>
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        var lis = ul.querySelectorAll('li');
        console.log(ul.children);
        //children获取所有子元素节点，也是我们实际开发常用的
    </script>
</body>
</html>
```

##### 1.5.4 节点操作之获取第一个和最后一个节点

`parentNode.firstChild`返回第一个**子节点**，找不到则返回`null`同样包含所有节点

`parentNode.firstElementChild`返回第一个**子元素**

`parentNode.lastChild`返回最后一个子节点

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    
</head>

<body>
    <ol>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ol>
    <script>
        var ol = document.querySelector('ol');
        console.log(ol.firstChild);//获取ol的第一个子节点
        console.log(ol.firstElementChild);//获取ol的第一个子元素
        console.log(ol.lastChild);
        console.log(ol.lastElementChild);
        //实际开发的写法，没有兼容性问题，又返回第一个子元素
        console.log(ol.children[0]);//返回子节点的第一个元素
        console.log(ol.children[ol.children.length-1]);
    </script>
</body>
</html>
```

##### 1.5.5 兄弟节点操作

`node.nextSilbling`返回当前元素的下一个兄弟节点，找不到返回null，同样包含所有节点

`node.previousSibling`返回当前元素的上一个兄弟节点，找不到返回null，同样包含所有节点

`node.nextElementSilbing`返回当前元素的下一个兄弟元素节点，找不到返回null，只包含元素

`node.previousElementSilbing`返回当前元素的上一个兄弟元素节点

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    
</head>

<body>
    <div>div</div>
    <span>span</span>
    <script>
        var div = document.querySelector('div');
        console.log(div.nextSibling);//下一个节点
        console.log(div.nextElementSibling);//下一个元素
    </script>
</body>
</html>
```

##### 1.5.6 节点操作之创建/添加节点

`document.creatElement('tagName')`创建元素节点

此方法创建由tagName指定的HTML元素。由于这些匀速原本不存在，是根据我们的需求动态生成的，所以我们也称之为**动态创建元素节点**。

`node.appendChild(child)`添加元素节点（追加元素）

此方法将一个节点添加到指定父节点的列表**末尾**，类似于CSS里面的atter伪元素。类似于数组中的push。

`node.insertBefore(child,指定元素)`添加元素节点（指定位置）

此方法将一个节点添加到父节点的指定子节点前面，类似于CSS里面的before伪元素。



##### 1.5.7 删除节点

`node.removeChild(chiild)`删除父节点里面的一个子节点

````html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>
    
</head>

<body>
    <button>dlete</button>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
    <script>
        //1.获取元素
        var btn = document.querySelector('button');
        var ul = document.querySelector('ul');
        //2.删除元素
        btn.onclick = function()//点击按钮依次删除元素
        {
            if(ul.children.length == 0)
            {
                this.disabled = true;
            }
            ul.removeChild(ul.children[0]);
        }
    </script>
</body>
</html>
````

##### 1.5.8 节点操作之复制节点

`node.cloneNode()`复制节点，括号里面是空或者0时位浅拷贝，只复制节点不复制内容，括号是1时深拷贝，复制内容

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2333333</title>   
</head>
<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
    <script>
        var ul = document.querySelector('ul');
        //1.node.cloneNode()括号里面是空或者是false浅拷贝支付至标签不复制内容
        var clone = ul.children[0].cloneNode(1);
        ul.appendChild(clone);
    </script>
</body>
</html>
```

**动态生成表格案例：**

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>动态生成表格</title>   
</head>
<style>
    table {
        width: 500px;
        margin: 100px auto;
        border-collapse: collapse;
        text-align: center;
    }
    td,th {
        border: 1px solid #333;
    }
    thead tr {
        height: 40px;
        background-color: #ccc;
    }
</style>
<body>
    <table cellspacing="">
        <thead>
            <tr>
                <th>姓名</th>
                <th>科目</th>
                <th>成绩</th>
                <th>操作</th>
            </tr>
        </thead>
        <tbody>

        </tbody>
    </table>
    <script>
        //1.先去准备好学生数据
        var dates = [{
            name : '张三',
            subject : 'javascript',
            score : 98
        },{
            name : '法外狂徒',
            subject : 'javascript',
            score : 95   
        },{
            name : '你爹',
            subject : 'javascript',
            score : 92   
        }];
        //所有数据都放在tbody的行里面
        //多少行跟多少人有关系，通过循环创建行
        //2.向tbody里面创建行
        var tbody= document.querySelector('tbody');
        for(var i = 0;i<dates.length;i++)
        {
            var tr = document.createElement('tr');
            tbody.appendChild(tr);
            //行里面的单元格个数取决于每个对象里面的属性个数
            var th = document.createElement('td');
            for(var k in dates[i])//k得到的时属性名，dates[i]得到的是属性值
            {
                
                var td = document.createElement('td');
                //把对象里面的属性值给单元格
                
                td.innerHTML = dates[i][k] ;
                tr.appendChild(td);
                
            }
            var dlete = document.createElement('td');
            dlete.innerHTML = '<a href="">删除</a>';
            tr.appendChild(dlete);
            
        }
        var as = document.querySelectorAll('a');
        for (var i = 0; i < as.length; i++) {
            as[i].onclick = function() {
                // 点击a 删除 当前a 所在的行(链接的爸爸的爸爸)  node.removeChild(child)  
                tbody.removeChild(this.parentNode.parentNode)
            }
        }
    </script>
</body>
</html>
```

##### 1.5.9 三种动态创建元素的区别；

* `document.write`也可以添加元素，但是会导致页面重绘，去掉文档里面的所有内容

  ````html
  <!DOCTYPE html>
  <html lang="zh_cn">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>动态生成表格</title>   
  </head>
  <body>
      <button>点击</button>
      <p>8456132</p>
      <script>
          var btn = document.querySelector('button');
          btn.onclick = function()
          {
              document.write('<div>7894512</div>');
          }   
      </script>
  </body>
  </html>
  ````

* 

* `innerHTML`创建元素

* `document.creatElement`创建元素

**innerHTML与document.creatElement效率对比：**

​	在创建多个（大量)元素时，`innerHTML`的效率远低于`creatElement`	

​	在使用数组的方法去创建大量元素时，`innerHTML`的效率更高（避免拼接字符串时更快）

#### 1.6 DOM重点核心

获取过来的DOM元素时一个对象object，关于DOM操作，主要得有增、删、查、改、属性操作、事件操作等。。。

##### 1.6.1 创建

* `document.write`
* `innerHTML`
* `creatElement`

##### 1.6.2 增

* `appendChild`//在后面添加
* `insertBefore`//在前面添加

##### 1.6.3 删

* `removeChild`//删除指定元素

##### 1.6.4 改

**主要是修改DOM的元素属性，DOM匀速的内容、属性、表单的值等等**

* 修改元素属性：`src`,`herf`,`title`

* 修改普通元素内容：`innerHTML`,`innerText`
* 修改表单元素：`value`,`type`,`disabled`等
* 修改元素样式：`style`,`className`

##### 1.6.5 查

**主要查询DOM元素**

* DOM提供的API方法：`getElementById`,`getElementsByTagName`古老用法，不推荐

* H5提供的新方法：`querySelector`,`querySelectorAll`

* 利用节点操作获取元素：父`parentNode`,子`children`,兄`previousElementSilbing`,`nextElementSilbing`

##### 1.6.6 属性操作

**主要针对自定义属性**

* `setAttribute`设置DOM的属性值
* `getAttribute`得到DOM的属性值
* `removeAttribute`移除属性值

##### 1.6.7 事件操作

* onclick 鼠标点击触发事件
* onmouseover 鼠标经过触发
* onmouseout 鼠标离开触发
* onfocus 获得鼠标焦点触发
* onblur 失去鼠标焦点触发
* onmousemove 鼠标移动触发
* onmousedown 鼠标按下触发
* onmouseup 鼠标弹起触发

### 2.DOM高级

**目标：**

* 能够写出元素注册的两种方式
* 能够说出删除事件的梁总方式
* 能够说出DOM事件流的三个阶段
* 能够利用事件对象完成跟随鼠标的鼠标案例
* 能够封装冒泡的兼容性函数
* 能够输出事件委托的原理
* 能够说出承勇的鼠标和键盘事件

#### 2.1 注册事件

##### 1.1.1 注册事件概述

给元素添加事件，称为注册事件或者绑定事件

**注册事件有两种方式**：传统方式和方法监听注册方式

**传统注册方式：**

* 利用on开头的事件`onclick`
* `<button onclick="alert(hi~)"></button>`
* `btn.onclick = function(){}`

**特点：注册事件的唯一性，一个事件只能对应着一个处理函数**

**方法监听注册方式：**

* W3C标准推荐方式
* addEventListener()他是一个方法
* 兼容性问题，垃圾IE

**特点：同一个元素同一个事件可以注册多个处理函数**

##### 1.1.2 `addEventListener`事件监听方式

`注册的事件t.addEventListenter(事件类型,处理函数)`

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>233</title>   
</head>
<body>
    <button>点击</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click',function(){
            alert('我是你爹');
        })//里面的时事件时字符串 必定加引号 而且不带on
    </script>
</body>
</html>
```

##### 1.1.3 attachEvent注册事件（不提倡使用）

很老很老很辣鸡.....

#### 2.2 删除事件（解绑事件）

* 传统方法：在函数执行过后将其事件null掉
* 新方法：`元素名.removeEventListener('事件类型',函数名)`此方法需要将绑定的函数单独命名，不可使用匿名函数，其中的函数名不需要调用加小括号。

```html
<!DOCTYPE html>
<html lang="zh_cn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>233</title>  
    <style>
        * {
            width: 200px;
            height: 200px;

            /* border: 3px solid #cccccc; */
        }
        div {
            background-color: coral;
            border: 1px solid #cccccc;
        }
    </style> 
</head>
<body>
    <div>div1</div>
    <div>div2</div>
    <div>div3</div>
    <div>div4</div>
    <script>
        var divs  = document.querySelectorAll('div');
        //传统方式删除事件
        divs[0].onclick = function()
        {
            alert('我是你爹！');
            divs[0].onclick = null;
        }
        divs[1].addEventListener('click',dlete);
        function dlete()
        {
            alert('点过了');
            divs[1].removeEventListener('click',dlete);
        }
    </script>
</body>
</html>

```

**下面提供一种用来判断事件兼容性解决措施的办法：通杀所有浏览器**

````javascript
//删除事件兼容性解决方案
        function removeEventListener(elment,eventName,fn)
        {
            //判断当前浏览器是否支持removeEventListener方法；
            if(element.removeEventListener)
            {
                event.removeEventListener(eventName,fn);
            }else if(element.detachEvent)
            {
                element.detachEvent('on'+eventName,fn)
            }else
            {
                elment['on',eventName] = null;
            }
        }
````

#### 2.3 DOM事件流（理论）

**什么是 DOM事件流：**事件流描述的是从页面中接受时间的顺序

**事件发生时会在元素节点间按照特定的顺序传播，这个传播过程就是DOM事件流**

比如给也页面中的div注册一个点击事件，从整个文档开hi，从上向下搜寻捕获，整个页面都会接收到点击信号

**DOM事件流分三个阶段：**

* 1.捕获阶段
* 2.当前目标阶段
* 3.冒泡阶段

**事件冒泡：**（从下往上走）

IE最早提出，事件开始时由最具体的元素接受，然后主机向上传播到DOM最顶层节点的过程

**事件捕获：**（从上往下走）

网景最早提出，由DOM最顶层节点开始，然后主机向下传播到最具体的元素接受的过程

<img src="_media/dom/dom06.png" style="zoom:150%;" />

##### 2.3.1 DOM事件流代码验证

**注意：**

* JS代码只能执行捕获或者冒泡的其中一个阶段
* `onclick`和`attachEvent`(可忽略)只能得到冒泡阶段

##### 2.3.2 什么是事件对象

<img src="_media/dom/dom07.png">

##### 2.3.3 事件对象常见的属性和方法

* `e.target`返回触发事件的对象，标准
* `e.srcElement`返回触发事件的对象，非标准，ie678使用
* `e.type`返回事件的类型，比如click mouseover不带on
* `e.cancelBubble`该属性阻止冒泡，ie678使用
* `e.returnValue`该属性阻止默认事件（默认行为），非标准，ie678使用，比如不让链接直接跳转
* `e.preventDafault()`该方法组织默认事件，标准，比如不让链接直接跳转
* `e.stopPropagation`阻止冒泡，标准

#### 2.4 target和this的区别

`e.target`返回的是触发事件的对象

`this`返回的是绑定时间的对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>233333</title>
</head>
<body>
  <div>
894651
  </div>
  <ul>
    <li>123</li>
    <li>8451</li>
    <li>4512</li>
  </ul>
  <script>
    var div = document.querySelector('div');
    div.addEventListener('click',function(e){
      console.log(e.target);
      console.log(this);
    })
    var ul = document.querySelector('ul');
    ul.addEventListener('click',function(e){
      //给ul绑定了事件
      console.log(e.target);
      console.log(this);
    })
  </script>
</body>
</html>
```



<img src="/_media/dom/dom08.png">

#### 2.5 阻止默认对象

 ` e.preventDefault()`;//方法
      e.returnValue;//属性，低版本垃圾
      return false;

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>233333</title>
</head>
<body>
  <div>78451</div>
  <a href="www.baidu.com">百度</a>
  <form action="www,baidu.com">
    <input type="submit" name="sub" value="提交">
  </form>
  <script>
    //返回事件类型
    var div = document.querySelector('div');
    div.addEventListener('click',fn);
    div.addEventListener('mouseover',fn);
    div.addEventListener('mouseout',fn);
    function fn(e)
    {
      console.log(e.type);//e.type返回事件类型
    }
    //2.阻止默认行为（事件）
    var a = document.querySelector('a')
    a.addEventListener('click',function(e)
    {
      e.preventDefault();//dom推荐的的标准写法
    })
    //3.传统的注册方式
    a.onclick = function(e)
    {
      e.preventDefault();//方法
      e.returnValue;//属性，低版本垃圾
      return false;//无任何兼容性问题,但是return后面的代码不再执行，而且只限于传统的注册方式
    }
  </script>
</body>
</html>
```

##### 2.6 阻止默认事件冒泡

**事件冒泡：开始时由最具体的元素接受，然后向上逐级传递到DOM最顶层节点**

##### 2.6.1 阻止事件冒泡的两种方式

* 标准写法：利用事件对象里面的`stopPropagation()`方法
* 傻逼IE用:`cancleBubble = true`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
    <div class="father">
      <div class="son">son</div>
    </div>
    <script>
        var son = document.querySelector('.son');
        son.addEventListener('click',function(e){
          alert('son');
          e.stopPropagation();//事件方法
        })
        var father = document.querySelector('.father');
        father.addEventListener('click',function(){
          alert('father');

        },false)
        document.addEventListener('click',function(){
          alert('document');
        })
    </script>
</body>
</html>
```

##### 2.5.2 事件委托（代理、委派）

**事件委托的核心原理：给父节点添加侦听器，利用事件冒泡影响子节点**

事件冒泡本身的特性，会**带来好处**也会带来坏处，需要我们灵活掌握，如下场景

**事件委托：**

事件委托也称为事件代理，在jQuery里面称为时间委派

````html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2333</title>
</head>
<body>
  <ul>
    <li>123</li>
    <li>849561</li>
    <li>45</li>
    <li>8945</li>
  </ul>
  <script>
    var ul = document.querySelector('ul');
    ul.addEventListener('click',function(){
      alert('点击了li')
    })
  </script> 
</body>
</html>
````

#### 2.6 禁止复制页面文字和禁止右键菜单



```javascript
contextmenu.addeventListener('contextmenu',function(e){
    e.preventDefault();
})
```

`contextmenu`主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单

```javascript
document.addEventListener('selectstart',function(e){
      e.preventDefault();
    })
```

`selectstart`是鼠标开始选中的事件，阻止后无法进行选中操作

#### 2.7 获得鼠标在页面中的位置

`event`对象代表事件的状态，跟事件相关的一系列信息的集合，现阶段我们主要是用鼠标事件对象`MouseEvent`和键盘事件对象`KeyBoardEvent`

* `e.clentX` 返回鼠标相对于浏览器窗口可视区的X坐标
* `e.clintY`返回鼠标相对于浏览器可视窗口的Y坐标
* `e.pageX`返回鼠标相对于文档页面的X坐标
* `e.pageY`返回鼠标相对于文档页面的Y坐标
* `e.screenX`返回鼠标相对于电脑屏幕的X坐标
* `e.screenY`返回鼠标相对于电脑屏幕的Y坐标

##### 2.7.1 案例：跟随鼠标的小玩意

* 鼠标不断移动，使用鼠标移动时间：mousemove
* 在页面中移动，给document注册事件
* 鼠标要移动距离，而且不占位置，我们使用绝对定位即可
* 核心：每次移动鼠标我们都会获得鼠标相对整个文档的位置坐标信息，把这个XY坐标作为图片的位置即可

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2333</title>
  <style>
    img {
      position: absolute;
      top: 2px;
    }
  </style>
</head>
<body>
  <img src="imgs/logo.ico" alt="">
  <script>
    var img = document.querySelector('img');
 document.addEventListener('mousemove',function(e){
      console.log(1);
      var x = e.pageX;
      var y = e.pageY;
      img.style.left = x+'px';
      img.style.top = y+'px';
    })
  </script>
</body>
</html>
```

#### 2.8 键盘事件

**常用的键盘事件：**

* `onkeyup`键盘某个按键松开时触发
* `onkeydown`某个键按下时触发
* `onkeypress`某个键被按下时触发，但不识别功能按键如ctrl shift 箭头等
* `keyup`和`keydown`不区分键盘大小写，不论按下的是大写A还是小写a都是返回一样的
* `keypress`能区分键盘大小写，但是不识别功能键

##### 2.8.1 通过keycode判断用户按下了哪个键

```javascript
<script>
    document.addEventListener('keydown',function(e){
      console.log(e.keyCode);
    })
  </script>
```

##### 2.8.2 京东s键定位搜索框案例

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2333</title>
  <style>
    img {
      position: absolute;
      top: 2px;
    }
  </style>
</head>
<body>
  <input type="text">
  <script>
    var input  = document.querySelector('input');
    document.addEventListener('keyup',function(e) {
      if(e.keyCode==83)
      {
        input.focus()
      }
    })
  </script>
</body>
</html>
```

##### 2.8.3 模拟京东快递单号查询

```html
    //这里不想写东西
```

