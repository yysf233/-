# WebAPI - BOM

### 学习目标

![image-20210216094120849](C:\Users\23271\AppData\Roaming\Typora\typora-user-images\image-20210216094120849.png)

## 1.BOM 概述

### 1.1 什么是BOM

​	`BOM`即浏览器对象模型，它提供了**独立于内容**而与**浏览器窗口进行交互的对象**，其核心对象是`window`

例如页面中页面的前进后退，浏览器窗口页面大小发生变化，滚轮滑动等等

但是：**BOM缺乏统一标准！**

​	BOM提供了一系列相关的对象构成，并且每个对象提供了许多方法和属性。

**BOM**

* 浏览器对象模型
* 把浏览器当作一个对象来蓝带
* BOM的顶级对象是window
* BOM学习的是浏览器窗口交互的一些对象
* BOM是**浏览器厂商在各自浏览器上定义的**兼容性比较差

### 1.2 BOM的构成

BOM比DOM更大，它包含DOM

window->document,location,navigation,screen,histroy

`window`对象是浏览器的顶级对象，它具有双重角色

* 1.他是JS访问浏览器窗口的一个接口
* 2.他是一个全局变量，定义在全局作用域中的变量、函数都会变成`window`对象的属性和方法（在调用时可以省略window，前面学的对话框都属于window对象方法，如laaert(),prompt()等）

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
  <script>
    var num = 10;
    console.log(num);
    console.log(window.num);
    function fn()
    {
      console.log(11);
    }
    fn();
    window.fn();
    console.log(fn);//只填写函数名的话会输出函数的内容的
  </script>
</body>
</html>
```

**注意：window下的一个特殊属性window.name**

## 2.window常见事件

###  2.1 窗口加载事件

#### 2.1.1 window.onload事件

```javascript
<script>
    window.onload = function()
    {
      window.addEventListener("load",function(){});
    }
  </script>
```

* 这个函数的功能是让浏览器加载完所有HTML\CSS的内容后再去加载JS

* 有了这个函数，可以把jS放到页面的任何一个位置，但是一个文档只能有一个`window.onload`函数

````html
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
  <script>
    window.onload = function()
    {
      var btn = document.querySelector('button');
      btn.addEventListener('click',function(){
        alert('哪个吊人点我了？')
      })
    }
  </script>
  <button>我是个按钮</button>
</body>
</html>
````

#### 2.1.2 窗口加载事件分支:DOMContentLoaded

```

```

* `DOMContentLoaded`事件触发时，仅仅当DOM加载完毕后，不包括样式表，图片，flash等等

* 如果页面的图片很多的话，从用户访问的到onload触发可能需要很长事件，交互效果就不能实现，必然营销哪个用户体验，此时用`DOMContentLoaded`事件比较合适。

* `onload`事件是当页面内容全部加载完成时在会执行，包含页面的图片 flash css
* `DOMContentLoaded`事件是DOM加载完毕，不包含图片flash css等就可以执行，加载速度比`onload`更快一些

### 2.2 调整窗口大小事件

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
  <script>
    var i= 0;
    window.onresize = function()
    {
      console.log(i);
      i++;
    }
  </script>
</body>
</html>
```

* 只要浏览器窗口发生升序变化，就会触发这个事件。
* 我们经常利用这个事件来完成响应式布局。`window.innerWidth`当前屏幕的宽度

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2333</title>
  <style>
    div {
      width: 200px;
      height: 200px;
      background-color: blue;
    }
  </style>
</head>
<body>
  <div>1111</div>
  <script>
    var div = document.querySelector('div')
    var i= 0;
    window.onresize = function()
    {
      console.log('当前宽度：'+window.innerWidth);
      console.log('当前高度：'+window.innerHeight);
      console.log(i);
      i++;
      if(window.innerWidth<800)
      {
        div.style.display = 'none';
      }else
      {
        div.style.display = '';
      }
    }
  </script>
</body>
</html>
```

### 2.3 定时器：与时间有关的函数

#### 2.3.1 两种定时器

`window`对象给我们提供了两种定时器

* `setTimeout()`
* `setInttravel()`

```javascript
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2333</title>
  
</head>
<body>
  <script>
    // window.setTimeout(调用函数，[延迟的毫秒数])
    //该方法用于设定一个函数，作用是在定时到期后执行该调用的函数
    //因为定时器可能有很多，所以经常欸定时器赋值一个标识符
    function fn()
    {
      alert('电脑没电了草');
    }
    setTimeout(function()
    {
      alert('午时已到~');
      fn();
    },[2000])
  </script>
</body>
</html>
```

#### 2.3.2 回调函数以及五秒后自动关闭的广告

`setTimeout()`这个调用函数我们也成为回调函数`callback`，普通函数是按照代码顺序直接调用，而这个函数需要等待时间，等时间到了再去调用用这个函数。

**回调：就是回头调用的意思**

​	以前讲的`element.onclick = function(){},element.addEventListener(`

`"click",fn)`也是回调函数

````java
<img src="imgs/logo.ico" alt="" class="ad">
  <script>
    var ad = document.querySelector('.ad');
    setTimeout(function(){
      ad.style.display = 'none';
    },5000);
  </script>
````

#### 2.3.3 如何停止 setTimeout() 定时器

`window.clearTimeout(timeoutID)`**要给定时器赋值一个标识符 **

```javascript
<img src="imgs/logo.ico" alt="" class="ad">
  <button>停止计时</button>
  <script>
    var btn = document.querySelector('button');
    btn.addEventListener('click',function(){
      clearTimeout(dingshi);
    })
    var ad = document.querySelector('.ad');
    var dingshi = setTimeout(function(){
      ad.style.display = 'none';
    },5000);
  </script>
```

#### 2.3.4 第二个定时器setInterval(回调函数，间隔时间)

`setInterval()`方法重复调用一个函数。每个这个时间，就去调用一次回调函数，其他注意事项与`setTimeout()`相同

```javascript
<p>我是一段文字</p>
  <script>
    var time = 1;
    var p = document.querySelector('p')
    window.setInterval(function()
    {
      time++;
      console.log(time);
      p.innerText = '午时已到';
    },1000);
  </script>
```

#### 2.3.5 案例：倒计时效果

**案例分析：**

* 这个倒计时是不断变化的，需要定时器来自动变化
* 三个小的黑色盒子分别存放时分秒
* 三个盒子利用innerHTML来放入需要计算的呃小时分钟秒数、

```javascript
<span class="hour">1</span>
  <span class="minute">2</span>
  <span class="second">3</span>
  <script>
    var hour = document.querySelector('.hour');
    var min = document.querySelector('.minute');
    var sec = document.querySelector('.second');
    var inputtime = +new Date('2021-2-17 10:30:00');//返回用户输入的毫秒时间
    countDown();//先调用一次这个函数，防止第一次刷新有空白
    function countDown(){
      var newtime = +new Date();//返回当前总的毫秒时间
      var times = (inputtime - newtime)/1000;//times是剩余时间的秒数
      var h = parseInt(times/60/60%24);
      h = h<10?'0'+h:h;
      hour.innerHTML = h;
      var m = parseInt(times/60%60);
      m = m<10?'0'+m:m;
      min.innerHTML = m;
      var s = parseInt(times%60);
      s = s<10?'0'+s:s;
      sec.innerHTML = s;
      console.log(h);
      console.log(m);
      console.log(s);
    }
    setInterval(countDown,1000);
  </script>
```



#### 2.3.6停止setInterval()定时器

```
window.clearInterval(intervalID);
```

`clearInterval()`方法取消了先前通过调用`setInterval()`建立的定时器

**注意**

* window可以忽略
* 里面的参数就是定时器的标识符

```javascript
	<button class="begin">开启定时器</button>
    <button class="stop">停止定时器</button>
    <script>
      let begin = document.querySelector('.begin');
      let stop = document.querySelector('.stop');
      let timer = null;//全局变量
      begin.addEventListener('click',function(){
          timer = setInterval(function(){
            console.log('2333');
        },500);
      });
      stop.addEventListener('click',function(){
        clearInterval(timer);
      })
    </script>
```

#### 2.3.7 案例：发送短信案例

**案例分析：**

* 按钮点击之后，会禁用`disabled`为`true`
* 同时按妞妞里面的内容会变化，注意`button`里面的内容通过`innerHTML`修改
* 里面的描述是有百年化的，因此需要用到计时器
* 定义一个变量，不断递减并显示出来
* 如果变量为0 了，需要停止计时，并自动复原

```javascript
  <input type="number">
    <button>发送</button>
    <script>
      window.setTimeout(function(){
        var timee = 10;//变量
      var btn = document.querySelector('button');
      btn.addEventListener('click',function(){
        btn.disabled = true;
        var timer = setInterval(function(){
          btn.innerHTML = '还剩下'+timee+'秒';
          timee = timee-1;
        },1000);
      });
      },1000);
    </script>
```

### 2.4 js 的执行机制

#### 2.4.1 同步和异步

​	js的一大特点是单线程，同一时间只能做一件事。

​	H5提出了web worker标准，允许js脚本同时执行多线程任务，于是js中出现了同步和异步。

````javascript
<script>
        console.log(1);
        setTimeout(function() {
            console.log(3);
        }, 1000);
        console.log(2)
    </script>
````



#### 2.4.2 同步执行和异步执行的过程

```javascript
<script>
        console.log(1);
        setTimeout(function() {
            console.log(3);
        }, 0);
        console.log(2)
    </script>
```

**同步任务：**

​	同步任务都在主线程上执行，形成一个**执行栈**。

**异步任务：**

​	JS的异步任务是通过回调函数完成的

​	一般而言，异步任务有以下几种类型

* 普通事件：`click`,`resize`等等
* 资源加载：`load`,`error`等
* 定时器：包括`setInterval`,`setTimeout`等

**异步任务的相关回调函数添加到任务队列当中**

#### 2.4.3 执行过程

* 先执行主线程中的同步任务
* 异步函数（回调函数）放到任务执行队列当中
* 等待同步任务执行完毕，系统会按顺序读取异步任务，进入执行过程

### 2.5 location 对象

#### 2.5.1 什么是 location 对象

​	`location`对象是`window`对象下的一个属性，用于获取或设置窗体的`URL`,并且可以用于解析`URL`.因为这个属性返回的是一个对象，多以我们班这个属性也叫做`location`对象。

#### 2.5.2 URL

​	**统一资源定位符（url）**是互联网上的标准资源地址。互联网上的每个文件都有一个唯一的URL，它包含的的信息指出文件的位置以及浏览器应该怎样处理它。

​	**URL的一般格式：**

````javascript
protocol://host[:port]/path/[?query]#fragment
http://www.itcast.cn/index.html?name=andy&age=19#link
````

* protocol 通讯协议 常用的http,ftp,maito等等
* host 主机（域名）www.itheima.com
* port 端口号（可选），省略时使用方案的默认端口 如http的默认端口为80
* path 路径 由零或多个''/''符号隔开的字符串，一般用来表示主机上的一个目录或文件地址
* query 参数以键值对的形式，通过&符号分割开来
* fragment 片段 #后面内容 常用于链接 锚点

#### 2.5.3 location 对象的属性

![image-20210305214237069](C:\Users\23271\AppData\Roaming\Typora\typora-user-images\image-20210305214237069.png)

#### 2.5.4 案例：获取URL的参数和应用

**案例分析：**

* 第一个登陆页面，里面有提交表单，`action`提交到index.html页面
* 第二个页面，可以使用第一个页面的参数，这样实现了一个数据不同页面之间的传递效果
* 第二个页面之所以可以使用第一个页面的数据，是利用了URL里面的`location.search`参数
* 在第二个页面中，提取参数
* 第一步去掉？利用`substr`
* 第二部 利用=号分割键和值 `split('=')`

```javascript
	<div>
		 欢迎！
    </div>
    <script>
        console.log(location.search);//拿到url参数
        //筛选参数
        //1.去掉问号 substr('起始的位置'，截取几个字符)
        
        var username = location.search.substr(1);//username = ****
        console.log(name);
        //2.利用等号把字符串分割成数组
        var arr = username.split('=');
        console.log(arr[1]);
        var div = document.querySelector('div');
        div.innerHTML = arr[1];
    </script>
```



#### 2.5.5 location常见方法

* `location.assign()`跟`herf`一样，可以跳转页面（也成为重定向页面）
* `location.replace`替换当前页面，因为不记录历史，所以不能后退页面
* `location.reload`重新加载页面，相当于刷新按钮或者f5 富国参数为true强制刷新ctrl+f5

```javascript
<button>跳转</button>
  <script>
    var btn = document.querySelector('button');
    btn.addEventListener('click',function(){
      // location.assign('http://www.baidu.com');
      //保留历史，可以回退
      location.replace('http://www.baidu.com');
      //replace方法不保留历史，不能后退
    })
  </script>
```

### 2.6 navigation 对象

BOM对象中的`navigation`对象

其中包含有关浏览器的信息，有很多属性，最常用的是`userAgent`，该属性可以返回由客户机发送服务器的`user-agent`头部的值

下列代码可以判断用户那个终端打开页面，实现跳转

### 2.7 history 对象

`window`对象俄国i我们提供了一个`history`对象，与浏览器历史记录进行交互啊。包含用户访问过的URL

* `back（）`可以后退功能
* `forward()`前进功能
* `go(参数)`前进和后退功能 参数如果是1，前进一格页面 如果是-1 则后退一个页面

## 3.PC端网页特效

### 3.1 元素偏移量 offset 系列

#### 3.1.1 offset 概述

​	`offset`翻译过来就是偏移量的意思，我们使用`offset`系列相关属性可以动态的得到该元素的位置（偏移）、大小等等。

**offset 系列常用属性：**

<img src="C:\Users\23271\AppData\Roaming\Typora\typora-user-images\image-20210306141008464.png" alt="image-20210306141008464" style="zoom:150%;" />

#### 3.1.2 offset 与 style 的区别

![image-20210306150700015](C:\Users\23271\AppData\Roaming\Typora\typora-user-images\image-20210306150700015.png)

#### 3.1.3 案例：获取鼠标在盒子内的坐标

**作用：购物网站放大镜效果**

**案例分析：**

* 在盒子内点击，想要的到鼠标距离盒子左右的距离
* 首先得到鼠标在页面中的坐标（`e.pageX`,`e.pageY`）
* 其次得到盒子在页面中的距离（`box.offsetLeft`,`box.offsetRight`）

```javascript
<div class="a">awdawd</div>
  <script>
    var box = document.querySelector('.a');
    box.addEventListener('mousemove',function(e){
      console.log(e.pageX);//鼠标相对于页面左侧的距离
      console.log(e.pageY);//鼠标相对于页面顶部的距离
      console.log(box.offsetLeft);//电机的盒子相对于body的距离
      var x = e.pageX - this.offsetLeft;
      var y = e.pageY - this.offsetTop;
      console.log(x);
      console.log(y);
      this.innerHTML = 'x坐标'+x+'y坐标是'+y;
    })
  </script>
```

#### 3.1.4 模态框的拖拽

#### 3.1.5 鼠标移入移出模拟

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>倒计时效果</title>
</head>
<style>
  .a{
    width: 120px;
    height: 120px;
    margin-top: 200px;
    margin-left:300px ;
    background-color: rgb(41, 167, 167);
    display: block;
    transition: 0.9s;
  }
</style>
<body>
  <div class="a">1111111</div>
  <script>
    var a = document.querySelector('.a');
    a.addEventListener('mouseover',function() {
      a.style.display = 'block';
      a.style.width = '1200px';
      console.log('2333');
    })
    a.addEventListener('mouseout',function() {
      a.style.display = 'block';
      a.style.width = '80px';
      
      console.log('2333');
    })
  </script>
</body>
</html>
```

### 3.2 元素可视区 client 系列

#### 3.2.1 概述

​	`client`翻译过来就是客户端，我们使用`client`系列的相关属性来获取元素可视区的相关信息。通过`client`系列的相关属性可以动态的得到该元素的边框大小元素大小等。

​	`client`返回的值是不包含边框的。

<img src="C:\Users\23271\AppData\Roaming\Typora\typora-user-images\image-20210306165012328.png" alt="image-20210306165012328" style="zoom:80%;" />

#### 3.2.2 案例：淘宝flexible.js源码分析--立即执行函数

**案例分析：**

`(function(){})()`立即执行函数

主要作用：创建一个独立的作用域，不需要调用，立马自己执行

#### 3.3 mouseover和mouseenter事件

 **mousuenter鼠标事件**

* 当鼠标移动到元素上时就会触发`mouseenter`事件
* 类似`mouseover`，他们之间的差别是`mouseover`鼠标经过自身盒子会触发，经过子盒子还是会触发，`mouseenter`只会经过自身盒子触发



### 3.4 动画函数封装

#### 3.4.1 动画实现原理

**核心原理：**通过定时器`setInterval()`不断移动盒子位置

**实现步骤：**

* 获得盒子当前位置
* 让盒子在当前位置加上一个移动距离
* 利用定时器不断重复这个函数
* 加入判断条件
* 注意加入元素定位`positon:relitive`相对位置属性才可以使用定位

#### 3.4.2 简单动画函数的封装

```javascript
<div class="a">1111111</div>
   <script>
     var obj = document.querySelector('.a');
     function 动画函数(obj,target){
        var timer = setInterval(function(){
          if(obj.offsetLeft>=target)
          {
            clearInterval(timer);
          }
          obj.style.left = obj.offsetLeft + 100 +'px';
        },1000)
     }
     动画函数(obj,300);
   </script>
```

#### 3.4.3 动画函数-给不同元素记录不同定时器

​		如果多个元素都是用这个动画函数，每次都要var 生命定时器。我们可以给不同的元素使用不同的定时器（自己专门用自己的定时器）。

**核心原理：**利用JS 是一门动态语言，可以很方便的给当前对象添加属性



