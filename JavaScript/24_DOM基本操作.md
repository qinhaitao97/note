---
title: DOM基本操作
date: 2018-05-13 21:33:41
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

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu9p46dcxlj30kp07pjss.jpg)

### 创建DOM元素

#### document.createElement()

创建元素节点

#### document.createTextNode()

创建文本节点

#### document.createComment()

创建注释结点

#### document.createDocumentFragment()

创建文本碎片结点（以后讲）

``` html
<script type="text/javascript">
    var divNew = document.createElement('div');
    var textNew = document.createTextNode('This is a text');
    var commentNew = document.createComment('This is a comment');
    document.body.appendChild(divNew);
    document.body.appendChild(textNew);
    document.body.appendChild(commentNew);
    console.log(document.body);
</script>
```

### 添加DOM元素

#### parentNode.appendChild()

+ 向父元素节点中插入子节点，任何一个元素节点中都有这个方法

+ 插入顺序：可以吧append方法比作push方法，向末尾插入

  ```html
  <div class="parentNode"></div>
  <script type="text/javascript">
      var divParent = document.getElementsByTagName('div')[0];
      var firstText = document.createTextNode('第一个插入的');
      var secondText = document.createTextNode('第二个插入的');
      var thirdText = document.createTextNode('第三个插入的');
      divParent.appendChild(firstText);
      divParent.appendChild(secondText);
      divParent.appendChild(thirdText);
      console.log(divParent);
  </script>
  ```


+ 将文档中一个元素从一个位置插入到另一个位置，实现的是剪切操作

  ```html
  <div class="box1"></div>
  <div class="box2">
      <div class="box2Inner"></div>
  </div>
  <script type="text/javascript">
      var divBox1 = document.getElementsByTagName('div')[0];
      var divBox2 = document.getElementsByTagName('div')[1];
      var divBox2Inner = divBox2.getElementsByTagName('div')[0];
      divBox1.appendChild(divBox2Inner);
      console.log(divBox1);
  </script>
  ```

#### parentNode.insertBefore(a, b)

在父元素下的子节点 b 之前 插入 a 节点

```html
<div class="wrapper">
    <div class="divOrigin"></div>
</div>
<script type="text/javascript">
    var divWrapper = document.getElementsByTagName('div')[0];
    var divOrigin = divWrapper.getElementsByTagName('div')[0];
    var divNew = document.createElement('div');
    divNew.className = 'divNew';
    divWrapper.insertBefore(divNew, divOrigin);
    console.log(divWrapper);
</script>
```

> 写这个 demo 时有个思考，关于之前提到的 documen.getElementsByTagName() 方法是动态选取元素：
>
> divOrigin 是用 getElementsByTagName 方法选取出来的元素，在没有进行后面的添加操作前，它是divWrapper 元素的第一个子元素；当后面添加了新的元素后，divNew 成了 divWrapper 的第一个元素，那么之前选取出来的 divOrigin 有没有动态的更新呢？
>
> 答案当然是没有，动态更新的是用这个方法选取出来的类数组，divOrigin 已经是一个确定的值了， 不会再动态更新

### 删除DOM元素

#### parentNode.removeChild(node)

+ 父元素删除自己的一个子节点
+ 这个方法的返回值是被删除的节点对象，所以这个操作相当于是剪切操作

```html
<div class="wrapper">
    <div class="inner"></div>
</div>
<script type="text/javascript">
    var divWrapper = document.getElementsByTagName('div')[0];
    var divInner = divWrapper.getElementsByTagName('div')[0];
    divWrapper.removeChild(divInner);
    console.log(divWrapper);
</script>
```

#### node.remove()

+ 节点自己将自己删除，没有返回值
+ ES5中的新方法，IE9+可以自己填充remove()方法（这个问题先记下，用到再查）

```html
<div class="wrapper">
    <div class="inner"></div>
</div>
<script type="text/javascript">
    var divWrapper = document.getElementsByTagName('div')[0];
    var divInner = divWrapper.getElementsByTagName('div')[0];
    divInner.remove();
    console.log(divWrapper);
    divWrapper.remove();
    console.log(document.body);
</script>
```

> 这个demo说明，如果被删除节点下还有子节点，那么这些子节点也都会被一起删除

### 替换DOM元素

#### parentNode.replaceChild(new, origin)

+ 将父节点中某一个子节点替换成新的节点
+ 返回被替换对象的引用

```html
<div class="wrapper">
    <div class="inner"></div>
</div>
<script type="text/javascript">
    var divWrapper = document.getElementsByTagName('div')[0];
    var divInner = divWrapper.getElementsByTagName('div')[0];
    var spanNew = document.createElement('span');     
    divWrapper.replaceChild(spanNew, divInner);
    console.log(divWrapper);
</script>
```

### Element节点的一些属性

#### innerHTML

+ 可以查看元素的 HTML 的结构内容

+ 可以修改元素的 HTML

+ 可以向 HTML 结构里面添加结构

+ IE 兼容

  ```html
  <div class="wrapper">
      <div class="inner" style="width:100px;height:100px;background-color:green;">text</div>
  </div>
  <script type="text/javascript">
      var divWrapper = document.getElementsByTagName('div')[0];
      var divInner = divWrapper.getElementsByTagName('div')[0];
   
      // 查看元素HTML的内容结构
      console.log(divWrapper.innerHTML);
   
      // 修改元素HTML的内容结构
      divInner.innerHTML = 'textNew';
      console.log(divInner.innerHTML);
   
      // 向元素HTML结构中添加结构，会把原来的内容都覆盖掉
      divWrapper.innerHTML = "<span style='color:red;'>把原来的内容覆盖掉了</span>";
  ```

#### innerText

+ 查看元素的文本内容
+ 修改元素的文本内容(覆盖)
+ 与老版本火狐不兼容，老版本的火狐实现相同功能用的是 textContent() 方法，但是这个方法又和老版本的 IE不兼容；现代主流浏览器普遍支持 innerText

```html
<div class="wrapper">
    <div class="inner">text</div>
</div>
<script type="text/javascript">
    var divWrapper = document.getElementsByTagName('div')[0];
    var divInner = divWrapper.getElementsByTagName('div')[0];
 
    divInner.innerText = 'textNew';
    console.log(divInner.innerText);       
</script>
```

### Element 节点的一些方法

#### setAttribute(name, value)

给元素节点设置属性

#### getAttribute(name)

获取元素节点的属性

```html
<div></div>
<script type="text/javascript">
    var div = document.getElementsByTagName('div')[0];
    div.setAttribute('class', 'demo');
    console.log(div);
    var divClassName = div.getAttribute('class');
    console.log(divClassName);
</script>
```