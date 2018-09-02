---
title: DOM简述
date: 2018-05-12 12:03:21
updated:
categories:
  - JavaScript
tags:
  - JavaScript
  - DOM
top: false
comments:
keywords:
description: " "
---

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu9mcf8r8uj30eo0b7dgf.jpg)

#### 什么是DOM

DOM(文档对象模型)是针对HTML和XML文档的一个API(应用程序编程接口)。DOM描绘了一个层次化的节点树，允许开发人员添加、移除和修改页面中的某一个部分。DOM脱胎于Netscape及微软公司创世的DHTML(动态HTML)，但现在他已经成为表现和操作页面标记的真正的跨平台、语言中立的方式。

W3C DOM由一下三部分组成：

+ 核心 DOM - 针对任何结构化文档
+ XML DOM - 针对XML文档的标准模型
+ HTML DOM - 针对HTML文档的标准模型

#### DOM的地位

我们知道，一个网页是由html来搭建结构的，通过css来定义网页的样式，而JavaScript赋予了页面的行为，通过它我们可以与页面进行交互，实现页面的动画效果等等。那javascript究竟通过什么来实现的呢？通过ECMAScript这个标准，我们可以编写程序让浏览器来解析，利用ECMAScript，我们可以通过BOM对象（即browser object model）来操作浏览器窗口、浏览器导航对象(navigator)、屏幕分辨率(screen)、浏览器历史(history)、cookie等等。但这个通过BOM来实现的交互远远不够。要实现页面的动态交互和效果，操作html才是核心。那如何操作html呢？对，就是DOM，简单的说，DOM给我们提供了用程序来动态控制html的接口，也就是早期的DHTMl的概念。因此，DOM处在javascript赋予html具备动态交互和效果的能力的核心地位上。

#### DOM的发展

##### 1. DOM0

JavaScript在早期版本中提供了查询和操作web文档内容的API(如图片、表单)，在JavaScript中定义了'images'、'forms'等，因为我们可以像下面这样访问第一张图片或者名为'user'的表单：

```js
document.images[0];
document.forms['user'];
```

这实际上是未形成标准的试验性质的初级阶段的DOM，现在习惯上被称为DOM0，即第0级DOM。由于DOM0在W3C进行标准化之前出现，还处于未形成标准的初级阶段，这时Netscape和Microsoft各自退出自己的第四代浏览器，自此DOM便开始出现各种问题。

##### 2. DOM0与DHTML

Netscape Navigator 4 和 IE4分别发布于1997年6月和10月，这两种浏览器都大幅扩展了DOM，使JavaScript的功能大大增加，此时也开始出现了一个新名词：DHTML

DHTML(Dynamic HTML)，叫做'动态HTML'。DHTML并不是一项新技术，而是将HTML、CSS、JavaScript技术组合的一种描述。即：

+ 利用HTML把网页标记为各种元素
+ 利用CSS设置元素样式即显示位置
+ 利用JavaScript操控页面元素和样式

利用DHTML看起来可以很容易的控制页面元素，并实现原本很复杂的效果，但事实并非如此。因为没有规范和标准，两种浏览器对相同功能的实现完全不一样。为了保持程序的兼容性，程序员必须写一些探查代码以检测JavaScript是运行在哪种浏览器下，并提供与之对应的脚本。JavaScript下入了前所未有的混乱，DHTML也因此在人们心中留下了很差的印象。

我们在阅读DOM标准的时候，经常会看到DOM0级这样的字眼，实际上DOM0级这个标准是不存在的。所谓DOM0级只是DOM
历史坐标系中的一个参照点而已，具体地说DOM0级就是指IE4.0和Netscape navigator4.0最初支持的那个DHTML。

##### 3. DOM1

在浏览器厂商进行浏览器大站的同时，W3C结合大家的优点推出了一个标准化的DOM，并于1998年10月完成了第一级 DOM，即：DOM1。W3C将DOM定义为一个与平台和编程语言无关的接口，通过这个接口程序和脚本可以动态的访问和修改文档的内容、结构和样式。

DOM1级主要定义了HTML和XML文档的底层结构。在DOM1中，DOM由两个模块组成：DOM Core（DOM核心）和DOM HTML。其中，DOM Core规定了基于XML的文档结构标准，通过这个标准简化了对文档中任意部分的访问和操作。DOM HTML则在DOM核心的基础上加以扩展，添加了针对HTML的对象和方法，如：JavaScript中的Document对象.

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fpy1w90nqjj30j60ajta7.jpg)

##### 4. DOM2

在DOM1的基础上DOM2引入了更多的交互能力，也支持了更高级的XML特性。DOM2将DOM分为更多具有联系的模块。DOM2级在原来DOM的基础上又扩充了鼠标、用户界面事件、范围、遍历等细分模块，而且通过对象接口增加了对CSS的支持。DOM1级中的DOM核心模块也经过扩展开始支持XML命名空间。在DOM2中引入了下列模块，在模块包含了众多新类型和新接口：

- DOM视图（DOM Views）：定义了跟踪不同文档视图的接口
- DOM事件（DOM Events）：定义了事件和事件处理的接口
- DOM样式（DOM Style）：定义了基于CSS为元素应用样式的接口
- DOM遍历和范围（DOM Traversal and Range）：定义了遍历和操作文档树的接口

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fpy1xnhsd4j30j60elwhc.jpg)

完整的DOM2标准(图片来自百度百科)：

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fpy1yfd410j30hs0c80ts.jpg)

##### 5. DOM3
进一步扩展了DOM，引入了以统一方式加载和保存文档的方法，它在DOM Load And Save这个模块中定义；同时新增了验证文档的方法，是在DOM Validation这个模块中定义的.

DOM3进一步扩展了DOM，在DOM3中引入了以下模块：

- DOM加载和保存模块（DOM Load and Save）：引入了以统一方式加载和保存文档的方法
- DOM验证模块（DOM Validation）：定义了验证文档的方法
- DOM核心的扩展（DOM Style）：支持XML 1.0规范，涉及XML Infoset、XPath和XML Base

![DOM3](https://ws1.sinaimg.cn/large/006eYMu7ly1fpy1zk1g5cj30j60cw766.jpg)