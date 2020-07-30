## 1. 页面导入样式时,用link和import的区别

1. ### 类型不同

   link: 是html标签, 除了加载CSS外,还能用于定义rel连接属性等作用

   @import: 是css语法,只能用于加载css, 

2. ### 加载时机不同

   link: 引入的样式在页面加载时同时加载

   @import: 引入的样式需等页面完全载入以后再加载

3. ### 兼容性

   由于@import是CSS2.1提出的,@import只有在IE5以上的才能识别,而link标签无此问题

   link: 是XHTML标签没有兼容性问题

   @import: 不兼容ie5以下

4. ### 动态改变

   link: 支持使用Javascript控制DOM去改变样式

   @import: 不支持

5. ### @import次数

   限制@import只能引入31次css文件

   

   ## 不推荐使用@import的原因

   1. #### **原因一、使用@import引入CSS会影响浏览器的并行下载**

      使用@import引用的CSS文件只有在引用它的那个css文件被下载、解析之后，浏览器才会知道还有另外一个css需要下载，这时才去下载，然后下载后开始解析、构建render tree等一系列操作。这就导致了浏览器无法并行下载所需的样式文件。

   2. **原因二：多个@import会导致下载顺序紊乱。**

      在IE中，@import会引发资源文件的下载顺序被打乱，即排列在@import后面的js文件先于@import下载，并且打乱甚至破坏@import自身的并行下载。



## 2. 用递归算法实现,数组长度为5且随机数在2-32间不重复的值

```
<script>
  let arr = new Array(5);
    function getRandomInsertArr(length) {
      if (length < 0) return;
      const tempItem = Math.floor(2 + Math.random() * 32);
      if (arr.includes(tempItem)) return getRandomInsertArr(length);
      arr[length] = tempItem;
      return getRandomInsertArr(length - 1);
    }
    getRandomInsertArr(arr.length - 1);
    console.log(arr)
</script>
```

**1.递归定义**

递归,就是在运行的过程中调用自己。

**2.递归原理**

递归和栈的原理差不多,递归也是先进后出,递归也是利用堆栈来实现的

递归: 由 new (malloc)分配的内存块，他们的释放编译器不去管，由我们的应用程序去控制。如果忘记释放，则会发生严重的内存泄漏。只有程序结束后，操作系统才会收回这些内存。

递归由于函数要调用自身，函数调用时的参数通过栈空间来传递( 调用函数会占用线程栈资源，所以递归调用会不断的向栈中压入参数来进行操作,函数执行结束才依次退出)，每一次函数调用，都需要在内存栈中分配空间以保存参数、返回地址及临时变量，而且往栈里压入数据和弹出数据都需要时间. 当深度过大时，占用的栈空间也越来越大，而每个进程的栈容量是有限的 ,当递归调用的层级太多时，就会超出栈的容量，就可能导致占用的栈资源超过线程最大值，从而导致调用栈溢出



## 3. 圣杯布局和双飞翼布局的区别和理解, 用代码实现

圣杯布局和双飞翼布局一直是前端面试的高频考点，圣杯布局的出现是来自由 Matthew Levine 在 2006 年写的一篇文章 [《In Search of the Holy Grail》](https://link.juejin.im/?target=https%3A%2F%2Falistapart.com%2Farticle%2Fholygrail)。 比起双飞翼布局，它的起源不是源于对页面的形象表达。在西方，圣杯是表达“渴求之物”的意思。而双飞翼布局则是源于淘宝的UED，可以说是灵感来自于页面渲染。


middle占满一行，要把left拉到middle所在行的最左边，区别就是两边的布局是用中间的padding撑开还是margin撑开 

**圣杯布局中加padding, 双飞翼布局加margin**

不管是圣杯布局还是双飞翼布局, 其中这样的好处就是突出中间的内容,就是中间内容在网络不太稳定的情况下先展示,有良好的用户体验

其中圣杯布局有个缺点:main的宽度不能小于left的宽度,否则圣杯布局会变形

**圣杯**

```html
<!DOCTYPE HTML>
<html lang="en-US">

<head>
  <meta charset="UTF-8">
  <title>圣杯布局</title>
  <style type="text/css">
    body {
      text-align: center;
      ;
    }

  
    #container {
      overflow: hidden;
      margin: 10px 0;
      padding: 0 210px;
    }

    #left {
      background-color: red;
      float: left;
      position: relative;
      left: -210px;
      width: 200px;
      margin-left: -100%;
    }

    #right {
      background-color: green;
      width: 200px;
      margin-left: -200px;
      float: left;
      right: -210px;
      position: relative;
    }

    #middle {
      background-color: yellow;
      float: left;
      width: 100%;
    }
  </style>
</head>

<body>
  <div id="demo">
    <div id="container">
      <div id="middle">
        middle<br>主内容区域
      </div>
      <div id="left">
        left<br>左侧边栏区域
      </div>
      <div id="right">
        right<br>右侧边栏区域
      </div>
    </div>
  </div>
</body>

</html>
```

**双飞翼布局**

```html
<!DOCTYPE HTML>
<html lang="en-US">

<head>
  <meta charset="UTF-8">
  <title>双飞翼布局</title>
  <style type="text/css">
    body {
      text-align: center;
      ;
    }

    #left {
      background-color: red;
      float: left;
      width: 200px;
      margin-left: -100%;
    }

    #right {
      background-color: green;
      width: 200px;
      float: left;
      margin-left: -200px;
    }

    #middle {
      float: left;
      width: 100%;
    }

    #middle_content {
      background-color: yellow;
      margin: 0 210px;
    }
  </style>
</head>

<body>
  <div id="demo">
    <div id="container">
      <div id="middle">
        <div id="middle_content">
          middle_content<br>主内容区域
        </div>
      </div>
      <div id="left">
        left<br>左侧边栏区域
      </div>
      <div id="right">
        right<br>右侧边栏区域
      </div>
    </div>
  </div>
</body>

</html>
```

