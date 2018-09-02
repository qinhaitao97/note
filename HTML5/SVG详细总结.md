### 引入

#### SVG是什么

```
- SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
- SVG 用来定义用于网络的基于矢量的图形
- SVG 使用 XML 格式定义图形
- SVG 图像在放大或改变尺寸的情况下其图形质量不会有所损失
- SVG 是万维网联盟的标准
- SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体
```

#### SVG 和 canvas 的区别



| canvas                                   | svg                                              |
| ---------------------------------------- | ------------------------------------------------ |
| 依赖分辨率（位图）                       | 不依赖分辨率（矢量图）                           |
| 单个HTML元素                             | 每一个图形都是一个DOM元素                        |
| 只能通过脚本绘制图形                     | 可以通过css也可以通过脚本绘制图形                |
| 不支持事件处理程序                       | 支持事件处理程序                                 |
| 弱的文本渲染能力                         | 最适合带有大型渲染区域的应用程序（比如谷歌地图） |
| 图面较小，对象数量较大（>10k）时性能较佳 | 对象数量较小（<10k）、图片更大时性能较佳         |

svg 本质上是一种使用 XML 描述 2D 图形的语言。

 svg 创建的每一个元素都是一个独立的 DOM 元素，既然是独立的 DOM 元素，那么我们就可以通过 css 和 JavaScript 来操控 dom，可以对每一个 DOM 元素进行监听，并且因为每一个元素都是一个 DOM 元素，所以修改 svg 中的 DOM 元素，系统会自动进行 DOM 重绘。

 Canvas 通过 JavaScript 来绘制 2D 图形，Canvas 只是一个 HTML 元素，其中的图形不会单独创建 DOM 元素。因此我们不能通过 JavaScript 操控 Canvas 内单独的图形，不能对其中的具体图形进行监控。 在 Canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象

> 实际上 Canvas 是基于像素的即时模式图形系统，绘制完对象后不保存对象到内存中，当再次需要这个对象时，需要重新绘制；svg 是基于形状的保留模式图形系统，绘制完对象后会将其保存在内存中，当需要修改这个对象信息时，直接修改就可以了。这种根本的区别导致了很多应用场景的不同.

#### 应用场景

> https://zhuanlan.zhihu.com/p/33093211

### 使用方法

+ 创建 svg 根标签，并声明命名空间

  ```html
  <svg xmlns="http://www.w3.org/2000/svg"
       xmlns:xlink="http://www.w3.org/1999/xlink">
  </svg>
  ```

+ 设置svg元素的大小

  三种方法（属性设置，css设置，JS设置效果相同），默认大小是300 * 150

  ```html
  <!-- 属性设置 -->
  <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
  
  </svg>
  ```

  ```html
  <!-- css设置 -->
  <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="width: 500px;height: 300px">
  
  </svg>
  ```

  ```html
  <!-- JS设置 -->
  <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  
  </svg>
  <script>
      document.getElementsByTagName('svg')[0].style.width = '500px';
      document.getElementsByTagName('svg')[0].style.height = '300px';
  </script>
  ```

+ 在 `<svg>` 标签下，添加图形元素

  svg中的图形使用标签定义的，根据需要将合适的标签填入 `<svg>`标签下，svg中的图形元素有很多，这里只简单的举个例子

  ```html
  <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
      <rect x="100" y="100" width="200" height="100"></rect>
  </svg>
  ```

### 绘制图形

#### 总览

再开始绘制图形之前，我们先来了解一下有哪些基本图形，以及他们是怎么定义的，属性该怎样设置，为后续的介绍做铺垫

##### 基本图形

```
   - rect		矩形
   - circle		圆形
   - ellipse	椭圆形
   - line		直线
   - polyline	折线
   - polygon	多边形
```

##### html属性(或css属性)(常用)

```
   - stroke			   边框颜色
   - stroke-width	    边框宽度
   - stroke-opacity		边框透明度
   - stroke-dasharray	虚线边框
   - stroke-dashoffset	缩进
   - stroke-linecap		线段两边样式
   - stroke-linejoin	线段连接处的样式
   - fill			    填充颜色
   - fill-opacity		填充透明度
   - transform			变形
   - filter				滤镜
```

##### 图形定义的方法

```html
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
    <rect x="100" y="100" width="200" height="100"></rect>
</svg>
```

在 `<svg>`根标签下定义图形元素，并设置该图形对应的必须的属性值（如这里的x、y、width、height，不同图形对应不同的属性，后面详细给出）

##### html属性（或css属性）设置方法

这里讲的属性不同于图形定义中提到的属性，这里要设置的是图形的样式属性（如颜色，宽度等），他可能不是必须的，有两种设置方法

+ 在html属性中设置

  ```html
  <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
      <rect x="100" y="100" width="200" height="100" fill="orange"></rect>
  </svg>
  ```

+ 在css样式中设置

  ```html
  <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
      <rect x="100" y="100" width="200" height="100" style="fill: orange"></rect>
  </svg>
  ```

  这为了设置方便，使用了行间css

#### 基本图形用法

为了方便起见，下面的讲解不再列出根标签 `<svg>`，但是要知道这时必须的

##### 矩形

基本用法

```html
<rect x="100" y="100" width="200" height="100"></rect>
<!-- (x, y)：矩形左上角顶点坐标	width：矩形宽度	height：矩形高度 -->
```

设置样式

```html
<rect x="100" y="100" width="200" height="100" 
    stroke="red" stroke-width="5px" stroke-opacity="0.5" fill="green" fill-opacity="0.5"></rect>
```

```html
<rect x="100" y="100" width="200" height="100"
    style="stroke: red;stroke-width: 5px;stroke-opacity: 0.5;fill: green;fill-opacity: 0.5"></rect>
```

##### 直线

基本用法

```html
<line x1="100" y1="100" x2="200" y2="200"></line>
<!-- (x1, y1)：直线起点坐标    (x2, y2)：直线终点坐标 -->
```

设置样式

```html
<line x1="100" y1="100" x2="200" y2="200"
    stroke="red" stroke-width="5px" stroke-opacity="0.5"></line>
<!-- 直线要在描边（stroke）以后才会显示出来 -->
```

```html
<line x1="100" y1="100" x2="200" y2="200"
    style="stroke: red; stroke-width: 5px;stroke-opacity: 0.5;"></line>
```

##### 圆形

基本用法

```html
<circle cx="250" cy="150" r="100"></circle>
<!-- (cx, cy)：圆形的坐标    r：半径 -->
```

设置样式

```html
<circle cx="250" cy="150" r="100"
    stroke="red" stroke-width="5px" stroke-opacity="0.5" fill="green" fill-opacity="0.5"></circle>
```

```html
<circle cx="250" cy="150" r="100"
    style="stroke: red;stroke-width: 5px;stroke-opacity: 0.5;fill: green;fill-opacity: 0.5"></circle>
```

##### 椭圆

基本用法

```html
<ellipse cx="250" cy="150" rx="100" ry="50"></ellipse>
<!-- (cx, cy)：圆心坐标    rx：x轴上的半径    ry：y轴上上的半径 -->
```

设置样式

```html
<ellipse cx="250" cy="150" rx="100" ry="50"
    stroke="red" stroke-width="5px" stroke-opacity="0.5" fill="green" fill-opacity="0.5"></ellipse>
```

```html
<ellipse cx="250" cy="150" rx="100" ry="50"
    style="stroke: red;stroke-width: 5px;stroke-opacity: 0.5;fill: green;fill-opacity: 0.5;"></ellipse>
```

##### 折线

基本用法

```html
<polyline points="50 50, 80 50, 80 80, 110 80, 110 110, 140 110, 140 140"></polyline>
<!-- points：折线上点的坐标 -->
<!-- 逗号不是必须的，但是建议写，这样便于区分不同的点 -->
```

设置样式

```html
<polyline points="50 50, 80 50, 80 80, 110 80, 110 110, 140 110, 140 140"
    stroke="red" stroke-width="5px" stroke-opacity="0.5" fill="transparent"></polyline>
<!-- 因为图形默认是填充为黑色，所以这里把填充颜色设置成透明色，以便看到折线的效果 -->
<!-- 也可以将fill设置为none -->
```

```html
<polyline points="50 50, 80 50, 80 80, 110 80, 110 110, 140 110, 140 140"
    style="stroke: red;stroke-width: 5px;stroke-opacity: 0.5;fill: none;"></polyline>
```

##### 多边形

基本用法

```html
<polygon points="50 50, 80 50, 80 80, 110 80, 110 110, 140 110, 140 140"></polygon>
<!-- points：多边形的顶点 -->
```

设置样式

```html
<polygon points="50 50, 80 50, 80 80, 110 80, 110 110, 140 110, 140 140"
    stroke="red" stroke-width="2px" fill="green" fill-opacity="0.5"></polygon>
```

```html
<polygon points="50 50, 80 50, 80 80, 110 80, 110 110, 140 110, 140 140"
    style="stroke:red; stroke-width: 2px;fill: green;"></polygon>
```

#### path

##### 简介

路径也是用来绘制图形的，与基本图形相比，path具有更加强大的能力，使用一系列命令来实现画图操作

##### 基本语法

```html
<path d="" />
```

引号中的部分填写命令

##### 命令



| 命令 | 参数                                                  | 功能                   |
| ---- | ----------------------------------------------------- | ---------------------- |
| M    | (x, y)                                                | 移动到                 |
| L    | (x, y)                                                | 画直线到               |
| H    | x                                                     | 画水平线到             |
| V    | y                                                     | 画竖直线到             |
| Z    | 无                                                    | 关闭路径               |
| Q    | (x1, y1, x, y)                                        | 画二次贝塞尔曲线到     |
| T    | (x, y)                                                | 画光滑二次贝塞尔曲线到 |
| C    | (x1, y1, x2, y2, x, y)                                | 画三次贝塞尔曲线到     |
| S    | (x2, y2, x, y)                                        | 画光滑三次贝塞尔曲线到 |
| A    | (rx ry x-axis-rotation large-arc-flag sweep-flag x y) | 圆弧                   |

**备注**：指令是**区分大小写的**，大写命令表示绝对位置，小写命令表示相对位置，Z指令不区分大小写

```
M 100 100 L 200 100
// M：起始点移动到(100, 100)
// L：画直线到(100, 100)

m 100 100 l 200 100
// m：起始点相对上一个点，向x轴正方向移动了100，向y轴正方向移动了100，如果没有上一个点，则默认为(0, 0)
// l：相对于上一个点，向x轴正方向增加了100，y轴正方向增加了100的点画直线
```

```html
<path d="M 100 100 L 200 100 z" stroke="#000" />
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftlx1djhhbj30eb08q0sh.jpg)

```html
<path d="m 100 100 l 200 100 z" stroke="#000" />
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftlx2nvlysj30e808v3y9.jpg)

##### 示例

**二次贝塞尔曲线**

```html
<path d="M 50 100 Q 125 300 200 100" stroke="#000" fill="none" />
<!-- 
    Q x1 y1 x y
    (x1, y1)：控制点坐标
    (x, y)：终止点坐标
-->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftlxeqzdpgj30e808n3ya.jpg)

**光滑二次贝塞尔曲线**

```html
<path d="M 50 100 Q 125 300 200 100 T 375 100" stroke="#000" fill="none" />
<!--
    T：x y
	(x, y): 新结束点坐标
    整个过程是：Q 命令控制点(x1, y1) 以 Q 命令结束点 (x, y) 为对称点
               做对称点 (x', y')，以 Q 命令结束点 (x, y) 为起始点，
               对称点 (x', y') 为控制点，T 命令结束点 (x, y) 为结束点
               三点再做一条二次贝塞尔曲线，以此绘成整条光滑二次贝塞尔曲线
-->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftlxhcrq46j30ed08s3yc.jpg)

**三次贝塞尔曲线**

```html
<path d="M 50 100 C 100 200 150 100 200 200" stroke="#000" fill="none" />
<!--
    C x1 y1 x2 y2 x y
    (x1, y1): 控制点1
    (x2, y2): 控制点2
    (x, y): 结束点
-->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftly3fxuf4j30eg08wdfm.jpg)

```html
<path d="M 50 100 C 100 200 150 100 200 200 S 250 100 300 200" stroke="#000" fill="none" />
<!--
    S x2 y2 x y
    (x2, y2): 新控制点2
    (x, y): 新结束点
    整个过程是：Q 命令控制点 (x2, y2) 以 Q 命令结束点 (x, y) 为对称点做对称点 (x', y'),
               以 Q 命令结束点 (x,y) 为起始点，对称点 (x', y') 为控制点1，T 命令控制点
               (x2, y2) 为控制点2，T 命令结束点 (x, y) 为结束点，四点再做一条三次贝塞尔
               曲线，以此绘成整条光滑三次贝塞尔曲线
-->
```

**圆弧**

```html
<path d="M 100 100 A 70 120 90 1 1 150 200" stroke="#000" fill="none" />
<!--
    A rx ry x-deg large-arc sweep-flag x y
    rx: x轴上半径
    ry：y轴上半径
    x-deg：x轴旋转角度
    large-arc：圆弧的角度大于还是小于180度(0表示小于，1表示大于)
    sweep-flag：表示弧线方向(0沿逆时针，1沿顺时针)
    (x, y): 终点坐标
-->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm42dlkdjj30ee08q744.jpg)

> 因为(椭)圆弧参数较多，所以这里再附一张图讲解一下参数

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm45mqi7fj30ga0bi74t.jpg)

图中共有四条弧线，分别标号为1、2、3、4，设A为起始点，B为终止点，且x轴方向没有旋转，则

弧线1：顺时针(sweep-flag=1)大弧(large-arc=1)

弧线2：顺时针(sweep-flag=1)小弧(large-arc=0)

弧线3：逆时针(sweep-flag=0)小弧(large-arc=0)

弧线4：逆时针(sweep-flag=0)大弧(large-arc=1)

其他属性如半径、终点坐标等很好理解

### 文本

#### 基本用法

```html
<text x="250" y="150">Hello World!</text>
<!--
	x: 文本最左侧在坐标系中的坐标
	y: 文本的baseline在坐标系中的坐标
-->
```

#### 对齐

text-anchor

```html
<path d="M 200 10 200 200" style="stroke: gray; fill: none;" />
<text x="200" y="30" style="text-anchor: start">Start</text>
<text x="200" y="90" style="text-anchor: middle">Middle</text>
<text x="200" y="150" style="text-anchor: end">End</text>
<!-- text-anchor 属性可以设置文本竖直轴线的位置 -->
```

#### tspan

```html
<text x="200" y="150" text-anchor="middle">
    Hello
    <tspan fill="none" stroke="deeppink" font-size="20px">World!</tspan>
</text>
<!-- <tspan></span>用来包裹文本中样式不同的部分 -->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm6lm0padj30ea08o742.jpg)

#### dx、dy

dx、dy可以设置文本中每一个字符相对于自身在x轴方向和在y轴方向上的偏移量，默认是0

```html
<text x="200" y="150" text-anchor="middle">
    Hello
    <tspan fill="none" stroke="deeppink" font-size="20px" dx="10" dy="-5">World!</tspan>
</text>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm6no52rhj30e808u742.jpg)

上面的代码给 "World1" 文本的第一个字符设置了x轴和y轴方向上的偏移量，现在以dy为例讨论下面的问题，即代码中 `dy="-5"` 说明只给 "World!" 文本的第一个字符 'W' 设置了偏移量，其他的字符没有设置偏移量默认是0，那么怎么 "World!" 中所有的字符都跟着一起偏移了呢，原因是文本中的字符默认会与前一个字符保持对齐，所以只设置了第一个字符的偏移量，那么后面的字符会默认与前一个元素保持对齐，想要达到不同偏移量的效果，要给每个字符都设置偏移量

```html
<text x="200" y="150" text-anchor="middle">
    <tspan fill="deeppink" font-size="20px" dx="10" dy="-5">Hello</tspan>
    <tspan fill="none" stroke="deepskyblue" font-size="30px" dx="1 2 3 4 5" dy="5 4 3 2 1">World</tspan>
</text>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm6xjtcoxj30ec08qmwy.jpg)

#### rotate

```html
<text x="200" y="150" text-anchor="middle">
    Hello
    <tspan fill="none" stroke="deepskyblue" font-size="30px" dx="5 10 15 20 40" dy="0" rotate="30 45 60 90 180">World</tspan>
</text>
<!--
    rotate可控制文本中字符的旋转
    当rotate只有一个参数时，文本每一个字符均以自身中心点为旋转中心，旋转指定的角度，正值顺时针
    当rotate参数个数与文本中字符对应时，每个字符的旋转角度由相应的参数决定
-->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm77n9fjwj30ei08rdfn.jpg)

#### 角标

```html
<text x="200" y="150" text-anchor="middle" font-size="20px">
    Hello
    <tspan font-size="10px" baseline-shift="sub">[1]</tspan>
    World
    <tspan font-size="10px" baseline-shift="super">[2]</tspan>
</text>
<!-- 也可以直接使用baseline-shift属性设置上下角标 -->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm7rmwz6jj30e808sq2p.jpg)

```html
<text x="200" y="150" text-anchor="middle" font-size="20px">
    Hello
    <tspan font-size="10px" dx="-3" dy="8">[2]</tspan>
    World
</text>
<!-- 利用dx、dy属性来调整文字的位置，以达到角标的效果 -->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm7qmrqe2j30e908pq2p.jpg)

> 最好使用第一种方法，因为如果使用dx、dy，将某一段文本移动后，因为后面的文字会与它对齐，如上图中的World与[2]对齐，导致后面的文本偏离原来的位置

#### 文本长度及字符间隔

默认情况下无法获得 `<text>` 文本长度，但是我们可以通过 `textLength` 属性设置文本的长度，文本会根据 `textLength` 的值自适应变化，变化的规则可用通过 `lengthAdjust` 属性来设置

`lengthAdjust` 有两个可选的值：

+ spacing
+ spacingAndGlyphs

spacing只调整字符之间的间隔，spacingAndGlyphs则会根据一定的比例同时调整间距和字符的大小

```html
<path d="M 100 50 L 100 140 M 350 50 L 350 140" stroke="#000"></path>
<text x="100" y="80" font-size="20px" textLength="250" lengthAdjust="spacing">Hello world</text>
<text x="100" y="130" font-size="20px" textLength="250" lengthAdjust="spacingAndGlyphs">Hello world</text>

<text x="110" y ="180" font-size="20px">
    Hello world
    <tspan font-size="16px">(normal)</tspan>
</text>

<path d="M 180 200 L 180 290 M 270 200 L 270 290" stroke="#000"></path>
<text x="180" y="230" font-size="20px" textLength="90" lengthAdjust="spacing">Hello world</text>
<text x="180" y="280" font-size="20px" textLength="90" lengthAdjust="spacingAndGlyphs">Hello world</text>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm8vm67mbj30e708njr8.jpg)

#### 垂直文本

方法一: `writing-mode` + `rotate` + `letter-spacing`

方法二: `transform="rotate()"` + `rotate` + `letter-spacing`

```html
<text x="200" y="100" writing-mode="tb" letter-spacing="5" rotate="-90">hello world</text>
<text x="220" y="100" transform="rotate(90, 220, 100)" letter-spacing="5" rotate="-90">hello world</text>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm9gy6641j30ea08p742.jpg)

垂直文本有些字符不在竖直轴线上（如上图的 "l"），可以利用dx，dy进行微调

```html
<text x="200" y="100" writing-mode="tb" letter-spacing="7" rotate="-90" dx="0 0 2 0 -2 0 0 0 2 0 -2" dy="0">hello world</text>
<text x="220" y="100" transform="rotate(90, 220, 100)" letter-spacing="7" rotate="-90">hello world</text>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftm9uknrypj30e908p742.jpg)

#### textPath

内嵌于 `<text>` 中的 `<textPath>` 元素，通过 `xlink:href` 属性指向一个 `<path>` 元素，可以将文本的baseline设置成指定的path，即文本沿path排列

```html
<path id="arc" d="M 100 100 A 100 100 0 1 0 400 100" stroke="#000" fill="none" />
<text font-size="20">
    <textPath xlink:href="#arc">
        I Love SVG!
    </textPath>
</text>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftmb2i3yxtj30e608nwed.jpg)

> `<text>` 元素的坐标轴改变

text原本是相对于坐标轴定位的，其属性值x,y设置text元素再坐标系中的位置，当时用textPath后，text的坐标系不再是它原理的坐标系，而变成了path路径，即path路径作为text元素的x轴，y轴是不固定的，它满足的条件是与x轴上每一个点的切线垂直

```html
<path id="arc" d="M 100 100 A 100 100 0 1 0 400 100" stroke="#000" fill="none" />
<text x="100" y="10" font-size="20">
    <textPath xlink:href="#arc">
        I Love SVG!
    </textPath>
</text>
<!--
    此时text元素的坐标原点应该在path路径的起点，这里设置了x和y的值
    x应该是沿path路径偏移path起点的距离，y应该是沿垂直于path路径，
    偏离path路径的距离，但是这里x的值符合预期，y的值却不生效，没有
    搞懂是为什么?
-->
```

> 超出path路径长度的文本将被隐藏

```html
<path id="arc" d="M 100 100 A 100 100 0 1 0 400 100" stroke="#000" fill="none" />
<text font-size="35" fill="none" stroke="deepskyblue">
    <textPath xlink:href="#arc" >
        ABCSEFGHIJKLMNOPQRSTUVWXYZ
    </textPath>
</text>
<!-- U以后的字母超出路径长度，被隐藏 -->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftmbo4n1hnj30eg08omx7.jpg)

> `<textPath>`  的 `startOffset` 属性

`startOffset` 属性可以调整 `<text>` 元素再path路径上的位置，它表示 `<text>` 元素再path路径上偏离path起点的距离，可以是具体的数字或者百分比，配合 `text-anchor` 属性可以实现  `<text>` 元素再path路径上的居中显示

```html
<path id="arc" d="M 100 100 A 100 100 0 1 0 400 100" stroke="#000" fill="none" />
<text font-size="20" fill="none" stroke="deepskyblue" text-anchor="middle">
    <textPath xlink:href="#arc" startOffset="50%">
        ABCSEFGHIJKLMNOPQRSTUVWXYZ
    </textPath>
</text>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftmbuk12otj30e608q749.jpg)

#### 空白符

svg没有换行符！svg默认会把所有单个或连续多个空格、tabs、换行符转成单个空格。即使在css中将white-space设置为pre，换行符依然会被转换成空格！ 

### 渐变

#### 线性渐变

**使用预览**

```html
<!-- 在defs中定义渐变 -->
<defs>
    <!-- 从左到右-->
    <linearGradient id="linearGra" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="red" />
        <stop offset="50%" stop-color="green" />
        <stop offset="100%" stop-color="blue" stop-opacity="0.5" />
    </linearGradient>
</defs>

<!-- 应用渐变样式 -->
<rect x="100" y="50" width="200" height="50" fill="url(#linearGra)" />
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftogdg8rhuj30e808ugle.jpg)

**stop 元素的属性**

`offset`

	表示渐变矢量的位置，可以是0~1之间的值，也可以是0%~100%之间的值

`stop-color`

	定义颜色在offset节点的位置

`stop-opacity`

	定义颜色的透明度

**linearGradient的属性**

+ (x1, y1)、(x2, y2)

  定义渐变的起始位置、终止位置，决定了渐变的方向

+ `xlink:href`

  再一个渐变中引用另一个渐变，被引用的渐变是可继承的，也可以进行修改

  ```html
  <defs>
      <linearGradient id="linearGra1" x1="0%" y1="0%" x2="100%" y2="0%">
          <stop offset="0%" stop-color="red" />
          <stop offset="50%" stop-color="green" />
          <stop offset="100%" stop-color="blue" stop-opacity="0.5" />
      </linearGradient>
  
      <linearGradient id="linearGra2" x1="0%" y1="0%" x2="0%" y2="100%"
          xlink:href="#linearGra1"></linearGradient>
  </defs>
  
  <!-- 应用渐变样式 -->
  <rect x="100" y="50" width="200" height="50" fill="url(#linearGra1)" />
  
  <!-- 应用渐变样式 -->
  <rect x="100" y="150" width="200" height="100" fill="url(#linearGra2)" />
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftog636s4zj30eb08qa9v.jpg)

+ gradientUnits 

  > gradientUnits（渐变单元）的属性，它描述了用来描述渐变的大小和方向的单元系统。该属性有两个值：`userSpaceOnUse` 、`objectBoundingBox`。默认值为`objectBoundingBox`，我们目前看到的效果都是在这种系统下的，它大体上定义了对象的渐变大小范围，所以你只要指定从0到1的坐标值，渐变就会自动的缩放到对象相同大小。`userSpaceOnUse`使用绝对单元，所以你必须知道对象的位置，并将渐变放在同样地位置上 

  ```html
  <!-- 在defs中定义渐变 -->
  <defs>
      <!-- 从左到右，绝对位置坐标-->
      <linearGradient id="linearGra" x1="100" y1="0" x2="300" y2="0" gradientUnits="userSpaceOnUse">
          <stop offset="0%" stop-color="red" />
          <stop offset="50%" stop-color="green" />
          <stop offset="100%" stop-color="blue" stop-opacity="0.5" />
      </linearGradient>
  </defs>
  
  <!-- 应用渐变样式 -->
  <rect x="100" y="50" width="200" height="50" fill="url(#linearGra)" />
  ```

  明显 `objectBoundingBox` 属性要更方便，只需要定义相对值

+ gradientTransform

  给渐变添加变化效果

  ```html
  <defs>
      <linearGradient id="linearGra1" x1="0%" y1="0%" x2="100%" y2="0%">
          <stop offset="0%" stop-color="red" />
          <stop offset="50%" stop-color="green" />
          <stop offset="100%" stop-color="blue" stop-opacity="0.5" />
      </linearGradient>
  
      <linearGradient id="linearGra2" x1="0%" y1="0%" x2="100%" y2="0%"
          xlink:href="#linearGra1" gradientTransform="rotate(45)"></linearGradient>
          <!-- 旋转角最好在0~90度之间 -->
  
  </defs>
  
  <!-- 应用渐变样式 -->
  <rect x="100" y="50" width="200" height="50" fill="url(#linearGra1)" />
  
  <!-- 应用渐变样式 -->
  <rect x="100" y="150" width="200" height="100" fill="url(#linearGra2)" />
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftogrgg9a5j30e608pq2s.jpg)

+ spreadMethod

  `spreadMethod="pad(默认) | reflect | repeat"`

  ```
  - pad:使用渐变的颜色结点来填充剩余的空间。例如，如果第一个结点是20%，那么0%到20%这部分就是相同的颜色
  - reflect:映射渐变图案，从'start-to-end'，再从'end-to-start'，然后'start-to-end'，直到空间都填满
  - repeat:重复渐变图案，从起点->终点，直到空间填满
  - 后两个属性的兼容性很不好，不建议使用
  ```

  ```html
  <defs>
      <!-- 默认情况下就是 pad 的效果，"reflect" 和 "repeat" 的兼容性都很不好，不建议使用 -->
      <linearGradient id="linearGra" x1="0%" y1="0%" x2="100%" y2="0%" spreadMethod="pad">
          <stop offset="20%" stop-color="red" />
          <stop offset="50%" stop-color="green" />
          <stop offset="70%" stop-color="blue" stop-opacity="0.5" />
      </linearGradient>
  </defs>
  
  <rect x="100" y="100" width="200" height="50" fill="url(#linearGra)" />
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftoh52usyhj30e808vt8h.jpg)



#### 径向渐变(未完善)

**使用预览**

```html

```

### 滤镜

**高斯滤镜**

```html
<defs>
    <!-- 高斯滤镜 -->
    <filter id="Gaussian_Blur">
        <feGaussianBlur in="SourceGraphic" stdDeviation="20" />
    </filter>
</defs>

<rect x="100" y="100" width="200" height="100" fill="red" filter="url(#Gaussian_Blur)"></rect>
```

**其他滤镜**

> 使用时将 `<filter>` 标签下的 `<feGaussianBlur>`标签替换成相应的标签即可

```html
- feBlend
- feColorMatrix
- feComponentTransfer
- feComposite
- feConvolveMatrix
- feDiffuseLighting
- feDisplacementMap
- feFlood
- feGaussianBlur
- feImage
- feMerge
- feMorphology
- feOffset
- feSpecularLighting
- feTile
- feTurbulence
- feDistantLight
- fePointLight
- feSpotLight
```

### transform

transform用于svg图形的形变，与css3中的transform属性有所相同

**强调，所有的变形操作都是基于元素所在的坐标系进行变化的**

#### translate

+ 功能

  改变变形元素所在坐标系原点的位置

+ 语法

  `transform="transform(x, y)"`

+ 参数

  x: 元素所在坐标系在x轴方向上的偏移量

  y: 元素所在坐标系在y轴方向上的偏移量

+ 图解

  ```html
  <rect x="0" y="0" width="50" height="50"  transform="translate(100, 100)"></rect>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftmesf6q9lj30m00ezdfp.jpg)

  如图，一个宽高50的矩形所在的坐标系，被向右、向下平移了100px，即由A点平移到了B点，坐标系的原点移动了位置，但它还是坐标原点，坐标系中元素的坐标不变；因为坐标系被平移了，所以坐标系中的元素也跟着一起平移了

#### rotate

+ 功能

  改变变形元素所在坐标系坐标轴的方向

+ 语法

  `transform="rotate(angle [, x, y])"`

+ 参数

  angle： 元素所在的坐标系旋转的角度（正值顺时针）

  (x, y)：元素所在的坐标系的旋转中心点（此值可以省略，默认为(0, 0)）

+ 图解

  ```html
  <rect x="200" y="0" width="50" height="50"  transform="rotate(45)"></rect>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftmfimvz7sj30nw0jg74b.jpg)


只设置了旋转的角度，则旋转的中心点默认是(0, 0)点，上图表示黑色元素所在的坐标系以(0, 0)为旋转中心，旋转了45度，我们改变旋转中心再转一次

```html
<rect x="200" y="0" width="50" height="50"  transform="rotate(45, 225, 25)"></rect>
<!-- 旋转中心在矩形元素的中心点 -->
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftnabisr1aj30ld0h5wej.jpg)

可以看到，发生旋转的依然是矩形区域所在的坐标系，但是因为旋转中心是矩形的中心点，所以也相当于矩形区域自身进行了旋转，所以如果我们的需求是元素相对于自身发生旋转时，可以使用这种方法

#### scale

+ 功能

  改变变形元素所在的坐标系的单位长度

+ 语法

  `transform="scale(x-value, y-value)"`

+ 参数

  x-value：x轴方向上的缩放因子

  y-value：y轴方向上的缩放因子

+ 单位长度

  默认一个单位代表一个像素，如果我们改变缩放因子，使一个单位表示像素多余或者少于一个，就起到了放大或者是缩小的效果

+ 图解

  ```html
  <path d="M 100 150 L 200 150" stroke="#000" fill="none" transform="scale(2, 1)"></path>
  <!-- x轴缩放因子扩大两倍，y轴缩放因子不变 -->
  ```

  

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftnb44johqj30gw0a1q2q.jpg)

  在这个例子中，我们将x轴方向上的缩放因子设置为2，也就是说x轴由原来的一个单位一个像素在缩放后一个单位两个像素，所以缩放前由x=100到x=200的直线（红色部分），缩放后变成了图中绿色部分（坐标不变，视觉上变成了两倍）

#### skew

+ 功能

  改变变形元素所在的坐标系坐标网格在x轴方向或在y轴方向的倾斜程度

+ 语法

   `transform: skewX(angle) skewY(angle)`

+ 参数

  angle表示倾斜的角度

+ 说明

  `skewX(angle)` 表示变形元素所在坐标系坐标网格沿x轴方向倾斜，角度为angle(正值向x轴正方向倾斜)

  `skewY(angle)` 表示变形元素所在坐标系坐标网格沿y轴方向倾斜，角度为angle(正值向y轴正方向倾斜)

+ 图解

  ```html
  <path d="M 100 100 L 300 100 M 100 100 L 100 200 z" stroke="red"></path>
  <path d="M 100 100 L 300 100 M 100 100 L 100 200 z" stroke="green" transform="skewX(45)"></path>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fto6t6qj34j30ef090dfl.jpg)

  红色是没有倾斜前的图形，绿色是经过倾斜变心之后的图形，我们来看看在这个过程中坐标网格发生了什么变化

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fto6uudme7j30kf0bxmx4.jpg)

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fto6vfygl5j30pp0dfmxa.jpg)

  以上两图分别表示倾斜前后的坐标系，可以看到，在设置 `skewX(45)` 之后，整个坐标网格向x轴正方向倾斜了45度，每一个单独的坐标网格由原来的正矩形变成了菱形，其他元素均保持不变，我们将图形的坐标分别填入两个坐标系中并连线，得到两个形状不同的折线，这也就是上述图形变化中红色图形到绿色图形的变化过程


#### 居中变化处理(未完善)

在上述所有的变形操作中，都是以变形元素的坐标系为单位进行整体变化的，这同时也强调了另一件事情，**变形操作的中心点是坐标原点**，但是有时我们不想以原点为中心点对图形进行变形操作，而是以图形自身的中心点为变形操作的中心点进行变化，那该怎么实现呢？（旋转操作比较特殊，他可以自己设置旋转的中心点，所以这里的方法主要针对其他几种变形操作）

+ "平移 -> 变形 -> 平移" 三部曲

  ```html
  transform="translate(centerX，centerY) doTransform translate(-centerX, -centerY)";
  ```

  ```
  - (centerX, centerY)： 变形元素自身中心点的坐标
  
  - doTransform：		  变形操作
  
  - (-centerX, centerY)： 变形元素自身中心点的坐标的负值
  ```

  以缩放变形为例

  ```html
  <rect x="200" y="100" width="100" height="100" transform="translate(250, 150) scale(2, 1) translate(-250, -150)"></rect>
  <!-- 这里矩形元素自身的中心点为(250, 150) -->
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fto7qhekbhg30h0093743.gif)

+ 公式计算

  这种计算方式仅针对缩放操作

  ```html
  transform="translate(-centerX * (fX - 1)， -centerY * (fY - 1)) scale(fX, fY)";
  ```

  ```
  - (centerX, centerY)：变形元素自身的中心点坐标
  - fX：x轴方向的缩放因子
  - fY：y轴方向的缩放因子
  ```

  ```html
  
  ```

+ "调整位置 -> 平移 -> 变形"

  ```html
  x="-width * 1 / 2" y="-height * 1 / 2" transform="translate(centerX, centerY) doTransform";
  ```

  ```
  - 调整位置：				在定义变形元素位置的时候，将变形元素的中心点放在原点
  - -width * 1 / 2：		变形元素自身宽度一半的负值
  - -height * 1 / 2：		变形元素自身高度一半的负值
  - (centerX, centerY)：	变形元素自身的中心点的坐标
  - doTransform：		    变形操作
  ```

  以倾斜举例

  ```html
  <rect x="-50" y="-50" width="100" height="100" transform="translate(250, 150) skewX(45)"></rect>
  ```

  ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fto88u78a2j30ea08sa9t.jpg)

+ viewBox

#### svg transform 与 css transform

两者在基本功能上是相似的，但有一些细节之处不相同，这里列举一些

+ 单位

  在css中绝大多数属性的长度单位默认都是px，而在svg中不写单位，因为一个单位对应的长度不固定

+ 语法

  两者语法基本相同，但是有不同之处

+ 中心点

  css中使用 transform 变化图形，其中心点默认就在图形的中心点；而svg中图形变化的中心点默认是坐标原点

### 辅助标签

#### g

> `<g>` 元素通常用来对相关图形元素进行分组，以便统一操作，比如旋转，缩放或者添加相关样式等 

看一组同心圆的实例

```html
<circle cx="250" cy="150" r="30" fill="none" stroke="#000"></circle>
<circle cx="250" cy="150" r="50" fill="none" stroke="#000"></circle>
<circle cx="250" cy="150" r="70" fill="none" stroke="#000"></circle>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftojtdovj4j30el08s0sn.jpg)

可以看到，设置中很多属性都是重复的，每一个圆都要写的话会写很多重复代码，而且如果要对圆进行修改的话，还有去修改每一个圆的属性值，下面使用 `<g>` 标签来定义这组同心圆，效果是一样的，但省了很多代码

```html
<!-- 不设置圆心坐标，默认在(0, 0), 使用平移操作将一组元素全部平移到相应的坐标，并给他们设置样式 -->
<g transform="translate(250, 150)" fill="none" stroke="#000">
    <circle r="30"></circle>
    <circle r="50"></circle>
    <circle r="70"></circle>
</g>
```

#### defs

> 定义以要重复使用的元素，可以增加SVG内容的易读性和可访问性；需要注意的是在 `<defs>` 标签中定义的元素，其内容不会直接显示，需要其他元素引用它进行实例化才能显示

`<defs>` 中定义的内容不会直接显示，需要其他元素引用它才会显示，这样大大增加了开发的灵活性，我们可以在`<defs>` 中指定义基本的框架而不定义样式，在其他元素引用它时再给他设置需要的样式，这样代码语义性好，可读性强，应用更加灵活

```html
<defs>
    <linearGradient id="linearGra" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="yellowgreen" />
        <stop offset="50%" stop-color="deeppink" />
        <stop offset="100%" stop-color="deepskyblue" />
    </linearGradient>

    <radialGradient id="radialGra" fx="50%" fy="50%" cx="50%" cy="50%" r="50%">
        <stop offset="0%" stop-color="yellowgreen" />
        <stop offset="50%" stop-color="deeppink" />
        <stop offset="100%" stop-color="deepskyblue" />
    </radialGradient>
</defs>

<!-- 上面<defs>中定义的渐变属于一种样式，需要具体的元素应用它以达到实例化的效果 -->
<rect x="100" y="50" width="300" height="50" fill="url(#linearGra)" />
<circle cx="250" cy="200" r="50" fill="url(#radialGra)" />
```

```html
<defs>
    <rect id="rectDefs" x="100" y="100" width="200" height="100" />
</defs>

<!-- 上面<defs>中定义的<rect>属于具体的元素，需要使用<use>进行实例化，实例化时可以设置不同的样式 -->
<use fill="purple" fill-opacity="0.5" stroke="deepskyblue" stroke-width="5" xlink:href="#rectDefs" />
```

#### use

> `<use>` 元素在SVG文档内取得目标节点，并在别的地方复制它们。它的效果等同于这些节点被深克隆到一个不可见的DOM中，然后将其粘贴到 `<use>`元素的位置 

需要注意的是：

+ 因为克隆的节点是不可见的，所以当使用CSS样式化一个 `<use>` 元素以及它的隐藏的后代元素的时候，隐藏的、克隆的DOM不能保证继承CSS属性，除非明文设置使用CSS继承 
+ 出于安全原因，一些浏览器可能在use元素上应用同源策略，还有可能拒绝载入`xlink:href`属性内的跨域URL

```html
<defs>
    <circle id="circleDefs" cx="250" cy="50" r="30" />
</defs>

<use id="orange" fill="orange" xlink:href="#circleDefs" />
<use id="pink" fill="deeppink" transform="translate(0, 100) rotate(45, 250, -50)" xlink:href="#circleDefs" />
<use id="pink" fill="deepskyblue" transform="translate(0, 100) rotate(-45, 250, -50)" xlink:href="#circleDefs" />
```

#### symbol

> `<symbol>` 兼具 `<g> `的分组功能和 `<defs> `初始不可见的特性，`<symbol>` 能够创建自己的视窗，所以能够应用viewBox和preserveAspectRatio属性 

```html
<symbol id="sym" viewBox="0 0 150 110">
    <circle cx="50" cy="50" r="40" stroke-width="8" stroke="red" fill="red" />
    <circle cx="90" cy="60" r="40" stroke-width="8" stroke="green" fill="white" />
</symbol>
<use xlink:href="#sym" x="200" y="70" width="100" height="50" />
<use xlink:href="#sym" x="200" y="120" width="75" height="38" />
<use xlink:href="#sym" x="200" y="170" width="50" height="25" />
```

#### a

> 在SVG中，可以使用超链接 `<a>`，超链接可以添加到任意的图形上 

```
- xlink:href  指定链接的地址
- xlink:title 指定链接的标题
- target      指定打开的方式
```

```html
<a xlink:title="百度一下" xlink:href="https://www.baidu.com" target="_blank">
    <text x="250" y="150" text-anchor="middle" fill="none" stroke="deepskyblue" font-size="30" cursor="pointer" >百度一下</text>
</a>
```

#### image

> SVG有一个 `<image>` 元素，可以利用它嵌入任意光栅（以及矢量）图像。它的规格要求应用至少支持PNG、JPG和SVG格式文件

嵌入的图像变成一个普通的SVG元素。这意味着，可以在其内容上用剪切、遮罩、滤镜、旋转等操作

```html
<defs>
    <filter id="gs">
        <feGaussianBlur in="SourceGraphic" stdDeviation="1" />
    </filter>
</defs>

<image x="100" y="20" height="100" xlink:href="https://ws1.sinaimg.cn/large/006eYMu7ly1ftopu9hgs2j30zk0k0jv7.jpg" />
<image x="100" y="150" height="100" xlink:href="https://ws1.sinaimg.cn/large/006eYMu7ly1ftopu9hgs2j30zk0k0jv7.jpg" filter="url(#gs)" />
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftopgphsbnj30eb08pdi2.jpg)

### 元素的坐标系

> 建议看完 transform 和 辅助标签，再看这个知识点

以一个矩形的平移操作为例

```html
<rect x="0" y="0" width="50" height="50" transform="translate(50, 50)" />
```

经过前面的讲解我们知道，这段代码的含义是将矩形所在的坐标系的坐标原点由(0, 0)的位置，平移到了(50, 50)的位置，如下图所示

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftosdln1hhj30ls0dgmx2.jpg)

接下来我们在这个操作的基础上，在(0, 0)的位置上在画一个矩形，宽高为20，填充颜色为红色

```html
<rect x="0" y="0" width="50" height="50" transform="translate(50, 50)" />
<rect x="0" y="0" width="20" height="20" fill="red" />
```

**预期**结果如下图

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftosvndavdj30ed08q3y9.jpg)

**实际**结果如下图

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftoswkc31uj30ee08q3y9.jpg)

咦，不是坐标系已经被平移了么？怎么第二个矩形的原点坐标又回到了平移前的位置？其实原因很简单，**svg中不同元素不共享统一坐标系**，可以理解为每一个图形元素都已自己独立的坐标系，自己坐标系的变化不会影响到其他元素的坐标系不会影响到其他元素的坐标系，那么问题来了，如果每个元素都拥有自己独立的坐标系，如果我们想让一些元素共同在一个坐标系下进行图形变化该怎么办呢，这就要用到上一个知识点讲到的辅助标签，举个例子

```html
<g transform="translate(50, 50)">
    <rect x="0" y="0" width="50" height="50" />
    <rect x="0" y="0" width="20" height="20" fill="red" />
</g>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftosvndavdj30ed08q3y9.jpg)

我们只需要将共同变化的元素放在带有分组性质的标签中，然后对分组标签统一变换即可

### svg动画

首先要有一个svg图形，且该图形具有 `stroke` 属性

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        svg {
            border: 1px solid #000;
        }
        #heart {
            stroke: red;
            stroke-width: 1.5;
            fill: none;
            fill-opacity: none;      
        }
    </style>
</head>

<body>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
        <g>
            <title>Loving heart</title>
            <path stroke="red" id="heart" d="m 243 103 c 57 -116 282 0 0 149 c-282 -149 -57 -265 0 -149 z" />
        </g>
    </svg>
</body>

</html>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpa0cmmfyj30ec08pmx2.jpg)

给图形线条设置虚线样式

```html
#heart {
	.....;
	stroke-dasharray: 15; /* 设置规则同canvas中虚线的设置规则相同 */
}
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpa7ucrjgj30eb08s0sj.jpg)

给虚线设置偏移量，让线条产生动的效果

```html
#heart {
	.....;
	stroke-dasharray: 15; /* 设置规则同canvas中虚线的设置规则相同 */
	stroke-dashoffset: -100;
}
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpa9w1xkug30f60973yc.gif)

给动的效果设置动画，让它持续动起来

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        svg {
            border: 1px solid #000;
        }
        #heart {
            stroke: red;
            stroke-width: 1.5;
            stroke-dasharray: 15; /* 设置规则同canvas中虚线的设置规则相同 */
            stroke-dashoffset: -100;
            fill: none;
            fill-opacity: none;
            animation: move 0.5s linear infinite;
        }
        @keyframes move {
            to {
                stroke-dashoffset: 0;
            }
        }
    </style>
</head>

<body>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
        <g>
            <title>Loving heart</title>
            <path stroke="red" id="heart" d="m 243 103 c 57 -116 282 0 0 149 c-282 -149 -57 -265 0 -149 z" />
        </g>
    </svg>
</body>

</html>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpaj0hmqzg30f6097dgz.gif)

以上便有了动画基本的模型，接下来我们重新设置 `stroke-dasharray` 的值，使 `stroke-dasharray` 超过路径的长度，路径的长度要用js获取

```javascript
// 获取路径的总长度
dom.getTotalLength

// 获取路径上距离起始点长度x的点的坐标
dom.getPointAtLength(x)

// 严格来说，dom元素只能是path元素，即上面两方法只适用于path元素，但各个浏览器实现起来都会有一点区别
// 例如谷歌浏览器也能获取到line元素的路径长度
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        svg {
            border: 1px solid #000;
        }
        #heart {
            stroke: red;
            stroke-width: 1.5;
            fill: none;
            fill-opacity: none;
            animation: move 2s linear infinite;
        }
        @keyframes move {
            to {
                stroke-dashoffset: 0;
            }
        }
    </style>
</head>

<body>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
        <g>
            <title>Loving heart</title>
            <path stroke="red" id="heart" d="m 243 103 c 57 -116 282 0 0 149 c-282 -149 -57 -265 0 -149 z" />
        </g>
    </svg>

    <script>
        var oHeart = document.getElementById('heart');
        var len = oHeart.getTotalLength();
        
        oHeart.style.strokeDasharray = len;
    </script>
</body>

</html>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpb3pd6bpj30ed08vmx2.jpg)

咦这样不是不动了？别急，将 `stroke-dashoffset` 的值设置成路径长度的相反数

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        svg {
            border: 1px solid #000;
        }
        #heart {
            stroke: red;
            stroke-width: 1.5;
            fill: none;
            fill-opacity: none;
            animation: move 2s linear infinite;
        }
        @keyframes move {
            to {
                stroke-dashoffset: 0;
            }
        }
    </style>
</head>

<body>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
        <g>
            <title>Loving heart</title>
            <path stroke="red" id="heart" d="m 243 103 c 57 -116 282 0 0 149 c-282 -149 -57 -265 0 -149 z" />
        </g>
    </svg>

    <script>
        var oHeart = document.getElementById('heart');
        var len = oHeart.getTotalLength();
        
        oHeart.style.strokeDasharray = len;
        oHeart.style.strokeDashoffset = -len;
    </script>
</body>

</html>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpb9b21bcg30f60970ud.gif)

取消无限次播放，将动画停留在最后的关键帧上

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        svg {
            border: 1px solid #000;
        }
        #heart {
            stroke: red;
            stroke-width: 1.5;
            fill: none;
            fill-opacity: none;
            animation: move 3s linear forwards;
        }
        @keyframes move {
            to {
                stroke-dashoffset: 0;
            }
        }
    </style>
</head>

<body>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
        <g>
            <title>Loving heart</title>
            <path stroke="red" id="heart" d="m 243 103 c 57 -116 282 0 0 149 c-282 -149 -57 -265 0 -149 z" />
        </g>
    </svg>

    <script>
        var oHeart = document.getElementById('heart');
        var len = oHeart.getTotalLength();
        
        oHeart.style.strokeDasharray = len;
        oHeart.style.strokeDashoffset = -len;
    </script>
</body>

</html>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpbak8b32g30f609774s.gif)

### viewBox

#### viewport

```html
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="500" height="300">
</svg>
```

这里的 500 * 300 便是 viewport的大小

#### viewBox

**使用预览**

```html
<svg 
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink" 
    width="500" height="300"
    viewBox="0, 0, 50, 30">
</svg>
```

viewBox表示一个矩形区域，(0, 0) 表示矩形左上角的坐标，(50, 30) 表示矩形区域的宽高

**功能展示**

```html
<svg 
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink" 
    width="500" height="300"
    viewBox="0, 0, 50, 30">
<rect x="10" y="10" width="20" height="10" />
</svg>
```

预期效果

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpcz6z6lij30eg08y0sh.jpg)

实际效果

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpcsbs2gjj30ei08qa9t.jpg)

注意这里矩形元素的设置，起点在(10, 10)，宽高为 20 * 10，但是实际效果却不是这样，实际效果是起点(100, 100)，宽高 200 * 100的矩形，为什么会这样呢？因为viewBox的缘故，它的作用是将它作用区域剪切下来，然后在整个viewport区域中显示，也就是说，上面的代码中，viewBox将起点为(0, 0)，宽高为50 * 30 的区域剪切了下来然后放到了整个viewport区域中显示，因为viewport和viewBox的宽高比例是相同的，所以viewBox可以完美的展示在viewport中，可参照下图理解

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpdey88j5g30f6097dg2.gif)

#### preserveAspectRatio

上述的viewBox与viewport比例相同的情况是一种最好的情况，viewBox裁剪下来的区域正好能在viewport中显示，但如果他们的比例不一致呢，viewBox应该怎么在viewport中展示

先来看一下 `preserveAspectRatio` 长什么样子

```
preserveAspectRatio="xMidYMid meet";
```

共分为两部分属性，中间由空格分开

前半部分：设置viewBox与viewport的对齐方式



| 值   | 含义                                         |
| ---- | -------------------------------------------- |
| xMin | viewport和viewBox左边对齐                    |
| xMid | viewport和viewBox x轴中心对齐                |
| xMax | viewport和viewBox右边对齐                    |
| YMin | viewport和viewBox上边缘对齐。注意Y是大写     |
| YMid | viewport和viewBox y轴中心点对齐。注意Y是大写 |
| YMax | viewport和viewBox下边缘对齐。注意Y是大写     |

后半部分：设置viewBox在viewport中的填充方式



| 值    | 含义                                            |
| ----- | ----------------------------------------------- |
| meet  | 保持横纵比，缩放使viewBox尽可能小的适应viewport |
| slice | 保持横纵比，缩放是viewBox尽可能大的适应viewport |
| none  | 扭曲横纵比以适应viewport                        |

备注

1.  因为 "meet" 和 "slice" 都是在保持横纵比的前提下进行缩放，所以这两个属性的变化只能以一条边(宽或高)为准，另一条边的缩放由这条边决定
2.  当属性值为none时，前半部分对齐方式不能再设置，只写一个none

**meet**

首先来讲解 "meet"，接下俩将以三个实例来充分理解 "保持横纵比，缩放使viewBox尽可能小的适应viewport" 这句话的含义

`实例1`

viewBox的宽为250， 高为300

```html
<svg xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     width="500" height="300"
     viewBox="0 0 250 300"
     preserveAspectRatio="xMinYMin meet">

    <rect x="0" y="0" width="200" height="100" fill="#B4C7E7" />

</svg>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftph40gt4oj30eg08s741.jpg)

效果如上图，矩形区域没有进行缩放，下面我们画一些辅助线来解释一下

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftph2qls67j30jv0cca9x.jpg)

```
- 图示
- 黑色实线区域：500 * 300 viewport区域
- 红色虚线区域：350 * 300 viewBox区域
- 深紫矩形区域：200 * 100 矩形区域
```

```html
- 计算符号(缩放前)
- viewportW: viewport的宽
- viewportH: viewport的高
- viewBoxW:  viewBox的宽
- viewBoxH： viewBox的高
- scaleX = viewportW / viewBoxW: 以宽为基准的缩放因子
- scaleY = viewportH / viewBoxH：以高为基准的缩放因子
```

```
- 计算过程
scaleX = viewportW / viewBoxW = 500 / 250 = 2;
scaleY = viewportH / viewBoxH = 300 / 300 = 1;
scaleX > scaleY
```

计算结果的解释：

如果以宽为基准进行缩放，则要将viewBox的宽扩大两倍，高也随之扩大两倍；

如果以高为基准进行缩放，则不需要对viewBox区域进行缩放；

在两者都能适应viewport区域的情况下，为了满足 "尽可能小" 条件，选择以高为基准，这里比例是1所以不缩放，与之对应的viewBox区域内的矩形区也不会缩放

`实例2`

接下来我们修改viewBox区域的宽高，我们把 viewBox的高度由原来的300改成200

```html
<svg xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     width="500" height="300"
     viewBox="0 0 250 200"
     preserveAspectRatio="xMinYMin meet">

    <rect x="0" y="0" width="200" height="100" fill="#B4C7E7" />
</svg>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpkuvzckij30fx09awe9.jpg)

实际效果如上图，矩形的宽高扩大了1.5倍，加一些辅助线讲解（辅助线好像有点多，没关系，一点一点来看）

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftphthjbabj30kp0chjrf.jpg)

```
- 图示
- 黑色实线区域：500 * 300 viewport区域
- 红色虚线区域：250 * 200 缩放前viewBox区域
- 绿色虚线区域：375 * 300 缩放后viewBox区域
- 浅紫矩形区域：200 * 100 缩放前矩形区域
- 深紫矩形区域：300 * 150 缩放后矩形区域
```

```
- 计算符号(缩放前)
- viewportW: viewport的宽
- viewportH: viewport的高
- viewBoxW:  viewBox的宽
- viewBoxH： viewBox的高
- scaleX = viewportW / viewBoxW: 以宽为基准的缩放因子
- scaleY = viewportH / viewBoxH：以高为基准的缩放因子
```

```
- 计算过程
- scaleX = viewportW / viewBoxW = 500 / 200 = 2.5;
- scaleY = viewportH / viewBoxH = 300 / 200 = 1.5;
- scaleX > scaleY
```

计算结果的解释：

如果以宽为基准进行缩放，则需要将viewBox的宽扩大2.5倍，高也随之扩大2.5倍；

如果以高为基准进行缩放，则需要将viewBox的高扩大1.5倍，宽也随之扩大1.5倍；

在两种情况都能适应viewport的情况下，为了保证 "尽可能小"，选择以高为基准，宽高均扩大为原来的1.5倍，相应的，viewBox中的矩形区域的宽高也扩大1.5倍

`实例3`

接下来我们再做一些修改，将viewBox的宽由原来的250改为1000，高由原来的300改为450

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftplxx0gaaj30gb09egld.jpg)

实际效果如上图，矩形区域宽高均缩小了2倍，添加辅助线理解

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpmkv1jf5j30rk0fgt8o.jpg)

```
- 图示
- 黑色实线区域：500 * 300  viewport区域
- 红色虚线区域：1000 * 450 缩放前viewBox区域
- 绿色虚线区域：500 * 225  缩放后viewBox区域
- 浅紫矩形区域：200 * 100  缩放前矩形区域
- 深紫矩形区域：100 * 50   缩放后矩形区域
```

```
- 计算符号(缩放前)
- viewportW: viewport的宽
- viewportH: viewport的高
- viewBoxW:  viewBox的宽
- viewBoxH： viewBox的高
- scaleX = viewportW / viewBoxW: 以宽为基准的缩放因子
- scaleY = viewportH / viewBoxH：以高为基准的缩放因子
```

```
- 计算过程
- scaleX：viewportW / viewBoxW = 500 / 1000 = 0.5;
- scaleY: viewportH / viewBoxH = 300 / 450 = 0.67;
- scaleX < scaleY
```

计算结果解释：

如果以宽为基准进行缩放，则需要将viewport的宽放大0.5倍，高也随之放大0.5倍；

如果以高为基准进行缩放，则需要将viewport的高放大0.67倍，高也随之放大0.67倍；

在两种情况都能适应viewport的情况下，为了保证 "尽可能小"，选择以宽为基准，宽高均扩大为原来的0.5倍，相应的，viewBox中的矩形区域的宽高也扩大0.5倍（放大0.5倍就是缩小两倍）

> 结论：
>
> 对于设置了 "meet" 属性的viewBox，缩放的倍数由 viewport 与 viewBox 宽的比值或者高的比值决定，谁小取谁
>
> 公式：
>
> scaleX = viewportW / viewBoxW
>
> scaleY = viewportH / viewBoxH
>
> scale = scaleX < scaleY ? scaleX : scaleY

**slice**

同样以三个实例（就用meet讲解中的三个实例）来讲解 "保持横纵比，缩放是viewBox尽可能大的适应viewport" 的含义（其实就是与meet确定宽高的方法相反，meet取小的，slice取大的）

`实例1`

viewBox宽250，高300

```
<svg xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     width="500" height="300"
     viewBox="0 0 250 300"
     preserveAspectRatio="xMinYMin slice">

    <rect x="0" y="0" width="200" height="100" fill="#B4C7E7" />

</svg>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpnk2t9a7j30c207njr5.jpg)

实际效果如上图，矩形区域宽高均放大了2倍

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpnjanrlbj30fb0f5mx3.jpg)

```
- 图示
- 黑色实线区域：500 * 300  viewport区域
- 红色虚线区域：250 * 300  缩放前viewBox区域
- 绿色虚线区域：500 * 600  缩放后viewBox区域
- 浅紫矩形区域：200 * 100  缩放前矩形区域
- 深紫矩形区域：400 * 200  缩放后矩形区域
```

```
- 计算符号(缩放前)
- viewportW: viewport的宽
- viewportH: viewport的高
- viewBoxW:  viewBox的宽
- viewBoxH： viewBox的高
- scaleX = viewportW / viewBoxW: 以宽为基准的缩放因子
- scaleY = viewportH / viewBoxH：以高为基准的缩放因子
```

```
- 计算过程
- scaleX = viewportW / viewBoxW = 500 / 250 = 2
- scaleY = viewportH / viewBoxH = 300 / 300 = 1
- scaleX > scaleY
```

计算结果的解释：

如果以宽为基准进行缩放，则要将viewBox的宽扩大两倍，高也随之扩大两倍；

如果以高为基准进行缩放，则不需要对viewBox区域进行缩放；

在两者都能适应viewport区域的情况下，为了满足 "尽可能大" 条件，选择以宽为基准，viewBox的宽扩大两倍，高也随之扩大两倍，相应的viewBox内的矩形区域的宽高也扩大两倍

`实例2`

接下来我们修改viewBox区域的宽高，我们把 viewBox的高度由原来的300改成200

```html
<svg xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     width="500" height="300"
     viewBox="0 0 250 200"
     preserveAspectRatio="xMinYMin slice">

    <rect x="0" y="0" width="200" height="100" fill="#B4C7E7" />
</svg>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpnk2t9a7j30c207njr5.jpg)

实际效果如上图，矩形区域的宽高均扩大了2倍，图解如下

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpoi99x4cj30ji0dc0sp.jpg)

```
- 图示
- 黑色实线区域：500 * 300  viewport区域
- 红色虚线区域：250 * 300  缩放前viewBox区域
- 绿色虚线区域：500 * 400  缩放后viewBox区域
- 浅紫矩形区域：200 * 100  缩放前矩形区域
- 深紫矩形区域：400 * 200  缩放后矩形区域
```

```
- 计算符号(缩放前)
- viewportW: viewport的宽
- viewportH: viewport的高
- viewBoxW:  viewBox的宽
- viewBoxH： viewBox的高
- scaleX = viewportW / viewBoxW: 以宽为基准的缩放因子
- scaleY = viewportH / viewBoxH：以高为基准的缩放因子
```

```
- 计算过程
- scaleX = viewportW / viewBoxW = 500 / 250 = 2
- scaleY = viewportH / viewBoxH = 300 / 200 = 1.5
- scaleX > scaleY
```

计算结果的解释：

如果以宽为基准进行缩放，则要将viewBox的宽扩大两倍，高也随之扩大两倍；

如果以高为基准进行缩放，则要将viewBox的高扩大1.5倍，高也随之扩大1.5倍；

在两者都能适应viewport区域的情况下，为了满足 "尽可能大" 条件，选择以宽为基准，viewBox的宽扩大两倍，高也随之扩大两倍，相应的viewBox内的矩形区域的宽高也扩大两倍

`实例3`

接下来我们再做一些修改，将viewBox的宽由原来的250改为1000，高由原来的300改为450

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpoa5znjkj30dv0883y9.jpg)

实际效果如上图，矩形区域的宽高均放大了0.67倍，图解如下

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpomnizckj30rg0fsgll.jpg)

```
- 图示
- 黑色实线区域：500 * 300     viewport区域
- 红色虚线区域：450 * 1000    缩放前viewBox区域
- 绿色虚线区域：666.7 * 450   缩放后viewBox区域
- 浅紫矩形区域：200 * 100     缩放前矩形区域
- 深紫矩形区域：133.3 * 66.7  缩放后矩形区域
```

```
- 计算符号(缩放前)
- viewportW: viewport的宽
- viewportH: viewport的高
- viewBoxW:  viewBox的宽
- viewBoxH： viewBox的高
- scaleX = viewportW / viewBoxW: 以宽为基准的缩放因子
- scaleY = viewportH / viewBoxH：以高为基准的缩放因子
```

```
- 计算过程
- scaleX：viewportW / viewBoxW = 500 / 1000 = 0.5;
- scaleY: viewportH / viewBoxH = 300 / 450 = 0.67;
- scaleX < scaleY
```

计算结果解释：

如果以宽为基准进行缩放，则需要将viewport的宽放大0.5倍，高也随之放大0.5倍；

如果以高为基准进行缩放，则需要将viewport的高放大0.67倍，高也随之放大0.67倍；

在两种情况都能适应viewport的情况下，为了保证 "尽可能大"，选择以高为基准，宽高均扩大为原来的0.67倍，相应的，viewBox中的矩形区域的宽高也扩大0.67倍

> 结论：
>
> 对于设置了 "slice" 属性的viewBox，缩放的倍数由 viewport 与 viewBox 宽的比值或者高的比值决定，谁大取谁
>
> 公式：
>
> scaleX = viewportW / viewBoxW
>
> scaleY = viewportH / viewBoxH
>
> scale = scaleX > scaleY ? scaleX : scaleY

**none**

"none" 属性不要维持viewBox的横纵比，所以设置了 "none" 属性的viewBox不需要以宽或者高中的一个为基准，他们可以各自基准，即宽高同时适应viewport

```html
<svg xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     width="500" height="300"
     viewBox="0 0 250 200"
     preserveAspectRatio="xMinYMin slice">

    <rect x="0" y="0" width="200" height="100" fill="#B4C7E7" />
</svg>
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpotuokauj30f60a1q2p.jpg)

实际效果如上图，矩形区域宽度放大了2倍，高度放大了1.5倍，图解如下

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftpp69s3f4j30hu0bymx3.jpg)

```
- 图示
- 黑色实线区域：500 * 300  viewport区域
- 红色虚线区域：250 * 300  缩放前viewBox区域
- 绿色虚线区域：500 * 400  缩放后viewBox区域
- 浅紫矩形区域：200 * 100  缩放前矩形区域
- 深紫矩形区域：400 * 200  缩放后矩形区域
```

```
- 计算符号(缩放前)
- viewportW: viewport的宽
- viewportH: viewport的高
- viewBoxW:  viewBox的宽
- viewBoxH： viewBox的高
- scaleX = viewportW / viewBoxW: 以宽为基准的缩放因子
- scaleY = viewportH / viewBoxH：以高为基准的缩放因子
```

```
- 计算过程
- scaleX = viewportW / viewBoxW = 500 / 250 = 2
- scaleY = viewportH / viewBoxH = 300 / 200 = 1.5
```

计算结果解释：

因为没有保持横纵比的要求，所以viewBox在宽度和高度上均适应viewport，宽度扩大2倍，高度扩大1.5倍，相应的viewBox内的矩形区域宽也扩大2倍，高扩大1.5倍，这样的结果会是矩形发生形变

> 结论：
>
> 对于设置了 "none" 属性的viewBox，缩放的倍数由 viewport 与 viewBox 宽的比值或者高的比值决定，各自缩放适应，互不影响
>
> 公式：
>
> scaleX = viewportW / viewBoxW
>
> scaleY = viewportH / viewBoxH

**对齐**

前面讲的填充方式没有提到对齐，实例中都是 "xMinYMin" 的对齐方式，其实这个很简单，这里的对齐指的是缩放后的vieWBox怎么与viewport区域进行对齐，即上面实例中的绿色区域怎么与黑色区域进行对齐，对比对齐属性的表格理解即可

### JS 生成 SVG 元素

创建svg标签并指定命名空间

```javascript
var char = 'http://www.w3.org/2000/svg';
var svg = document.createElementNS(char, 'svg');
```

用 `setAttribute` 方法设置属性

```javascript
svg.setAttribute('width', 500);
svg.setAttribute('height', 300);
svg.setAttribute('viewBox', '0 0 50 30');
```

添加图形元素

```javascript
var rect = document.createElementNS(char, 'rect');

rect.setAttribute('x', 10);
rect.setAttribute('y', 10);
rect.setAttribute('width', 20);
rect.setAttribute('height', 10);
rect.setAttribute('fill', 'deepskyblue');
```

添加dom结构

```javascript
svg.appendChild(rect);
document.body.appendChild(svg);
```

全部代码如下

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        svg {
            border: 1px solid #000;
        }
    </style>
</head>

<body>
    <script type="text/javascript">
        var char = 'http://www.w3.org/2000/svg';
        var svg = document.createElementNS(char, 'svg');

        svg.setAttribute('width', 500);
        svg.setAttribute('height', 300);
        svg.setAttribute('viewBox', '0 0 50 30');
        
        var rect = document.createElementNS(char, 'rect');

        rect.setAttribute('x', 10);
        rect.setAttribute('y', 10);
        rect.setAttribute('width', 20);
        rect.setAttribute('height', 10);
        rect.setAttribute('fill', 'deepskyblue');
        svg.appendChild(rect);
        document.body.appendChild(svg);
    </script>
</body>

</html>
```
