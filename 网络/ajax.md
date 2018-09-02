#### form

首先回忆一下from表单请求数据的方法

+ action

  表单提交的地址，表示请求该地址的网络资源

+ method

  浏览器使用 method 属性设置的方法将表单中的数据传送给服务器进行处理

  + get

    浏览器会与表单处理服务器建立连接，然后直接在一个传输步骤中发送所有的表单数据：浏览器会将数据直接附在表单的 action URL 之后。这两者之间用问号进行分隔

  + post

    浏览器将会按照下面两步来发送数据。首先，浏览器将与 action 属性中指定的表单处理服务器建立联系，一旦建立连接之后，浏览器就会按分段传输的方法将数据发送给服务器。 在服务器端，一旦 POST 样式的应用程序开始执行时，就应该从一个标志位置读取参数，而一旦读到参数，在应用程序能够使用这些表单值以前，必须对这些参数进行解码。用户特定的服务器会明确指定应用程序应该如何接受这些参数。

  > 'get' 和 'post' 的区别
  >
  > + 传输数据的长度
  >
  >   get方法会将数据添加在 action URL后进行数据传输，而post方法是按照分段的方法将数据发送给请求地址，所以一般发送较短的数据时可以使用get，这样也可以获得表单最佳传输性能，而发送比较长的数据时使用post；其实两种方法传递的数据都会有长度的限制，get方法传递数据较少，因为get方法传递的数据拼接在URL后面，所以不能太长；而post的方法，数据放在请求主体中，所以可以传递较多的数据，但是也同样有限制，因为如果请求的数据过大，那么频繁的向服务器请求资源可能会导致服务器崩溃，为了服务器的安全考虑，post也有长度限制
  >
  > + 安全性
  >
  >   get方法发送数据是直接把数据添加到URL后面，这样任何人都可以看到请求的数据，post方法更安全，一般用get方法做一些不重要的只读操作，如果要修改服务器上的数据那么用post更好；其实安全也只是相对的，get方法数据可以直接从地址栏中看到，我们认为他不安全，但是post请求的数据我们也可以打开控制台，在请求主体中看到，只不过小白不知道而已
  >
  > + 浏览器缓存
  >
  >   GET请求返回的内容可以被浏览器缓存起来。而每次提交的POST，浏览器在你按下F5的时候会跳出确认框，浏览器不会缓存POST请求返回的内容。
  >
  > + 表单之外
  >
  >   如果想在表单之外调用服务器端的应用程序，而且包括向其传递参数的过程，就要采用 GET 方法，因为该方法允许把表单这样的参数包括进来作为 URL 的一部分。而另一方面，使用 POST 样式的应用程序却希望在 URL 后还能有一个来自浏览器额外的传输过程，其中传输的内容不能作为传统 a 标签的内容

+ enctype

  规定在发送表单数据之前如何对其进行编码

  + application/x-www-form-urlencoded （默认）

    在发送前编码所有字符

  + `multipart/form-data(<input type='file'>)`

    不对字符编码。在使用包含文件上传控件的表单时，必须使用该值

#### ajax

既然form表单可以请求数据，那么为什么要用ajax呢？因为form表单请求数据会对页面进行整体刷新，而ajax方式请求数据是使用**异步**的方式对页面进行**局部**刷新

##### Asynchronous javascript and xml

"异步的JavaScript和xml"。xml也是一种数据传输格式，现在基本被JSON取代，所以这里其实可以写成Asynchronous javascript and json，但是习惯还是写成 'ajax'

##### ajax请求数据的过程

1. 构造一个 ajax 对象

2. ajax.open(method, url, boolean)

   设置请求的属性

   URL：请求的地址

   method：请求的方式

   boolean：是否是异步方式请求数据

3. ajax.send()

   发送ajax请求

4. ajax.onreadystatechange

    存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数

   ajax.readyState： 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化

   - 0: 请求未初始化
   - 1: 服务器连接已建立
   - 2: 请求已接收
   - 3: 请求处理中
   - 4: 请求已完成，且响应已就绪

5. ajax.status

   表示请求相应的结果

   + 200

     'OK'

   + 304

     资源未被修改

   + 404

     未找到页面

   + 500

     服务器内部错误

   + .......（还有很多，遇到补充）

##### ajax对象的一些方法



| 方法                           | 描述                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| abort()                        | 停止当前请求                                                 |
| getAllResponseHeaders()        | 把http请求的所有相应首部作为键/值对返回                      |
| getResponseHeader('server')    | 返回指定首部的串值                                           |
| open(method, url, ture/false)  | 建立对服务器的调用                                           |
| send(content)                  | 先服务器发送请求                                             |
| setRequestHeader(label, value) | 把指定首部设置为所提供的值，在设置任何首部前必须先调用open() |

##### ajax对象的一些属性



| 属性               | 描述                     |
| ------------------ | ------------------------ |
| onreadystatechange | 状态改变的事件触发器     |
| readyState         | 对象的状态值             |
| responseText       | 获得字符串形式的相应数据 |
| responseXML        | 获得XML形式的相应数据    |
| status             | 服务器返回的状态码       |
| statusText         | 服务器返回的状态文本信息 |

##### 原生JS封装ajax方法

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