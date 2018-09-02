### 3D变换

利用`transform: rotate();` 的一些列值可以实现3D变换的效果

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

**注意**

  1. 当元素进行旋转的同时，非旋转轴也会跟着元素一同进行旋转。比如 `rotateX(90deg);`，旋转结束后，旋转轴x方向不变水平向右，非旋转轴y轴和z轴分别垂直屏幕向外和竖直向上

  2. `transform: rotateX(45deg) rotateY(45deg) rotateZ(45deg);` 和 `transform: rotate3d(1, 1, 1, 45deg);` 的效果是不一样的：前者是有先后顺序，先沿x轴旋转，再沿y轴旋转，再沿z轴旋转；后者直接沿合成的轴进行旋转

     前者

     ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fskf5cjjlaj307304xt8h.jpg)

     后者

     ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fskf6abgc4j30ax066a9u.jpg)

### 保留3D效果

前面介绍了利用`transform` 可以实现一系列的3D变换效果，但是实际看来，好像并没有我们想象中的3D效果，都是一些平面效果，没错是这样的，因为虽然我们实现了3D变换的效果，但是在默认情况下，这个效果是展示在二维平面中的，如果想要看到3D的效果，就要设置保留3D效果，让元素再三维空间内展示，这就要用到下面的属性

**transform-style: preserve-3d**

+ **定义**

  为进行3D变换的元素保留3D效果，让其在三维空间内展示

+ **语法**

  `transform-style: flat(默认) | preserve-3d;`

  flat 是默认值，元素只能在二维平面内展示，看不到3D效果

+ **注意**

  + `transform-style: preserve-3d;` 要设置在实现了3D效果元素的**父元素（即舞台元素）**上使用
  + 要与 `transform` 属性一同使用
  + 设置了 `transform-style: preserve-3d` 的元素就不能为了防止子元素溢出而设置 `overflow: hidden;` 属性，该做法会导致 `preserve-3d` 失效

+ **demo**

  ```html
  <style>
      .wrapper {
          ......;
          transform: preserve-3d; /* 这个属性在父元素上设置 */
      }
      .wrapper .demo {
          .......;
          transform: rotateX(angle);
      }
  </style>
  ```


### 理解景深

首先来看一组设置了 `transform` 属性的元素，在二维平面和在三维空间的效果

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5obbnu3gj30dh055t8i.jpg)

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5obp35uaj30f306u0sk.jpg)

两组中三个子元素的3D变换操作分别是 `transform: rotateX(45deg);`，`transform: rotateY(45deg);`，`transform: rotateZ(45deg);`，但是很明显第一组看不出来3D效果，第二组才能看出来3D效果，那你可能想是不是第一组没有使用 `transform-style` 属性来保留3D效果，但可以明确说明的是，两组都设置了 `transform-stye` 属性来保留3D效果，那为什么第一组我们看不到3D效果呢，这就要介绍下一个属性**景深**

**定义**

> **景深**（DOF），是指在摄影机镜头或其他成像器前沿能够取得清晰图像的成像所测定的被摄物体前后距离范围。 而光圈、镜头、及拍摄物的距离是影响**景深**的重要因素。 在聚焦完成后，焦点前后的范围内所呈现的清晰图像，这一前一后的距离范围，便叫做**景深**。                       __百度百科

可以简单的把景深理解为人距离显示器的距离，此值的大小会决定你看物体的程度，比如距离100米和1米去看一个边长为1米的立方体的效果是不一样的（自行脑补）

**语法**

`transform: perspective(length);`

默认值是none，length代表景深的大小，单位是像素

**demo**

```html
<style>
    .wrapper {
        ......;
        transform: preserve-3d;
    }
    .wrapper .demo {
        .......;
        transform: perspective(length) rotateX(angle);
    }
</style>
```

### 视点

在理解了景深的后，介绍其语法之前我们先来了解另一个概念 "视点"

**定义**

简单的理解，视点就是我们观察物体的角度，默认位置在物体(x, y) (50%, 50%)的位置上，y的距离（即远近）可以自己调整

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5pcvvlv8j30ga077743.jpg)

**语法**

`perspective-origin: locX locY;`

locX, locY 表示视点在x轴，y轴上的距离，默认是50%，50%

这里的值可以是百分比、像素、关键词（center、top、left、bottom）

**demo**

不同视点看到的3D效果是不一样的

以元素沿x轴旋转为例，默认视点下，我们让物体旋转45度，效果如下

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5pkrfmw2j304h03udfl.jpg)

改变旋转的角度为90度，效果如下

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5pm5ws7pj30cj04o741.jpg)

我们发现，元素消失了，其实不是元素消失了，而是在当前视点下，我们看不到它了，想想一下，你的视线与在x轴与z轴构成的平面上且与x轴垂直，那么当元素沿x轴旋转90度以后，是不是就看不到了，那么如果我们想要看到它，可以调整视点，比如我们把视点调整到（center，top）的位置，效果如下

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5ppy66lfj306u04i3y9.jpg)

### 景深的两种写法

前面我们提到过一种设置景深的方法，是利用 `transform: perspective(length);` 来设置，除了这种方法外，还可以通过利用 `perspective: length;` 方法来设置景深，不同的是 `transform: perspective(length);` 设置在变换的子元素上，而 `perspective: length;` 设置在舞台元素上（形变元素的父元素），这两种设置方法所造成的不同，我们来讲解一下

现有一舞台元素，它有三个子元素均沿x轴旋转80度，默认视点

+ 在舞台元素上设置景深

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5qaegygpj308m0afgle.jpg)

+ 在子元素上设置景深

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5qdm5zzaj3065093t8h.jpg)

可以看到，元素发生的3D变换是相同的，但在舞台元素上设置景深和在子元素上设置景深的效果明显不一样，前者每一个子元素看起来好像都不一样，而后者所有子元素看起来都相同，其实这是视点不同而造成的问题

如果在舞台元素上设置景深，那么**视点就只有一个**，即在舞台元素（50%，50%）处，这个视点看第一个元素还正常，但是看下面的子元素就会是俯视的效果，所以看到的形状不同；而如果在子元素中设置景深，那么每一个元素都会拥有一个**单独的视点**，所以每一个看起来都是正视的效果

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5qt08udhj30n30bmwfd.jpg)

### backface-visibility

**定义**

在元素运动的过程中是否展示背面

**语法**

`backface-visibility: visible | hidden;`

### 性能优化

3D动画很消耗页面的性能，所以使用3D动画时要进行一些性能优化

+ 使用3D变形开启GPU加速

  GPU加速属于系统硬件能力，使用3D变化能开启GPU加速，提高性能

  ```css
  .demo {
  	......;
      /* bad */
      transform: rotateX(10deg);
      
  	/* good */
      transform: rotate3d(10deg, 0, 0);
  }
  ```

  但是一定要注意`transform: rotateX(45deg) rotateY(45deg) rotateZ(45deg);` 和 `transform: rotate3d(1, 1, 1, 45deg);` 的效果是不一样的，这一点之前就提到过

+ 尽可能的少用`box-shadow`，`text-shadow`，`gradient` 这些很消耗行呢的属性，他们被称为性能杀手，所以尽量减少使用

+ 尽可能让动画元素脱离文档流，以减少重排

### 注意点

1. 当元素进行旋转的同时，非旋转轴也会跟着元素一同进行旋转。比如 `rotateX(90deg);`，旋转结束后，旋转轴x方向不变水平向右，非旋转轴y轴和z轴分别垂直屏幕向外和竖直向上

   比如，现在有两个要进行3D变换的元素，两元素均沿x轴旋转，一个旋转90度，另一个旋转-90度，然后两元素均沿z轴平移100px，为了旋转90度以后能看到元素，我们把视点调到（center， top）的位置，想一下结果是什么效果

   ![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft5rwj1i5rj305f0af0sh.jpg)

   结果两个元素相差在竖直方向上相差了200px，此时的竖直方向是z轴的方向，因为元素进行西旋转的同时，坐标轴也跟着旋转了

2. 如果动画有闪烁，通常发生在动画开始的时候，可以尝试以下解决方法

   ```css
   -webkit-backface-visibility: hidden;
   -moz-backface-visibility: hidden;
   -ms-backface-visibility: hidden;
   backface-visibility: hidden;
   -webkit-perspective: 1000;
   -moz-perspective: 1000;
   -ms-perspective: 1000;
   perspective: 1000;
   ```

### demo

#### 3D透视旋转照片墙

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft65dxxqx8g30q30ct48f.gif)

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

        @keyframes rotate {
            from {
                transform: rotate3d(0, 1, 0, 0);
            }
            to {
                transform: rotate3d(0, 1, 0, 360deg);
            }
        }

        .wrapper {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 800px;
            height: 500px;
            /* border: 1px solid #000; */
            transform: translate(-50%, -50%);
            transform-style: preserve-3d;
            perspective: 1500px;
            perspective-origin: center top;
        }

        .wrapper ul {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate3d(-50%, -50%, 0);
            transform-style: preserve-3d;
            animation: rotate 3s linear infinite;
        }

        .wrapper ul li {
            position: absolute;
            width: 350px;
            height: 150px;
            opacity: 0.5;
            font-size: 30px;
            text-align: center;
            line-height: 150px;
        }

        .wrapper ul li:nth-child(1) {
            background-color: deeppink;
            transform: translate(-50%, -50%) rotate3d(0, 1, 0, 0) translate3d(0, 0, 323px);
        }

        .wrapper ul li:nth-child(2) {
            background-color: deepskyblue;
            transform: translate(-50%, -50%) rotate3d(0, 1, 0, 60deg) translate3d(0, 0, 323px);
        }

        .wrapper ul li:nth-child(3) {
            background-color: greenyellow;
            transform: translate(-50%, -50%) rotate3d(0, 1, 0, 120deg) translate3d(0, 0, 323px);
        }

        .wrapper ul li:nth-child(4) {
            background-color: purple;
            transform: translate(-50%, -50%) rotate3d(0, 1, 0, 180deg) translate3d(0, 0, 323px);
        }

        .wrapper ul li:nth-child(5) {
            background-color: orange;
            transform: translate(-50%, -50%) rotate3d(0, 1, 0, 240deg) translate3d(0, 0, 323px);
        }

        .wrapper ul li:nth-child(6) {
            background-color: red;
            transform: translate(-50%, -50%) rotate3d(0, 1, 0, 300deg) translate3d(0, 0, 323px);
        }
    </style>
</head>

<body>
    <div class="wrapper">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
        </ul>
    </div>
</body>

</html>

<!--
    1.只要子元素要实现3d效果，就要给其直接父级设置 transform-style: preserve-3d; 属性
    2.子元素要实现3d效果，不是要给每一个子元素的直接父级都设置 perspective，给最外层的那层父级设置即可
-->
```

#### 旋转立方体

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft67cd37d0g30bf0bxwks.gif)

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

        @keyframes rotate {
            form {
                transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
            }
            to {
                transform: rotateX(360deg) rotateY(360deg) rotateZ(360deg);
            }
        }

        .wrapper {
            position: relative;
            width: 300px;
            height: 300px;
            border: 1px solid #000;
            margin: 100px;
            transform-style: preserve-3d;
            perspective: 800px;
        }
        
        .wrapper ul {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 200px;
            height: 200px;
            margin-left: -100px;
            margin-top: -100px;
            transform-style: preserve-3d;
            animation: rotate 5s linear infinite;   
        }

        .wrapper ul li {
            position: absolute;
            top: 0%;
            left: 0%;
            width: 200px;
            height: 200px;
            font-size: 30px;
            text-align: center;
            line-height: 200px;
            opacity: 0.5;
            transform-style: preserve-3d;
        }

        .wrapper ul li:nth-child(1) {
            background-color: deeppink;
            transform: rotate3d(0, 0, 0, 0deg) translate3d(0, 0, 100px);
        }

        .wrapper ul li:nth-child(2) {
            background-color: deepskyblue;
            transform: rotate3d(0, 1, 0, 90deg) translate3d(0, 0, 100px);
        }

        .wrapper ul li:nth-child(3) {
            background-color: greenyellow;
            transform: rotate3d(0, 1, 0, 180deg) translate3d(0, 0, 100px);
        }

        .wrapper ul li:nth-child(4) {
            background-color: purple;
            transform: rotate3d(0, 1, 0, 270deg) translate3d(0, 0, 100px);
        }
        .wrapper ul li:nth-child(5) {
            background-color: orange;
            transform: rotate3d(1, 0, 0, 90deg) translate3d(0, 0, 100px);
        }

        .wrapper ul li:nth-child(6) {
            background-color: red;
            transform: rotate3d(1, 0, 0, -90deg) translate3d(0, 0, 100px);
        }

    </style>
</head>
<body>
    <div class="wrapper">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
        </ul>
    </div>
</body>
</html>
```
