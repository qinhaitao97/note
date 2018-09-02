## canvas是什么

> `<canvas>`  是HTML5新增的元素，可用于通过使用 JavaScript 中的脚本来绘制图形。例如他可以用来绘制图形、制作照片、创建动画、甚至可以进行实时的视频处理和渲染

需要强调的是，`<canvas>` 只是一个画布，本身并不具有画图能力，绘图必须使用 JavaScript 等脚本语言。

我们可以认为 canvas 是画布，JavaScript 是画笔

## 相关概念

### canvas元素

**定义**

```html
<canvas id='demo' width='500' height='500'></canvas>
```

**属性**

`width` 和 `height` 属性用来设置 `<canvas>` 元素的大小，单位默认是像素；如果没有设置 `width` 和 `height` 值，其**默认大小**是 `300 * 150`；除了使用HTML标签中的 `width` 和 `height` 属性来设置大小，还可以通过CSS中的 `width` 和 `height` 以及JS中的 `width` 和 `height` 来设置

**设置大小**

前面我们了解了为 `<canvas>` 元素设置大小的方法有三种，接下来就看一下这三种设置方法到底有什么区别我们以在400 * 400 的画布上画一个半径为50px的圆为例，以此来观察用不同的方法设置画布的大小绘制图案造成什么影响

+ HTML设置大小

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #demo {
              background-color: lightsalmon;
          }
      </style>
  </head>
  <body>
      <canvas id="demo" width="400" height="400"></canvas>
      <script>
          var oCanvas = document.getElementById('demo');
          var ctx = oCanvas.getContext('2d');
  
          ctx.arc(100, 100, 50, 0, Math.PI * 2, true);
          ctx.fillStyle = 'lightgreen';
          ctx.fill();
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftgjxdvlhgj30f10dljr7.jpg)

+ JS设置大小

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #demo {
              background-color: lightsalmon;
          }
      </style>
  </head>
  <body>
      <canvas id="demo"></canvas>
      <script>
          var oCanvas = document.getElementById('demo');
          var ctx = oCanvas.getContext('2d');
  
          oCanvas.width = 400;
          oCanvas.height = 400;
  
          ctx.arc(100, 100, 50, 0, Math.PI * 2, true);
          ctx.fillStyle = 'lightgreen';
          ctx.fill();
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftgjxdvlhgj30f10dljr7.jpg)

+ CSS设置大小

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #demo {
              width: 400px;
              height: 400px;
              background-color: lightsalmon;
          }
      </style>
  </head>
  <body>
      <canvas id="demo"></canvas>
      <script>
          var oCanvas = document.getElementById('demo');
          var ctx = oCanvas.getContext('2d');
  
          ctx.arc(100, 100, 50, 0, Math.PI * 2, true);
          ctx.fillStyle = 'lightgreen';
          ctx.fill();
      </script>
  </body>
  </html>
  ```

  ![红配绿大法](http://ww1.sinaimg.cn/large/006eYMu7ly1ftgjuv542uj30cx0ccmx5.jpg)

可以看到，利用HTML标签和JS方法设置 `<canvas>` 元素的大小，结果都复合我们的预期，然而用CSS设置的情况下，圆竟然变形了，这是为什么呢？

> 以CSS方法设置画布的大小，在绘制时图像会伸缩以适应它的框架尺寸：如果CSS的尺寸与初始画布的比例不一致，它会出现扭曲。 

画布初始的大小（即默认大小）是 300px * 150px，相当于HTML标签设置的大小是300 * 150，当用CSS属性设置画布的大小为 400px * 400px时，画布会在HTML标签设置的大小的基础上进行缩放以适应后面设置的这个大小，换句话说就是将 300px * 150px 大小的画布放在 400px * 200px 的容器中显示，在这个过程中，所以画布上的图像会发生扭曲变形，所以一般都采用HTML或者JS的方法来为画布设置大小，但是用CSS方法设置画布大小在解决 “**canvas高分屏模糊**” 的问题上有重要作用，后面会讲

### 渲染上下文

**定义**

> `<canvas>` 元素创造了一个固定大小的画布，它公开了一个或多个**渲染上下文**，其可以用来绘制和处理要展示的内容 

**获取方法**

利用JavaScript中的 `getContext()` 方法，该方法接受一个参数：上下文格式

上下文格式可以是 `2d`、或者 `webGL` 等，这里我们只讨论二维平面，所以我们只需要将其参数设置为 `2d` 即可

### 兼容

虽然现在主流的浏览器都已经较好的支持了 `<canvas>` 标签，但是有些老版本的浏览器，尤其是IE9以下的浏览器并不支持，所以考虑到使用 `<canvas>` 的友好性，提供两种方法

+ 替换内容

  在 canvas 的开始标签和闭合标签之间写入要替代的内容，这样，不支持 `<canvas>` 标签的浏览器会忽略容器，并在其中渲染后备内容；而支持 `<canvas>` 的标签则会忽略容器中的内容，只是正常的渲染 `<canvas>`元素

  比如我们可以把文本或者图片当做替换内容

  ```html
  <body>
      <canvas id="demo" width="500" height="500">
          如果不支持canvas元素就显示这段文字hhhhhhh
      </canvas>
      <canvas id="demo2">
          <img src="http://ww1.sinaimg.cn/large/006eYMu7ly1ftgky0ok92j30g103ot8j.jpg" alt="如果不支持canvas就显示这张图片">
      </canvas>
  </body>
  ```

  PS：也正是因为canvas替换内容的这种机制，使canvas的闭合标签（`</canvas>`）不可省略，因为如果省略的话，文档的其余部分都会被认为是替代内容导致canvas无法正常使用

+ 检查支持性

  通过简单的测试 `getContext()` 方法的存在，检查其可编程的支持性

  ```javascript
  var oCanvas = document.getElementById('demo');
  if (oCanvas.getContext()) {
  	// 绘图
  } else {
  	// 如果不存在的操作
  }
  ```

## 使用canvas

### 准备步骤

#### 创建canvas元素

```html
<canvas id="myCanvas" width="500" height="500"></canvas>
```

#### 获取渲染上下文

```javascript
// 获取canvas元素
var oCanvas = document.getElementById('myCanvas');
// 获取该canvas元素的渲染上下文
var ctx = oCanvas.getContext('2d');
```

### 了解画布栅格的概念

> 在我们开始画图之前，我们需要了解一下画布栅格（canvas grid）以及坐标空间。 如下图所示，canvas元素默认被网格所覆盖。通常来说网格中的一个单元相当于canvas元素中的一像素。栅格的起点为左上角（坐标为（0,0））。所有元素的位置都相对于原点定位。所以图中蓝色方形左上角的坐标为距离左边（X轴）x像素，距离上边（Y轴）y像素（坐标为（x,y））。 

![来源于MDN](http://ww1.sinaimg.cn/large/006eYMu7ly1ftglm4f656j3064064741.jpg)

### 绘制形状

#### 移动笔触

想象真实环境中绘图的过程，在落笔开始绘制之前，我们是不是要先想好在哪落笔？canvas绘图也是一样，在绘图之前要现将画笔移动到开始绘制的地方

```javascript
var oCanvas = document.getElementById('myCanvas');
var ctx = oCanvas.getContext('2d');
ctx.moveTo(100, 100);  // 把笔触移动到坐标为（100，100）的位置
```

#### 绘制直线

**功能**

绘制一条**直线路径**

**语法**

`lineTo(x, y)`

| 参数 | 含义          |
| ---- | ------------- |
| x    | 终止点的x坐标 |
| y    | 终止点y的坐标 |

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .myCanvas { border: 1px solid #000; }
    </style>
</head>
<body>
    <canvas class="myCanvas" width="500" height="300"></canvas>
    <script type="text/javascript">
        var oCanvas = document.getElementsByClassName('myCanvas')[0];
        var ctx = oCanvas.getContext('2d');

        ctx.moveTo(100, 100);
        ctx.lineTo(200, 200);
    </script>
</body>
</html>
```

预想中的结果：画布上有一条从（100,100）位置到（200， 200）位置的一条倾斜的直线

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftgqcph7y1j30fw09jjr5.jpg)

实际运行结果：画布上一片空白，什么都没有

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftgqdq2vt6j30gt091gld.jpg)

出现这样结果的原因是，`lineTo()` 方法并不是直接绘制一条直线出来，而是绘制了一条直线路径，那什么是路径呢，接线来我们来仔细的讲解一下关于路径的概念

**开始的位置**

直线路径开始的位置有三种情况

+ 当前路径下，起笔位置默认从上一次绘图结束的地方开始

+ 如果使用了 `moveTo()` 方法，则从 `moveT()` 方法设定的位置开始
+ 如果开启了一段新的路径，如果不用 `moveTo()` 方法设置其实点，则当前路径第一个 `lineTo()` 方法，会被当成 `moveTo()` 方法

#### 路径

##### 概念

> 路径是图形的基本元素，从绘制起点到绘制终点所经历的这些点，就成为路径

##### 使用路径绘图

canvas中所有的基本图形，包括线段、矩形、圆弧、贝塞尔曲线等都时基于路径绘制的，简单地说就是我们要先绘制出路径，然后给这些路径添加颜色和样式，才有了我们能看到的图形，也就是说在给路径添加样式和颜色之前，我们是看不到它的。打个比方，以一张神秘的寻宝图为例，一般寻宝图不会直接将地图画在上面然我们看到，而是有一些 ”隐形“的路径，需要我们泼上墨汁等才能 “显形” ，我们才能看到所谓的寻宝路线，这里隐形的路线就相当于是我们的 “路径”，他确实存在但是我们还看不到，墨汁就相当于是我们要给路径添加的 “颜色和样式”

一个路径可以包含多个子路径，子路径也是由多个点组成的，在某一时刻，canvas中只能包含一条路径，canvas规范把它称为 **当前路径**

使用路径绘图的一般步骤为

1. 调用 `beginPath()` 方法开始一条新的路径
2. 使用 `moveTo(x, y)` 方法以（x，y）为起点开始一条新的子路径，并把画笔移动到该起点
3. 定义子路径的内容（比如画一条直线路径、圆弧路径等）
4. 调用 `closePath()` 方法**封闭**当前子路径（一定要注意是封闭路径，而不是关闭路径）
5. 调用 `stroke()` 或 `fill()` 方法显示路径 （描边、填充）

说明：

1. `beginPath()` 方法不是必须的

   比如画布的初始状态默认就是一条新的路径，如果是第一次在画布上作图，不需要开启新的路径；同样，如果所有绘制的图形都在一条路径下，那也不需要开启新的路径

2. `moveTo(x, y)` 方法不是必须的

   第一条路径默认是画布的原点，其他子路径的起点是上一次路径的终点，因此，再不需要重新指定子路径起点的情况先，他不是必须的

3. 定义子路径的内容

   以绘制直线中我们demo为例，从（100,100）到（200,200）绘制了一条直线路径，这个过程就是定义子路径的内容

4. `closePath()` 方法不是必须的

   `closePath()` 方法是用来封闭当前路径的，在我们的绘制中，往往一条子路径就是一个图形，所以也可以把它的功能理解为闭合图形的，它的作用是将当前子路径的终点与当前子路径的起点相连，如果我们的图形原本就是封闭的或者我们不希望图形被封闭，那就不需要调用这个方法

5. 使用 `stroke()` 或 `fill()` 方法显示路径

   这里 `stroke()` 方法相是给路径描边，`fill()` 方法是填充路径，这两个方法的作用就是让路径显示出来能被我们看到，至于以什么样式和颜色显示出来，是颜色和样式要讲的内容，这里不提

6. 每调用一次 `beginPath()` 方法，会定义一条新的路径，会把当前路径列表清空重置，注意这里的清空不是说之前绘制图形就从画布上消失了，它们不会消失，这里清空的是路径，这意味着我们可以开始新的图形绘制，使新的绘制不会与之前的图形有相互影响

7. 每使用 `beginPath()` 开启新的路径，一般都要使用 `moveTo(x, y)` 方法设置起始位置，所以这两个方法一般是成对出现的

##### 五个方法

+ `beginPath()`：开启一条新的路径
+ `moveTo(x, y)`：移动笔触，开启一条子路径
+ `closePath()`：封闭（闭合）当前子路径
+ `stroke()`：描边
+ `fill()`：填充，自动闭合所有的子路径

##### 举例

+ 绘制一条直线

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          .myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas class="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementsByClassName('myCanvas')[0];
          var ctx = oCanvas.getContext('2d');
  
          ctx.beginPath();
          ctx.moveTo(100, 100);
          ctx.lineTo(200, 200);
          ctx.stroke();  // 给路径描边
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fth97eur4rj30eu090a9t.jpg)

+ 绘制一个三角形，用stroke描边

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          .myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas class="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementsByClassName('myCanvas')[0];
          var ctx = oCanvas.getContext('2d');
  
          ctx.beginPath();
          ctx.moveTo(100, 100);
          ctx.lineTo(200, 100);
          ctx.lineTo(200, 200);
          ctx.closePath();
          ctx.stroke();
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fth9avud0gj30ej08ydfl.jpg)

  这个例子我们只用 `lineTo(x, y)` 方法画了两条直角边，斜边是调用 `closePath()` 方法，闭合当前路径自动连上的，假如说我们在 `closePath()` 语句的位置写了 `lineTo(100, 100)` ，就不需要 `closePath()` 方法了，效果是一样的（PS: 线比较细时效果是一样的，但是当线条变粗是效果就明显不一样了，这里买个伏笔，后买讲到样式的时候再解释）

+ 绘制一个三角形，用fill填充

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          .myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas class="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementsByClassName('myCanvas')[0];
          var ctx = oCanvas.getContext('2d');
  
          ctx.beginPath();
          ctx.moveTo(100, 100);
          ctx.lineTo(200, 100);
          ctx.lineTo(200, 200);
          ctx.fill();
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fth9i5ad21j30eh08wa9t.jpg)

  看代码，这里我们并没有使用 `closePath()` 方法闭合路径，因为当我们使用 `fill()` 的时候，所有没有闭合的图形都会自动闭合，所以不需要使用 `closePath()` 方法

+ 绘制两个三角形，一个用红色填充，一个用绿色填充

  为了实现这个demo，这里先提示一下设置填充颜色的方法，即在使用 `fill()` 方法前，给 `fill()` 方法设置样式，利用 `fillStyle = color` 的方法，颜色值可以是任何形式

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          .myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas class="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementsByClassName('myCanvas')[0];
          var ctx = oCanvas.getContext('2d');
  
          // 绘制第一个三角形
          ctx.beginPath();
          ctx.moveTo(100, 100);
          ctx.lineTo(200, 100);
          ctx.lineTo(200, 200);
          ctx.fillStyle = 'rgba(255, 0, 0)';
          ctx.fill();
  
          // 绘制第二个三角形
          ctx.moveTo(250, 100);
          ctx.lineTo(350, 100);
          ctx.lineTo(350, 200);
          ctx.fillStyle = 'rgba(0, 255, 0)';
          ctx.fill();
      </script>
  </body>
  </html>
  ```

  看完代码，在没有看运行结果前，你一定以为结果是这样的

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftha7fgnfjj30ej08rmwx.jpg)

  然后结果却是

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftha8fvqhbj30e808umwx.jpg)

  是不是心态爆炸，其实这就是我们之前一直强调的路径问题，再开代码，我们先用 `beginPath()` 方法开启一条新的路径，然后用 `moveTo(100, 100)` 方法开启一条新的子路径，在这个子路径上绘制了第一个三角形路径，填充为红色；接着我们又用 `moveTo(350, 100)` 开启了另一条子路径，在这个子路径上绘制了第二个三角形路径，填充为绿色；需要强调的是，这两个子路径都**在同一条路径下**，同一路径下的不同子路径之间的样式颜色等会产生相互影响，比如我们这个例子中，两个路径上的三角形都显示了第二条路径上的颜色，所以如果我们要设置不同的颜色，就要让他们之间无关联不会相互影响，方法很简单，就是为每一个图形都开启一条新的路径，而不是子路径

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          .myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas class="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementsByClassName('myCanvas')[0];
          var ctx = oCanvas.getContext('2d');
  
          // 开启一条路径（可省略，因为画布初始状态就是一条新的路径），绘制第一个三角形
          ctx.beginPath();
          ctx.moveTo(100, 100);
          ctx.lineTo(200, 100);
          ctx.lineTo(200, 200);
          ctx.fillStyle = 'rgba(255, 0, 0)';
          ctx.fill();
  
          // 开启一条新的路径，绘制第二个三角形
          ctx.beginPath();
          ctx.moveTo(250, 100);
          ctx.lineTo(350, 100);
          ctx.lineTo(350, 200);
          ctx.fillStyle = 'rgba(0, 255, 0)';
          ctx.fill();
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftha7fgnfjj30ej08rmwx.jpg)

##### 不同子路径之间是怎么相互影响的

上面两个画两个三角形的例子说明了不同子路径之间会相互影响，那他们之间到底是怎么影响的呢？看了三角形的例子，你可能会这样想，第二条路径设置了绿色，然后第一条路径上得三角形也变成绿色，那不就是后面路径上的样式覆盖掉了前面路径上的样式么？这么说可能不太准确，下面用两句话来说明他们之间的影响，后续的解释也将围绕这两句话展开

> 1. 样式生效即存在
> 2. 子路径上的颜色或样式，会作用在当前的整个路径上

**样式生效即存在**

首先看下面一个例子

```javascript
var a;
a = 1;
console.log(a);
a = 2;
console.log(a);
```

因为JS是顺序执行的，所以这里第一次打印结果是1，第二次打印结果是2，类比到画三角形的例子

```javascript
ctx.fillStyle = 'rgba(255, 0, 0)';
ctx.fill();
ctx.fillStyle = 'rgba(0, 255, 0)';
ctx.fill();
```

`ctx.fillStyle = 'rgba(255, 0, 0)';` 相当于 `a = 1` ，第一个 `ctx.fill()` 相当于第一个 `console.log(a)`，这里的样式应用成功即生效，生效即存在，就是说第一个三角形已经被填充为红色且存在于画布上，那为什么最终只看到了绿色而没有红色的区域呢？别急，我们只看了一半（第一个子路径），剩下的一半（第二个子路径）我们结合第二句话来看

**子路径上的颜色样式，会作用在当前的整个路径上**

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthhbz91usj30vx0fomx6.jpg)

两个三角形分别代表当前路径下的一个子路径，设置在子路径上的样式，都会作用在当前的整个路径上，我们一步一步来看，在开启第二条路径之前，只有第一个三角形所在的一条子路径，所以它也就是当前的整个路径，所以样式作用在整个路径上就是作用在第一个三角形所在的子路径上，这是第一个三角形所在的子路径变成红色；然后开启第二条子路径，这时当前的整个路径是第一条子路径加上第二条子路径，所以给第二条子路径设置的样式会作用在整个路径上也就是第一条子路径加第二条子路径上，这时两条子路径上的三角形都会应用绿色样式，那么问题来了，对于第二条子路径，本来就没什么样式，现在给他应用绿色的样式，他肯定是绿色没有问题，那对于第一条子路径呢，在这之前它是红色，难道在他应用了绿色的样式以后红色的样式就不存在了么？答案是否定的，上一句话就说过，生效即存在，他已经生效了那他就存在于画布上，那他去哪了呢？

还是画两个三角形的例子，这次我们给每个三角形添加上0.5的透明度

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .myCanvas { border: 1px solid #000; }
    </style>
</head>
<body>
    <canvas class="myCanvas" width="500" height="300"></canvas>
    <script type="text/javascript">
        var oCanvas = document.getElementsByClassName('myCanvas')[0];
        var ctx = oCanvas.getContext('2d');

        // 开启一条路径（可省略，因为画布初始状态就是一条新的路径），绘制第一个三角形
        ctx.beginPath();
        ctx.moveTo(100, 100);
        ctx.lineTo(200, 100);
        ctx.lineTo(200, 200);
        ctx.fillStyle = 'rgba(255, 0, 0, 0.5)';
        ctx.fill();

        // 开启一条新的路径，绘制第二个三角形
        ctx.moveTo(250, 100);
        ctx.lineTo(350, 100);
        ctx.lineTo(350, 200);
        ctx.fillStyle = 'rgba(0, 255, 0, 0.5)';
        ctx.fill();
    </script>
</body>
</html>
```

结果是这样的

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthhi0qyxaj30fs0910si.jpg)

很明显，这两个绿色不太一样，第一个绿色要深一些，原因是绿色底下还有红色，在没有设置透明度之前绿色把红色区域给挡住了，所以好像看起来红色没有了，但其实红色依然存在于画布上，只是被绿色区域给挡住了，现在我们设置了透明度，看到的就是两种颜色叠加在一起的颜色了

> 至此，我们搞清楚了不同路径之间是怎么相互影响的：当前路径下，每一条子路径的样式都会作用在当前的整个路径下，已经生效的样式即存在于画布上，不会消失

#### 矩形

四种绘制方法

> + rect(x, y, width, height)
> + strokeRect(x, y, width, height)
> + fillRect(x, y, width, height)
> + clearRect(x, y, width, height)

**rect(x, y, width, height)**

+ 功能

  绘制一个矩形路径

+ 参数

  x, y：矩形左上角在坐标轴上的坐标

  width：矩形的宽度

  height：矩形的高度

+ 说明

  1. 方法需要选择（x，y）的坐标，说明该方法会开启一条新的路径
  2. 因为是绘制一条路径，所以如果想要看到，需要给它描边或者填充

+ 练习

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementById('myCanvas');
          var ctx = oCanvas.getContext('2d');
          
          ctx.rect(100, 100, 200, 100);
          ctx.stroke();
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthjnd96cgj30ei08wdfl.jpg)

**strokeRect(x, y, width, height)**

+ 功能

  绘制一条矩形路径并描边

+ 参数

  同上

+ 练习

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementById('myCanvas');
          var ctx = oCanvas.getContext('2d');
          
          ctx.strokeRect(100, 100, 200, 100);
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthjnd96cgj30ei08wdfl.jpg)

**fillRect(x, y, width, height)**

+ 功能

  绘制一条矩形路径并填充

+ 参数

  同上

+ 练习

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementById('myCanvas');
          var ctx = oCanvas.getContext('2d');
          
          ctx.fillRect(100, 100, 200, 100);
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthk1jknywj30en08wa9t.jpg)

**clearRect(x, y, width, height)**

+ 功能

  清除一块矩形区域

+ 参数

  同上

+ 练习

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementById('myCanvas');
          var ctx = oCanvas.getContext('2d');
          
          ctx.fillRect(100, 100, 200, 100);
          ctx.clearRect(150, 125, 100, 50);
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthkaevg8tj30ej08ydfl.jpg)

#### 圆弧 

> + arc(x, y, raidus, startAngle, endAngle, anticlockwise)
> + arcTo(x1, y1, x2, y2, radius)

**arc(x, y, radius, startAngle, endAngle, direction）**

+ 功能

  以给定的点连接**当前点**
```
sequenceDiagram
A->>B: How are you?
B->>A: Great!
```

```
gantt
dateFormat YYYY-MM-DD
section S1
T1: 2014-01-01, 9d
section S2
T2: 2014-01-11, 9d
section S3
T3: 2014-01-02, 9d
```
(下面有解释)，并按要求绘制圆弧路径

+ 参数

  (x, y)：圆心在坐标轴上的位置

  radius：圆弧路径的半径

  startAngle：圆弧路径的起始位置

  endAngle：圆弧路径的终止位置

  direction：圆弧路径绘制的方向

+ 说明

  1. 如果绘制圆弧子路径前开启了新的路径，那么当前点就是(x, y)
  2. 如果绘制圆弧子路径前没有开启新的路径，那么当前点为上一子路径的终点或者是使用 moveTo(x, y) 方法设置的点
  3. 起始弧度和终止弧度必须用 **弧度（Math.PI）** 来描述，比如 45度应该用 `Math.PI * 1 / 4` 来描述
  4. 路径绘制的方向有顺时针和逆时针两种，`true` 为逆时针（默认），`false` 为顺时针

+ 练习

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementById('myCanvas');
          var ctx = oCanvas.getContext('2d');
          
          ctx.arc(100, 100, 50, 0, Math.PI, false);
          ctx.stroke();
  
          // ctx.beginPath();
          ctx.arc(300, 100, 50, 0, -Math.PI, true);
          ctx.stroke();
      </script>
  </body>
  </html>
  ```

  打开注释前

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthlowb24gj30es08p3yb.jpg)

  打开注释后

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthlp6ih5fj30eg08vwea.jpg)

**arcTo(x1, y1, x2, y2, radius)**

+ 功能

  绘制的弧线路径与**当前点**和(x1,y1)连线，(x1,y1)和(x2,y2)连线都相切 

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthmi334o2j30d606zmx7.jpg)

+ 参数

  (x1, y1)：与当前点进行连接的点

  (x2, y2)：与(x1, y1)进行连接的点

  radius：与两条直线相切的圆的半径

+ 说明

  这里的当前点和上一个当前点不太一样，这里的当前点要通过 `moveTo(x, y)` 方法进行设置，如果不设置的话，他会找当前路径下上一个子路径的终点作为当前点，如果没有这个值的话，就不能绘制出图形，也就是说只要使用了 `beginPath()` 开启路径，就要先用 `moveTo(x, Y)` 方法设置当前点，然后才能开始使用这个方法（因为新开启的路径中肯定没有上一个路径的终点）

+ 练习

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style>
          #myCanvas { border: 1px solid #000; }
      </style>
  </head>
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var oCanvas = document.getElementById('myCanvas');
          var ctx = oCanvas.getContext('2d');
          
          ctx.moveTo(100, 100);   
          ctx.arcTo(200, 100, 200, 200, 50);
          ctx.stroke();
  
          // ctx.moveTo(300, 100);
          ctx.arcTo(400, 100, 400, 200, 50);
          ctx.stroke();
  
      </script>
  </body>
  </html>
  ```

  打开注释前：

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthmdxhzm1j30en08vdfm.jpg)

  打开注释后：

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthmebf3kej30en08z742.jpg)

#### 贝塞尔曲线

+ 介绍

  > N次贝塞尔曲线有一个开始点，一个结束点，N-1个控制点

  二次贝塞尔曲线

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthoxa4nk0g30a0046ady.gif)

  三次贝塞尔曲线

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthoxjiuzhg30a004679v.gif)

  四次贝塞尔曲线

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthoxyue9xg30a0046ah6.gif)

  五次贝塞尔曲线

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthoybbxn3g30d50aiu0x.gif)

  以上时二次~五次贝塞尔曲线的运动轨迹，其中二次和三次使用较多，这里了解一下二次贝塞尔曲线的运动轨迹

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthoxa4nk0g30a0046ady.gif)

  P0和P2分别称为开始点和结束点，P1称为控制点，假设有两点分别从P0和P1同时出发，要求从P0出发的的点到达P1的时间，和从P1出发的点到达P2的时间相同，运动过程中，过P0作两个运动的点的连线（绿线）的切线（红线），这个切线就是二次贝塞尔曲线

  三次、四次、五次贝塞尔曲线同理

+ 语法（二次）

  quadraticCurve(x1, y1, endX, endY);

+ 功能

  以当前点为开始点，与参数中的控制点和结束点一起构成二次贝塞尔曲线 

+ 参数（二次贝塞尔曲线）

  (x1, y1)：控制点的坐标

  (endX, endY)：结束点的坐标

+ 说明

  当前点的含义与 `arcTo()` 方法中当前点的含义相同

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              // 二次贝塞尔曲线
              ctx.beginPath();
              ctx.moveTo(75, 25);
              ctx.quadraticCurveTo(25, 25, 25, 62.5);
              ctx.quadraticCurveTo(25, 100, 50, 100);
              ctx.quadraticCurveTo(50, 120, 30, 125);
              ctx.quadraticCurveTo(60, 120, 65, 100);
              ctx.quadraticCurveTo(125, 100, 125, 62.5);
              ctx.quadraticCurveTo(125, 25, 75, 25);
              ctx.stroke();
          }
      </script>
  </body>
  
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthpqq8p8qj30ec08sjr7.jpg)

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              //三次贝塞尔曲线
              ctx.beginPath();
              ctx.moveTo(75, 40);
              ctx.bezierCurveTo(75, 37, 70, 25, 50, 25);
              ctx.bezierCurveTo(20, 25, 20, 62.5, 20, 62.5);
              ctx.bezierCurveTo(20, 80, 40, 102, 75, 120);
              ctx.bezierCurveTo(110, 102, 130, 80, 130, 62.5);
              ctx.bezierCurveTo(130, 62.5, 130, 25, 100, 25);
              ctx.bezierCurveTo(85, 25, 75, 37, 75, 40);
              ctx.fill();
          }
      </script>
  </body>
  
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthpry1tpbj30en08xjr6.jpg)

#### Path2D对象（没搞懂，等待补充）



### 颜色和填充样式

#### 颜色

我们之前了解了使用 `stroke()` 方法和 `fill()` 方法可以显示路径，`stroke()` 相当于是画笔，`fill()` 相当于是刷子，通过改变这些 “工具”的颜色，可以让路径显示不同的颜色

##### strokeStyle

+ 语法

  `strokeStyle = color`

+ color

  color可以是颜色名(re)、rgb(255, 0, 0),、rgba(255, 0, 0, 1)、颜色代码(#FF0000)

##### fillStyle

+ 语法

  `fillStyle = color`

+ color

  颜色名、rgb、rgba、颜色代码

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
    </style>
</head>

<body>
    <canvas id="myCanvas" width="500" height="300"></canvas>
    <script type="text/javascript">
        var canvas = document.getElementById('myCanvas');
        if (canvas.getContext) {
            var ctx = canvas.getContext('2d');

            ctx.beginPath();
            ctx.strokeStyle = 'red';
            ctx.strokeRect(100, 100, 200, 100);

            ctx.beginPath();
            ctx.fillStyle = 'green';
            ctx.fillRect(350, 100, 100, 100);
        }
    </script>
</body>

</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthr5oxsmsj30ei08xjr5.jpg)

#### 透明度

##### 全局透明度

+ 功能

  给画布中所有元素设置透明度，使用以下语法

+ 语法

  `globalAlpha = value`

  value的取值：0.0~1.0

+ demo

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
              
              ctx.globalAlpha = 0.2;
  
              ctx.beginPath();
              ctx.fillStyle = 'red';
              ctx.fillRect(100, 100, 200, 100);
  
              ctx.beginPath();
              ctx.fillStyle = 'green';
              ctx.fillRect(350, 100, 100, 100);
          }
      </script>
  </body>
  
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthrbwgdoij30ej08wgld.jpg)

##### 局部透明度

+ 功能

  给指定的元素设置透明度

+ 语法

  要给那个元素单独设置透明度，就要在给这个元素设置颜色时，采用rgba的方法设置

+ demo

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              ctx.beginPath();
              ctx.fillStyle = 'rgba(255, 0, 0, 0.2)';
              ctx.fillRect(100, 100, 200, 100);
  
              ctx.beginPath();
              ctx.fillStyle = 'green';
              ctx.fillRect(350, 100, 100, 100);
          }
      </script>
  </body>
  
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fthre9soxfj30ei091gld.jpg)

#### 线型

可以通过一系列属性来设置线的样式

##### lineWidth

+ 功能

  设置线的宽度

+ 语法

  `lineWidth = value`

  value是正整数，默认值是1

+ 线宽

  线宽是指给定路径的中心到两边的粗细。换句话说就是在路径的两边各绘制线宽的一半。 

+ 图像不能精确呈现的问题

  + 首先一个实例来说明要讲的问题，我们在画布的两个不同的位置各画一条 `lineWidth = 1` 的直线

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
        </style>
    </head>
    
    <body>
        <canvas id="myCanvas" width="500" height="300"></canvas>
        <script type="text/javascript">
            var canvas = document.getElementById('myCanvas');
            if (canvas.getContext) {
                var ctx = canvas.getContext('2d');
    
                ctx.moveTo(100, 100);
                ctx.lineWidth = 1;
                ctx.lineTo(200, 100);
    
                ctx.moveTo(100, 110.5);
                ctx.lineTo(200, 110.5);
                ctx.strokeStyle = 'deepskyblue';
                ctx.stroke();   
            }
        </script>
    </body>
    
    </html>
    ```

    ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fticmlau2mj30ek0903y9.jpg)

    很明显，虽然我们给这两条直线设置了相同的线宽，但是他们显示出来的宽度确不一样，下面那条比较标准，上面那条变宽了，这是为什么呢？要解决这个问题，我们需要先了解坐标网格中的一些概念

  + 坐标网格中的一些概念

    ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftid8uc83vj30qw0coa9x.jpg)

    + 坐标点

      坐标网格中坐标轴相交的点。如上图所示的(0, 0)点、(5, 5)点

    + 像素

      坐标网格中一个单元格代表一像素。上图画出了两个像素（紫色区域）

    + 半像素

      坐标网格中一个单元格的一部分，半像素不一定必须是像素的一半，只要是一个完整像素的一部分，都可以称为是半像素。上图画出了两个半像素（粉色区域）

  + 半像素的渲染方式

    如果给半像素指定了渲染颜色，则该像素单元格中的其余部分会以指定渲染颜色一半的色调来填充满整个区域

  + 解释线宽不准确的原因

    了解了以上的概念后就很好理解为什么同样是1单位的线宽呈现结果会不同了

    ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftidlxrrtej30gk04uglf.jpg)

    左图在坐标网格(3,1)到(3,5)的区域绘制了一条直线路径，线宽为1单位所以向左右各延展0.5单位，这时问题来了，因为只想左右延展了0.5个单位，那么就存在半像素，半像素的剩余部分会渲染颜色一半的色调来填充，所以我们最后看到的其实是2单位线宽的直线

    右图在坐标网格(3.5,1)到(3.5,5)的区域绘制了一条直线路径，线宽为1单位向左右两侧延展0.5单位，这时左右两侧的渲染区域就正好是1个单位的像素，不存在半像素，所以直线的线宽是准确的

  + 结论

    图像能否精确展示，和路径的定义的位置有关，最终着色的部分的边缘落在坐标网格的轴线上，那么就不存在半像素的问题，可以精确展示；最终着色部分的边缘落在坐标网格内，那么久存在半像素的问题，展示结果就会不精确

+ 图形闭合处锯齿问题

  还是先来看一个例子，绘制一个三角形，线宽为10

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              ctx.moveTo(100, 100);
              ctx.lineTo(200, 100);
              ctx.lineTo(100, 200);
              ctx.lineTo(100, 100);
              ctx.lineWidth = 10;
              ctx.stroke();
          }
      </script>
  </body>
  
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftielouompj30em08rdfl.jpg)

  结果如图，将直线练回起点想要封闭图形时，发现不能完全封闭，存在类似锯齿的小缺口，解决这样的问题很简单，使用 `closePath()` 方法封闭路径即可

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              ctx.moveTo(100, 100);
              ctx.lineTo(200, 100);
              ctx.lineTo(100, 200);
  
              // 如果使用closePath()方法封闭路径，那么这条语句就没什么必要了
              // ctx.lineTo(100, 100);
              
              ctx.lineWidth = 10;
              ctx.closePath();
              ctx.stroke();
          }
      </script>
  </body>
  
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftieq4jqadj30ep08wgld.jpg)


##### lineCap

+ 功能

  决定线段端点显示的样子

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftie113iloj305705c741.jpg)

+ 语法

  `lineCap = 'butt'(默认) | 'round' | 'square';`

  butt：与辅助线平齐

  round：端点处加上了直径为线宽的半圆

  square：端点处加上了宽高为线宽的矩形

##### lineJoin

+ 功能

  定义了线段在连接处所显示的样子

+ 语法

  `lineJoin = 'round' | 'bevel' | 'miter'(默认);`

  round：接口处是圆角。圆的半径等于线宽

  bevel：接口处是斜线。

  miter：线段在连接处外侧延伸直至交于一点

+ miterLimit

  针对 `lineJoin = 'miter'`，为了防止线段连接处延伸过远，使用 `miterLimit` 属性可以限制其延伸，当lineJoin是miter时，用于控制斜接部分的长度

  PS：实际运算是大于limit*lineWidth/2的值，了解就好

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftifephmjpj30h609uq4g.jpg)

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              ctx.moveTo(100, 100);
              ctx.lineTo(200, 100);
              ctx.lineTo(100, 120);
              ctx.closePath();
              ctx.lineWidth = 10;
              ctx.lineJoin = 'miter';
              ctx.stroke();
  
              ctx.beginPath();
              ctx.moveTo(250, 100);
              ctx.lineTo(350, 100);
              ctx.lineTo(250, 120);
              ctx.closePath();
              ctx.lineJoin = 'miter';
              ctx.miterLimit = 20;
              ctx.stroke();
          }
      </script>
  </body>
  
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftifj8e7q3j30el08xdfl.jpg)

##### 虚线

+ 功能

  如题

+ 语法

  `setLineDash(prop);`

+ 参数

  参数prop是一个数组，用来制定线段与间隙的交替

  如：[10, 5] ---------------------- [线长是10，线之间的间隙是5，.......] 如此反复交替

  	[40, 30, 20, 10] ---------- [线长40，间隙30，线长20，间隙10，线长40，......] 如此反复交替

  	[40, 30, 20] --------------- 如果参数是奇数个，数组会先复制一次，变成偶数个参数，然后同上

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
              
              ctx.beginPath();
              ctx.moveTo(0, 100);
              ctx.setLineDash([40, 30]);
              ctx.lineTo(500, 100);
              ctx.stroke();
  
              ctx.beginPath();
              ctx.moveTo(0, 150);
              ctx.setLineDash([40, 30, 20, 10]);
              ctx.lineTo(500, 150);
              ctx.stroke();
  
              ctx.beginPath();
              ctx.moveTo(0, 200);
              ctx.setLineDash([40, 30, 20]);
              ctx.lineTo(500, 200);
              ctx.stroke();
          }
      </script>
  </body>
  
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftigsi9kqej30el092742.jpg)

  如果想要变回直线，可以利用这个巧妙地方法：`ctx.setLineDash([]);`


#### 渐变

+ 功能

  可以利用渐变来进行填充或者描边

+ 使用方法

  + 创建 `canvasGradient` 对象

    + 线性渐变

      `creatLinearGradient(x1, y1, x2, y2)`

      (x1, y1)：渐变的起点

      (x2, y2)：渐变的终点

    + 径向渐变

      `createRadialGradient(x1, y1, r1, x2, y2, r2)`

      (x1, y1, r1)：渐变开始的圆

      (x2, y2, r2)：渐变结束的圆

  + 给 `canvasGradient` 对象添加渐变色

    + 方法

      `canvasGradient.addColorStop(position, color)`

    + 参数

      position：0.0~1.0之间的数值，表示渐变颜色的相对位置

      color：必须是一个有效的CSS颜色值

  + 将 `canvasGradient` 对象赋给 `strokeStyle` 或者 `fillStyle` 

  + 使用

+ 练习

  + 线性渐变

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
        </style>
    </head>
    
    <body>
        <canvas id="myCanvas" width="500" height="300"></canvas>
        <script type="text/javascript">
            var canvas = document.getElementById('myCanvas');
            if (canvas.getContext) {
                var ctx = canvas.getContext('2d');
                var linearGradient = ctx.createLinearGradient(100, 100, 100, 200);
                
                ctx.beginPath();
                linearGradient.addColorStop(0, 'red');
                linearGradient.addColorStop(0.3, 'green');
                linearGradient.addColorStop(0.4, 'blue');
                linearGradient.addColorStop(1.0, 'transparent');
                ctx.fillStyle = linearGradient;
                ctx.fillRect(100, 100, 200, 100);
            }
        </script>
    </body>
    
    </html>
    ```

    ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftimydvmixj30ei08x3ya.jpg)

  + 径向渐变

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
        </style>
    </head>
    
    <body>
        <canvas id="myCanvas" width="500" height="300"></canvas>
        <script type="text/javascript">
            var canvas = document.getElementById('myCanvas');
            if (canvas.getContext) {
                var ctx = canvas.getContext('2d');
                var radialGradient = ctx.createRadialGradient(200, 150, 10, 250, 150, 100);
    
                ctx.beginPath();
                radialGradient.addColorStop(0, 'red');
                radialGradient.addColorStop(0.3, 'green');
                radialGradient.addColorStop(0.6, 'blue');
                radialGradient.addColorStop(1.0, 'transparent');
                ctx.fillStyle = radialGradient;
                ctx.arc(250, 150, 100, 0, Math.PI * 2, true);
                ctx.fill();
            }
        </script>
    </body>
    
    </html>
    ```

    ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ftineo2m4jj30en0963zn.jpg)

#### 填充图案

+ 功能

  与渐变功能相似，只不过填充的是图案

+ 使用方法

  + 创建 `pattern` 对象

    + 语法

      `pattern = createPattern(image, type)`

    + 参数

      image：img元素、canvas元素、video元素（有图形的）

      type：repeat | repeat-x | repeat-y | no-repeat

    + 注意

      如果参数是img元素，那么这个方法要等到图片加载完成之后才能使用

  + 将 `pattern` 对象赋给 `strokeStyle` 或者 `fillStyle`

  + 使用

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
              var oImg = new Image();
              oImg.src = 'http://ww1.sinaimg.cn/large/006eYMu7ly1ftioar0jtnj308w050jv1.jpg';
              oImg.onload = function () {
                  ctx.fillStyle = ctx.createPattern(oImg, 'repeat');
                  ctx.fillRect(0, 0, 500, 300);
              }
          }
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftiofewl0wj30ef0950z5.jpg)

#### 阴影

+ 功能

  如题

+ 使用方法

  + 设置阴影半径

    `shadowBlur = float`

  + 设置横纵偏移量

    `shadowOffsetX = float`

    `shadowOffsetY = float`

  + 设置阴影颜色

    `shadowColor = color`

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              ctx.beginPath();
              ctx.shadowBlur = 10;
              ctx.shadowOffsetX = 10;
              ctx.shadowOffsetY = 10;
              ctx.shadowColor = '#ccc';
              ctx.fillStyle = '#999';
              ctx.fillRect(100, 100, 200, 100);
          }
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftiony81afj30ed08wgle.jpg)

### 绘制文本

#### storkeText()

+ 功能

  在指定区域描绘文本

+ 语法

  `strokeText(text, x, y [, maxWidth])`

+ 参数

  + text

    文本内容

  + (x, y)

    文本起点坐标

  + maxWidth

    可选项，表示绘制的最大宽度，如果指定了该值，并且经过计算字符串的值比最大宽度还要宽，字体为了适应会水平缩放（如果通过水平缩放当前字体，可以进行有效的或者合理可读的处理）或者使用小号的字体。

#### fillText()

+ 功能

  在指定区域填充文本

+ 语法

  `fillText(text, x, y [, maxWidth])`

+ 参数

  同 `strokeText()`

#### 设置文本样式

在绘制文本之前我们可以通过一些属性来设置要绘制的文本的样式

##### 字体样式

+ 功能

  设置字体的大小、风格等，同CSS种 `font` 用法相同

+ 语法

  `font = "font-style font-variant font-width font-size font-family"`

+ 参数

  默认值是："10px sans-serif"

  其他的不解释了，不懂先去学css

##### 文本对齐选项

**引入**

前面绘制本文的样式语法中提到，要绘制文本需要文本内容和起始点的坐标，现在我们把关注点放在起始点的坐标上，抛出一个问题，这个起始点的坐标是文本内容区域的哪一个点呢？（以绘制矩形为例，绘制矩形的起始点是矩形的左上角顶点在坐标轴中的位置）为了解决这个问题，我们来看下面两个属性


**textAlign**

+ 功能

  文本在水平方向的对齐选项

+ 语法

  `textAlign = 'start'(默认) | 'end' | 'left' | 'right' | 'center';`

+ 图解参数

  起始点x的坐标在蓝色的线上，蓝色的线与文本展示了不同对齐方式水平上的差别

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftiuasvyc1j30eq09k744.jpg)

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              ctx.strokeStyle = "blue";
              ctx.moveTo(250, 20);
              ctx.lineTo(250, 280);
              ctx.stroke();
  
              ctx.font = "15px Arial";
              ctx.textAlign = "start";
              ctx.fillText("textAlign=start", 250, 50);
              ctx.textAlign = "end";
              ctx.fillText("textAlign=end", 250, 100);
              ctx.textAlign = "left";
              ctx.fillText("textAlign=left", 250, 150);
              ctx.textAlign = "center";
              ctx.fillText("textAlign=center", 250, 200);
              ctx.textAlign = "right";
              ctx.fillText("textAlign=right", 250, 250);
          }
      </script>
  </body>
  
  </html>
  ```


**textBaseLine**

+ 功能

  文本在竖直方向上的对齐选项

+ 语法

  `textBaseline = 'top' | 'hanging' | 'middle' | 'alphabetic'(默认) | 'ideagrophic' | 'bottom';`

+ 图解参数

  起始点y的坐标在蓝色的线上，蓝色的线与文本展示了不同对齐方式在竖直方向上的差别

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftiugllis6j30ef08y745.jpg)

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              //在位置 y=150 绘制蓝色线条
              ctx.strokeStyle = "blue";
              ctx.moveTo(5, 150);
              ctx.lineTo(495, 150);
              ctx.stroke();
  
              ctx.font = "20px Arial"
  
              //在 y=200 以不同的 textBaseline 值放置每个单词
              ctx.textBaseline = "top";
              ctx.fillText("Top", 25, 150);
              ctx.textBaseline = "bottom";
              ctx.fillText("Bottom", 80, 150);
              ctx.textBaseline = "middle";
              ctx.fillText("Middle", 180, 150);
              ctx.textBaseline = "alphabetic";
              ctx.fillText("Alphabetic", 280, 150);
              ctx.textBaseline = "hanging";
              ctx.fillText("Hanging", 400, 150);
          }
      </script>
  </body>
  
  </html>
  ```

  下面的图片展示了textBaseline属性支持的不同的基线情况 

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftiuun8pw5j30k007mjru.jpg)

### 变形

我们之前学习的坐标网格和画布，都是默认情况下的状态。通过变形，我们可以将原点移动到另外一点，可以对网格进行旋转和缩放等操作

#### 状态保存和恢复

状态保存 `save()` 方法，和状态恢复 `restore()` 方法是用来保存和恢复canvas状态的。canvas状态就是当前画面应用的所有样式和变形的一个快照

一个canvas状态包括：

+ 当前应用的变形（即移动、旋转和缩放）
+ `strokeStyle`, `fillStyle`, `globalAlpha`, `lineWidth`, `lineCap`, `lineJoin`, `miterLimit`, `shadowOffsetX`, `shadowOffsetY`, `shadowBlur`, `shadowColor`, `globalCompositeOperation 的值`
+ 当前的裁切路径（后面会讲到）

Canvas状态存储在栈中，每当 `save()` 方法被调用后，当前的状态就被推送到栈中保存；每一次调用 `restore` 方法，上一个保存的状态就从栈中弹出，所有设定都恢复 

#### 移动

+ 功能

  用来移动canvas和坐标原点到另外一个位置

+ 语法

  `translate(x, y)`

+ 参数

  x：左右偏移量

  y：上下偏移量

+ 注意

  在进行移动之前先保存状态是一个好习惯

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d'),
                  oImg = new Image();
                  oImg.src = 'https://ws1.sinaimg.cn/large/006eYMu7ly1ftiw9x8975j30dw08cwnv.jpg';
                  oImg.onload = function (){
                      ctx.beginPath();
                      ctx.save();
                      ctx.translate(50, 50);
                      ctx.fillStyle = ctx.createPattern(oImg, 'no-repeat');
                      ctx.fillRect(0, 0, 500, 300);
                  }
          }
      </script>
  </body>
  
  </html>
  ```

  图片是充满整个canvas的，所以图片的变换就能体现canvas的变化

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftiwjt7eoog30p80fxdri.gif)

  如果我们要接着在画布上**移动前的**(0, 0) 的位置填充一个边长为50的正矩形，如果不用 `restore()` 方法的话，就要用 `restore()`方法先恢复到平移前的状态

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d'),
                  oImg = new Image();
                  oImg.src = 'https://ws1.sinaimg.cn/large/006eYMu7ly1ftiw9x8975j30dw08cwnv.jpg';
                  oImg.onload = function (){
                      ctx.beginPath();
                      ctx.save();
                      ctx.translate(50, 50);
                      ctx.fillStyle = ctx.createPattern(oImg, 'no-repeat');
                      ctx.fillRect(0, 0, 500, 300);
  
                      ctx.restore();
                      ctx.fillStyle = 'yellow';
                      ctx.fillRect(0, 0, 50, 50);
                  }
          }
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftiwrlbywjj30ei08ttfn.jpg)

#### 旋转

+ 功能

  以原点为中心，旋转canvas

+ 语法

  `rotate(angle)`

+ 参数

  angle：旋转的角度值，顺时针方向，以弧度为单位值

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d'),
                  oImg = new Image();
                  oImg.src = 'https://ws1.sinaimg.cn/large/006eYMu7ly1ftiw9x8975j30dw08cwnv.jpg';
                  oImg.onload = function (){
                      ctx.beginPath();
                      ctx.save();
                      ctx.rotate(Math.PI * 1 / 10);
                      ctx.fillStyle = ctx.createPattern(oImg, 'no-repeat');
                      ctx.fillRect(0, 0, 500, 300);
                  }
          }
      </script>
  </body>
  
  </html>
  ```

  图片是充满整个canvas的，所以图片的变换就能体现canvas的变化

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftixdh70peg30p80fxwot.gif)

  如果我们要接着在画布上**旋转前的**(200, 0) 的位置填充一个边长为50的正矩形，如果不用 `restore()` 方法的话，就要用 `restore()`方法先恢复到平移前的状态

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d'),
                  oImg = new Image();
                  oImg.src = 'https://ws1.sinaimg.cn/large/006eYMu7ly1ftiw9x8975j30dw08cwnv.jpg';
                  oImg.onload = function (){
                      ctx.beginPath();
                      ctx.save();
                      ctx.rotate(Math.PI * 1 / 10);
                      ctx.fillStyle = ctx.createPattern(oImg, 'no-repeat');
                      ctx.fillRect(0, 0, 500, 300);
                      ctx.restore();
                      ctx.fillStyle = 'yellow';
                      ctx.fillRect(200, 0, 50, 50);
                  }
          }
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftixi95f6rj30ej08uago.jpg)

#### 缩放

+ 功能

  我们用它来增减图形在 canvas 中的像素数目，对形状，位图进行缩小或者放大 

+ 语法

  `scale(x, y)`

+ 参数

  x：横轴上的缩放因子

  y：纵轴上的缩放因子

  默认情况下，canvas 的 1 单位就是 1 个像素。举例说，如果我们设置缩放因子是 0.5，1 个单位就变成对应 0.5 个像素，这样绘制出来的形状就会是原先的一半。同理，设置为 2.0 时，1 个单位就对应变成了 2 像素，绘制的结果就是图形放大了 2 倍。

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d'),
                  oImg = new Image();
                  oImg.src = 'https://ws1.sinaimg.cn/large/006eYMu7ly1ftiw9x8975j30dw08cwnv.jpg';
                  oImg.onload = function (){
                      ctx.beginPath();
                      ctx.save();
                      ctx.scale(0.5, 0.5);
                      ctx.fillStyle = ctx.createPattern(oImg, 'no-repeat');
                      ctx.fillRect(0, 0, 500, 300);
                  }
          }
      </script>
  </body>
  
  </html>
  ```

  

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftixp2k99pg30p80fx12j.gif)

#### transform

+ 功能

  将移动、旋转、缩放功能合到了一起

+ 语法

  `setTransform(a, b, c, d, e, f)`

  `transform(a, b, c, d, e, f)`

+ 两种方法不同

  第一种是先重置之前画布上进行的变形操作，然后再进行自己的变形操作，及不受前面操作的影响

  第二种是在之前画布变形操作的基础上进行操作，受前面操作的影响，一般不使用这种方法

+ 参数

  a：水平缩放

  b：水平倾斜

  c：垂直倾斜

  d：垂直缩放

  e：水平移动

  f：垂直移动

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <button style="display: block;">setTransform</button>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas'),
              btn = document.getElementsByTagName('button')[0];
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
  
              ctx.beginPath();
              ctx.font = '20px arial';
              ctx.textAlign = 'center';
              ctx.textBaseline = 'middle';
              ctx.fillText('Hello World', 250, 150);
  
              function sovle() {
                  ctx.clearRect(0, 0, 500, 300);
                  ctx.setTransform(1, -0.12, 0.2, 1, 0, 12);
                  ctx.fillText('Hello World', 250, 150);
              }
          }
          btn.onclick = function () {
              sovle();
          }
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftkqvjq3mog30gz0aidfw.gif)

### 合成与剪裁

#### 裁剪

+ 功能

  将当前绘制的路径裁剪下来，裁剪区域外的区域不能继续绘制

+ 语法

  `clip()`

+ 说明

  如果在裁剪完之后还想在画布上裁剪区域以外的区域绘制，需要利用 `save()` 方法保存裁剪前的画布状态，然后利用 `restore()` 方法恢复保存的状态

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
              
              ctx.beginPath();
              ctx.arc(250, 150, 100, 0, Math.PI * 2, true);
              ctx.stroke();
              // ctx.save();
              ctx.clip();
  
              ctx.font = '20px arial';
              ctx.textAlign = 'center';
              ctx.textBaseline = 'middle';
              ctx.fillText("被裁减的区域", 250, 150);
  
              // ctx.restore();
              ctx.moveTo(0, 0);
              ctx.fillRect(0, 0, 100, 100);
          }
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftjt939xxqj30eh08va9y.jpg)

  裁剪了一个圆形区域后，我想在画布上圆形区域以外在填充一个矩形，发现没有效果，因为被裁减区域以外的区域无法继续绘制，所以需要使用 `save()` 和 `resotre()` 方法（将上述代码的注释打开）

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftjt9m7k52j30eb08va9y.jpg)

#### 合成

+ 功能

  当两个图形重合时，控制他们该以什么样的形式合成

+ 语法

  `globalCompositeOperation = value`

+ value

  11种值，默认是 "source-over"

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftjtit3bw9j30dj0ae0v9.jpg)

+ 练习

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
              
  
              ctx.beginPath();
              ctx.fillStyle = 'rgba(255, 0, 0)';
              ctx.fillRect(100, 100, 150, 100);
  
              ctx.globalCompositeOperation = 'source-over';
              ctx.globalCompositeOperation = 'source-atop';
              ctx.globalCompositeOperation = 'source-in';
              ctx.globalCompositeOperation = 'source-out';
              ctx.globalCompositeOperation = 'destination-over';
              ctx.globalCompositeOperation = 'destination-atop';
              ctx.globalCompositeOperation = 'destination-in';
              ctx.globalCompositeOperation = 'destination-out';
              ctx.globalCompositeOperation = 'copy';
              ctx.globalCompositeOperation = 'lighter';
              ctx.globalCompositeOperation = 'xor';
  
              ctx.beginPath();
              ctx.fillStyle = 'rgba(0, 255, 0)';
              ctx.fillRect(150, 150, 150, 100);
          }
      </script>
  </body>
  
  </html>
  ```

  逐行注释，观察效果

### 使用图片

> canvas更有意思的一项特性就是图像操作能力。可以用于动态的图像合成或者作为图形的背景，以及游戏界面（Sprites）等等。浏览器支持的任意格式的外部图片都可以使用，比如PNG、GIF或者JPEG。 你甚至可以将同一个页面中其他canvas元素生成的图片作为图片源。 

既然我们要利用canvas处理图片，那么首先我们要获取到图片，然后将图片绘制到canvas中，这时我们便可以利用canvas中提供的API对绘制的图片进行一系列的操作，紧接着我们还可以将处理完成的图片导出，这便是一个canvas处理图片比较完整的流程

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftjxlt2dr2j30ma03b3yc.jpg)

#### 获取图片

**图片类型**

这里我们说的图片是泛指，它包括图片类型但是不限于图片类型，它的类型可以是下列几种类型

+ `HTMLImageElement`

  由 `Image()`方法构造出来的，或者是用JS获取的\<img>类型的dom元素

+ `HTMLCanvasElement`

  可以是另外一个canvas元素

+ `HTMLVideoElement`

  用一个HTML的\<video>元素作为你的图片源，可以从视频中抓取当前帧作为一个图像

+ `ImageBitmap`

  这是一个高性能的位图，可以低延迟地绘制，它可以从上述的所有源以及其它几种源中生成 

**获取图片**

+ 获取 `HTMLImageElement` 类型的图片

  **！！！使用这种方法格外需要注意的一点就是要等图片加载完毕之后再进行对图片的操作**

  + 使用 `Image()` 方法创建一个img对象

    使用这种方法是创建一个图片元素，需要指定image对象的 `src` 属性

    ```javascript
    var oImg = new Image();
    oImg.src = 'demo.jpg';
    oImg.onload = function () {
    	// 处理图片操作
    }
    ```

  + 使用 `data:url` 方法来引用图像

    `data:url` 允许使用一串 base64 格式编码的字符串来定义一个图片

    ```javascript
    img.src = 'data:image/gif;base64,R0lGODlhCwALAIAAAAAA3pn/ZiH5BAEAAAEALAAAAAALAAsAAAIUhA+hkcuO4lmNVindo7qyrIXiGBYAOw==';
    ```

    优点：图片内容即时可用，无需向服务器请求

    缺点：图像没法缓存图片太大的话内嵌的url数据会过长

  + 使用相同页面内的图片

    使用同一个页面下的图片，我们可以通过JS获取dom的操作获取同一页面中的img元素，也可以使用 `document.images` 获取图片集合

  + 跨域获取图片

    在 `HTMLImageElement` 上使用 `crossOrigin` 属性，可以跨域请求图片，前提是被请求的图片服务器支持跨域访问，那么使用这个属性可以请求到图片且不污染canvas，如果不使用这个属性的话会[污染canvas]('https://developer.mozilla.org/zh-CN/docs/Web/HTML/CORS_enabled_image#.E4.BB.80.E4.B9.88.E6.98.AF.22.E8.A2.AB.E6.B1.A1.E6.9F.93.22.E7.9A.84canvas')

+ 获取 `HTMLCanvasElement` 类型的图片

  即使用另外一个canvas类型来当做图片，我们可以用JS获取dom操作获取指定的canvas

  ```javascript
  var newCanvas = document.getElementById('mycanvas');
  ```

+ 获取 `HTMLVideoElement` 类型的图片

  可以使用\<video>中的视频帧（即便视频是不可见的）

#### 绘制图片

当我们成功的获取到图片时，我们就可以把它绘制到canvas中了，利用 `drawImage()` 方法，`drawImage()` 方法共有三总形式 ，每一种的绘制方法都有所不同，下面我们来学习一下

**普通绘制**

+ 功能

  将获取到的图片绘制到canvas中

+ 参数

  image：上一步获取到的图片资源

  (x, y)：是图片要绘制到canvas中的起始坐标

+ 练习

  引入一张坐标图纸，利用canvas在图纸上图表

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas');;
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
              var oImg = new Image();
  
              oImg.src = 'https://ws1.sinaimg.cn/large/006eYMu7ly1ftjy0y6iymj309q078q2p.jpg';
              oImg.onload = function () {
                  ctx.beginPath();
                  ctx.drawImage(oImg, 50, 10);
                  ctx.moveTo(88, 255);
                  ctx.lineTo(140, 209);
                  ctx.lineTo(250, 167);
                  ctx.lineTo(330, 40);
                  ctx.stroke();
              }
          }
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftk02osv7kj30ed08rdfp.jpg)

**缩放**

+ 功能

  与 `drawImage(image, x, y, width, height)` 不同的是，他增加了图片的缩放功能

+ 语法

  `drawImage(image, x, y, width, height)`

+ 参数

  image：获取到的图片

  (x, y)：图片在canvas中的起始位置

  width：图片被引入canvas中的宽度

  height：图片被引入canvas中的height

+ 注意

  图像可能会因为大幅度的缩放而变得起杂点或者模糊。如果您的图像里面有文字，那么最好还是不要进行缩放，因为那样处理之后很可能图像里的文字就会变得无法辨认了 

+ 练习

  在一个canvas中引入另一个canvas元素，并把他的宽高都缩小为原来的一半

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
          #myCanvas1 {
              border: 1px solid #000;
          }
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300">Don't support canvas.</canvas>
      <canvas id="myCanvas1" width="500" height="320">Don't support canvas.</canvas>
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas'),
              canvas1 = document.getElementById('myCanvas1');
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
              var linearGrad = ctx.createLinearGradient(0, 0, 500, 0);
  
              ctx.beginPath();
              linearGrad.addColorStop(0.2, 'rgba(255, 0, 0)');
              linearGrad.addColorStop(0.5, 'rgba(0, 255, 0)');
              linearGrad.addColorStop(0.8, 'rgba(0, 0, 255)');
              linearGrad.addColorStop(1.0, 'transparent');
              ctx.fillStyle = linearGrad;
              ctx.fillRect(0, 0, 500, 300);
          }
          
          if (canvas1.getContext) {
              var ctx1 = canvas1.getContext('2d');
              
              ctx1.beginPath();
              ctx1.drawImage(canvas, 0, 0, 250, 150);
              ctx1.drawImage(canvas, 250, 0, 250, 150);
              ctx1.drawImage(canvas, 0, 170, 250, 150);
              ctx1.drawImage(canvas, 250, 170, 250, 150);
          }
  
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftk0vf5e6tj30si099q2x.jpg)

**切片**

+ 功能

  从源图片上裁剪一块区域下来，绘制到canvas中

+ 语法

  `drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)`

+ 参数

  image：获取的源图片

  (sx, sy)：在源图片上裁剪的起始点坐标

  sWidth, sHeight：在源图片上裁剪的图片的宽高

  (dx, dy)：将裁剪下的图片放在canvas中的起始点坐标

  dWidth, dHeight：将裁减下图片放在canvas中的宽高

+ 图解参数

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftk12gu2mxj308n08275i.jpg)

  第一个参数和其它的是相同的，都是一个图像或者另一个 canvas 的引用。其它8个参数最好是参照右边的图解，前4个是定义图像源的切片位置和大小，后4个则是定义切片的目标显示位置和大小 

+ 练习

  将图片中的文字部分 “往往” 裁剪下来，以canvas画布的大小绘制canvas中

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <img src="https://ws1.sinaimg.cn/large/006eYMu7ly1ftiw9x8975j30dw08cwnv.jpg" alt="">
      <script type="text/javascript">
          var canvas = document.getElementById('myCanvas'),
              oImg = document.getElementsByTagName('img')[0];
          if (canvas.getContext) {
              var ctx = canvas.getContext('2d');
                  oImg.onload = function () {
                      ctx.beginPath();
                      ctx.drawImage(oImg, 150, 0, 200, 100, 0, 0, 500, 300);
                  }
          }
      </script>
  </body>
  
  </html>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftk1jvefc2j30s908tarn.jpg)

  左侧是canvas，右侧是源图片

#### 处理图片

前面的步骤已经帮我们把图片放到了canvas画布中，接下来我们就可以按照自己的需求去处理图片，但处理这个说法好像说的有些抽象，什么叫处理图片？是针对图片裁裁剪剪么？我们一步一步来分析

我们都知道，canvas画布排列着一行行的像素点，我们看到的不同图形就是因为像素点的着色不同导致的，既然每个像素点的着色可以不同，那么他们身上一定记录着不同的信息，那有没有一个东西记录着这些不同像素点的信息呢？答案是肯定的

**ImageData对象**

+ 功能

  存储着canvas对象真实的像素数据 

+ 属性值

  `ImageData` 对象中存储着canvas对象真实的像素数据，它包含以下几个只读属性

  + width

    图片的宽度，单位是像素

  + height

    图片的高度，单位是像素

  + data

    `Unit8ClampedArray` 类型的一维数组，包含着RGBA格式的**整型**数据，范围是 [0, 255]

大概了解了 `ImageData` 对象以后我们肯定立马会有下一个问题，我们该怎么拿到这个对象呢？

**获取像素数据**

+ 目的

  获取画布指定矩形范围内的像素数据 

+ 方法

  `getImageData(x, y, width, height)`

+ 参数

  (x, y)：要获得的像素区域在画布上的起始点坐标

  width, height：要获得的像素区域的宽高

+ 注意

  使用这个方法要满足**同源策略**，或者服务器允许你进行跨域读取图片数据

+ 说明

  这个方法的返回值，就是我们想获得的保存着像素数据 `ImageData` 对象，它包含了我们获取的区域每个像素点的像素数据，我们可以通过改变这些数据，改变其像素值，像素值不一样了，他所对应的图片也就会产生相应的变化，这个过程就是处理图片的过程，也就是我们一开始抛出的问题

+ 处理像素数据

  比如现在我们想把一个黑色的矩形变成灰色的，我们可以把这个矩形的像素数据拿到，然后修改其像素数据，然后再放回到画布上，就实现了这一需求，但是还有一个问题就是，怎么把修改后的数据放回去呢？

**创建ImageData对象**

+ 目的

  除了用 `getImageData()` 方法获取一个 `imageData` 对象外，我们还可以自己创造一个 `imageData` 对象（这一点不常用，可以选择性跳过）

+ 方法

  `createImageData(width, height)`

  `createImageData(anotherData)`

+ 参数

  有两种方法可以实现这一功能，第一种是创建一个特定尺寸的 `imageData` 对象，所有像素被预设为透明黑；第二种方法可以创建一个被 `anotherData` 对象指定的相同像素的 `imageData` 对象，这个新的对象的像素全部被预设为透明黑，所以这种方法并**非是复制了图片数据**

**重写像素数据**

+ 目的

  将图像数据重写至Canvas画布中 

+ 方法

  `putImageData(ImageData, x, y)`

+ 参数

  ImageData：要放回画布中的像素数据对象

  (x, y)：ImageData对象左上角的坐标

#### 导出图片

图片处理完成后，我们可以将图片从canvas中导出，使用以下方法

**语法**

`HTMLCanvasElement.toDataURL(type, encoderOptions)`

**参数**

type：可选，图片格式，默认为 image/png，可能的值还有 image/jpeg，image/webp

encoderOptions：可选，在制定图片格式为 image/jpeg 或者 image/webp 的情况下，可以该值从0到1表示图片的质量，值越大质量越高，默认值是0.92，如果设置的值超过了范围，也会按默认值处理

**返回值**

返回一个包含被类型参数规定的图像表现格式的数据连接（url）

**注意**

需要格外注意的是，这个和之前的方法不同，不属于上下文格式对象，它是canvas对象的方法，我们调用的时候要是用canvas对象调用

**练习**

针对使用图片的四个步骤做一个完整的练习，将一张彩色图片处理成黑白图片，并导出为jpeg格式

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
    <script type="text/javascript">
        var oImg = new Image();

        oImg.src = './xiaohei.png';
        oImg.onload = function () {
            var canvas = document.getElementById('myCanvas'),
                canvasWidth = canvas.width,
                canvasHeight = canvas.height;

            var btn = document.getElementsByTagName('button')[0];
            btn.onclick = function () {
                sovle();
            }

            function sovle() {
                if (canvas.getContext) {
                    var ctx = canvas.getContext('2d');
                    var imageData,
                        imageDataLen;

                    ctx.drawImage(oImg, 0, 0, canvasWidth, canvasHeight);

                    imageData = ctx.getImageData(0, 0, canvasWidth, canvasHeight);
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
                    ctx.putImageData(imageData, 0, 0);
                    var url = canvas.toDataURL('image/jpeg', 0.5);
                    document.getElementsByTagName('img')[0].src = url;
                }
            }
        }
    </script>
</body>

</html>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftkns4r8nbg30sf0aotcl.gif)

左侧是canvas元素，右侧是导出的图片，可以看到导出的图片不是很清晰，是因为我设置的导出的品质是0.5， 提高这个值可以提高图片的品质

[更多处理实例看这里]('https://www.cnblogs.com/st-leslie/p/8317850.html?utm_source=debugrun&utm_medium=referral')

### 命中检测

+ isPointInStroke(x, y)

  检测坐标点(x, y)是否在**当前路径**上，返回值是true/false

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
      </style>
  </head>
  
  <body>
      <canvas id="myCanvas" width="500" height="300"></canvas>
      <script type="text/javascript">
              var canvas = document.getElementById('myCanvas');
  
              if (canvas.getContext) {
                  var ctx = canvas.getContext('2d');
                  var a, b;
                  
                  ctx.beginPath();
                  ctx.rect(100, 100, 200, 100);
                  a = ctx.isPointInStroke(100, 100);
                  ctx.stroke();
  
                  ctx.beginPath();
                  ctx.rect(350, 50, 100, 200);
                  b = ctx.isPointInStroke(100, 100);
                  ctx.stroke();
  
                  console.log(a + ' ' + b);
              }
      </script>
  </body>
  
  </html>
  ```

  可以看到，两次命中检测都是检查(100, 100)这个点是否在当前路径上，很明显第一次检测时在，第二次检测时开启了新的路径，所以不在

+ isPointInPath(x, y)

  检测坐标点(x, y)是否在当前路径区域内

+ 像素点

  还可以通过检测当前像素点的值，如果透明（RGBA中的A为0），则该点不在路径上

### 非零绕数准则

https://blog.csdn.net/itpinpai/article/details/50412260

### 解决canvas高分屏模糊的问题

在分辨率比较高的屏幕，例如 iPhone6/6s/max等机器上，因为canvas绘制的是位图，所以会导致模糊，解决方法是根据屏幕分辨率修改canvas样式代码（CSS）中宽和高的与canvas的width 和 height属性（html）的比例，要让两者在等比例的情况下，css中的宽高小于canvas属性中的宽高

## canvas性能优化

> + 离屏canvas
> + 避免浮点数坐标
> + 使用多层画布
> + 使用css设置大背景图
> + 使用 moz-opaque 属性
> + 将画布的函数调用集合到一起
> + 避免不必要的画布状态改变
> + 渲染画布中的不同点，而非整个新状态
> + 尽可能避免 `shadowBlur` 属性
> + 尽可能避免 text render
> + 使用不同的方法去清理画布(`clearRect()`、`fillRect()`、调整canvas大小)
> + 有动画使用 `window.requestAnimationFrame()` 而非 `window.setInterval()`
> + 谨慎使用大型物理库
>
> 可以使用 [JSPerf]('https://jsperf.com/')测试性能

+ 离屏canvas

  > 如果你发现你的在每一帧里有好多复杂的画图运算，请考虑创建一个离屏canvas，将图像在这个画布上画一次（或者每当图像改变的时候画一次），然后在每帧上画出视线以外的这个画布 

  对比文档碎片节点理解

+ 避免浮点数坐标

  当你画一个没有整数坐标点的对象时会发生子像素渲染（之前提到的半像素问题）,所以最好对浮点数坐标取整再渲染样式

+ 使用多层画布

  你可能会发现，你有些元素不断地改变或者移动，而其它的元素，例如外观，永远不变。这种情况的一种优化是去用多个画布元素去创建不同层次

+ 使用css设置大背景图

  如果像大多数游戏那样，你有一张静态的背景图，用一个静态的\<div>元素，结合background特性，以及将它置于画布元素之后。这么做可以避免在每一帧在画布上绘制大图

+ 使用CSS transform 属性缩放画布

  CSS transform 特性由于调用GPU，因此更快捷。最好的情况是，不要将小画布放大，而是去将大画布缩小

+ 使用 `moz-opaque` 属性（仅 Gecko）

  如果你的游戏使用画布而且不需要透明，请在画布上设置moz-opaque属性。这能够用于内部渲染优化 

  ```html
  <canvas id="mycanvas" moz-opaque></canvas>
  ```

## 参考

[MDN]('https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial')

[canvas图像处理总汇]('https://www.cnblogs.com/st-leslie/p/8317850.html?utm_source=debugrun&utm_medium=referral')

[canvas非零绕数规则]('https://blog.csdn.net/itpinpai/article/details/50412260')