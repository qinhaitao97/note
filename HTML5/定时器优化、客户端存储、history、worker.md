### requestAniamtionFrame

#### setInterval 做动画的缺点

+ 动画延迟执行

  js是单线程的，当某一个进程在排队期间，插入了其他执行时间过长的进程，会导致原排队进程延迟执行

+ 延迟不准确

  如果把动画延迟时间设置太长了，则会感觉到动画卡顿，那就设置延迟短一点，但是实际执行的延迟不是我们设置的准确的延迟，因为要把计时器放到异步执行当中，再放到异步执行当中，然后主线程访问看拿哪个计时器；所以即使设置了0ms的响应时间，也不会立即执行，还是会有一个大概4ms的延迟

+ 丢帧问题

  我们能看到的动画是由一帧一帧的静态效果所连成的，比我们使用setInterval方法让一个物体每隔4ms动一次，即每隔4ms都是新的一帧，但是浏览器大概是每隔16ms才刷新一次，浏览器不刷新我们也就看不到帧的变化，这部分我们看不到的效果就叫做丢帧，设置的延迟时间越小，丢帧越多，但是设置的延迟时间大了又会造成视觉卡顿，比较合理的时间是浏览器的刷新周期，前面说了浏览器大概16ms刷新一次，但是也只是大概的时间，并不是说准确的就是16ms，所以如果使用setInterval，那么把延迟时间设置成16ms比较合理，但也不是最好的方法

#### requestAnimationFrame

1. 页面刷新前执行一次

2. 1000ms 60fps -> 16ms

3. 用法类似于setTimeout，而不是setInterval

4. cancelAnimationFrame 取消

5. 兼容性（IE10以上）

   在不能使用这个方法的浏览器中，还是要用setTimeout方法

   ```javascript
   // 设置的兼容性写法
   window.requestAnimationFrame = (function () {
       return window.requestAnimationFrame ||
           window.webkitRequestAnimationFrame ||
           window.mozRequestAnimationFrame ||
           function (callback) {
          		window.setTimeout(callback, 1000 / 60);
       	}
   })();
   
   // 取消的兼容性写法
   window.cancelAnimationFrame = (function () {
       return window.cancelAnimationFrame ||
           window.webkitCancelAnimationFrame ||
           window.mozCancelAnimationFrame ||
           function (id) {
               window.clearTimeout(id);
           }
   })();
   ```

使用实例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        #box {
            position: absolute;
            top: 0px;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: deepskyblue;
        }
    </style>
</head>

<body>
    <div id="box"></div>
    <script type="text/javascript">
        window.requestAnimationFrame = (function () {
            return window.requestAnimationFrame ||
                window.webkitRequestAnimationFrame ||
                window.mozRequestAnimationFrame ||
                function (callback) {
                    window.setTimeout(callback, 1000 / 60);
                }
        })();
        window.cancelAnimationFrame = (function () {
            return window.cancelAnimationFrame ||
                window.webkitCancelAnimationFrame ||
                window.mozCancelAnimationFrame ||
                function (id) {
                    window.clearTimeout(id);
                }
        })();

        var req;

        function move() {
            if (box.offsetLeft >= 300) {
                window.cancelAnimationFrame(req);
                box.style.left = '300px';
            } else {
                box.style.left = box.offsetLeft + 10 + 'px';
                req = window.requestAnimationFrame(move);
            }
        }
        move();
    </script>
</body>

</html>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftqqlyq80bg30ey098q2u.gif)

### 客户端存储

#### storage简介

之前介绍过利用cookie实现客户端存储，但是cookie有一些限制、不足：

+ 使用cookie要在http请求头中设置字段，服务器接收到请求后，在响应头中返回相应的信息，所以cookie是随着http传输的，会浪费一些宽带
+ 有路径的限制
+ cookie只能存储少量的数据

现在介绍另一中客户端存储技术 storage，不需要通过http传输，可以存储大量的数据



| 特性           | cookie                                                       | localStorage                                                 | sessionStorage                                 |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------------------------- |
| 数据的生命周期 | 一般有服务器生成，可设置失效时间。如果在浏览器端生成cookie，默认是关闭浏览器后失效 | 除非被清除，否则永久保存                                     | 尽在当前会话下有效，关闭页面或者浏览器后被清除 |
| 存放数据大小   | 4k左右                                                       | 一般为5MB                                                    | 同localStorage                                 |
| 与服务器端通信 | 每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题 | 尽在客户端（即浏览器）中保存，不参与和服务器的通信           | 同localStorage                                 |
| 易用性         | 需要程序员自己封装，原生的cookie接口不友好                   | 原生接口可以接受，亦可再次封装来对Object 和 Array有更友好的支持 | 同localStorage                                 |

#### 分类

+ localstorage

  永久存储

+ sessionStorage

  临时存储

#### 属性方法

查看storage

```
- 1.直接打开控制台，在 application -> localStorage / sessionStorage / files 下查看

- 2.window.localStorage / window.sessionStorage

注： localStorage / sessionStorage 是window上的属性，cookie是document上的属性
```

存储数据

```javascript
// 存储的数据必须是字符串格式
localStorage.name = 'qht';
localStorage.info = JSON.stringify({"name": "qht", "age": 20});

sessionStorage.name = 'qht';
sessionStorage.info = JSON.stringify({"name": "qht", "age": 20});
```

取出数据

```javascript
localStorage.name
localStorage.info

sessionStorage.name
sessionStorage.info
```

查看数据个数

```javascript
localStorage.length

sessionStorage.length
```

存取的有效期

```
- localStorage：  永久的，除非手动删除
- sessionStorage：临时的，窗口关闭就没有了
```

作用域

```
- localStorage:   受文档源限制（同源）
- sessionStorage：受文档源限制（同源）+ 受窗口限制
```

API

```javascript
// 设置属性
localStorage.setItem(name, value)
// 获取属性值
localStorage.getItem(name)
// 移除属性值
localStorage.removeItem(name);
// 清除所有属性
localStorage.clear();

// sessionStorage的使用方法一样
```

### history

#### 概述

`window.history` 指向 history 对象，表示浏览器当前窗口的浏览历史；history对象保存了当前窗口访问过的所有页面地址，可以通过前进/后退操作或者history的方法来前进/后退到后/前一个网址，出于安全性的考虑，我们只能通过前进后退操作进行导航，但是不能获取这些历史网页的地址

#### 属性

> + history.length
> + history.state

##### length

获得浏览器当前窗口历史记录的条数

```javascript
history.length;
```

##### state

history堆栈最上层的状态值

```javascript
history.state
```

#### 方法

> html中的方法
>
> + history.back()
> + history.forward()
> + history.go()
>
> html5新增的方法
>
> + history.pushState()
> + history.replaceState()

##### back()

回退到上一条历史记录对应的页面，相当于浏览器后退按钮的作用

```javascript
history.back();
```

##### forward()

前进到下一条历史记录对应的页面，相当于浏览器前进按钮的作用

```javascript
history.forward();
```

##### go()

跳转到历史记录中相对于当前页面的前/后 n 个页面

```javascript
history.go(n);
// 举例:
// history.go(0)	跳转到当前页面，相当于刷新操作
// history.go(1)	跳转到当前页面的下一个页面
// history.go(-1)	跳转到当前页面的上一个页面
```

通过以上三个方法，浏览器跳转到某个页面，页面通常是从浏览器缓存中加载的，而不是重新向服务器发送请求

##### pushState()

+ 功能

  在当前历史记录中，添加一条新的记录

+ 语法

  ```javascript
  history.pushState(state, title, url);
  ```

+ 参数

  + state

    一个对象或者字符串，用于描述新纪录的一些特性，由开发者自由给出，以便后续使用(主要用于 `popstate` 事件，该事件触发时，该参数被传入回调函数，浏览器会将这个参数序列化之后保存在本地，重新载入这个页面的时候，可以拿到这个参数)

  + title

    新页面的标题，现在所有的浏览器都会忽略这个参数，所以一般传 `null` 即可

  + url

    新页面的地址，与当前页面要在同一个域下

+ 强调

  + **该方法受同源策略的限制**

    新添加的记录的地址要和当前页面在同一个域下

  + **使用该方法后，浏览器地址栏会立即显示新添加的地址**

    浏览器的历史记录可以看做一个栈，前进操作或者打开新的网页或者添加新的历史记录，新的网址入栈；后退操作会使最上面的记录出栈，而浏览器向用户展示的是栈顶的记录，所以，使用了这个方法添加了一条新的记录后，栈顶记录就成了新的网址，浏览器的地址栏就会显示这个网址

  + **使用该方法不会刷新网页**

    使用这个方法可以是地址栏显示新的地址，但是却不会刷新当前的页面，也就是说在使用js添加了一条新的历史记录后，只有地址栏会产生变化（显示新的地址），页面还是显示当前的页面，不会进行刷新

+ 举例

  > 样例1：展示整个过程

  我们在服务器中创建一个 "history-pushState" 文件夹作为测试文件夹，在此文件夹中创建两个文件 "currentPage.html" 和 "newPage"，分别代表当前页面和新的页面，我们要做的就是在当前页面中把新的页面添加到历史记录中，为了区别当前页面和新页面，在两个页面中写入了不同的文字

  ```html
  <!-- currentPage.html -->
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>currentPage</title>
  </head>
  <body>
      <!-- currentPage 页面中显示的内容 -->
      <h3>This is currentPage!</h3>
  
      <script>
          // 添加新的记录
          history.pushState(null, null, './newPage.html');
      </script>
  </body>
  </html>
  ```

  ```html
  <!-- newPage.html -->
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>newPage</title>
  </head>
  <body>
      <h3>This is newPage!</h3>
  </body>
  </html>
  ```

  接下类，为了能看清楚当前页面在执行了 `pushState()` 方法后有哪些变化，我们通过输入 "currentPage.html" 的地址来打开这个页面

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftrqgyif4og30fw08nk0b.gif)

  可以看到，我们输入地址是 "currentPage.html" 的地址，按下回车后，地址栏却变成了 "newPage.html" 的地址，这是因为我们在 "currentPage.html" 页面中使用 `pushState()` 方法添加了一条新的历史记录，这条记录的地址就是 "newPage.html" 页面的地址，所以地址栏会立即变成当前新记录的地址；不过虽然地址栏变成了新纪录的地址，但显示的还是 "currentPage.html" 的页面，这因为使用 `pushState()` 方法不执行刷新操作，即便地址栏已经改成了新页面的地址，但如果我们不进行手动刷新，它依然会显示当前的页面

  > 样例2：读取 `history.state` 状态属性

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>currentPage</title>
  </head>
  <body>
      <!-- currentPage 页面中显示的内容 -->
      <h3>This is currentPage!</h3>
  
      <script>
          // 添加新的记录
          history.pushState({name: 'new'}, null, './newPage.html');
  
          // 读取状态属性
          console.log(history.state);
      </script>
  </body>
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftrsvr6xk6j309r01lwe9.jpg)

  > 样例3：禁止添加跨域站点

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>currentPage</title>
  </head>
  <body>
      <!-- currentPage 页面中显示的内容 -->
      <h3>This is currentPage!</h3>
  
      <script>
          // 添加跨域的新记录
          history.pushState(null, null, 'https://www.baidu.com');
      </script>
  </body>
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftrsy1dil3j30la01u0sn.jpg)

  

  > 样例4："query string" 形式的url

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>currentPage</title>
  </head>
  <body>
      <!-- currentPage 页面中显示的内容 -->
      <h3>This is currentPage!</h3>
  
      <script>
          history.pushState(null, null, './newPage.html?page=newPage');
  
          // 如果只写查询字符串，则会被拼接到当前页面url后面
          // history.pushState(null, null, '?page=currentPage');
      </script>
  </body>
  </html>
  ```

##### replaceState()

+ 功能

  修改history对象当前记录

+ 语法

  ```javascript
  history.repalceState(state, title, url);
  ```

+ 参数

  同 pushState

+ 强调

  同 pushState

#### popstate 事件

+ 触发条件

  同一个文档的浏览历史(即 history 对象)发生变化时，该事件被触发

+ 注意

  + `pushState()` 和 `replaceState()` 方法不会触发该事件
  + 点击浏览器的前进 / 后退按钮、JS调用 `history.back()`、`history.forward()`、`history.go()`等方法可以触发该事件
  + 该事件只针对同一个文档，如果浏览器历史的切换导致加载了不同的文档，该事件不会触发
  + 页面第一次加载的时候，不会触发该事件

+ event.state

  该事件的事件对象的属性 `event.state` 指向 `pushState()` 、`replaceState()` 方法为当前URL提供的状态对象（即这两个方法的第一个参数 state），这个 state 对象也可以通过 `history.state` 方法直接获取，但获取的条件和 popstate 事件触发的条件相同

+ 举例

  > 样例1：同一个文档

  ```html
  <!-- currentPage.html -->
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>currentPage</title>
  </head>
  <body>
      <h3>This is currentPage!</h3>
  
      <script>
          history.pushState({name: 'current'}, null, '?page=currentPage');
          
          window.onpopstate = function (e) {
              console.log(e);
              console.log(e.state);
          }
      </script>
  </body>
  </html>
  ```

  以上代码意思是当 popstate 事件触发时，打印事件对象 event 即 状态属性 event.state，当我们在浏览器中打开这个页面时，地址栏地址显示 `http://localhost/test/history-pushState/currentPage.html?page=currentPage`，此时控制台没有任何输出，因为还没有历史记录变化触发 popstate 事件；我们点击浏览器的回退按钮，此时浏览器地址栏显示 `http://localhost/test/history-pushState/currentPage.html`，控制台打印结果如下

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftrwyyo2t0j30cz01xjr8.jpg)

  首先有东西打印出来，说明刚才的回退操作造成了历史记录变化，触发了 popstate 事件，所以才会执行 popstate 事件的回调函数；下面我们来关注打印内容的第二个值 `event.state` ，它的值是 `null` ，明明我们在使用 `pushState()` 方法时，第一个参数设置了 `{name: 'current'}` ，为什么这里是 `null` 呢？别急，接下来，我们再点击浏览器的前进按钮，地址栏显示 `http://localhost/test/history-pushState/currentPage.html?page=currentPage`，控制台又增加了两条打印内容，结果如下

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftrx3vgdr3j30cw01xt8k.jpg)

  有打印内容说明出发了 popstate 事件这个就不再多说了，继续来关注第二个打印内容 `event.state` ，这次它的值变成了我们给他设置的值，结合地址栏中不同的url，发现在 `http://localhost/test/history-pushState/currentPage.html` 这个地址下，`event.state` 结果为 `null`，而在 `http://localhost/test/history-pushState/currentPage.html?page=currentPage`这个地址下，`event.state` 结果为 `{name: 'current'}`，这是因为我们在使用 `pushState()` 方法的时候，参数是这样设置的 `pushState({name: "current"}, null, '?page=currentPage')`，关注第一个和第三个参数，我们把state状态传给了 `http://localhost/test/history-pushState/currentPage.html?page=currentPage` 这个地址的页面，所以只有在这个地址页面下，才能打印我们设置的state

  > 样例2：不同文档

  ```html
  <!-- currentPage.html -->
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>currentPage</title>
  </head>
  <body>
      <h3>This is currentPage!</h3>
  
      <script>
          history.pushState({name: 'current'}, null, '?page=currentPage');
          
          window.onpopstate = function (e) {
              console.log(e);
              console.log(e.state);
          }
      </script>
  </body>
  </html>
  ```

  与上一个样例一样的代码，操作的步骤有所不同，首先打开一个新标签页（新标签页是为了保证历史记录的干净），然后在地址栏中输入 `https://www.baidu.com`，回车打开百度页面，打开后将地址栏中百度的url删除，输入 `http://localhost/test/history-pushState/currentPage.html` ，回车打开页面，此时地址栏中显示的是 `http://localhost/test/history-pushState/currentPage.html?page=currentPage`，我们点击浏览器的回退按钮，地址回退到 `http://localhost/test/history-pushState/currentPage.html`，此时控制台中有打印内容，这个过程上面一个样例已经解释清楚，接下来我们继续点击回退按钮，使地址回退到 `https://www.baidu.com`，这时控制台没有任何打印内容，因为历史记录变化的过程中加载百度页面，这与我们的 "currentPage.html" 是不同的文档，所以不会触发 popState 事件

#### pjax

pushState + ajax的应用

如果我们要做一个单页应用，简单地说我们要是实现的内容是通过ajax请求获得实现的，而不是通过页面跳转的其他页面显示内容实现的；但是仅仅通过ajax实现单页应用也有一定的限制，因为ajax是局部刷新而不刷新整个页面，这也就意味着我们虽然可以通过点击不同的标签显示不同的内容，但是因为过程种地址栏中的url没有发生变化导致我们无法通过前进或者是后退操作访问我们已经访问过的内容，这样对用户的习惯很不友好，而 history API 正好可以弥补这一缺陷，它只改变地址栏而不刷新页面的特性，使我们能够轻松的修改url，模拟出多页面的效果，实现前进或者后退的导航

下面做一个简单的例子来描述整个过程

功能演示

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fts1ja7k8yg30ik0c548f.gif)

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>pajx</title>
    <link rel="stylesheet" href="./index.css">
</head>
<body>
    <div class="wrapper">
        <div class="header">
            <button class="btn" name="one">one</button>
            <button class="btn" name="two">two</button>
            <button class="btn" name="three">three</button>
        </div>
        <div class="content"></div>
    </div>

    <script src="./ajax.js"></script>
    <script src="./index.js"></script>
</body>
</html>
```

index.css

```css
.wrapper {
    width: 450px;
    height: 300px;
    border: 1px solid #000;
}

.wrapper .header {
    display: flex;
    width: 100%;
    height: 100px;
}

.wrapper .header .btn {
    width: 33.3%;
    height: 100%;
    box-sizing: content-box;
    border: 1px solid #000;
    outline: none;
    cursor: pointer;
}

.wrapper .content {
    width: 100%;
    height: 200px;
    text-align: center;
    line-height: 200px;
}
```

getDate.php

```php
<?php
header('content-type:text/html;charset="utf-8"');
error_reporting(0);

$page = $_GET['page'];
if ($page == 'one') {
    $data = 'This is page one';
} else if ($page == 'two') {
    $data = 'This is page two';
} else if ($page == 'three') {
    $data = 'This is page three';
}

echo "$data";
```

ajax.js

```javascript
function ajax(method, url, data, flag, callback) {
    method = method.toUpperCase();
    var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHttp');
 
    if (method == 'GET') {
        xhr.open('GET', url + '?' + data, flag);
        xhr.send();
    } else if (method == 'POST') {
        xhr.open('POST', url, flag);
        xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
        xhr.send(data);
    }
 
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4 && xhr.status == 200) {
            callback(xhr.responseText);
        }
    };
}
```

index.js

```javascript
var header = document.getElementsByClassName('header')[0],
    content = document.getElementsByClassName('content')[0];

// 页面第一次加载默认显示第一个页的内容
function init() {
    var data = 'page=one';
    ajax('GET', './getData.php', data, true, sovle);
    history.replaceState({ dataFlag: data }, null, '?' + data);
}
init();

// 绑定点击事件，点击不同的按钮，发送不同的ajax请求
header.onclick = function (e) {
    var event = e || window.event,
        target = event.target || event.srcElement,
        data;

    data = 'page=' + target.getAttribute('name');
    ajax('GET', './getData.php', data, true, sovle);
    
    // 发送ajax请求后，在当前页面的url后拼接不同的页面标记
    history.pushState({ dataFlag: data }, null, '?' + data);
}

// ajax请求成功的回调函数
function sovle(data) {
    // 调用添加文本的方法
    addContent(data);
}

// 将ajax响应数据添加到dom结构中
function addContent(data) {
    content.innerText = data;
}

// 每当有state的变化(导航操作)，重新发送ajax请求，获得当前页面标记对应的数据
window.onpopstate = function (e) {
    var event = e || window.event,
        data = event.state.dataFlag || 'page=one';
    ajax('GET', './getData.php', data, true, sovle);
}
```

主要是index.js文件中的内容

### worker

我们都知道JavaScript是由一个主线程单线程执行的，这样的机制会有一些问题，如果在他执行的过程中，某一个方法需要大量大计算，那这个方法就会占用主线程很多的时间，性能不好，所以我们可不可以单独开辟一个线程，去处理这些非常耗时的操作呢？

+ 方法

  使用worker创建子线程

+ 语法

  ```javascript
  var worker = new Worker('worker.js');
  // 主线程所在的文件和子线程worker所在的文件要满足同源策略
  ```

+ worker和主线程之间的通信

  + postMessage() 方法

    用于主线程和子线程之间的消息传递

  + message 事件

    用于监听主线程和子线程之间的消息传递

+ 结束worker线程

  + close() 方法

    在worker的作用域中调用，来结束自己（相当于辞职）

  + terminate() 方法

    在主线程的作用域中调用，来结束worker线程（相当于解雇）

  一般使用第二种方法比较好

+ 其他特性

  + importScripts('./math1.js', './math2.js')

    worker 是window的子集，只能实现部分功能，不能获取到window、document，所以也就不能使用jQuery、zepto等类库，通常都是引入一些计算行的类库进行运算

  + navigator

    可以使用navigator对象的某些属性方法，不是全部

  + XMLHttpRequest

    可以发送ajax请求

  + setTimeout / setInterval

    可以使用定时器、计时器

+ demo

  简单的使用范例，这里以平方运算为例（假装平方运算是高计算量的运算，hh~）

  index.html

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>worker</title>
  </head>
  <body>
      <script src="./worker.js"></script>
      <script src="./main.js"></script>
  </body>
  </html>
  ```

  main.js

  ```javascript
  var data = 10;
  var worker = new Worker('worker.js');
  
  worker.postMessage(data);
  
  worker.onmessage = function (e) {
      console.log(e.data);
  }
  ```

  worker.js

  ```javascript
  onmessage = function (e) {
      var res = e.data * e.data;
      this.postMessage(res);
  }
  ```

  canvas图片处理的样例

  index.html

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #myCanvas {
              border: 1px solid #000;
          }
  
          button {
              display: block;
          }
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <img src="">
      <button>start</button>
      <script src="./worker.js"></script>
      <script src="./main.js"></script>
  </body>
  
  </html>
  ```

  main.js

  ```javascript
  var oImg = new Image();
  
  oImg.src = './xiaohei.png';
  oImg.onload = function () {
      var canvas = document.getElementById('myCanvas'),
          canvasWidth = canvas.width,
          canvasHeight = canvas.height;
  
      var worker = new Worker('worker.js');
  
      var btn = document.getElementsByTagName('button')[0];
      btn.onclick = function () {
          sovle();
      }
  
      function sovle() {
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
              var imageData;
  
              ctx.drawImage(oImg, 0, 0, canvasWidth, canvasHeight);
  
              imageData = ctx.getImageData(0, 0, canvasWidth, canvasHeight);
  
              worker.postMessage(imageData);
              worker.onmessage = function (e) {
                  ctx.putImageData(e.data, 0, 0);
                  var url = canvas.toDataURL('image/jpeg', 0.5);
                  document.getElementsByTagName('img')[0].src = url;
                  worker.terminate();
              }
          }
      }
  }
  ```

  worker.js

  ```javascript
  onmessage = function (e) {
      var imageData = e.data,
          imageDataLen;
  
      imageDataLen = imageData.data.length / 4;
  
      for (var i = 0; i < imageDataLen; i++) {
          var red = imageData.data[i * 4];
          var green = imageData.data[i * 4 + 1];
          var blue = imageData.data[i * 4 + 2];
          var gray = 0.3 * red + 0.59 * green + 0.11 * blue;
      
          imageData.data[i * 4] = gray;
          imageData.data[i * 4 + 1] = gray;
          imageData.data[i * 4 + 2] = gray;
      }
      postMessage(imageData);
  }
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fts5zu9bl4g30sp0a60x2.gif)

  第二次点击start没有对图片进行处理是因为子第一遍处理完毕后，主线程关闭了worker线程，所以后面无法对图形进行处理