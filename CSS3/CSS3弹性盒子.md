### 弹性盒子简介

> CSS3弹性盒子是一种用于在页面上布置元素的**布局模式**，使得当页面布局必须使用不同的屏幕尺寸和不同的显示设备时，元素可预测的运行。对于许多应用程序，弹性盒子模型提供了对模型的改进，因为它不使元素浮动，flex容器的边缘也不会与其内容的边缘折叠

### 弹性布局

#### 基本概念

> 在定义方面来说，弹性布局是指通过调整其内元素的宽高，从而在任何显示设备上实现对可用显示空间最佳填充的能力。弹性容器扩展其内元素来填充可用空间，或将其收缩来避免溢出。
>
> 块级布局更侧重于垂直方向、行内布局更侧重于水平方向，与此相对的，弹性盒子布局算法是方向无关的。虽然块级布局对于单独一个页面来说是行之有效的，但其仍缺乏足够的定义来支持那些必须随用户代理(user agent)不同或设备方向从水平转为垂直等各种变化而变换方向、调整大小、拉伸、收缩的应用程序组件。 弹性盒子布局主要适用于应用程序的组件及小规模的布局，而（新兴的）栅格布局则针对大规模的布局。这二者都是 CSS 工作组为在不同用户代理、不同书写模式和其他灵活性要求下的网页应用程序有更好的互操作性而做出的更广泛的努力的一部分
>
> 弹性布局是一种一维布局模型，说它是一维布局模型是因为一个flexbox一次只能处理一个维度上的元素布局，一行或者一列。作为对比的是另外一个二维布局 网格布局，可以同时处理行和列上的布局

#### 浮动布局的问题

+ 难以控制

  如果站点上存在一些不可预知的内容，则布局将难以维护

+ 源码依赖性

  浮动布局依赖HTML源码，在做响应式布局时难以为不同的媒体查询变更布局

+ 列等高问题（**这个问题用column解决不就行了？**）

  如果容器中有两到三列不同的内容，并且在任意内容的条件下，都需要设置为相同的高度。浮动布局难以实现这个要求

+ 内容居中

  浮动布局中元素的居中方法繁多，相较繁琐

#### 弹性盒子如何处理

+ 通过将弹性元素拉伸或者缩小充满可用空间或者溢出，这种方式解决了新内容的溢出问题并且以开发者期望的情况实施布局
+ 给与弹性盒子元素成比例的尺寸
+ 弹性容器内的弹性元素可以从横、纵方向布局；可以解决在不同媒体查询中元素顺序问题，使得可见内容的顺序独立于HTML的渲染顺序，有利于站点的相应设计

#### 相关词汇

在学习弹性盒子强大的功能之前，我们先来了解一下该怎样描述弹性盒子，下图以一个 `flex-direction: row;` 的弹性容器为例进行描述

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft1ld3iu3qj30fn099t8t.jpg)

##### 弹性容器

包含弹性项目的父元素。通过设置 `display: flex;` 或者 `display: inline-flex` 来定义弹性容器

##### 弹性项目

弹性容器中的每一个子元素称为弹性项目。弹性容器中直接包含的文本元素被包覆成匿名弹性单元。

##### 轴

每个弹性框布局包含两个轴：弹性项目沿其一次排列的那一根叫做**主轴**；垂直于主轴的轴叫做**侧轴**或者**交叉轴**

##### 方向

弹性项目的**主轴起点**/**主轴终点**和**测轴起点**/**侧轴终点**描述了弹性项目排布的起点与终点。它们具体取决于弹性容器的主轴与侧轴中由 `writing-mode` 确立的方向

##### 行

根据 `flex-wrap` 属性，弹性项目可以排布在单个行或者多个行中

##### 尺寸

根据弹性容器的主轴与侧轴，弹性项目的宽和高中，对应主轴的称为**主轴尺寸**，对应侧轴的称为**侧轴尺寸**

### 定义一个弹性盒子

#### 语法

如果要指定一个盒子为弹性盒子，则需要给他指定CSS样式，按以下方式设置 `display` 属性

` display: flex;`

或者

`display: inline-flex;`

这样将元素定义为弹性容器，其子元素称为弹性项目。值 `flex` 使弹性容器称为块级元素，值 `inline-flex` 使弹性容器单个不可分的行内元素

#### 兼容

现代浏览器能够很好的支持flexbox，并且大多数浏览器不需要前缀，2个需要注意浏览器兼容的浏览器是：

> Internet Explorer 10：使用 -ms- 前缀；
>
> UC浏览器：使用 -webkit- 前缀

现在IE11已经支持 `display: flex;` 但是在使用时会有一些bug（不太清楚是什么bug）

所以一般考虑兼容只需要加上 -webkit- 前缀即可，如果要支持非常旧的浏览器，则在css中加入：

```html
<style>
    .wrapper {
        display: -webkit-box;
        display: -webkit-flex;
        display: -ms-flexbox;
        display: flex;
    }
</style>
```

#### 不影响弹性盒子的属性

由于弹性盒子采用了不同的布局算法，所以某些属性在弹性盒子上无效

+ 多栏布局模块的 `column-*` 属性对弹性项目无效
+ `float` 与 `clear` 属性对弹性项目无效。使用 `float` 将使元素的 `display` 属性记为 `block`
+ `vertical-align` 对弹性项目的对齐无效

### 弹性容器

```
+ flex-direction
+ flex-wrap
+ flex-flow
+ justify-content
+ align-items
+ align-content
```

#### flex-direction

**定义**

> `flex-direction` 属性通过设置容器主轴来定义弹性元素如何在容器内排列。这个属性确定了弹性元素的排列方向

**语法**

`flex-direction: row(默认) | row-reverse | column | column-reverse;`



|                | 主轴方向 | 侧轴方向 | 书写方向 | 起始线   | 终止线   | 元素排列方向 |
| -------------- | -------- | -------- | -------- | -------- | -------- | ------------ |
| row            | 水平反向 | 竖直方向 | 左->右   | 主轴左侧 | 主轴右侧 | 左->右       |
| row            | 水平方向 | 竖直方向 | 右->左   | 主轴右侧 | 主轴左侧 | 右->左       |
| row-reverse    | 水平方向 | 竖直方向 | 左->右   | 主轴右侧 | 主轴左侧 | 右->左       |
| row-reverse    | 水平方向 | 竖直方向 | 右->左   | 主轴左侧 | 主轴右侧 | 左->右       |
| column         | 竖直方向 | 水平方向 | 上->下   | 主轴上方 | 主轴下方 | 上->下       |
| column         | 竖直方向 | 水平方向 | 下->上   | 主轴下方 | 主轴上放 | 下->上       |
| column-reverse | 竖直方向 | 水平方向 | 上->下   | 主轴下方 | 主轴上方 | 下->上       |
| column-reverse | 竖直方向 | 水平方向 | 下->上   | 主轴上方 | 主轴现房 | 上->下       |

**表格解释**

如果选择了 `row` 或者 `row-reverse` ，主轴方向将沿水平方向延伸

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft28023wp4j30ei048jrc.jpg)

此时的侧轴垂直于主轴，方向沿竖直方向

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft2824e8u1j30ii03hgll.jpg)

如果选择 `column` 或者 `column-reverse` ，主轴方向沿竖直方向延伸

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft2837oogpj30jp06bq2z.jpg)

此时侧轴垂直于主轴，方向沿水平方向

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft2837oogpj30jp06bq2z.jpg)

以上描述只是说明了元素再什么方向上排列（水平方向或者竖直方向），但元素具体的排列方向是怎么样的呢？比如如果设置了 `flex-direction: row;` ，即主轴方向沿水平方向延伸，那元素是从左向右排列呢还是从右向左排列呢？这个就要取决于我们设置的书写方向了：书写方向是从左到右，则元素排列方向是从左到右；书写方向是从右到左，则元素排列方向是从右到左；`flex-direction: row-reverse;` 与之相反；`flex-direction: column;` 和 `flex-direction: column-reverse;` 道理相同

> 默认的排列方向是从左到右，从上到下

-> 改变元素的排列方向：[参考链接](http://yunkus.com/css-writing-mode-property/)

#### flex-wrap

**定义**

> `flex-wrap` 属性控制了容器为单行还是多行

**语法**

`flex-wrap: nowrap(默认) | wrap | wrap-reverse;`

+ no-wrap：单行显示
+ wrap：多行显示
+ wrap-reverse：多行显示，排列方向与 wrap 相反

设置了 `wrap` 值，如果项目太大而无法全部显示在一行中，则会换行显示；设置为 `nowrap`，如果项目过大，它们会缩小以适应容器，如果项目子元素无法缩小，使用 `nowrap` 会导致溢出，或者缩小的程度还不够

#### flex-flow

**定义**

`flex-direction` 和 `flex-wrap` 属性的简写

**语法**

`flex-flow: flex-direction || flex-wrap;`

默认值是：row nowrap；

#### justify-content

**定义**

> 用于在主轴上对齐伸缩项目。这一行为会在所有可伸缩长度及所有自动边距均被解释后进行。当一行上的所有伸缩项目都不能伸缩或者*可伸缩但是都已经达到其最大长度时*，这一属性才会对多余的空间进行分配。当项目溢出某一行时，这一属性也会在项目的对其上施加一些控制

**语法**

`justify-content: flex-start(默认) |flex-end | center | space-between | space-around | space-evenly;`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3bu9omx0j30dz07iglo.jpg)

+ flex-start

  伸缩项目向一行的起始位置靠齐，该行的第一个伸缩项目在起始线的外边距与起始线对齐，同时所有后续的伸缩项目与前一个项目对齐

+ flex-end

  伸缩项目向一行的结束位置靠齐，该行的最后一个伸缩项目在终止线的外边距与终止线对齐，同时所有前面的伸缩项目与其后一个项目对齐

+ center

  伸缩项目向一行的中间位置靠齐。该行的伸缩项目将相互对齐并在行中相互对齐。第一个项目距起始线的距离与最后一个项目距终止线的距离相同（如果剩余空间是负数，则保持两端溢出长度相等）

+ space-between

  伸缩项目会平均的分配在行里，如果剩余空间是负数或者该行只有一个伸缩项目，则此值等效于`flex-start`。在其他情况下，第一个项目在起始线的外边距与起始线对齐，最后一个项目在终止线的外边距与终止线对齐，而剩下的伸缩项目在确保两两之间的空白空间相等的情况下平均分布

+ space-around

  伸缩项目会平均地分布在行里，两端保留一半的空间。如果剩余空间是负数，或该行只有一个伸缩项目，则该值等效于center。在其它情况下，伸缩项目在确保两两之间的空白空间相等，同时第一个元素前的空间以及最后一个元素后的空间为其他空白空间的一半下平均分布

+ space-evenly

  flex项都沿着主轴均匀分布在指定的对齐容器中。相邻flex项之间的间距，主轴起始位置到第一个flex项的间距,，主轴结束位置到最后一个flex项的间距，都完全一样 

#### align-items

**定义**

> 可以设置弹性元素在容器侧轴上的对齐方式，与 `justify-content` 功能相似但是方向垂直。它设置弹性盒子所有子元素的对齐方式，包括匿名弹性元素。元素可以通过单独设置 `align-self` (后面讲) 来覆盖该属性

+ 对于匿名弹性元素，`align-self` 属性总是与 `align-items` 相同

+ 对于没有文字的弹性子元素来说它的基准线是它dom结构的最下部

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <title>Document</title>
      <style>
          .wrapper {
              display: flex;
              width: 400px;
              height: 300px;
              border: 1px solid #000;
              align-items: baseline;
          }
          .demo {
              width: 200px;
              height: 100px;
              border: 1px solid red;
              box-sizing: border-box;
              
          }
      </style>
  </head>
  <body>
      <div class="wrapper">
          <div class="demo">假装有字假装有字假装有字假装有字假装有字假装有字假装有字</div>
          <div class="demo"></div>
          <div class="demo">假装有字假装有字假装有字</div>
      </div>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3pdst65jj30bl08uq2q.jpg)

**语法**

`align-items: flex-start | flex-end | center | baseline | stretch(默认);`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3cmxaa8qj30e40af0st.jpg)

+ flex-start

  所有弹性项目在侧轴起始线的外边距与起始线对齐

+ flex-end

  所有弹性项目在侧轴终止线的外边距与终止线对齐

+ center

  所有伸缩项目在侧轴方向上的外边距距离起始线、终止线的距离相等（如果伸缩项目尺寸大于伸缩行尺寸，则伸缩项目两个方向的溢出量相同）

+ baseline

  如果伸缩项目的行内轴与侧轴为同一条，则该值和`flex-start`等效。其它情况下，该值将参与基线对齐。所有参与该对齐方式的伸缩项目将按下列方式排列：首先将这些伸缩项目的基线进行对齐，随后其中基线至侧轴起点边的外边距距离最长的那个项目将紧靠住该行在侧轴起点的边

  > 这里的基线指的是弹性项目内的第一行文本

+ stretch

  如果侧轴长度属性值是auto，则此值会使项目外边距盒的尺寸在遵照 min/max-width/height 属性的限制下尽可能接近所在行尺寸

#### align-content

**定义**

> 当伸缩容器的侧轴还有多余空间时，`align-content`属性可以用来调准伸缩行在伸缩容器里的对齐方式，这与调准伸缩项目在主轴上对齐方式的`justify-content`属性类似

注意：此属性在只有一行的伸缩容器上没有效果

**语法**

`align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch(默认);`

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3dig29ipj30gx0e10su.jpg)

+ flex-start

  各行向伸缩容器的起点位置堆叠。伸缩容器中第一行在侧轴起点的边会紧靠住伸缩容器在侧轴起点的边，之后的每一行都紧靠住前面一行

+ flex-end

  各行向伸缩容器的结束位置堆叠。伸缩容器中最后一行在侧轴终点的边会紧靠住该伸缩容器在侧轴终点的边，之前的每一行都紧靠住后面一行。

+ center

  各行向伸缩容器的中间位置堆叠。各行两两紧靠住同时在伸缩容器中居中对齐，保持伸缩容器在侧轴起点边的内容边和第一行之间的距离与该容器在侧轴终点边的内容边与第最后一行之间的距离相等。（如果剩下的空间是负数，则行的堆叠会向两个方向溢出的相等距离。）

+ space-between

  各行在伸缩容器中平均分布。如果剩余的空间是负数或伸缩容器中只有一行，该值等效于`flex-start`。在其它情况下，第一行在侧轴起点的边会紧靠住伸缩容器在侧轴起点边的内容边，最后一行在侧轴终点的边会紧靠住伸缩容器在侧轴终点的内容边，剩余的行在保持两两之间的空间相等的状况下排列

+ space-around

  各行在伸缩容器中平均分布，在两边各有一半的空间。如果剩余的空间是负数或伸缩容器中只有一行，该值等效于`center`。在其它情况下，各行会在保持两两之间的空间相等，同时第一行前面及最后一行后面的空间是其他空间的一半的状况下排列

+ stretch

  各行将会伸展以占用剩余的空间。如果剩余的空间是负数，该值等效于`flex-start`。在其它情况下，剩余空间被所有行平分，扩大各行的侧轴尺寸

**注意**

只有多行的伸缩容器才会在侧轴上有多余的空间以供对齐，因为仅包含一行的伸缩容器中，唯一的一行会自动伸展填充全部的空间

**align-items 和 align-content 的比较**

+ align-content强调**多行**元素在侧轴方向上**整体**的布局，align-items强调侧轴上**单行**元素的布局方式是怎么样的
+ 只有一行元素，align-content属性不起作用

对比下面两张图，图一代表`align-items` 属性值的效果，图二代表`align-content`属性值的效果，彩色部分代表弹性项目，可以看出图一每一个部分都在展示单独一行的对齐效果；而图二的每一部分在展示多行整体的对齐效果

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3cmxaa8qj30e40af0st.jpg)

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3dig29ipj30gx0e10su.jpg)

### 弹性项目

#### order

> `order` 属性通过将这些元素分配到序数分组来控制它们出现的顺序

排序规则：有最小值的项目排在第一个，若有多个相同的值，这些项目按照文件顺序排序

**语法**

`order: number;`

默认值：0

number值是整数（正、负、0）

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        .wrapper {
            display: flex;
            width: 300px;
            height: 100px;
            border: 1px solid #000;
        }
        .demo {
            width: 75px;
            height: 50px;
            border: 1px solid red;
            box-sizing: border-box;
        }
        .wrapper .demo:nth-child(1) { order: 2; }
        .wrapper .demo:nth-child(2) { order: -1; }
        .wrapper .demo:nth-child(3) { order: 0; }
    </style>
</head>
<body>
    <div class="wrapper">
        <div class="demo">1</div>
        <div class="demo">2</div>
        <div class="demo">3</div>
    </div>
</body>
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3e5gccekj309n03e0n1.jpg)

#### flex

> `flex` 是 `flex-flow`，`flex-shrink`，`flex-basis` 三个属性的简写

+ 第二个和第三个参数是可选值，默认值是 `flex: 0 1 auto`
+ `flex: none` 与 `flex: 0 0 auto;` 等效
+ 注意 `flex-grow` 与 `flex-basis` 的初始值与它们在 `flex` 简写被省略时的默认值不同。这里的设计是为了让 `flex` 简写在最常见的情景下比较好用

在具体学习  `flex-flow`，`flex-shrink`，`flex-basis` 三个属性之前，先来了解一些概念

+ min-content / max-content

  https://www.zhangxinxu.com/wordpress/2016/05/css3-width-max-contnet-min-content-fit-content/

+ 正负自由空间

  Flex 布局中有flex容器和flex子元素， flex子元素包含在flex容器中， 那么当flex子元素在主轴上的尺寸（大小）之和小于flex容器 的尺寸时， flex容器中就会有多余的空间没有被填充， 这些空间就被叫做 **positive free space**。当flex子元素在主轴上的尺寸之和大于flex容器的尺寸时， flex容器的空间就不够用，此时flex子元素的尺寸之和减去flex容器的尺寸（flex 子元素溢出的尺寸）就是**negative free space**, 这个negative free space加上flex容器的尺寸刚好可以容纳flex子元素 

##### flex-grow

当flex容器中存在 positive free space 时，如果想要消除这部分空间，则需要把这些空间转移到flex项目身上，而`flex-grow` 属性是用来确定每个flex项目所分配空间的比例

**语法**

`flex-grow: number;`

number是非负整数，默认值是0

**计算方法**

某一flex项目负责消除positive free space空间的比例的计算方法：

该项目的`flex-grow` 属性值 **除以** 所有参与分配的flex项目的 `flex-grow` 值的总和

**实例解释**

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3h59r8d6j30jo06dmxb.jpg)

图中的 positive free space 就是我们要分配给三个flex项目的空间，看以下几种情况：

+ 三个flex项目都不设置`flex-grow` 属性

  都不设置，按照默认值来，默认值是0，所以flex1，flex2，flex3分配到的负责消除的空间是

  100px * (0 / (0 + 0 + 0))

  结果如下图：

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3hruxfewj30eg07n0sq.jpg)

  因为他们分配到的空间都是0 ，所以默认情况下是不对剩余空间进行分配的

+ 三个flex项目 `flex-grow: 1;`

  三个flex的值相同，所以计算方法相同，每个flex项目负责分配的空间是

  100px * (1 / (1 + 1 + 1))

  结果如下图

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3htfrv3ij30cp07cglo.jpg)

  这种情况中，三个flex项目positive free space 均分了，注意如果这里三个 `flex-grow` 的值均为2或者均为100，结果和1是一样的，因为这个值是用来计算比例的，看的是他们之间的比例关系

+ 三个flex项目分别是 `flex-grow: 1;` ，`flex-grow: 2;`，`flex-grow: 3`

  flex1项目分配空间：100px * (1 / (1 + 2 + 3))

  flex2项目分配空间：100px * (2 / (1 + 2 + 3))

  flex3项目分配空间：100px * (3 / (1 + 2 + 3))

  结果如图：

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3hx87xn9j30dc072q2x.jpg)

> 在所有flex项目中，只要有一个flex项目的`flex-grow` 属性不为0，则positive free space就会被分配掉（没有剩余空间）

##### flex-shrink

当flex容器中存在 negative free space 时，如果想要消除这部分空间，则需要从每个flex项目身上减掉一些他们原来的空间，而`flex-shrink` 属性是用来确定每个flex项目所分配空间的比例

**语法**

`flex-shrink: number;`

number是非负整数，默认值是1

默认值是1，也就是说，在默认情况下flex 项目不会溢出容器，因为按照默认情况，一旦溢出，negative free space这部分就被等比例的拆分成n份，n个flex项目各减掉一份的大小

**实例解释**

与 `flex-shrink` 的用法功能相同，对比理解即可

##### flex-basis

> flex-basis 属性在任何空间分配发生之前初始化flex子元素的尺寸

**语法**

`flex-basis: auto(默认) | content | length;`

此属性的初始值为 `auto`. 如果 `flex-basis` 设置为 `auto` , 浏览器会先检查flex子元素的主尺寸是否设置了绝对值再计算出flex子元素的初始值. 比如说你已经给你的felx子元素设置了200px 的宽，则200px 就是这个flex子元素的 `flex-basis`.

如果你的flex子元素 为自动调整大小， 则`auto` 会解析为其内容的大小.  此时你所熟知的min-content和max-content大小会变得有用,  flexbox 会将flex子元素的 `max-content` 大小作为 `flex-basis`. 

除了关键字 `auto` 以外, 你还可以使用关键字 `content` 作为 `flex-basis`的值. 这会导致 `flex-basis` 根据内容大小设置即使flex子元素 设置了宽度. 这是一个新关键字而且获得浏览器支持的比较少, 但是你还是可以通过设置`flex-basis: auto`并确保你的flex子元素没有设置宽度来达到相同的效果 , 以便它能自动调整大小.

length代表整非负长度值，单位可以是px、em等

空间分配时， 如果你想flexbox 完全忽略flex子元素的尺寸就设置`flex-basis` 为 `0`. 这基本上告诉flexbox所有空间都可以抢占，并按比例分享.

**demo**

继续使用前面`flex-grow`中的例子，对于第三种情况（ `flex-grow: 1;` ，`flex-grow: 2;`，`flex-grow: 3`），我们让每个盒子所承担的 positive free space 的比例是1:2:3，但是最终分配完成后他们的比例不是1:2:3（显然a+m: a+2m:a+3m 不是1:2:3），如果我们想让分配结果是1:2:3的关系，可以将`flex-basis` 属性设为0，这样分配的比例即为最终每个flex元素所占的比例

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3kn84n9wj30cf0350m3.jpg)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        .wrapper {
            display: flex;
            width: 400px;
            height: 100px;
            border: 1px solid #000;
        }
        .demo {
            width: 200px;
            height: 50px;
            border: 1px solid red;
            box-sizing: border-box;
            flex-basis: 0px;
        }
        .wrapper .demo:nth-child(1) { flex-grow: 1;}
        .wrapper .demo:nth-child(2) { flex-grow: 2;}
        .wrapper .demo:nth-child(3) { flex-grow: 3;}
    </style>
</head>
<body>
    <div class="wrapper">
        <div class="demo">1</div>
        <div class="demo">2</div>
        <div class="demo">3</div>
    </div>
</body>
</html>
```

> 实际 coding 中，建议使用 `flex` 简写 `flex-grow`，`flex-shrink`，`flex-basis`三个属性，而不是单独设置这些属性

#### algin-self

**定义**

> `align-self` 用来在单独的伸缩项目上覆写默认的对齐方式

**语法**

`align-self: auto(默认) | flex-start | flex-end | center | baseline | stretch;`

如果`align-self`的值为`auto`，则其计算值为元素的父元素的`align-items`值，如果该元素没有父元素，则计算值为`stretch`

### flex典型布局

#### 三栏布局

> 左右两栏固定，中间自适应

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft3r8t57fnj312r0bkwel.jpg)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        html,body {
            display: flex;
            width: 100%;
            height: 100%;
            margin: 0px;
            padding: 0px;
        }
        .left, .right {
            width: 200px;
            height: 100%;
            background-color: pink;
        }
        .center {
            min-width: 200px;
            height: 100%;
            background-color: orange;
            flex-grow: 1;
        }
    </style>
</head>
<body>
    <div class="left"></div>
    <div class="center"></div>
    <div class="right"></div>
</body>
</html>
```

### 参考链接

https://www.w3.org/TR/css-flexbox-1/#justify-content-property

[使用CSS弹性盒子](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)

[flex布局的基本概念](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)

[使用弹性盒子进行高级布局](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Mixins)

[沿主轴控制Flex子元素的比例](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Controlling_Ratios_of_Flex_Items_Along_the_Main_Ax)

https://www.w3cplus.com/css3/a-guide-to-flexbox-new.html