### transform

可以实现元素的形状、角度、位置等的变换

#### rotate()

以x轴，y轴，z轴或者某个合成的矢量轴为旋转轴进行指定角度的旋转，默认情况下是以z轴为旋转轴

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fske5noljyj30fe07lmwy.jpg)

+ rotate(deg)

  这是默认情况，以z轴为旋转轴进行旋转。deg是旋转的角度，当角度值为正时，正视图顺时针旋转

+ rotateX(deg)

  以x轴为旋转轴进行旋转。deg是旋转的角度，当角度值为正时，右视图顺时针旋转

+ rotateY(deg)

  以y轴为旋转轴进行旋转。deg是旋转的角度，当角度值为正时，仰视图顺时针旋转

+ rotateZ(deg)

  以z轴为旋转轴进行旋转。deg是旋转的角度，当角度值为正时，正视图顺时针旋转

+ rotate3d(x, y, z, deg)

  以x，y，z三个轴方向上的矢量合成的矢量为旋转轴进行旋转。x，y，z均为number类型，可以是0到1之间的数值，表示x、y、z方向上的矢量；deg代表旋转的角度

  > 这里数值的大小代表什么呢？不同的数值会导致什么不同？
  >
  > 参考：https://blog.csdn.net/u010552788/article/details/51505152

  ```html
  <!DOCTYPE html>
  <html lang="en">
   
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style type="text/css">
   
          #demo {
              width: 100px;
              height: 100px;
              margin: 100px;
              background-color: red;
              transform: rotate3d(1, 1, 0, 45deg);
          }
   
      </style>
  </head>
   
  <body>
      <div id="demo">a</div>
  </body>
   
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fskegyj51ij30h308eq2q.jpg)

  **注意**

  1. 当元素进行旋转的同时，非旋转轴也会跟着元素一同进行旋转。比如 `rotateX(90deg);`，旋转结束后，旋转轴x方向不变水平向右，非旋转轴y轴和z轴分别垂直屏幕向外和竖直向上

  2. `transform: rotateX(45deg) rotateY(45deg) rotateZ(45deg);` 和 `transform: rotate3d(1, 1, 1, 45deg);` 的效果是不一样的：前者是有先后顺序，先沿x轴旋转，再沿y轴旋转，再沿z轴旋转；后者直接沿合成的轴进行旋转

     前者

     ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fskf5cjjlaj307304xt8h.jpg)

     后者

     ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fskf6abgc4j30ax066a9u.jpg)

#### scale()

以x轴，y轴，z轴为轴进行指定比例的缩放

+ scale(x, y)

  x，y分别是在各自方向上，以该方向上元素尺寸大小为基准，放大或者缩小的倍数；如果第二值没有给出，则第二个值取第一个值

  

  |        | 0         | (0, 1) | 1        | \>1  |
  | ------ | --------- | ------ | -------- | ---- |
  | 绝对值 | 尺寸变成0 | 缩小   | 尺寸不变 | 放大 |

  |      | \>0              | \<0                                    |
  | ---- | ---------------- | -------------------------------------- |
  | 值   | 直接按照比例缩放 | 先以轴为镜面做镜像对称，再按照比例缩放 |

  ```html
  <!DOCTYPE html>
  <html lang="en">
   
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <style type="text/css">
   
          #wrapper {
              width: 100px;
              height: 100px;
              background-color: #ccc;
              margin: 100px;
          }
   
          #demo {
              width: 100px;
              height: 100px;
              background-color: rgba(255, 0, 0, 0.5);
              font-size: 30px;
              /* transform: scale(0); */
              /* transform: scale(1, 1); */
              /* transform: scale(2, 1); */
              /* transform: scale(1, 0.5); */
              /* transform: scale(1, -2); */
              /* transform: scale(-0.5, 1); */
              /* transform: scale(-2, -2); */
          }
   
      </style>
  </head>
   
  <body>
      <div id="wrapper">
          <div id="demo">a</div>
      </div>
  </body>
   
  </html>
  ```

  依次打开注释观察效果，#wrapper是模拟元素原始效果，与变化之后的效果作比较

+ scaleX(m)、scaleY(m)、scaleZ(m)

  分别以x、y、z轴为轴，进行缩放，括号中的值m表示倍数

+ scale3d(mx, my, mz)

  在各自的方向上以各自的轴为轴，进行x、y、z倍数的缩放，等效于`transform: scaleX(m) scaleY(m) scaleZ(m);`

#### skew()

对元素进行倾斜扭曲

+ skew()

  接受两个参数x，y，表示在y方向上以及x方向上倾斜的角度，角度为正向右倾斜，为负向左倾斜，为0不倾斜；如果不提供第二个参数，默认是0

+ skewX()

  元素在x方向上的大小不变，y方向上进行倾斜

+ skewY()

  元素在y方向上的大小不变，x方向上进行倾斜

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
 
        #wrapper {
            width: 100px;
            height: 100px;
            background-color: #ccc;
            margin: 100px;
        }
 
        #demo {
            width: 100px;
            height: 100px;
            background-color: rgba(255, 0, 0, 0.5);
            font-size: 30px;
            transform: skew(20deg, 20deg);
        }
 
    </style>
</head>
 
<body>
    <div id="wrapper">
        <div id="demo">a</div>
    </div>
</body>
 
</html>
```

#### translate()

平移产生位置变化，相对于自身的位置

+ translate(x, y)

  接受两个参数x、y，分别代表沿x轴平移的x的距离、沿y轴移动y的距离，单位可以是px或者%（**注意，如果是%，是相对于自身的大小**）；如果不提供第二个参数，则默认为0

+ translateX(s)、translateY(s)、translateZ(s)

  沿x轴、y轴、z轴平移指定的距离

+ translate3d(sx, sy, sz)

  沿x轴、y轴、z轴平移指定的距离，等效于`transform: translateX(s) translateY(s) translateZ(s);`

利用这个属性的功能，可以实现元素的居中

```html
<!DOCTYPE html>
<html lang="en">
 
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
 
        #wrapper {
            position: relative;
            width: 200px;
            height: 200px;
            background-color: #ccc;
        }
 
        #demo {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 40%;
            height: 40%;
            background-color: red;
            transform: translate(-50%, -50%);
        }
 
    </style>
</head>
 
<body>
    <div id="wrapper">
        <div id="demo"></div>
    </div>
</body>
 
</html>
```

这里因为不知道#demo具体的宽高，所以不能用margin来调整位置，而translate是相对于元素自身的大小，利用%可以实现调整

### transform-origin

**定义**

任何元素都有一个中心点，默认情况下，其中心店居于x轴和y轴的50%处，可以通过transform-origin属性改变其原点；transform-origin有两个属性值，分别表示原点在x轴方向上的位置与原点在y轴方向的位置，这些属性值可以是以下几种形式：

+ 关键字

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fskz1p9nqrj30ek0a43yb.jpg)

+ 百分比%

  这个百分比的值是相对于元素自身的大小

+ 像素值px

  可以通过像素将元素的中心店设置在任意的位置

**语法**

现在主流的浏览器不仅支持 `transition-origin` 的2D属性，还支持他的3D属性，用来改变中心点在Z轴上的位置

`transform-origin: x-axis y-axis z-axis;` 



| 值     | 取值              |
| ------ | ----------------- |
| x-axis | 关键字，length，% |
| y-axis | 关键字，length，% |
| z-axis | length            |

练习：画一个简易的钟表

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
        .clock {
            width: 200px;
            height: 200px;
            border: 1px solid #000;
            border-radius: 50%;
            margin: 100px auto;
        }
        .clock ul {
            position: relative;
            width: 100%;
            height: 100%;
            font-size: 0px;
        }
        .clock ul li {
            position: absolute;
            top: 0px;
            left: 50%;
            width: 2px;
            height: 15px;
            background-color: #000;
            transform: translateX(-50%);
            transform-origin: 50% 100px;
        }
        .clock ul li:nth-child(2) {
            transform: rotateZ(90deg);
        }
        .clock ul li:nth-child(3) {
            transform: rotateZ(180deg);
        }
        .clock ul li:nth-child(4) {
            transform: rotateZ(270deg);
        }
        .clock ul li span {
            position: absolute;
            top: 14px;
            left: -9px;
            width: 20px;
            height: 20px;
            font-size: 16px;
            text-align: center;
            line-height: 20px;
        }
        .clock ul li:nth-child(2) span {
            transform: rotateZ(-90deg);
        }
        .clock ul li:nth-child(3) span {
            transform: rotateZ(-180deg);
        }
        .clock ul li:nth-child(4) span {
            transform: rotateZ(-270deg);
        }
    </style>
</head>
 
<body>
    <div class="clock">
        <ul>
            <li><span>12</span></li>
            <li><span>3</span></li>
            <li><span>6</span></li>
            <li><span>9</span></li>
        </ul>
    </div>
</body>
 
</html>
```

当刻度旋转到指定位置时，数字也会跟着旋转，这时我们看到的效果是这样的

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsl2tqtwi8j30az087glh.jpg)

所以我们要把数字自身旋转到正面的位置，在数字外面包裹一层span，对span进行旋转

![](http://ww1.sinaimg.cn/large/006eYMu7ly1fsl2ur5flkj30cs080jr9.jpg)

### transition

过渡动画，是CSS3的一个复合属性，**只对block级元素生效**，主要包括以下几个子属性

#### 触发条件

> 单纯的代码不会触发任何过渡操作，需要通过用户的行为（如点击，悬浮等）触发，可以触发的方式有：`:hover`、`:checked`、`:focus`、媒体查询、JavaScript

transition是实现元素从一种状态变到另一种状态时过渡动画的效果，所以很明显，要想让transition生效，就要产生元素状态的变化，比如说一个方块初始状态下宽高100px，当鼠标hover时，宽高变成了200px，这个过程就是方块状态改变的过程，正常情况下它的宽高瞬间就变成了200px，我们不想让这个过程变的太快，想让它慢慢的过渡到最终的状态，这就要使用transition来实现过渡效果

![正常变换](http://ww1.sinaimg.cn/large/006eYMu7ly1ftab511grvg30ev0a2jrd.gif)

![过渡变换](http://ww1.sinaimg.cn/large/006eYMu7ly1ftab5llbhag30ev0a2jri.gif)

#### transition-property

过渡或者模拟的css属性

语法：`transition-property: all|none|property;`



| 值       | 描述                                                      |
| -------- | --------------------------------------------------------- |
| none     | 没有属性会获得过渡效果。                                  |
| all      | 所有属性都将获得过渡效果。                                |
| property | 定义应用过渡效果的 CSS 属性名称列表，列表以**逗号**分隔。 |

不是所有的属性都可以参与过渡动画，需要属性具有中间状态，所有可以参与过渡属性动画的属性：[点击这里]('http://oli.jp/2010/css-animatable-properties/')

#### transition-duration

值过渡所需要的时间，单位可以是s或者ms，如果时间为0，则过渡效果不能实现

#### transition-timing-function

指过渡函数，规定过渡效果的速率曲线



| 值                            | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| linear                        | 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。 |
| ease（默认值）                | 规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）。 |
| ease-in                       | 规定以慢速开始的过渡效果（等于 cubic-bezier(0.42,0,1,1)）。  |
| ease-out                      | 规定以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)）。  |
| ease-in-out                   | 规定以慢速开始和结束的过渡效果（等于 cubic-bezier(0.42,0,0.58,1)）。 |
| cubic-bezier(*n*,*n*,*n*,*n*) | 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。 |

可以用最后一个贝塞尔函数的不同取值来代替上述的的所有速率曲线

#### transition-delay

指开始出现的延迟时间

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
        .demo1, .demo2, .demo3 { display: inline-block; }
        .hover {
            width: 60px;
            height: 30px;
            background-color: #ccc;
            text-align: center;
            line-height: 30px;
            cursor: pointer;
        }
        .item {
            position: absolute;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: #f40;
            text-align: center;
            line-height: 100px;
        }
        .demo1 .item1 {
            top: 100px;
            transition: all 1500ms linear;
        }
        .demo2 .item2 {
            top: 210px;
            transition: left 1000ms, top 1000ms;
        }
        .demo3 .item3 {
            top: 320px;
            opacity: 1;
            transition: top 1000ms ease-in, background-color 1000ms linear, left 1500ms ease-out 1000ms, opacity 1500ms linear 1000ms;
        }
 
        .demo1 .hover1:hover + .item1 {
            width: 300px;
            height: 200px;
        }
 
        .demo2 .hover2:hover + .item2 {
            left: 300px;
            top: 0px;
        }
 
        .demo3 .hover3:hover + .item3 {
            left: 200px;
            top: 400px;
            background-color: green;
            opacity: 0.1;
        }
 
 
    </style>
</head>
 
<body>
    <div class="demo1">
        <div class="hover hover1">hover1</div>
        <div class="item item1">item1</div>
    </div>
    <div class="demo2">
        <div class="hover hover2">hover2</div>
        <div class="item item2">item2</div>
    </div>
    <div class="demo3">
        <div class="hover hover3">hover3</div>
        <div class="item item3">item3</div>
    </div>
</body>
 
</html>
```
以上demo把transition的属性合起来写了，也可以分开来写

#### 局限性

1. transition过渡动画不能再网页加载时自动触发，需要事件触发
2. transition过渡动画是一次性的，不能重复播放，除非一再触发
3. transition过渡动画只能定义元素开始和结尾的两种状态，不能定义中间过程的状态

#### 使用位置

一个元素从初始状态过渡到最终状态要使用transition属性，那这个transition是设置在初始状态中还是最终状态中呢？这个要根据具体情况而定，推荐设置在最终状态中，这样在状态较多时不容易混乱

比如：还是以方块的宽高变换为例，现有一宽高100px的方块和三个按钮，点击`0.5s` 按钮，宽度0.5s变成200px；点击`1.0s` 按钮，高度1s变成300px；点击`origin` 按钮，2s回到初始状态

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftaclbiphgg30go0a5dgw.gif)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .demo {
            position: absolute;
            top: 100px;
            left: 200px;
            width: 100px;
            height: 100px;
            background-color: orange;
            transition: all 2s linear;
        }
        .half-second {
            width: 200px;
            transition: width 0.5s linear;
        }
        .one-second {
            width: 300px;
            transition: width 1s linear;
        }
    </style>
    <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
</head>

<body>
    <div class="demo"></div>
    <button class="half">0.5s</button>
    <button class="one">1.0s</button>
    <button class="origin">origin</button>
    <script>
        $('.half').on('click', function () {
            $('.demo').addClass('half-second');
        });
        $('.one').on('click', function () {
            $('.demo').addClass('one-second');
        });
        $('.origin').on('click', function () {
            $('.demo').prop('class', 'demo');
        });
    </script>
</body>

</html>
```

结合代码来讲，`.demo` 算是方块的初始状态，最终状态有两个 `.half-second` 和 `.one-second`，从初始状态到这两个状态的过渡动画是不同的（时间不同），如果把 `transition` 设置在 `.demo` 中就无法实现两个状态各自的变换，所以这里把他们的 `transition` 设置在了最终状态的元素中，不过你一定看到了 `.demo` 中的 `transition` 属性，这个属性并不是实现width变大的过渡效果，而是实现从最终状态变回初始状态的过渡效果，这时的两个最终状态就变成了初始状态，而原来的初始状态就成了这次变换中的最终状态，所以这个过程的 `transition` 属性设置在 `.demo` 中

### animation

animation通过动画关键帧来实现过渡动画的效果，是一个复合属性，主要包括下面将要介绍的几个子属性

#### 关键帧

**说明**

animation用来实现过渡动画的效果的，transition也是实现过渡动画效果的，那两者有什么区别呢？从定义可以 看的出来，animation是通过**关键帧**来实现过渡动画效果的，一个关键帧代表了整个动画过程中的一个状态（以视频中的每一帧类比），通过定义关键帧的样式来控制CSS动画序列的中间步骤，与transition相比能更好的控制中间状态的动画

**创建关键帧**

> 要使用关键帧, 先创建一个带名称的`@keyframes`规则，以便后续使用 `animation-name` 这个属性来将一个动画同其关键帧声明匹配。每个`@keyframes` 规则包含多个关键帧，也就是一段样式块语句，每个关键帧有一个百分比值作为名称，代表在动画进行中，在哪个阶段触发这个帧所包含的样式。 关键帧百分比列出的顺序不影响它被执行的顺序，他们会按照该发生的顺序来处理

**让关键帧生效**

> 如果一个关键帧规则没有指定动画的开始或结束状态（也就是，`0%`/`from` 和`100%`/`to`，浏览器将使用元素的现有样式作为起始/结束状态。这可以用来从初始状态开始元素动画，最终返回初始状态。
>
> 如果在关键帧的样式中使用了不能用作动画的属性，那么这些属性会被忽略掉，支持动画的属性仍然是有效的，不受波及。

除了百分比以外，还可以用关键词来表示某个状态(某个关键帧)：0% ==> from   100% ==> to

**重复定义**

下面说的不支持层叠样式是Firefox 14版本之前，现在主流的浏览器基本已经支持**百分比的层叠样式**了，但是对于多个重名关键帧的层叠样式，还没有较好的支持（即如果关键帧使用同一个名称，则以最后一个定义为准；如果百分比重复定义，则按照层叠规则进行判断）

> 如果多个关键帧使用同一个名称，以最后一次的定义为准。`@keyframes`不存在层叠样式的情况，所以动画在一个阶段只会使用一个关键帧的数据。
>
> 如果一个`@keyframes`里的关键帧的百分比存在重复的情况，以最后一次定义的关键帧为准。因为`@keyframes`的规则不存在层叠样式的情况，即使多个关键帧设置相同的百分值也不会全部执行（执行最后一个）

**属性个数不定**

> 如果一个关键帧中没有出现其他关键帧中的属性，那么这个属性将使用[插值]('https://baike.baidu.com/item/%E6%8F%92%E5%80%BC%E6%B3%95')(不能使用插值的属性除外，这些属性会被忽略掉)

这里要注意，如果没有定义 初始/结束 状态，浏览器使用元素的现有样式作为 初始/结束状态；或者 初始/结束 状态中有些属性没有设置，那么这些属性的值也是元素现有样式的值

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        #demo {
            width: 100px;
            height: 100px;
            background-color: #f40;
            animation: demo 1s linear;
        }
        @keyframes demo {
            50% {
                width: 300px;
            }
        }
        @keyframes demo {
            0% {
                width: 100px;
            }
            50% {
                width: 500px;
                height: 200px;
            }
            50% {
                width: 300px;
            }
        }
    </style>
</head>
<body>
    <div id="demo"></div>
</body>
</html>
```

关于demo的说明：

1. 在此样例中创建了两个同名的关键帧，以最后一个定义的关键帧为准，所以第一个关键帧不起作用

2. 在第二个关键帧中，一共涉及了两个属性，width和height，对于height属性来说，没有定义 初始/结束 状态，所以height属性的 初始/结束 状态即为元素初始的样式（100px）；对于width来说，定义了初始状态（与元素现有的样式相同），没有定义结束状态，则结束状态为100px；

3. 50%被重复定义，所以按照层叠样式，在50%这个时间点，元素的状态应该是width：300px；height：200px（相当于把两个50%中的定义都写在一个里面，然后判断最终的属性）

4. 整个过程的变化就是

   

   |        | 0% — 50%       | 50% — 100%     |
   | ------ | -------------- | -------------- |
   | width  | 100px -> 300px | 300px -> 100px |
   | height | 100px -> 200px | 200px -> 100px |

5. 还有一点需要注意的就是，一个关键帧内的多个状态之间的不要用 `;` 进行分隔，有可能会造成关键帧失效

#### animation-name

**定义**

> 指定应用的一系列动画，每个名称代表一个由@keyframes定义的动画序列

**语法**

```html
/* Single animation */
animation-name: none;
animation-name: test_05;
animation-name: -specific;
animation-name: sliding-vertically;
 
/* Multiple animations */
animation-name: test1, animation4;
animation-name: none, -moz-specific, sliding;
 
/* Global values */
animation-name: initial /* 设置属性为其默认值 */
animation-name: inherit /* 从父元素继承属性 */
animation-name: unset
```

**demo**

````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        #demo {
            width: 100px;
            height: 100px;
            background-color: #f40;
            /* 写法一： */
            animation-name: demo1, demo2;
            animation-duration: 1s, 1s;
 
            /* 写法二： */
            /* animation: demo1 1s, demo2 1s; */
        }
 
        @keyframes demo1 {
            100% {
                width: 200px;
            }
        }
        @keyframes demo2 {
            100% {
                height: 200px;
            }
        }
    </style>
</head>
<body>
    <div id="demo"></div>
</body>
</html>
````

**注意**

写法一与写法二是等效的

#### animation-duration

**定义**

> 指定一个动画周期的时长

**语法**

```html
animation-duration: 6s
animation-duration: 120ms
animation-duration: 1s, 15s
animation-duration: 10s, 30s, 230ms
```

#### animation-timing-function

**定义**

> 定义css动画在每一动画周期中执行的节奏。可能值为一个或多个
>
> 对于关键帧动画来说，timing function作用于一个关键帧周期而非整个动画周期，即从关键帧开始开始，到关键帧结束结束
>
> 定义一个关键帧区块的缓动函数应用到该关键帧；另外，若该关键帧没有定义缓动函数，则使用定义于整个动画的缓动函数

**语法**

```html
/* Keyword values */
animation-timing-function: ease;
animation-timing-function: ease-in;
animation-timing-function: ease-out;
animation-timing-function: ease-in-out;
animation-timing-function: linear;
animation-timing-function: step-start;
animation-timing-function: step-end;
 
/* Function values */
animation-timing-function: cubic-bezier(0.1, 0.7, 1.0, 0.1);
animation-timing-function: steps(4, end);
animation-timing-function: frames(10);
 
/* Multiple animations */
animation-timing-function: ease, step-start, cubic-bezier(0.1, 0.7, 1.0, 0.1);
 
/* Global values */
animation-timing-function: inherit;
animation-timing-function: initial;
animation-timing-function: unset;
```

| 值                            | 描述                                                        |
| ----------------------------- | ----------------------------------------------------------- |
| linear                        | 动画从开始到结束具有相同的速度。                            |
| ease                          | 动画有一个缓慢的开始，然后快，结束慢。                      |
| ease-in                       | 动画有一个缓慢的开始。                                      |
| ease-out                      | 动画结束缓慢。                                              |
| ease-in-out                   | 动画具有缓慢的开始和慢的结束。                              |
| cubic-bezier(*n*,*n*,*n*,*n*) | 在立方贝塞尔函数中定义速度函数。 可能的值是从0到1的数字值。 |

这里关于animation-timing-function值的其他几种类型如step-start、step-end、steps(n, start/end)等后面再讲

#### animation-delay

**定义**

> CSS属性定义动画开始于何时，即从动画应用在元素上到动画开始的这段时间

**说明**

1. 0s是该属性的默认值，代表动画在应用到元素上后立即开始执行。否则，该属性的值代表动画样式应用到元素上后到开始执行前的时间长度；
2. 定义一个正值m会让动画经过ns的延迟后，再开始运动
3. 定义一个负值n会让动画立即开始，开始的位置是元素运动的ns后的位置。例如，如果设定值为1s，动画会从它动画序列的第1s位置处立即开始。

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        @keyframes demo {
            to {
                left: 500px;
            }
        }
        #demo1, #demo2, #demo3 {
            position: absolute;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: red;
        }
        #demo1 {
            top: 0px;
            animation: demo 2s linear 0s;
        }
        #demo2 {
            top: 120px;
            animation: demo 2s linear 1s;
        }
        #demo3 {
            top: 240px;
            animation: demo 2s linear -1s;
        }
    </style>
</head>
<body>
    <div id="demo1">animation-delay: 0s</div>
    <div id="demo2">animation-delay: 1s</div>
    <div id="demo3">animation-delay: -1s</div>
</body>
</html>
```

#### animation-iteration-count

**定义**

> 定义动画在结束前播放的次数。可以是1次（默认）、多次、无限次。

**语法**

```
animation-iteration-count: infinite;
animation-iteration-count: 3;
animation-iteration-count: 2.3;
 
animation-iteration-count: 2, 0, infinite;
```

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        @keyframes demo {
            30% {
                width: 200px;
            }
            60% {
                width: 300px;
            }
            100% {
                width: 400px;
            }
        }
        #demo {
            width: 100px;
            height: 100px;
            background-color: red;
            animation: demo 3s linear 0s;
            animation-iteration-count: 1;
            /* animation-iteration-count: 2.5; */
            /* animation-iteration-count: infinite; */
        }
    </style>
</head>
<body>
    <div id="demo"></div>
</body>
</html>
```

#### animation-direction

**定义**

> 指示动画播放的方向

**语法**

```
animation-direction: normal
animation-direction: reverse
animation-direction: alternate
animation-direction: alternate-reverse
animation-direction: normal, reverse
animation-direction: alternate, reverse, normal
```



| 值                | 含义                                 |
| ----------------- | ------------------------------------ |
| normal（默认）    | 动画正向播放                         |
| reverse           | 反向播放动画，每周期动画由尾到头运行 |
| alternate         | 动画按照 “正反正反...”的顺序交替播放 |
| alternate-reverse | 动画按照 “反正反正...”的顺序交替播放 |

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        @keyframes demo {
            30% {
                width: 200px;
            }
            60% {
                width: 300px;
            }
            100% {
                width: 400px;
            }
        }
        #demo {
            width: 100px;
            height: 100px;
            background-color: red;
            animation: demo 3s linear 0s 3;
            animation-direction: normal;
            /* animation-direction: reverse; */
            /* animation-direction: alternate; */
            /* animation-direction: alternate-reverse; */
        }
    </style>
</head>
<body>
    <div id="demo"></div>
</body>
</html>
```

#### animation-play-state

**定义**

> 定义一个动画是否运行或者暂停。可以通过查询它来确定动画是否正在运行。另外，它的值可以被设置为暂停和恢复的动画的重放

**语法**

```
/* Single animation */
animation-play-state: running; /* 运行 */
animation-play-state: paused;  /* 暂停 */
 
/* Multiple animations */
animation-play-state: paused, running, running;
 
/* Global values */
animation-play-state: inherited;
animation-play-state: initial;
animation-play-state: unset;
```

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        @keyframes demo {
            to {
                width: 500px;
            }
        }
        #demo {
            width: 100px;
            height: 100px;
            background-color: red;
            animation: demo 3s linear 0s infinite normal;
        }
    </style>
</head>
<body>
    <div id="demo"></div>
    <button>running/paused</button>
    <script type="text/javascript">
        var oBtn = document.getElementsByTagName('button')[0],
            oDiv = document.getElementById('demo');
        oBtn.onclick = function () {
            oDiv.style.animationPlayState = window.getComputedStyle(oDiv, null)['animationPlayState'] == 'running' ? 'paused' : 'running';
            console.log(window.getComputedStyle(oDiv, null)['animationPlayState']);
        }
    </script>
</body>
</html>
```

#### animation-fill-mode

**定义**

> 指定在动画执行之前和之后如何给动画的目标应用样式

**语法**

```
animation-fill-mode: none
animation-fill-mode: forwards
animation-fill-mode: backwards
animation-fill-mode: both
 
/* 可以应用多个参数，这个时候使用逗号隔开  */
/* 各个参数应用于与次序相对应的动画名 */
animation-fill-mode: none, backwards
animation-fill-mode: both, forwards, none
```



| 值        | 含义                                   |
| --------- | -------------------------------------- |
| forwards  | 动画结束时，目标保持动画最后一帧的样式 |
| backwards | 动画执行前，应用关键帧第一帧的样式     |
| both      | 执行 forwards 和 backwards的动作       |

**注意**

1. 上述的第一帧有可能是0%也有可能是100%（正向播放、反向播放）
2. 对于backwards，动画采用第一帧的样式，保持 `animation-delay`

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        @keyframes demo {
            0% {
                left: 100px;
            }
            50% {
                left: 200px;
            }
            100% {
                left: 300px;
            }
        }
        #demo1, #demo2 {
            position: absolute;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: red;
        }
        #demo1 {
            top: 0px;
            animation: demo 2s linear 1s;
        }
        #demo2 {
            top: 120px;
            animation: demo 2s linear 1s backwards;
        }
    </style>
</head>
<body>
    <div id="demo1"></div>
    <div id="demo2"></div>
</body>
</html>
```

效果如下：

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft0bx76hmig30mn0c6q42.gif)

可以看到，如果对于没有使用backwards值的小方块（上），在其初始位置等待延迟；对于使用backwards值的小方块（下），先立即应用第一帧的样式，然后在该位置等待延迟

下面这个demo是测试forwards和both：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        @keyframes demo {
            0% {
                left: 100px;
            }
            50% {
                left: 200px;
            }
            100% {
                left: 300px;
            }
        }
        #demo {
            position: absolute;
            top: 0px;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: red;
            animation: demo 2s linear 1s forwards;
            /* animation: demo 2s linear 1s both; */
        }
 
    </style>
</head>
<body>
    <div id="demo"></div>
</body>
</html>
```

#### transition 和 animation的比较

**区别**

1. 触发条件不同

   transition 通常和hover等事件配合使用，由事件触发。animation 则和 gif效果差不多

2. 循环

   transition 是一次性的，除非反复的触发事件；而 animation可以设定循环，重复播放

3. 精确性

   animation 可以设定每一帧的样式和时间；transition 只能设定头尾；animation 中可以设置每一帧需要的单独变化的样式属性，transition 中所有样式属性要一起变化

4. 与JavaScript交互

   animation 与 js 的交互不是很紧密；transition 和 js 的结合更强大。js设定要变化的样式，transition 负责动画效果

**应用场景**

1. 如果要灵活定制多个帧以及循环，用animation
2. 如果要加单的from to 效果，用transition
3. 如果要使用js灵活设定动画属性，用transition

### 参考链接

[mdn]('https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation')

[css3 animation 属性众妙]('https://aotu.io/notes/2016/11/28/css3-animation-properties/index.html')