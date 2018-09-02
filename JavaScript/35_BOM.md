---
title: BOM
date: 2018-05-22 19:24:24
updated:
categories:
  - JavaScript
tags:
  - JavaScript
  - BOM
top: false
comments:
keywords:
description: " "
---

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fua7a09hiqj30d509z74t.jpg)

### BOM简介

BOM是 "Browser Object Modle" 的缩写，简称 "浏览器对象模型"。主要处理浏览器窗口和框架，描述了与浏览器进行交互的方法和接口，可以对浏览器窗口进行访问和操作。

### BOM与DOM的关系

+ JavaScript 是通过访问 BOM 来访问、控制、修改浏览器的
+ BOM 的 window 包含了document，因此通过 window 对象的 document 属性可以访问、检索、修改文档内容与结构
+ document 对象是 DOM 模型的根节点

综上所述，BOM 包含 DOM，访问浏览器的是 BOM 对象，从 BOM 对象访问 DOM 对象，从而 js 可以操作浏览器以及浏览器读取到文档；除此之外，W3C 规定了关于 DOM 的标准规范，但是对于 BOM 来说，因为它是对浏览器的操作，而每个浏览器各自的实现不尽相同，所以有些方法在某些浏览器上适用，有些浏览器上不适用

### BOM 对象

BOM 对象包含以下内容

+ Window

  JavaScript 层级中的顶级对象，表示浏览器窗口

+ Navigator

  包含了客户端浏览器信息

+ History

  包含了浏览器访问过的URL

+ Location

  包含了浏览器当前访问的URL

+ Screen

  包含了客户端显示屏的信息

#### window对象

window对 象有很多属性和方法，这里只记录一些常用的，其他可以到 w3c 查找

##### 对象方法

+ close()

  关闭当前的浏览器窗口

+ alert()

  显示一段消息的弹出框

+ comfirm()

  显示一段消息以及确认按钮和取消按钮的对话框，返回值是Boolean类型

  ```html
  <script type="text/javascript">
      var value = confirm('真的要关闭当前窗口么?');
      if (value) {
          window.close();
      } else {
          window.alert('没有关闭!');
      }
  </script>
  ```

+ open(URL, name, features, replace)

  打开一个新的浏览器窗口或者查找一个已命名的窗口，新的文档对第四个标准不支持了，所以不考虑第四个参数

  + 参数都可以为空，但是如果不写第三个参数的话，是在当前浏览器中打开一个新的窗口（一个新的标签页），除非是打开已存在的窗口（比如第四点）

  ```html
  <script type="text/javascript">
      window.open('', '', '');
  </script>
  ```

  + 打开一个宽高为设定值的新的窗口

  ```html
  <script type="text/javascript">
      window.open('', '', 'width=500, height=400');
  </script>
  ```

  + 打开一个指定路径或网址的新的窗口

  ```html
  <script type="text/javascript">
      window.open('./new.html', '', 'width=500, height=400');
      window.open('https://www.baidu.com', '', 'width=500, height=400');
  </script>
  ```

  > 这里如果打开文件是自身的话，会循环无止境的打开新的窗口

  + 打开一个新的窗口，并为之命名

  ```html
  <script type="text/javascript">
      window.open('', 'newName', 'width=500, height=400');
      window.open('https://www.baidu.com', 'newName', '');
  </script>
  ```

  + 如果要关闭某一个新建的窗口，要用一个变量来接受这个窗口对象

  ```html
  <script type="text/javascript">
      var newWindow = window.open('', 'newW', 'width=500, height=400');
      // neW.close();  这样是不行的
      newWindow.close();
  </script>
  ```

+ moveBy(x, y)

  相对窗口的当前坐标，把他移动一定的距离（往右移x，往下移y）

  ```html
  <script type="text/javascript">
      var newWindow = window.open('', 'newW', 'width=500, height=400');
      newWindow.moveBy(200, 200);
  </script>
  ```

  > 操作对 window 无效

+ moveTo(x, y)

  把窗口移动到指定位置

  ```html
  <script type="text/javascript">
      var newWindow = window.open('', 'newW', 'width=500, height=400');
      newWindow.moveTo(200, 200);
  </script>
  ```

  > 操作对 window 无效

+ print()

  打印当前窗口的内容

+ prompt()

  显示可提示用户输入的对话框，点击确认返回值是输入内容，点击取消返回值是null

  ```html
  <script type="text/javascript">
      var name = window.prompt('请输入用户名');
      console.log(name);
  </script>
  ```

+ scrollBy(x, y)

  滚动条滚动指定的距离

+ scrollTo(x, y)

  滚动条滚动到指定位置

##### 对象属性

+ closed

  判断窗口是否被关闭，返回Boolean值

  ```html
  <script type="text/javascript">
      var newW = window.open('', '','width=100, height');
      console.log(newW.closed);
      newW.close();
      console.log(newW.closed);
  </script>
  ```

+ innerHeight / innerWidth

  返回窗口的文档显示区的高度、宽度

  ```html
  <script type="text/javascript">
      console.log('width:' + window.innerWidth);
      console.log('height:' + window.innerHeight);
  </script>
  ```

+ outerHeight / outerWidth

  返回浏览器窗口的高度、宽度

+ length

  设置或返回窗口中的框架数量（后面用到再补充）

+ name

  窗口的名称（后面会借助 window.name 实现数据的跨域）

+ pageXOffset / pageYOffset

  设置或者返回当前页面相对于窗口显示区左上角 X / Y 的位置

  > 这个的一个用途是：可以做页面中固定位置的广告，一般用position：fixed实现，但是position：fixed在IE中会存在兼容性问题，可以用这个做

+ screenLeft / screenTop

  screenX / screenY

  只读整数，声明了窗口左上角在屏幕上的x坐标和y坐标。IE、Safari、chrome、Opera 支持 screenLeft，chrome、Firefox、Safari 支持 screenX

#### Navigator对象

Navigator 对象包含的属性描述了正在使用的浏览器的。可以使用这些属性进行平台专用配置。虽然这个对象的名称显而易见是 Netscape 的 Navigator 浏览器，但是 JavaScript 的浏览器也支持这个对象

##### 对象属性

+ appVersion

  返回浏览器的平台和版本信息

+ cookieEnabled

  返回指定浏览器是否启用cookie的布尔值

+ onLine

  返回指定系统是否处于联机模式的布尔值

  > 做离线缓存可以用到这个

+ userAgent

  返回客户机发送服务器的 user-agent 头部的值，这个是有用的方法，后面讲

+ plugins

  返回包含客户端安装的所有插件的数组

##### 对象方法

#### History对象

History 对象包含用户（在浏览器中）访问过的 URL

##### 对象属性

+ length

  返回浏览器历史列表中访问过的URL

##### 对象方法

+ back()

  加载 history 列表中的前一个 URL

+ forward()

  加载 history 列表中后一个 URL

+ go(num)

  加载 history 列表中前 / 后 num 个页面

#### Location对象

Location 对象包含有关当前URL的信息

##### 对象属性

+ hash

  设置或返回从 # 开始的 URL（锚）

+ host

  设置或返回主机名和当前URL的端口号，如果端口号是默认端口号，就不显示端口号；如果是设置的别的端口号，就会返回端口号

+ hostname

  设置或者返回当前URL的主机名

+ post

  设置或者返回当前URL的端口号

+ href

  设置或者返回完整的URL

+ pathname

  设置或返回当前URL的路径部分

+ protocol

  设置或返回当前URL的协议

+ search

  设置或返回从 ？ 开始的 URL 部分

##### 对象方法

+ assign()

  加载新的文档

+ reload('force')

  重新加载当前文档，参数不可选，不填或填false则取浏览器缓存文档

+ replace()

  用新的文档替换当前文档

#### Screen对象

Screen 对象包含有关客户端显示屏幕的信息。每个 Window 对象的 screen 属性都引用一个 Screen 对象。JavaScript 将利用这些信息来优化他们的输出，已达到用户的显示要求。例如，一个程序可以根据显示器的尺寸选择大图像还是小图像，他还可以根据显示器的颜色深度选择使用16为色还是8为色的图形。另外，JavaScript 还能根据浏览器屏幕信息，将新的浏览器窗口固定到屏幕中间

##### 对象属性

+ availHeight / avaliWidth

  返回显示器高度 / 宽度 （不包含任务栏）

+ height / width

  返回显示屏幕的高度 / 宽度（不管是任务栏还是什么都包括）

