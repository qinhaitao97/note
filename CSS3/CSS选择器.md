### 基本选择器



| 选择器 | 含义                                           |
| ------ | ---------------------------------------------- |
| *      | 通配符选择器，选择任何元素                     |
| E      | 标签选择器，匹配所有使用E标签的元素            |
| .demo  | class选择器，匹配所有class属性中包含info的元素 |
| \#demo | id选择器，匹配所有id属性等于demo的元素         |

**demo**

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }
        p { font-size: 30px; }
        .demo1 { color: red; }
        #demo2 { color: green; }
    </style>
</head>
 
<body>
    <span>1</span>
    <p class="demo1">2</p>
    <p class="demo1 demo2">3</p>
    <p id="demo2">4</p>
</body>
 
</html>
```

### 多元素的组合选择器



| 选择器 | 含义                                                         |
| ------ | ------------------------------------------------------------ |
| E, F   | 多元素选择器，同时匹配所有E元素或者F元素，E和F之间用逗号分隔 |
| E  F   | 后代元素选择器，匹配所有属于E元素**后代的**F元素，E和F之间用空格分隔 |
| E > F  | 子元素选择器，匹配所有E元素的**子元素**F                     |
| E + F  | 毗邻元素选择器，匹配所有紧随E元素**之后**的**同级元素**F     |

**注意：**

1. 后代元素选择器是选择元素的后代元素，这里的后代元素包括子元素，孙元素，重孙元素等
2. 子元素选择器选择子元素，这里的子元素就只是父元素的直接子元素，不包括孙元素、重孙元素等
3. 毗邻元素选择器是选择**之后相邻**同级元素，重点是**之后相邻**和**同级元素**（之后并且相邻，不要忽略了之后）

**demo**

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        #demo1, #demo2 {
            color: red;
        }
        #demo3 span {
            color: yellow;
        }
        #demo4>span {
            color: blue;
        }
        #demo5+span {
            color: deeppink;
        }
    </style>
</head>
 
<body>
    <span id="demo1">1</span>
    <span id="demo2">2</span>
 
    <div id="demo3">
        <span>3</span>
        <p><span>4</span></p>
    </div>
 
    <div id="demo4">
        <span>5</span>
        <p><span>6</span></p>
    </div>
 
    <span>7</span>
    <p id="demo5">
        <span>8</span>
    </p>
    <span>9</span>
 
</body>
 
</html>
```

### CSS 2.1属性选择器



| 选择器       | 含义                                                         |
| ------------ | ------------------------------------------------------------ |
| E[att]       | 匹配所有具有att属性的E元素，不考虑它的值                     |
| E[att=val]   | 匹配所有att属性等于 val 的E元素                              |
| E[att~=val]  | 匹配所有att属性具有多个空格分隔的值、其中一个值等于"val"的E元素 |
| E[att\|=val] | 匹配所有att属性具有多个连字号分隔（hyphen-separated）的值、其中一个值以"val"开头的E元素，主要用于lang属性，比如"en"、"en-us"、"en-gb"等等 |

**注意**

1. 对于属性选择器，E可以省略，那么就是匹配所有满足属性条件的任何元素
2. 要区分属性和特性，特性指的是规范中有声明的属性，而属性包括特性，还包括我们自己定义的一些规范中没有声明的属性；比如对于 div 标签来讲，class、id等属于它的特性，而 name 就是它的属性；对于 input 标签来讲，name也属于它的特性。既然我们这里说的是属性选择器，那么就不只是能选择满足特性的元素，自己设置的属性也可以被选择出来

**demo**

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }
 
        /* 匹配所有具有name属性的p元素 */
        p[name] { font-size: 30px; }
 
        /* 匹配所有具有name属性的元素 */
        [name] { color: red; }
 
        /* 匹配所有class属性为 demo3 的p元素 */
        p[class='demo3'] { color: orange; }
 
        /* 匹配所有class属性中包含 demo4 的p元素 */
        p[class~='demo4'] { color: blue; }
 
        /* 匹配所有class属性中有连字号分隔的，以 demo5 开头的p元素 */
        p[class|='demo5'] { color: yellow; }
    </style>
</head>
 
<body>
    <p name='demo1'>1</p>
    <p name='demo2'>2</p>
 
    <p class="demo3">3</p>
 
    <p class="demo4 temp1">4</p>
    <p class="temp2 demo4">5</p>
 
    <p class="demo5-temp3">6</p>
    <p class="demo5">7</p><!-- 要注意这个没有连字符的也能被匹配 -->
    <p class="temp3-demo5">8</p>
</body>
 
</html>
```

### CSS 2.1 中的伪类选择器



| 选择器        | 含义                                |
| ------------- | ----------------------------------- |
| E:first-child | 匹配父元素的第一个子元素            |
| E:link        | 匹配所有未被点击的链接的E元素       |
| E:visited     | 匹配所有已被点击的链接的E元素       |
| E:active      | 匹配所有已经按下但还没有释放的E元素 |
| E:hover       | 匹配鼠标悬停其上的E元素             |
| E:focus       | 匹配获得焦点的E元素                 |
| E:lang(c)     | 匹配lang属性等于c的E元素            |

**E:first-child**

这个容易理解错，重点讲一下。这个选择器可以分成两部分，E 和 first-child

E：所要匹配的元素是E元素

first-child：所匹配的元素是它**直接父级**的**第一个子元素**

即匹配E元素直接父级下的第一个子元素，如果这个元素是E则被选中

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
            list-style: none;
        }
 
        li:first-child { color: red; }
 
    </style>
</head>
 
<body>
    <li id='demo1'>1</li>
    <ul>
        <li id='demo2'>2</li>
        <li id='demo3'>3</li>
    </ul>
</body>
 
</html>
```

我们一个一个的来分析，首先我们要匹配的元素是li，这里的三个li都满足，所以看第二个条件，li需要是它直接父级的第一个元素，对于#demo1来说，它的直接父级是body，body下第一个子元素就是#demo1，所以#demo1满足；对于#demo2，它的直接父级是ul，ul下的第一个子元素是#demo2，第二个子元素是#demo3，所以#demo2满足而#demo3不满足，接下来稍微变化一下html结构，选择器保持不变

```html
<body>
    <ul>
        <span></span>
        <li id='demo1'>1</li>
    </ul>
    <li id='demo2'>2</li>
</body>
```

还是一步一步来分析，首先第一个条件都满足，直接看第二个条件：对于#demo1来说，它的直接父级是ul，但是他不是ul下的第一个子元素，所以不满足；对于#demo2来说，它的直接父级是body，但是body的第一个子元素是ul，不是li，所以也不满足。

**demo**

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
            font-size: 30px;
        }
 
        a:link {
            color: blue;
        }
        a:visited { color: #ccc; }
 
        a:active { color: green; }
        span:active {color: green; }
 
        a:hover { font-size: 50px; }
        span:hover { font-size: 50px; }
 
        input:focus { background-color: yellow; }
 
        html:lang(en) { background-color: orange; }
 
    </style>
</head>
 
<body>
    <a href="">链接</a>
 
    <span>不是链接</span>
 
    <input type="text">
</body>
 
</html>
```

### CSS 2.1 中的伪元素



| 选择器          | 含义                                   |
| --------------- | -------------------------------------- |
| E::first-line   | 匹配E元素的第一行                      |
| E::first-letter | 匹配E元素的第一个字母                  |
| E::before       | 在E元素之前插入生成的内容（E元素内部） |
| E::after        | 在E元素之后插入生成的内容（E元素内部） |

**注意**

::before 和 ::after 这两个伪元素的之前和之后指的是**逻辑上的最前和最后**，且是在**元素内部**

**demo**

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
            width: 50px;
        }
 
        p::first-line { color: red; }
 
        p::first-letter { font-size: 30px; }
 
        div {
            width: 100px;
            height: 100px;
            border: 1px solid #000;
        }
        div::before {
            content: '';
            display: block;
            width: 20px;
            height: 20px;
            background-color: green;
        }
        div::after {
            content: '';
            display: block;
            width: 20px;
            height: 20px;
            background-color: orange;
        }
 
    </style>
</head>
 
<body>
    <p id="demo1">假装这里有很多字</p>
 
    <div id="demo2"></div>
</body>
 
</html>
```

### CSS 3 的同级元素通用选择器



| 选择器 | 含义                               |
| ------ | ---------------------------------- |
| E ~ F  | 匹配任何在E元素之后的**同级**F元素 |

**注意**

'E+F': 匹配任何在E元素之后的**毗邻同级**元素，两钟选择器只差两个字，意思稍有不同

**demo**

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
            list-style: none;
        }
 
        span~li { color: red; }
 
    </style>
</head>
 
<body>
    <ul>
        <span>1</span>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
</body>
 
</html>
```

### CSS 3 属性选择器



| 选择器        | 含义                               |
| ------------- | ---------------------------------- |
| E[att^='val'] | 属性att的值以 "val" 开头的E元素    |
| E[att$='val'] | 属性att的值以 "val" 结尾的E元素    |
| E[att*='val'] | 属性att的值包含 "val" 字符串的元素 |

**demo**

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }
 
        p[class^='demo1'] { color: red; }
 
        p[class$='demo2'] { color: blue; }
 
        p[class*='demo3'] { color: orange; }
    </style>
</head>
 
<body>
    <p class="demo1">1</p>
    <p class="demo1demo1">2</p>
    <p class="demo1 demo1">3</p>
    <p class="demo1-demo1">4</p>
 
    <p class="demo2">5</p>
    <p class="demo2demo2">6</p>
    <p class="demo2 demo2">7</p>
    <p class="demo2-demo2">8</p>
 
    <p class="demo3x">9</p>
    <p class="xdemo3x">10</p>
    <p class="xdemo3">11</p>
</body>
 
</html>
```

###  CSS 3 中用户界面相关伪类选择器



| 选择器     | 含义                                         |
| ---------- | -------------------------------------------- |
| E:enabled  | 匹配表单中激活的元素                         |
| E:disabled | 匹配表单中禁用的元素                         |
| E:checked  | 匹配表单中被选中的元素（radio、checkbox...） |

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
        }
 
        input:enabled { color: green; }
 
        input:disabled { color: red; }
 
        input:checked {
            width: 100px;
            height: 100px;
        }
 
    </style>
</head>
 
<body>
    <input id="demo1" type="text" value="激活">
 
    <input id="demo2" type="text" value="禁用" disabled>
 
    <input class="demo3" type="radio">
    <input class="demo3" type="checkbox">
</body>
 
</html>
```

备注：因为radio和checkbox不能修改默认的颜色样式，所以我用大小来区分效果

### CSS 3 中用户界面相关伪元素选择器



| 选择器       | 含义                   |
| ------------ | ---------------------- |
| E::selection | 匹配用户当前选中的元素 |

**demo**

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 100px;
            padding: 0px;
        }
 
       p::selection {
           background-color: #ccc;
           color: deeppink;
        }
    </style>
</head>
 
<body>
    <p>很多字很多字很多字很多字很多字很多字很多字很多字很多字</p>
</body>
 
</html>
```

修改之前选中文字的效果

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fse9nliro0g30i60atjrg.gif)

修改之后选中文字的效果

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fse9p0h4zug30i60atq2y.gif)

### CSS 3 中结构性伪类



| 选择器                | 含义                                                 |
| --------------------- | ---------------------------------------------------- |
| E:root                | 匹配文档的根元素                                     |
| E:empty               | 匹配一个不包含任何子元素的元素                       |
| E:nth-child(n)        | 匹配父元素的第n个子元素                              |
| E:nth-last-child(n)   | 匹配父元素的第n个子元素                              |
| E:last-child          | 匹配父元素的最后一个子元素，等同于:nth-last-child(1) |
| E:only-child          | 匹配父元素仅有的一个子元素                           |
| E:first-of-type       | 匹配直接父级下同E类型元素中的第一个                  |
| E:nth-of-type(n)      | 匹配直接父级下同E类型元素中的第n个                   |
| E:nth-last-of-type(n) | 匹配直接父级下同E类型元素中的倒数第n个               |
| E:last-of-type        | 匹配直接父级下同E类型元素中的最后一个                |
| E:only-of-type        | 匹配直接父级下同E类型唯一一个子元素                  |

**注意**

1. 在html文档中，用 E:root 或者 html 都能选中根标签，但是建议使用 E:root 方法来选择根标签，因为如果在xml文档中，根标签是xml，html就不能选中根标签了，所以一般都是用 E:root 方法选中根标签

   ```html
   <!DOCTYPE html>
   <html lang="en">
    
   <head>
       <meta charset="UTF-8">
       <title>Document</title>
       <style type="text/css">
           :root { background-color: orange; }
           html { background-color: orange; }
       </style>
   </head>
    
   <body>
       <div></div>
   </body>
    
   </html>
   ```

2. E:empty 方法是匹配不包含任何子元素的元素，这里文本节点也会被当成是子元素，但是利用 ::after 或者 ::before 等伪元素添加的文本，不在判定的范围内

   ```html
   <!DOCTYPE html>
   <html lang="en">
    
   <head>
       <meta charset="UTF-8">
       <title>Document</title>
       <style type="text/css">
           * {
               margin: 0px;
               padding: 0px;
           }
           /* 给三个p元素添加一些基础样式 */
           p {
               width: 100px;
               height: 100px;
               border: 1px solid black;
               margin-top: 10px;
           }
    
           /* 利用 ::after 伪元素 给#demo3填充内容 */
           #demo3::after { content: '3'; }
    
           p:empty { background-color: orange; }
       </style>
   </head>
    
   <body>
       <p id="demo1"></p>
       <p id="demo2">2</p>
       <p id="demo3"></p>
   </body>
    
   </html>
   ```

   可以发现，虽然在#demo3中有文本，但是这个文本并不是我们直接写在html结构中的，而是用 ::after 伪元素添加进去的，所以这个文本不算在 伪类 :empty 的判定范围之内。所以说，表面上看起来有文本的元素，也是有可能被 :empty伪类选中的

3. 从 E:nth-child(n) 到 E:only-child这些伪类的理解，与之前讲过的CSS 2.1中的E:first-child伪类的理解是相似的，对比理解即可，需要注意的是**n是从1开始的**，不是从0开始。

   ```html
   <!DOCTYPE html>
   <html lang="en">
    
   <head>
       <meta charset="UTF-8">
       <title>Document</title>
       <style type="text/css">
           * {
               margin: 0px;
               padding: 0px;
               font-size: 20px;
               list-style: none;
           }
    
           ul li:nth-child(3) { color: red; }
    
           ul li:nth-last-child(2) { color: green; }
    
           ul li:last-child { color: orange; }
    
           /* ul是它直接父级元素body下的唯一子元素 */
           ul:only-child { background-color: #ccc; }
       </style>
   </head>
    
   <body>
       <ul>
           <li>1</li>
           <li>2</li>
           <li>3</li>
           <li>4</li>
           <li>5</li>
       </ul>
   </body>
    
   </html>
   ```

4. n不仅仅能填数字，还可以填表达式

   > 比如 2n、2n+1、3n+1，这时n的取值就是**从0开始递增的自然数**(0,1,2,3,4,...)，所以利用表达式可以选出来一组元素，2n(0, 2, 4, 6,...)，2n+1(1, 3, 5, 7,...)，3n+1(1, 4, 7, 10...)

   n还可以是关键字

   > even代表偶数，odd代表奇数

   ```html
   <!DOCTYPE html>
   <html lang="en">
    
   <head>
       <meta charset="UTF-8">
       <title>Document</title>
       <style type="text/css">
           * {
               margin: 0px;
               padding: 0px;
               list-style: none;
           }
    
           ul li:nth-child(2n) { color: red; }
    
           ul li:nth-child(2n+1) { color: green; }
    
           ul li:nth-child(even) { font-size: 50px; }
    
           ul li:nth-child(odd) { font-size: 40px; }
    
       </style>
   </head>
    
   <body>
       <ul>
           <li>1</li>
           <li>2</li>
           <li>3</li>
           <li>4</li>
           <li>5</li>
           <li>6</li>
       </ul>
   </body>
    
   </html>
   ```

**E:first-of-type**

这一系列的伪类选择器的理解与 E:first-child 的理解有些相似但是不同，下面重点讲解一下同样，分成两部分：

E：所要匹配的元素是E元素

first-of-type：E元素是它直接父级下同E元素类型中的第一个子元素元素

重点是后半部分的理解，看起来好像比较绕口，但其实就是在之前 E:first-child 后半部分的理解上多了一个同类型的限制，first-child的理解是其直接父级下的第一个子元素，而first-of-type不是其直接父元素下的第一个，而是在其直接父级下的所有E类型的元素中的第一个，举例说明

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
            list-style: none;
        }
 
        li:first-of-type { color: red; }
 
    </style>
</head>
 
<body>
    <ul>
        <span>1</span>
        <li id="demo1">2</li>
        <li id="demo2">3</li>
    </ul>
    <li id="demo3">4</li>
</body>
 
</html>
```

\#demo1的直接父级是ul，ul下有两种类型的元素 span 和 li，#demo1是li类型中的第一个，所以可以被选中；#demo3的直接父级是body，body有两种类型的元素 ul 和 li，#demo3是，li类型中的第一个，所以可以被选中

**E:only-of-type**

表格中E:first-of-type之后的，E:only-of-type之前的这些伪类选择器，具体的理解参照E:first-of-type即可，下面在稍微强调一下最后一个E:only-of-type，它是匹配E元素直接父级下的E类型元素，如果这类型元素有且仅有一个，则这个E类型的元素被选中，简单的说就是E的直接父级下，如果仅有一个E类型的元素，那么他将会被选中

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0px;
            padding: 0px;
            list-style: none;
        }
 
        li:nth-of-type(1) { color: red; }
 
        li:nth-last-of-type(1) { color: orange; }
 
        li:last-of-type { font-size: 30px; }
        /* span 的直接父级ul下只有一个span类型的元素，那么他可以被选中 */
        span:only-of-type { color: blue; }
 
        /* em 的直接父级ul下有两个em类型的元素，那么他不可以被选中 */
        em:only-of-type { color: deeppink; }
    </style>
</head>
 
<body>
    <li id="demo1">1</li>
    <ul>
        <span>span</span>
        <em>em</em>
        <em>em</em>
        <li id="demo2">2</li>
        <li id="demo3">3</li>
        <li id="demo4">4</li>
    </ul>
    <li id="demo5">5</li>
</body>
 
</html>
```

### CSS 3 反选伪类



| 选择器   | 含义                      |
| -------- | ------------------------- |
| E:not(x) | 匹配不符合参数x描述的元素 |

**注意**

1. x是简单的选择器（属性选择器，标签选择器，类选择器，id选择器，通配符选择器等）。其实也可以使用多元素选择器作为其参数（','分隔的那个），但是这个只是实验性的，尚未得到广泛支持，所以最好不要使用
2. :not 伪类的优先级就是他参数选择器的优先级。:not 伪类不会增加选参数选择起的优先级，但是可以利用这个特点提高规则的优先级，比如`#foo:not(#bar)` 和 `#foo`匹配相同的元素，但是前者的优先级更高
3. `:not(foo)`会匹配任何非foo元素，包括 html 和 body，所以使用类似写法的时候要注意
4. 可以利用这个伪类写一个完全没有用处的选择器。例如，`:not(*) `，这个规则不会匹配任何元素

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        p:not([id='demo2']) { color: red; }
    </style>
</head>
 
<body>
    <p id="demo1">1</p>
    <p id="demo2">2</p>
</body>
 
</html>
```

### CSS 3 目标元素选择器



| 选择器   | 含义                              |
| -------- | --------------------------------- |
| E:target | 匹配被location.hash选中的目标元素 |

**注意**

即锚点元素，目标元素选择器可用于选取当前活动的目标元素

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
 
        #demo1, #demo2, #demo3 {
            width: 100px;
            height: 100px;
            border: 1px solid red;
        }
 
        div:target { background-color: orange; }
 
    </style>
</head>
 
<body>
    <a href="#demo1">demo1</a>
    <a href="#demo2">demo2</a>
    <a href="#demo3">demo3</a>
    <div id="demo1"></div>
    <div id="demo2"></div>
    <div id="demo3"></div>
</body>
 
</html>
```
