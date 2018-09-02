---
title: DOM继承树(DOM 接口)
date: 2018-05-12 23:13:21
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

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fpymq5jvpdj30fq0ds74h.jpg)

1. 图中的构造函数我们不能拿来构造对象，这是系统自己构造对象用的构造函数

2. document 对象的直接构造函数是 HMTLDocument()，而 document 对象的最终继承对象是 Object，可以通过原型链查看：document.\_\_proto\_\_.\_\_proto\_\_.\_\_proto\_\_.__proto\_\_.\_\_proto\_\_

3. getElementById 方法定义在 Document.prototype 上，HTML 和 XML 的 document 元素都可以使用这个方法，而 Element 元素不能使用这个方法

4. getElementsByName 方法定义在 HTMLDocument.prototype 上，即非 HTML 中的 document 元素不能使用（XMLDocument、Element）

5. getElementsByTagName、getElementsByClassName、querySelector、querySelectorAll这些方法在Document.prototype 和 Element.prototype上均有定义，也就是说 document 元素和 Element 元素均能使用这些方法

   ```html
   <div class="wrapper">
       <div class="inner"></div>
   </div>
   <script type="text/javascript">
       var divWrapper = document.getElementsByTagName('div')[0];
       var divInner = divWrapper.getElementsByTagName('div')[0];
       console.log(divInner);
   </script>
   ```

6. HTMLDocument.prototype 定义了一些 常用的属性，body、head 分别指代 HTML 文档中的 `<body>`和`<head>` 标签，不用专门取出来使用，直接 document.body 、document.head 就可以

7. Document.prototype 上定义了 documentElement 属性，指代文档的根元素，在HTML文档中，指代`<html>` 元素，即如果要使用 html 元素，直接用 document.documentElement 即可

   ```html
   <script type="text/javascript">
       console.log(document.body);
       console.log(document.head);
       console.log(document.documentElement);
   </script>
   ```