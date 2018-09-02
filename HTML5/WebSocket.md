### 概述

WebSocket是一种在单个TCP连接上进行全双工通信的协议，它使得客户端与服务器端的通信变得更加简单，允许服务端主动向客户端推送数据。在WebSocket API中，浏览器和服务器只需要完成一次握手，两者之间就可以建立持久性的连接，并进行双向数据传输

### 背景

#### HTTP协议的缺陷

我们已知的通信协议HTTP，有一个缺陷：只能由客户端发出请求，服务端不能主动的发送请求；这样如果我们需要获取服务端的数据就必须先在客户端发送HTTP请求，但有时我们并不想主动的发送数据，而期待客户端能主动地向客户端推送一些数据，典型的比如聊天室的功能，我们并不想点击某个接受按钮才接受消息，而是服务端一旦有了新的消息便推送到我们的客户端的，但实际中我们好像确实没有点击某个按钮才能接收到消息，这是因为采用了一种 "轮询" 技术

#### 轮询

轮询分为传统的轮询方式和一种较新的 "Comet" 轮询方式。传统的轮询是在特定的的时间间隔（如每1秒），由浏览器对服务器发出HTTP请求，然后由服务器返回最新的数据给客户端的浏览器，这种模式带来很明显的缺点，即浏览器需要不断的向服务器发出请求，然而HTTP请求可能包含较长的头部，其中真正有效的数据可能只是很小的一部分，显然这样会浪费很多的带宽等资源。 

而比较新的技术去做轮询的效果是[Comet](https://zh.wikipedia.org/wiki/Comet_(web%E6%8A%80%E6%9C%AF))。这种技术虽然可以双向通信，但依然需要反复发出请求。而且在Comet中，普遍采用的[长链接](https://zh.wikipedia.org/wiki/HTTP%E6%8C%81%E4%B9%85%E9%93%BE%E6%8E%A5)，也会消耗服务器资源

### 特点

在上述背景下，HTML5定义了WebSocket协议，能更好的节省服务器资源和带宽，并且能够更实时地进行双向通讯，有以下特点

+ 建立在 TCP 协议之上，服务端的实现比较容易
+ 与 HTTP 有良好的兼容性，默认端口也是 80 和 443 ，握手阶段采用 HTTP 协议
+ 数据格式比较轻量，性能开销较小，通信效率高
+ 可以发送文本也可以发送二进制数据
+ 没有同源限制，客户端可以与任意服务器通信
+ 协议标识符是 ws，如果加密则为 wss

### 建立连接的过程

当 web 应用程序调用 `new WebSocket(url)` 接口时，浏览器就开始了与地址为 url 的 webserver 建立握手连接的过程

1. 浏览器与 WebSocket 服务器通过 TCP 握手建立连接，如果这个链接失败，那么后面的过程就不会执行，web 应用程序就会收到错误通知
2. 在 TCP 建立成功之后，浏览器通过 HTTP 协议传送 WebSocket 支持的版本号、协议的字版本号、原始地址主机地址等一系列字段给服务器端
3. WebSocket 服务器收到浏览器发送的请求后，如果数据包的数据和格式正确，客户端和服务端的协议版本号匹配，就接受本次握手连接，并给出相应的数据回复，同样，回复数据也是采用 HTTP 协议传输
4. 浏览器收到服务器回复的数据包后，如果数据包内容、格式等没有问题，就表示本次连接成功，触发 onopen 事件，此时 web 开发者就可以通过 `send()` 接口向服务器发送数据。如果数据包内容、格式等不正确，则握手连接失败，触发 onerror 事件，可以获取失败的原因

### WebSocket API

创建连接

```javascript
var Socket = new WebSocket(url);
```

状态

```javascript
- readyState
	0:	CONNECTING，表示正在连接。
	1:	OPEN，表示连接成功，可以通信了。
	2:	CLOSING，表示连接正在关闭。
	3:	CLOSED，值为3，表示连接已经关闭，或者打开连接失败
```

方法

```javascript
// 传输数据
Socket.send(data);

// 终止任何现有连接
Socket.close();
```

事件

| 事件    | 描述                       |
| ------- | -------------------------- |
| open    | 连接建立时触发             |
| message | 客户端接受服务端数据时触发 |
| close   | 连接关闭时触发             |
| error   | 通信发生错误时触发         |

```html
<!--
	practice: WedSocket API
		针对上述API知识点的练习
-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>WebSocket</title>
</head>
<body>
    <script>
        // WebSocket.org 提供了一个专门用来测试WebSocket的服务器
        var socket = new WebSocket('ws://echo.websocket.org');

        console.log(socket.readyState);
        socket.onopen = function () {
            console.log(this.readyState);
            this.send('hello websocket');
        }
        
        socket.onmessage = function (e) {
            console.log(this.readyState);
            console.log(e.data);
            this.close();
        }

        socket.onclose = function () {
            console.log(this.readyState);
            console.log('closed');
        }

        socket.onerror = function () {
            console.log('error');
        }
    </script>
</body>
</html>
```
