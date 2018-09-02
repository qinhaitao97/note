### border-radius

#### 功能效果

实现边框圆角的功能

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsav9cjqp6j30qh07vdfo.jpg)

#### 用法

border-radius是一个复合属性，像border的设置方法一样，我们可以为border-radius的四个角设置不同大小的圆角

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 100px;
            height: 100px;
            background-color: orange;
            border-radius: 10px 30px 50px 70px; /* 分别代表 左上角，右上角、右下角、左下角 */
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsavf1cma9j30d906wjr6.jpg)

也可以把四个角拆开分别来写，效果也是一样的

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 100px;
            height: 100px;
            background-color: orange;
            border-top-left-radius: 10px;
            border-top-right-radius: 30px;
            border-bottom-right-radius: 50px;
            border-bottom-left-radius: 70px;
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsavf1cma9j30d906wjr6.jpg)

#### 原理

下面深入探究一下border-radius这个属性是怎么实现圆角的

以一个宽高都是100px的盒子为例，只设置`border-top-left-radius: 50px;`，这个过程的实现原理是：在距离左上定点宽50px、高50px的地方做垂线，以交点为圆心，50px为半径做圆，处于盒子中部分的圆弧即是我们实现的圆角效果（图不是很标准，理解意思就好）

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsavuumir8j30de0aat8h.jpg)

上面我们理解了如果设置`border-top-left-radius: 50px;`，其实是将左上角x方向和y方向设置相同的圆角大小，那么既然一个角上有x、y两个方向，那么我们可不可以将这两个方向也设置成不同的值呢？答案是可以的

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 100px;
            height: 100px;
            background-color: orange;
            border-top-left-radius: 40px 60px; /* 将坐上角x方向设置40px的圆角，y方向设置60px的圆角 */
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsaw1nus1jj30dk068jr5.jpg)

总结一下，我们可直接通过设置 `border-radius` 使四个角具有相同的圆角大小；也可以分别设置四个不同的角让他们具有不同的圆角尺寸；而对于每一个单独的角，我们还可以将它分为x方向和y方向设置它的圆角

#### 合并写法

通过以上介绍可以知道，如果细分的话，一个盒子可以设置8个方向的圆角大小，那么如何将这8个方向写到一起呢

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 100px;
            height: 100px;
            background-color: orange;
            border-radius: 10px 20px 30px 40px / 50px 60px 70px 80px;
            /*
    左上角x方向 右上角x方向 右下角x方向 左下角x方向 / 左上角y方向 右上角y方向 右下角y方向 左下角y方向
            */
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

虽然可以合起来这么写，但是这并不符合标准的代码规范，了解即可，一般不这么写

#### 单位

%，px，em...

#### 练习

画一个半圆

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 100px;
            height: 50px;
            background-color: orange;
            border-radius: 50px 50px 0px 0px;
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

### box-shadow

#### 功能

给指定的盒子添加阴影效果

#### 用法

box-shadow: x轴偏移量 y轴偏移量 \[阴影模糊半径] \[阴影扩展半径] \[阴影颜色] \[投影方式]

+ x、y轴偏移量

  如果没有x、要偏移量的话，物体的阴影是与之重合的，在物体的正下方，添加偏移量后可以看到阴影

  ```html
  <!DOCTYPE html>
  <html lang="en">
   
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style type="text/css">
          div {
              width: 100px;
              height: 50px;
              background-color: orange;
              box-shadow: 10px 10px;
          }
      </style>
  </head>
   
  <body>
      <div></div>
  </body>
   
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsaxcfeya7j30af05y0ol.jpg)

+ 阴影模糊半径

  上面的例子中，为阴影添加了偏移量使我们能够看到盒子的阴影，但是还没有模糊的效果，需要我么添加模糊半径来实现模糊的效果，模糊半径越大，模糊程度越重

  `box-shadow: 10px 10px 5px;`

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fscaispqv7j30a103m742.jpg)

+ 阴影扩展半径

  我们知道，阴影的大小与物体距离光源的距离有关，离光源远，影子较小，反之影子较大；那则么控制影子的大小呢，就要设置阴影的扩展半径（默认情况下是与物体等大的，0px是与物体等大的，往上（正值）增大，往下（负值）减小）

  `box-shadow: 10px 10px 5px 5px;`

  `box-shadow: 10px 10px 5px -5px;`

 

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsaxnl7cbdj309u06zq2p.jpg)

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsaxobt8hlj308w058gld.jpg)

+ 阴影颜色

  阴影的默认颜色是黑色，当然，我们可以自己设置这个颜色

  `box-shadow: 10px 10px 5px 5px #ccc;`

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsaxw1iuplj308005c741.jpg)

+ 投影方式

  默认的投影方式是向外投影的，我们也可以设置它向内投影，但多数情况下我们都是用向外投影

  `box-shadow: 10px 10px 5px 5px #ccc inset; `

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsaxx2fumrj309c05o0s3.jpg)

#### 性能杀手

box-shadow属性很消耗页面的性能，所以这个属性不建议过多的使用

#### 练习

给定一个列表，为列表的每一个元素添加hover效果：li边框产生阴影效果

![效果图](http://ww1.sinaimg.cn/large/006eYMu7ly1fsaz6oyk66g30i60at3yk.gif)

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            padding: 0px;
            margin: 0px;
        }
 
        ul {
            margin: 100px 0px 0px 100px;
            width: 300px;
            border: 1px solid #ccc;
            border-bottom: none;
        }
 
        li {
            list-style: none;
            width: 100%;
            height: 40px;
            border-bottom: 1px solid #ccc;
        }
 
        li:hover {
            box-shadow: 0px 0px 5px 0px #888;
        }
    </style>
</head>
 
<body>
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</body>
 
</html>
```

### text-shadow

#### 功能

为文本添加阴影效果（同box-shadow一样，text-shadow也很消耗页面的性能）

#### 用法

text-shadow: X偏移量 y偏移量 \[模糊半径] \[阴影颜色]

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        p {
            text-shadow: 10px 10px 1px #f40;
        }
    </style>
</head>
 
<body>
    <p>房东的猫</p>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsayyc7fhkj306u04a3yb.jpg)

### 颜色值 rgba

#### 定义

RGB是一种色彩标准，是由红(R)、绿(G)、蓝(B)的变化以及相互叠加来得到各式各样的颜色。RGBA是在RGB的基础上增加了控制alpha透明度的参数

#### 语法

`color: rgba(r, g, b, a)`

r: 红色的百分比（0-255 / 0.0% - 100.0%）

g: 绿色的百分比（0-255 / 0.0% - 100.0%）

b: 蓝色的百分比（0-255 / 0.0% - 100.0%）

a: 透明度的取值（0 - 1）

我们知道红、绿、蓝是颜色的三原色，通过这三种颜色的不同比例可以调配处任何颜色，所以这里通过设置这三种颜色的比例来设置颜色（最好用 0 - 255 来调配颜色，因为不是所有的浏览器都支持百分数）

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 100px;
            height: 100px;
            background-color: rgba(0, 255, 0, 0.5);
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

#### rgba和opacity

rgba中的a属性可以设置透明度，opacity属性也可以设置透明度，这两种设置透明度的方法有什么区别呢？

> 使用rgba设置的透明度，子代不会继承，而使用opacity设置的透明度，子代会自动继承

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        .wrapper {
            width: 200px;
            height: 200px;
            background-color: rgba(255, 0, 0, 0.5);
        }
 
        .inner {
            width: 100px;
            height: 100px;
            background-color: rgba(0, 255, 0, 1);
        }
 
        .wrapper1 {
            margin-top: 50px;
            width: 200px;
            height: 200px;
            background-color: rgb(255, 0, 0);
            opacity: 0.5;
        }
 
        .inner1 {
            width: 100px;
            height: 100px;
            background-color: rgba(0, 255, 0, 1);
        }
    </style>
</head>
 
<body>
    <div class="wrapper">
        <div class="inner"></div>
    </div>
 
    <div class="wrapper1">
        <div class="inner1"></div>
    </div>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsazu9pgqlj30ae0e93ya.jpg)

### 渐变的背景色gradient

渐变这个属性也是性能杀手，尽量减少使用

#### 线性渐变

`linear-gradient([direction], color[percent], color[percent], color[percent],.....);`

|           | 含义                                                         | 值          | 值                                                |
| --------- | ------------------------------------------------------------ | ----------- | ------------------------------------------------- |
| direction | 渐变的方向（默认是从上到下）                                 | 角度（deg） | to top/right/bottom/left/top left/top right/..... |
| color     | 颜色                                                         | 颜色值      | 颜色值                                            |
| percent   | **到**多少为止（重点强调“到”）（默认按照颜色的个数均分比例） | %           | px                                                |

这里重点强调percent这个属性的含义，是到设定的比例为止，而不是占多少设定的比例

举例

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 100px;
            height: 100px;
            background: linear-gradient(red 20%, green 50%, orange 100%);
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

这里渐变色所占的比例的正确含义是，红色所占比例到20%的位置，绿色所占比例到50%的位置，橘色所占区域到100%的位置

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsb37atj4ij308d04p0sh.jpg)

如果按照错误的理解，每个颜色的比例是占有的比例，比如我让每一个颜色各占33%，我们看看效果是什么

`background: linear-gradient(red 33%, green 33%, orange 33%);`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsb3ahp8ejj309204p0ge.jpg)

实际效果不是想象中的三个颜色均分，而是只有这两种颜色，这种结果首先证明了这种思路是错误的，其次我们要知道这种写法为什么会出现这样的结果

首先，盒子会把颜色列表中的最后一种颜色当做背景颜色

比如我们这样写

`background: linear-gradient(red 0%, green 0%, orange 0%); `

效果是这样的：

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsb3fa4l63j309704b0fk.jpg)

给红色加上一些比例：

`background: linear-gradient(red 30%, green 0%, orange 0%); `

效果是这样的

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsb3j95cm0j309y04j0ha.jpg)

如果我们给绿色和橘色也都设置30%的比例，这个区域已经被红色部分覆盖，所以这两个颜色就没有效果了，到此解释了之前提出的疑问，当然如果我们不希望看到最后一个颜色的多余效果，可以在最后添加一个透明色

`background: linear-gradient(red 20%, green 40%, orange 60%, transparent); `

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsbqwoi13rj30b003i0rg.jpg)

#### 径向渐变

`radial-gradient(shape at position, color[percent], color[percent],...);`



| shape                   | position      | position | position | color[percent] |
| ----------------------- | ------------- | -------- | -------- | -------------- |
| circle r(半径)          | center center | % %      | px px    | 同线性渐变     |
| ellipse a(长轴) b(短轴) | center center | % %      | px px    | 同线性渐变     |

注：position的值如果只写一个的话，第二个值默认是 center

`background: radial-gradient(circle 50px at center, red 20%, green 40%, orange 60%, transparent 100%); `

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsbs3jy2oej308n03bjrj.jpg)

`background: radial-gradient(ellipse 50px 40px at center, red 20%, green 40%, orange 60%, transparent 100%); `

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsbs4mzwlmj308s038wek.jpg)

### word-wrap

对于一段文本来说，如果他的长度超出了文本框的边界，那么会自动换行到下一行展示，前提条件是这段文本可以断句，即是多个单词构成的（有空格）；那如果现在有一个很长的单词，也想让它在要超出边界时自动换行，怎么做呢

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        p {
            width: 100px;
            border: 1px solid #000;
        }
    </style>
</head>
 
<body>
    <p>https://www.google.com</p>
</body>
 
</html>
```

正常情况下一个单词不会换行：

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsbse8w6eaj30a101p741.jpg)

添加`word-wrap: break-word;`样式

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsbsguimq5j307u024a9t.jpg)

### font-face

引入自己需要的字体样式

详细介绍：[font-face](http://www.w3school.com.cn/css3/css3_font.asp)

语法：

```html
@font-face {
    font-family: <YourWebFontName>;
    src: <source> [<format>][,<source> [<format>]]*;
  }
```

说明：

1. YourWebFontName:此值指的就是你自定义的字体名称，最好是使用你下载的默认字体，他将被引用到你的Web元素中的font-family。如“font-family:"YourWebFontName";”
2. source:此值指的是你自定义的字体的存放路径，可以是相对路径也可以是绝路径；
3. format：此值指的是你自定义的字体的格式，主要用来帮助浏览器识别，其值主要有以下几种类型：truetype,opentype,truetype-aat,embedded-opentype,avg等；

推荐字体下载网站：[Google Fonts](https://fonts.google.com/?selection.family=Handlee|Josefin+Slab|Nunito|Poiret+One|Poor+Story|Sacramento|Source+Code+Pro|Source+Sans+Pro|Titillium+Web)

示例：

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        @font-face {
            font-family: 'self';
            src: url('diyfont.eot'); /* IE9+ */
            src: url('diyfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
                 url('diyfont.woff') format('woff'), /* chrome、firefox */
                 url('./offer/font/Poor_Story/PoorStory-Regular.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
                 url('diyfont.svg#fontname') format('svg'); /* iOS 4.1- */
 
        }
        p {
            font-family: 'self';
            font-size: 25px;
            font-weight: blod;
        }
    </style>
</head>
 
<body>
    <p>My house is perfect. By great good fortune I have found a housekeeper no less to my mind</p>
</body>
 
</html>
```

上述多个url是兼容不同字体的兼容性写法

### border的一些属性

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
 
        ul {
            position: absolute;
            top: 100px;
            left: 600px;
            width: 300px;
            height: 300px;
            font-size: 0px;
        }
 
        li {
            display: inline-block;
            width: 100px;
            height: 100px;
            list-style: none;
            font-size: 50px;
            text-align: center;
            line-height: 100px;
        }
 
        li:nth-child(1) {
            background-color: rgb(168, 216, 185);
        }
 
        li:nth-child(2) {
            background-color: rgb(125, 185, 222);
        }
 
        li:nth-child(3) {
            background-color: rgb(141, 116, 42);
        }
 
        li:nth-child(4) {
            background-color: rgb(219, 142, 113);
        }
 
        li:nth-child(5) {
            background-color: rgb(155, 144, 194);
        }
 
        li:nth-child(6) {
            background-color: rgb(129, 199, 212);
        }
 
        li:nth-child(7) {
            background-color: rgb(215, 196, 187);
        }
 
        li:nth-child(8) {
            background-color: rgb(189, 182, 186);
        }
 
        li:nth-child(9) {
            background-color: rgb(145, 173, 112);
        }
 
        div {
            width: 100px;
            height: 100px;
            padding: 100px;
            border: 100px solid rgba(0, 0, 0, 0.5);
            border-image: url('./tmpPicture/html+css/border-image.png') 149;
            background-color: orange;
        }
 
    </style>
</head>
 
<body>
 
    <div></div>
 
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
        <li>7</li>
        <li>8</li>
        <li>9</li>
    </ul>
</body>
 
</html>
```

### background的一些属性

#### background-image

引入背景图片

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 300px;
            height: 300px;
            padding: 50px;
            border: 50px solid rgba(0, 0, 0);
            background-image: url('http://ww1.sinaimg.cn/large/006eYMu7ly1fsc0hczb81j308b08ct8m.jpg');
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc0q6bj60j30k10fa0sz.jpg)

#### background-origin

##### padding-box

引入背景图片后我们来思考一个问题，背景图片是以哪里为起点引入的呢，是从border？padding？还是content？我们把border的透明度设置为0.5，以方便看清border下的内容

`border: 50px solid rgba(0, 0, 0, 0.5);`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc0s85rwcj30j40ert97.jpg)

我们发现，border区域确实有图片存在，这是不是说明背景图片就是以border为起点引入的呢？其实并不是，仔细观察会发现，我们的背景图片是从1开始的但是这张图的的border区域（最左上角）却不是从1开始的，那就说明这里不是图片的起点，那这里为什么会有图片呢？这是因为background还有一个background-repeat属性，这个属性的默认值是repeat，就是说我们引入的背景图片会自动的重复展示，充满整个盒子；我们把这个属性设置为no-repeat后再观察

`background-repeat: no-repeat;`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc0xaxfwjj30ia0eaglq.jpg)

这次我们发现，引入的背景图片只剩下了一张，而且**起点是从padding区域开始的**，即background-origin的值默认是padding-box

默认情况下是从padding区域引入的，那我们可不可以修改这个值，让他从其他区域开始引入呢？当然可以

##### border-box

从border开始引入背景图片

`background-origin: border-box;`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc171lg2uj30fu0epq31.jpg)

##### content-box

从content区域开始引入背景图片

`background-origin: content-box;`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc18hl0hkj30fv0ee3ym.jpg)

#### background-repeat

上面已经提到过，用来控制背景图片是否重复以充满整个盒子

#### background-clip

border-clip: border-box | padding-box | content-box | no-clip

参数分别表示从边框（border），或内填充（padding），或者内容区（content）向外裁剪背景。no-clip表示不裁剪，和参数border-box显示同样的效果，background-clip默认值为border-box

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 300px;
            height: 300px;
            padding: 50px;
            border: 50px solid rgba(0, 0, 0, 0.5);
            background-image: url('http://ww1.sinaimg.cn/large/006eYMu7ly1fsc0hczb81j308b08ct8m.jpg');
            background-clip: content-box;
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc3ukr0tfj30gf0eoq32.jpg)

#### background-clip: text

从前景内容的形状（比如文字）作为裁剪区域向外裁剪，如此即可实现使用背景作为填充色之类的遮罩效果

注意：webkit独有属性，且必须配合text-fill-color属性

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
        div {
            width: 280px;
            height: 315px;
            background-image: url('http://ww1.sinaimg.cn/large/006eYMu7ly1fsc4fz9kuzj307s08racx.jpg');
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            word-wrap: break-word;
            overflow: hidden;
        }
    </style>
</head>
 
<body>
    <div>iuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiuiu
    </div>
    <img src="http://ww1.sinaimg.cn/large/006eYMu7ly1fsc4fz9kuzj307s08racx.jpg">
</body>
 
</html>
```

上面试效果图，下面是原图

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc4oehxkdj30bo0hl78c.jpg)

#### background-size

背景图片的尺寸

background-size: atuo | % | px | cover | contain;

auto: 默认值是 auto，即不改变图片的宽高

cover: 等比例伸缩

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
        div {
            width: 400px;
            height: 400px;
            border: 1px solid #000;
            background-image: url('http://ww1.sinaimg.cn/large/006eYMu7ly1fsc0hczb81j308b08ct8m.jpg');
            background-repeat: no-repeat;
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc6bh294lj30hr0d8wel.jpg)

添加`background-size: cover;`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc6cuq8i5j30l60cpwey.jpg)

contain：包含整个图片

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
        div {
            margin: 100px;
            width: 200px;
            height: 200px;
            border: 1px solid #000;
            background-image: url('http://ww1.sinaimg.cn/large/006eYMu7ly1fsc0hczb81j308b08ct8m.jpg');
            background-repeat: no-repeat;
        }
    </style>
</head>
 
<body>
    <div></div>
</body>
 
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc6fvukw9j30b306rt8k.jpg)

添加`background-size: contain;`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsc6gvfqdgj30ay06ujrc.jpg)

#### background-position

背景图片的位置

### box-sizing

可以改变某一个盒子的渲染方式

`box-sizing:content-box;` ：W3C标准盒模型

`box-sizing: border-box;`： IE6混杂模式下盒模型