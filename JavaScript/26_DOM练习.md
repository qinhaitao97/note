---
title: DOM练习
date: 2018-05-15 17:13:31
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

> 功能：封装一个方法，要求返回给定元素节点下的所有子元素节点（不使用children）
>
> 要求：原型链上编程
>
> 具体描述：及自己写一个方法，实现children的功能

```javascript
Element.prototype.myChildren = function () {
var tmpObj = {
    length: 0,
    push: Array.prototype.push,
    splice: Array.prototype.splice
}
var nodes = this.childNodes,
    len = nodes.length;
for (var i = 0; i < len; i++) {
    if (nodes[i].nodeType == 1) {
        tmpObj.push(nodes[i]);
    }
}
return tmpObj;
}
```

> 功能：遍历元素节点树
>
> 要求：原型链上编程
>
> 具体描述：要求打印每一个元素节点以及层级关系
>
> 思路：可以利用广度优先遍历

 ```js

 ```

> 功能：封装函数，返回元素e的第n层祖先元素节点
>
> 要求：原型链上编程

```javascript
Element.prototype.ancestor = function (n) {
    var elemNode = this;
    while (n-- && elemNode) {
        elemNode = elemNode.parentElement;
    }
    return elemNode;
}
```

> 功能：封装函数，返回元素e的第n个兄弟元素节点
>
> 要求：在原型链上编程
>
> 具体描述：n为正，返回后面的兄弟元素节点；n为负，返回前面的兄弟元素节点；n为0，返回自身

```javascript
Element.prototype.sibling = function (n) {
    var elemNode = this,
        loop = Math.abs(n);
    while (loop-- && elemNode) {
        elemNode = n > 0 ? elemNode.nextElementSibling : elemNode.previousElementSibling;
    }
    return elemNode;
}
```

> 功能：封装函数，判断给定元素节点下有没有元素子节点
>
> 要求：原型链上编程，不能使用children

```javascript
Element.prototype.hasElementChild = function () {
    var nodes = this.childNodes,
        len = nodes.length;
    for (var i = 0; i < len; i++) {
        if (nodes[i].nodeType == 1) {
            return true;
        }
    }
    return false;
}
```

> 给文档中的所有标签添加一个 thisname 属性，属性值为他们的标签名

```javascript
function addArr() {
    var arr = document.getElementsByTagName('*'),
        len = arr.length;
    for (var i = 0; i < len; i++) {
        arr[i].setAttribute('thisname', arr[i].nodeName);
    }
}
```

小技巧：用通配符选择文档中所有的标签

> 功能：使用标准的DOM方法或属性，实现以下DOM结构

```html
<div class="example">
    <p class="slogan">sth</p>
</div>
```

```html
<script type="text/javascript">
    var div = document.createElement('div'),
        p = document.createElement('p'),
        script = document.getElementsByTagName('script')[0];
 
    div.className = 'example';
    p.className = 'slogan';
    p.innerText = 'text';
 
    div.appendChild(p);
    document.body.insertBefore(div, script);
</script>
```

> 功能：封装函数 insertAfter()， 功能类似 insertBefore()
>
> 要求：
>
> + 在原型链上编程
> + 忽略老版本浏览器的兼容性问题

```javascript
Element.prototype.insertAfter = function (newNode, originNode) {
    if (!originNode.nextSibling) {
        this.appendChild(newNode);
    } else {
        this.insertBefore(newNode, originNode.nextSibling);
    }
}
```

> 功能：封装函数，功能是将节点内部的节点顺序逆序
>
> 要求：在原型链上编程

```javascript
Element.prototype.reverse = function () {
    var nodes = this.childNodes,
        len = nodes.length,
        startLoc = len - 2;
    for (var i = startLoc; i >= 0; i--) {
        this.appendChild(nodes[i]);
    }
}
```

> 功能：封装一个函数，求元素相对于文档的坐标
>
> 要求：在原型链上编程

```javascript
Element.prototype.getElementPosition = function () {
    var w = 0,
        h = 0,
        node = this;
    while (node) {
        w += node.offsetLeft;
        h += node.offsetTop;
        node = node.offsetParent;
    }
    return {
        w: w,
        h: h
    }
}
```

> 功能：封装一个函数解决 getElementsByClassName() 的兼容性
>
> 要求：在原型链上编程
>
> 注意：因为 getElementsByClassName() 在 Document 和 在Element上均有定义，所以兼容性方法也要分别在这两个原型链上

```javascript
// Document原型链上
Document.prototype.getByClassName = function(className) {
    if (this.getElementsByClassName) {
        return this.getElementsByClassName(className);
    } else {
        // 首先用兼容性较好的方法把所有标签都取出来
        var allDom = this.getElementsByTagName('*'),
            allDomArr = Array.prototype.slice.call(allDom, 0),
            ansArr = [];
 
        // 判断该dom节点的className是否满足要求
        function isTrue(dom) {
            // 用正则表达式将所有的连续空格替换为一个空格，并将首尾的空格去掉
            var oClassName = dom.className,
                reg = /\s+/g;
            oClassName = oClassName.replace(reg, ' ').trim();
 
            // 将字符串以空格为分隔符拆成数组
            var oClassNameArr = oClassName.split(' '),
                oClassNameArrLen = oClassNameArr.length;
 
            // 满足要求则返回true
            for (var i = 0; i < oClassNameArrLen; i++) {
                if (oClassNameArr[i] == className) {
                    return true;
                }
            }
            return false;   
        }
 
        allDomArr.forEach(function(elem, index) {
            if (isTrue(elem)) {
                // 满足要求就添加到新的数组中
                ansArr.push(elem);
            }
        });
        return ansArr;
    }
}
 
// Element原型链上
Element.prototype.getByClassName = function(className) {
    if (this.getElementsByClassName) {
        return this.getElementsByClassName(className);
    } else {
        var allDom = this.getElementsByTagName('*'),
            allDomArr = Array.prototype.slice.call(allDom, 0),
            ansArr = [];
 
        function isTrue(dom) {
            var oClassName = dom.className,
                reg = /\s+/g;
            oClassName = oClassName.replace(reg, ' ').trim();
 
            var oClassNameArr = oClassName.split(' '),
                oClassNameArrLen = oClassNameArr.length;
 
            for (var i = 0; i < oClassNameArrLen; i++) {
                if (oClassNameArr[i] == className) {
                    return true;
                }
            }
            return false;   
        }
 
        allDomArr.forEach(function(elem, index) {
            if (isTrue(elem)) {
                ansArr.push(elem);
            }
        });
        return ansArr;
    }
}
```