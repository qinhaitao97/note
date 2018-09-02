---
title: DOM节点
date: 2018-05-12 16:33:51
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

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu9o9u8ngnj30ew0az0tg.jpg)

### DOM节点

> 这一部分可以先看第1点，然后跳过2、3点，看完后面再回来看2、3点

#### 节点层次

DOM 可以将任何 HTML 或 XML 文档描绘成一个由多层次节点构成的结构。节点分为几种不同类型，每种类型分别表示文档中不同的信息或标记。每个节点都拥有各自的特点，数据和方法，另外也与其它节点存在某种关系。节点之间的关系构成了层次，而所有页面标记则表现为一个以特点节点为根节点的树形结构。以下面的 HTML 为例：

```html
<html>
    <head>
        <title>Sample Page</title>
    </head>
    <body>
        <p>Hello world!</p>
    </body>
</html>
```

将这个简单的HTML文档表示为一个层次结构图：

![nodeModle](https://ws1.sinaimg.cn/large/006eYMu7ly1fpy374nbtuj30oo0c4mxf.jpg)

Document 代表整个文档。\<html> 元素是每个文档的根节点，也是文档唯一的一个直接子节点，我们称 \<html>为文档元素。在 HTML 页面中，文档元素始终都是 \<html> 元素，在 XML 中，没有预定义的元素，任何元素都可能成为文档元素。

#### 结点类型

+ 介绍

  文档中的元素可以分为四大类节点：

  - 元素节点

    HTML元素通过元素节点表示

  - 特性节点

    特性通过特性节点表示

  - 文档类型节点

    文档类型通过文档类型节点表示

  - 注释结点

    注释通过注释结点表示

  这四大类型包括12种结点，他们都继承自一个基类型，Node 类型。DOM1 定义了一个 Node 接口，这个接口在 JavaScript 中是作为 Node 类型实现的；除了 IE 之外，其他所有的浏览器 中都可以访问到这个类型。JavaScript 中所有的结点类型都继承自 Node 类型，因此所有的结点类型都共享着相同的基本属性和方法。

+ 判断

  在 JavaScript 中该如何判断一个节点是哪一种节点呢？

  每一个节点都有一个 nodeType 属性，用于表明该节点的类型。节点类型由在 Node 类型中定义的下列 12 个数值常量来表示，任何节点必居其一：

  + Node.ELEMENT_NODE(1)
  + Node.ATTIRIBUTE_NODE(2)
  + Node.TEXT_NODE(3)
  + Node.CDATA_SECTION_NODE(4)
  + Node.ENTITY_REFERENCE_NODE(5)
  + Node.ENTITY_NODE(6)
  + Node.PROCESSING_INSTRUCTION_NODE(7)
  + Node.COMMENT_NODE(8)
  + Node.DOCUMENT_NODE(9)
  + Node.DOCUMENT_TYPE_NODE(10)
  + Node.DOCUMENT_FRAGMENT_NODE(11)
  + Node.NOTATION_NODEF(12)

  > 括号外面的部分代表常量名称，括号中部分代表常量名称对应的数值，一般在判断节点类型时用nodeType 属性和数值进行比较，因为IE没有公开 Node 类型的构造函数，因此通过 nodeType 与常量名进行比较的话在 IE 中无法实现，为了浏览器兼容，用数值比较即可

  记住几个常用的节点类型，即其相应的数值即可

  

  |          常用节点类型          | nodeType数值 |
  | :----------------------------: | :----------: |
  |            元素节点            |      1       |
  |            属性节点            |      2       |
  |            文本节点            |      3       |
  |            注释结点            |      8       |
  |            Document            |      9       |
  | DocumentFtagment(文档碎片结点) |      11      |

#### 节点属性

+ nodeName

  元素的标签名，以大写形式表示，只读(不可修改)，IE兼容

  ```html
  <div class="demo">
      <input type="hidden" name="inputName">
  </div>
  <script type="text/javascript">
      var div = document.getElementsByClassName('demo')[0];
      var input = document.getElementsByTagName('input')[0];
      console.log(document.nodeName);
      console.log(div.nodeName);
      console.log(input.nodeName);
   
      // 只读，不可修改
      div.nodeName = 'divDemo';
      console.log(div.nodeName);
  </script>
  ```

  > 注意:
  >
  > + nodeName 是标签的名字，而不是元素的属性 name 的值，参照以上代码中的 input
  > + nodeName 只读，不可修改，参照以上代码中修改后的输出

+ nodeValue

  节点的值，只有文本和注释结点的这个属性值有意义，且值可以修改，IE 兼容

  ```html
  <div>
      text
      <!-- comment -->
      <p>textInP</p>
  </div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0],
          nodes = div.childNodes;
      console.log(nodes[0].nodeValue);
      console.log(nodes[1].nodeValue);
      console.log(nodes[2].nodeValue);
   
      // nodeValue值可以修改
      nodes[0].nodeValue = 'textInDiv';
      console.log(nodes[0].nodeValue);
  </script>
  ```

+ nodeType

  节点类型常量对应的数值，IE兼容

  ```html
  <div>
      text
      <!-- comment -->
      <p>textInP</p>
  </div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0],
          nodes = div.childNodes;
      console.log(nodes[0].nodeType);
      console.log(nodes[1].nodeType);
      console.log(nodes[3].nodeType);
      console.log(document.nodeType);
  </script>
  ```

+ attributes

  代表一个元素的属性集合，属性值可以修改，属性名不可以修改，IE 兼容(了解即可，一般不用)

  ```html
  <div class="demo"></div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
   
      console.log(div.attributes[0].nodeType);
   
      // 属性值可以修改
      console.log(div.attributes[0].value);
      div.attributes[0].value = 'newValue'
      console.log(div.attributes[0].value);
   
      // 属性名不能修改
      console.log(div.attributes[0].name);
      div.attributes[0].name = 'newName'
      console.log(div.attributes[0].name);
  </script>
  ```

  可以用 getAttribute() 方法访问属性值：

  IE 兼容

  ```html
  <input type="hidden" name="demo">
  <script type="text/JavaScript">
      var input = document.getElementsByTagName('input')[0];
      console.log(input.getAttribute('type'));
      console.log(input.getAttribute('name'));
  </script>
  ```

  ​

  > class 的值可以一般 'className' 属性访问，不用上面的方法

  ```html
  <div class="demo"></div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
      console.log(div.className);
  </script>
  ```

### 查看DOM节点

#### 通过选择的方法查看元素节点

通过选择的方法，文档中的元素节点，返回值可能是元素对象或者类数组 (方法中写法是 element 的返回元素对象，方法中写法是 elements 的返回类数组)

+ document.getEelementById()

  + 通过id查找文档中的元素，返回元素对象
  + IE9 以下的浏览器会把 name 属性也当做 id 匹配，且不区分大小写
  + id 标签一般作为顶级框架的名称存在，在 html 的结构搭建中一般不要使用 id 选择器

  ```html
  <div id="demo"></div>
  <script type="text/javascript">
      var div = document.getElementById('demo');
      console.log(div);
  </script>
  ```

+ document.getElementsByTagName()

  + 通过标签名查找元素，返回类数组
  + IE兼容
  + 开发中常用

  ```html
  <div class="wrapper">
      <div class="inner"></div>
  </div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div');
      console.log(div);
      console.log(div[0].className);
      console.log(div[1].className);
  </script>
  ```

  一般用哪个标签，就直接取到那个标签，比如要用上个代码中的 inner

  > var divInner = document.getElementsByTagName('div')[1];

+ document.getElementsByClassName()

  + 通过类名查找标签，返回类数组
  + IE9 以下没有这个方法

  ```html
  <div class="wrapper">
      <div class="inner"></div>
  </div>
  <div class="wrapper"></div>
  <script type="text/javascript">
      var divWrapper = document.getElementsByClassName('wrapper')[0];
      console.log(divWrapper.className);
  </script>
  ```

+ document.getElementsByName()

  + 通过元素的名字查找标签，返回类数组
  + IE 兼容但是 IE9 及以下不好用
  + 一般不用

  ```html
  <input type="hidden" name="demo">
  <script type="text/javascript">
      var input = document.getElementsByName('demo')[0];
      console.log(input);
  </script>
  ```

  > 这里有一个疑问？
  >
  > 观察这段代码在 chrome 以及 IE11 浏览器上的运行结果，发现 input 标签内 type 和 name 属性的顺序是不同的，这是为什么呢？如果是这样，那按下表访问属性的话不就会出现差错呢？

+ document.querySelector()

  + css 选择器，选择元素的规则和 css 选择元素的规则是一样的，返回元素对象
  + IE8 以下不兼荣

  ```html
  <div>
      <p>
          <span></span>
      </p>
  </div>
  <script type="text/javascript">
      var span = document.querySelector('div>p>span');
      console.log(span);
  </script>
  ```

+ document.querySelectorAll()

  + 与 querySelector() 功能类似，只不过这个选择满足复合条件的所有元素，返回类数组
  + IE8 以下不兼荣

  ```html
  <div>
      <p>
          <span></span>
          <span></span>
          <span></span>
      </p>
  </div>
  <script type="text/javascript">
      var span = document.querySelectorAll('div>p>span');
      console.log(span);
  </script>
  ```

  虽然用 css 选择器的方法选择元素既直观又方便，但是开发中一般是不用这种方法选取元素的，原因如下：

  + 兼容性不好，IE8 以下不兼容
  + css 选择器选择元素的机制是静态的，不是实时的：即用这种方法选择出来的元素，当做副本存储起来了，这之后对页面结构做出任何的调整，都不会影响到之前已经选择出来的内容，无法做到实时更新。举个例子，比如某 p 标签下原来有 3 个 span 元素，这时分别用 document.querySelectorAll()  和 document.getElementsByTagName() 两种方法将3个span元素选择出来，然后用新建一个 span 元素，并把它添加到 p 中去，这时 p 中变成了 4 个 span，用前一种方法选择出来的 span 还是3个，而用后者选择出来的 span 元素是4个，是实时更新的

  ```html
  <div>
      <p>
          <span></span>
          <span></span>
          <span></span>
      </p>
  </div>
  <script type="text/javascript">
      var span = document.querySelectorAll('div>p>span');
      var spanTmp = document.getElementsByTagName('span');
      var newSpan = document.createElement('span');
      var p = document.getElementsByTagName('p')[0];
      p.appendChild(newSpan);
      console.log(span);
      console.log(spanTmp);
  </script>
  ```

#### 通过节点树查看节点（遍历节点树）

+ parentNode

  + DOM元素的父节点，一个元素的父节点只有一个，返回元素对象
  + IE兼容

  ```html
  <div>
      <span></span>
  </div>
  <script type="text/javascript">
      var span = document.getElementsByTagName('span')[0];
      console.log(span.parentNode);
      console.log(span.parentNode.parentNode);
      console.log(span.parentNode.parentNode.parentNode);
      console.log(span.parentNode.parentNode.parentNode.parentNode);
      console.log(span.parentNode.parentNode.parentNode.parentNode.parentNode);      
  </script>
  ```

+ childNodes

  + DOM元素的子节点们，一个DOM元素可能有很多子节点，返回类数组
  + IE9以下会自动忽略掉空格、回车、换行等文本节点

  ```html
  <div>
      textNode
      <!-- commentNode -->
      textNode
      <span></span>
      textNode
  </div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
      console.log(div.childNodes.length);
   
      // 观察div.childNodes的组成
      console.log(div.childNodes);
  </script>
  ```

  一定要清除，这里的 div.childNodes.length 为什么是 5 而不是 1：

  因为 childNodes 代表 DOM 元素的子节点，而不仅仅是元素节点，在 div 中除了有 span 元素节点，还有 1个注释结点，3 个文本节点（textNode)

+ firstChild / lastChild

  + 选择DOM元素的 第一个 / 最后一个 节点，返回元素对象
  + IE兼容

  ```html
  <div>
      textNode1
      <!-- commentNode -->
      textNode2
      <span></span>
      textNode3
  </div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
      console.log(div.firstChild);
      console.log(div.lastChild);
  </script>
  ```

+ nextSibling / previousSibling

  + 选择 下一个 / 上一个 兄弟结点，返回元素对象
  + IE兼容

  ```html
  <div>
      textNode1
      <!-- commentNode -->
      textNode2
      <span></span>
      textNode3
  </div>
  <script type="text/javascript">
      var span = document.getElementsByTagName('span')[0];
      console.log(span.previousSibling);
      console.log(span.nextSibling);
  </script>
  ```

+ 子节点的个数

  childNodes.length

#### 通过元素节点树来查看元素节点（遍历元素节点树）

以下方法中，除children外，都是IE9以下不兼容

+ parentElement

  DOM节点的父元素节点，返回元素对象

  ```html
  <div></div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
      console.log(div.parentElement);
      console.log(div.parentElement.parentElement);
      console.log(div.parentElement.parentElement.parentElement);
  </script>
  ```

  第三个打印结果是 null，说明document不属于元素节点的范畴

+ children

  DOM元素的子元素节点们，返回类数组

  ```html
  <div>
      <!-- comment -->
      <p></p>
      <span></span>
  </div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
      console.log(div.children[0]);
      console.log(div.children[1]);
  </script>
  ```

+ firstElementChild / lastElementChild

  DOM元素的 第一个 / 最后一个 元素节点，返回元素对象

  ```html
  <div>
      <!-- comment -->
      <p></p>
      <span></span>
      <strong></strong>
  </div>
  <script type="text/javascript">
      var div = document.getElementsByTagName('div')[0];
      console.log(div.firstElementChild);
      console.log(div.lastElementChild);
  </script>
  ```

+ nextElementSibling / previousElementSibling

  DOM元素 下一个 / 前一个 兄弟元素节点，返回元素对象

  ```html
  <div>
      <!-- comment -->
      <p></p>
      <span></span>
      <strong></strong>
  </div>
  <script type="text/javascript">
      var span = document.getElementsByTagName('span')[0];
      console.log(span.nextElementSibling);
      console.log(span.previousElementSibling);
  </script>
  ```

+ 子元素节点的个数

  children.length == childElementCount

#### hasChildNodes()

判断一个元素有没有子节点，返回值类型时 boolean

```html
<div></div>
<script type="text/javascript">
    var div = document.getElementsByTagName('div')[0];
    console.log(div.hasChildNodes());
</script>
```

false，div 中没有任何节点

```html
<div>
</div>
<script type="text/javascript">
    var div = document.getElementsByTagName('div')[0];
    console.log(div.hasChildNodes());
</script>
```

true，div 中有一个文本节点

#### nodeName 和 tagName
获取标签的名称，待补充
https://blog.csdn.net/wmjblog/article/details/9949035
https://blog.csdn.net/borishuai/article/details/5719227