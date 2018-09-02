---
title: DOM续
date: 2018-05-14 12:43:01
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

### 查看滚动条位置

#### W3C 标准方法

+ window.pageXOffset / window.pageYOffset

#### IE9 以下版本方法

+ document.body.scrollLeft / document.body.scrollTop
+ document.bodyElement.scrollLeft / document.bodyElement.scrollTop

IE9以下版本的浏览器，不支持 w3c 的标准方法，只能用这两种方法查看滚动条位置，但是这两种方法兼容性也很混乱，为了解决这个兼容性混乱的问题，对于这两种方法，一般使用两者之和，因为当一个方法有值时，另外一个方法的值一定是0

```javascript
// 查看x轴方向的滚动条位置
document.body.scrollLeft + document.documentElement.scrollLeft
// 查看y轴方向的滚动条位置
document.body.scrollTop + document.documentElement.scrollTop
```

>调试的时候可以先在页面中加一个大的盒子，让滚动条显示出来

```html
<div style="width:2000px;height:1000px"></div>
```

#### 兼容性方法

为了解决不同版本浏览器的兼容性问题，封装一个查看滚动条位置的兼容性方法

```javascript
function getScrollOffset() {
    if (window.pageXOffset) {
        return {
            x: window.pageXOffset,
            y: window.pageYOffset
        }
    } else {
        return {
            x: document.body.scrollLeft + document.documentElement.scrollLeft,
            y: document.body.scrollTop + document.documentElement.scrollTop
        }
    }
}
```

### 让滚动条滚动

#### 让滚动条滚动到指定位置

+ window.scroll(x, y)
+ window.scrollTo(x, y)

> 滚动到指定位置，重复的操作是不累加的

#### 让滚动条滚动了指定距离

window.scrollBy(x, y)

> 滚动了指定的距离，重复操作是累加的

### 查看可视窗口尺寸

#### W3C 标准方法

window.innerWidth / window.innerHeight

+ 现在网站的标准宽度一般是 1440px

+ 对于同一个大小的浏览器窗口，如果页面的缩放比例是不同的，那么他的可视区的大小也是不同的

  即把一个浏览器窗口固定大小，在页面缩放比例 100% 下求得一个 window.innerWidth，在缩放比例 150%下求得一个 window.innerWidth，后者的值小于前者的值。相当于是拿放大镜看同一块区域，看到的内容肯定要少了

#### IE9 以下版本方法

IE9 以下浏览器不兼容 w3c 的方法，使用以下两种方法

+ 标准模式下使用

  document.documentElement.clientWidth / document.documentElement.clientHeigth

+ 非标准模式下使用

  document.body.clientWidth / document.body.clientHeight

> 标准模式、非标准模式(怪异模式 / 混杂模式)
>
> 这里的模式说的是浏览器的渲染模式，如果把页面中的<!doctype html>去掉，就进入了怪异模式，加上就是标准模式怪异模式是为了解决浏览器向下兼容的问题: 浏览器升级的过程中，会更新一些语法规则，这些准则在标准模式下是不兼容的，那想象这样一个场景，一个工程师在IE8版本写的一个页面，当更新到IE9时，一些语法不兼容的情况下，该怎么去访问这个页面，怪异模式就是为了解决这样的问题，浏览器使用怪异模式渲染的情况下，可以向下兼容几个版本(具体几个版本不同的浏览器是不一样的)
>
> 怎么判断浏览器处于标准模式还是非标准模式：
>
> 利用 document.compatMode
>
> + 标准模式下的返回值：'CSS1Compat'
> + 怪异模式下的返回值：'BACKCompat'

#### 兼容性方法

封装一个解决不同版本浏览器对于查看窗口尺寸兼容性问题的兼容性方法

```javascript
function getViewPortOffset() {
    if (!window.innerWidth) {
        return {
            w: window.innerWidth,
            h: window.innerHeight
        }
    } else {
        if (document.compatMode == 'CSS1Compat') {
            return {
                w: document.documentElement.clientWidth,
                h: document.documentElement.clientHeight
            }
        } else {
            return {
                w: document.body.clientWidth,
                h: document.body.clientHeight
            }
        }
    }
}
```

### 查看元素尺寸、位置

#### 常用方法

+ dom.offsetWidth / dom.offsetHeight

  + 查看dom元素的宽高
  + 包含padding、border
  + 不包含margin

  ```html
  <div style="width:100px;height:100px;background-color:red;border:5px solid black;padding:5px;margin-left:20px"></div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
      console.log(div.offsetWidth);
      console.log(div.offsetHeight);
  </script>
  ```

+ dom.offsetLeft / dom.offsetTop

  + 查看元素位置
  + 对于父级没有定位的元素的，返回该元素相对于文档的坐标；对于父级有定位的元素，返回该元素相对于最近的有定位的父级的坐标。（这句话只强调了父级元素有没有定位，和被查看的元素本身有没有定位没有关系）

  ```html
  <div class="wrapper" style='width:100px;height:100px;background-color:green;'>
      <div class="inner" style='width:50px;height:50px;background-color:red;'></div>
  </div>
  <script type="text/javascript">
      var divWrapper = document.getElementsByTagName('div')[0];
      var divInner = divWrapper.getElementsByTagName('div')[0];
      divWrapper.style.position = 'static';
      // divWrapper.style.position = 'absolute';
      divInner.style.margin = '22px';
  </script>
  ```

  为了测试父级元素有没有定位对位置的影响， 先测试以上代码，然后将 divWrapper.style.position = 'static' 注释掉，将原来的注释关闭，再进行测试，观察两次测试的结果

  > 提示：左右margin相加，上下margin合并

+ 查看有定位父级元素

  返回最近的有定位的父级，如无，返回body，body.offsetParent 返回 null

#### 不常用方法

dom.getBoundingClientRect()

+ 返回一个对象，有top、right、bottom、left、width、height等属性
+ 兼容性很好，只在老版本IE中，height和width属性没有实现
+ 返回结果不是实时的
+ 返回值有时会出现小数
+ 这个方法不常用，了解即可

### 脚本化CSS

#### 读写css属性

dom.style

+ 返回值是一个名称为 'CSSStyleDeclaration' 的类数组，这个数组保存了css的所有属性

+ 读写操作的对象是dom元素的  **行间样式**

  在dom元素行间设置的css样式，才会出现在 CSSSstyleDeclararion 类数组的索引属性上；css所有的属性都在这个类数组中，只不过在行间设置的css属性，它才会以索引属性的形式出现在类数组中。

  ```html
  // head
  <style type="text/css">
      .demo { opacity: 0.5; }
  </style>
   
  // body
  <div class="demo" style='width:100px;height:100px;background-color:red;'></div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
      console.log(div.style);
  </script>
  ```

  这个demo一共在两个地方设置css样式，但是在head内设置的css样式，并没有在 CSSStyleDeclaration 中以索引属性的形式展示出来；而在demo行间设置的css样式，都展示了出来，说明 dom.style 只能读写 **行间样式**

+ **读写行间样式**

  + 读

    div.style.prop

  + 写

    div.style.prop = '...'

  + 没有兼容性问题

  + 组合单词变成小驼峰式写法

    background-color ---> backgroundColor

  + 有些css属性名是js中的关键字或者保留字，用另一种名称进行读写

    eg. float ---> cssFloat

  + 复合属性需要拆解

    eg. background: 1px solid red;

    ​       ---->

    ​       backgroundWidth: 1px;    backgroundStyle: solid;    backgroundColor: red;

    > 现在的语法不拆解也支持，但是建议拆开来写

  + 写入的之必须是字符串格式

    dom.style.backgroundColor = 'green';

  + JS中可以写入css的方法就这么一个，其他的都只是能够读取，不能写入

#### 查询计算样式

##### window.getComputedStyle(elem, null)

+ 两个参数

  元素节点 和 null / 伪元素

+ 属性值

  查询到的属性值是元素在浏览器中展现出来的样式的属性值，即这个无论以哪种方式设置的样式，最终展现出来的样式是什么，查询到的就是什么

+ 计算样式只读

  window.getComputedStyle(elem, null)[prop]

+ 返回的计算样式都是绝对值，没有相对单位

  这里说的绝对值不是数学意义上的那个绝对值，而是说他的返回值都是经过计算的，已经将一些相对单位进行了转换。比如给某元素设置得字体大小是 '1em'，用这个方法查询到的字体大小是 '16px'

+ IE9以下不兼容

+ 关于第二个参数 null

  这个参数是用来读取伪元素的： window.getComputedStyle(elem, 'after / before')[prop]

##### elem.currentStyle

+ 返回一个 CSSSstyleDeclaration 对象

+ 样式只读

  elem.currentStyle[prop]

+ 属性值不是绝对值

+ IE独有的属性

##### 兼容性方法

```javascript
function getStyle(elem, prop) {
    if (window.getComputedStyle) {
        return window.getComputedStyle(elem, null)[prop];
    } else {
        return elem.currentStyle[prop];
    }
}
```