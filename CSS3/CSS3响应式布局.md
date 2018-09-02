### 定义

> 随着越来越多的用户使用移动设备来浏览网站和应用，Web设计人员和开发人员需要确保他们的作品在移动设备上同样能正常运作，并且看上去和在传统台式电脑上一样好，这种方法被称为“响应式 Web 设计”。 

### 优劣势

**优势**

+ 无需为不同的设备维护不同的网站，节省了时间和成本
+ 响应式设计为每一个页面提供了一个单独且独有的URL
+ 社会化分享统计不会被割离开，因为移动端和PC端用的是一个URL
+ 响应式设计无需考虑用户代理检测

**劣势**

兼容各种设备时所需工作量大、效率低下、代码累赘，会隐藏无用的元素，加载时间延长，其实这是一种折中性质的十设计解决方案，由于多方面元素影响而达不到最佳效果，在一定程度上改变了网站原有的布局结构，会出现用户混淆的情况。 

### 策略

- 流式布局

   按照浏览器视窗的百分比来设定所有容器的宽度，从而使容器在浏览器窗口大小变化时自动缩放。

- 媒体查询

   基于显示设备的物理特性（例如：尺寸、分辨率、宽高比、颜色位深等）来调用不同的样式表。

- 流式图片

  设置图像所占宽度至多为设备的最大宽度

### 技术

+ Media Query（媒体查询）

  用于查询设备是否满足某一个特定的条件，这些特定条件包括屏幕尺寸，是否可触摸，屏幕精度，横屏竖屏信息等

+ 使用 em 或者 rem 做尺寸单位

  用于文字大小的响应和弹性布局

+ 禁止页面缩放

  `<meta name="viewport" content="initial-scale=1, width=device-width, maximum-scale=1, user-scalable=no" />`

+ 屏幕尺寸响应

  + 固定布局

    页面居中，两边留白，他能适应大于某个值一定范围的宽度，但是如果太宽就会有很多留白，太窄会出现滚动条，在PC页面上很常见 

  + 流动布局

    屏幕尺寸在一定范围内变化时，不改变模块布局，只改变模块尺寸比例。比固定布局更具响应能力，两边不留白，但是也只能适应有限的宽度变化范围，否则模块会被挤（拉）得不成样子 

  + 自定义布局

    上面几种布局方式都无法跨域大尺寸变化，所以适当时候我们需要改变模块的位置排列或者隐藏一些次要元素 

  + 栅格布局

    这种布局方式使得模块之间非常容易对齐，易于模块位置的改变用于辅助自定义布局 

### 注意

1. 宽度不固定可以使用百分比

2. 图片处理

   图片的宽度和高度设置等比缩放，可以设置图片的width为百分比，height:auto;背景图片可以使用background-size 指定背景图片的大小

### meta标签

meta标签用来规定内容视区大小与设备大小的关系，下面简单介绍用法及含义，详细讲解参考[文章](https://blog.csdn.net/u012402190/article/details/70172371)

如果要做不同设备的响应式设计，要在程序\<head>标签中加入\<meta>标签

`<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no"> `

+ name

  name="viewport" 代表内容可视区

+ content

  > viewport代表内容可视区，其大小可以大于或者小于设备可视区的大小，在做响应式设计时，要规定他们之间的大小关系，通过content中的属性

  

  | content       | 含义                                                         |
  | ------------- | ------------------------------------------------------------ |
  | width         | 内容可视区的宽度，其值可以是关键词"device-width"或者一个具体的数字 |
  | height        | 内容可视区的高度，其值可以是关键词"device-width"或者一个具体的数字 |
  | initial-scale | 页面首次被显示时内容可视区的缩放级别，取值为1.0时将使页面按照实际尺寸显示，无任何缩放 |
  | minimum-scale | 内容可视区最小的缩放级别，表示用户可以将页面缩小的程度，取值为1.0时将禁止用户缩小到实际尺寸以下 |
  | maximum-scale | 内容可视区最大的缩放级别，表示用户可以将页面放大的程度，取值为1.0时将禁止用于放大尺寸至实际尺寸以上 |
  | user-scalable | 指用户是否可以对页面进行缩放，设置 "yes" 允许缩放，设置 "no" 禁止缩放 |

### Media Query（媒体查询）

#### 简介

> 媒体查询是向不同设备提供不同样式的一种方式，它为每种类型的用户提供了最佳的体验

CSS2 中提供了 "media type" 媒体类型，我们可以对不同的设备指定不同的样式，但通过媒体类型我们只能简单的区分设备，功能单一，所以在CSS3中对提供了"media query"，它是对"media type"的增强，等于 "media type" + "media features"(媒体特性)

#### 语法

`media="(逻辑操作符) 媒体类型 逻辑操作符 零个或多个表达式"`

**媒体类型**



| 媒体类型   | 所有设备                                 |
| ---------- | ---------------------------------------- |
| all        | 所有设备                                 |
| braille    | 盲文                                     |
| embossed   | 盲文打印                                 |
| handheld   | 手持设备                                 |
| print      | 文档打印或者打印预览模式                 |
| projection | 项目演示，比如幻灯片                     |
| screen     | 彩色电脑屏幕                             |
| speech     | 演讲                                     |
| tty        | 固定字母间距的网格的媒体，比如电传打字机 |
| tv         | 电视                                     |

> 一般用 screen 和 all 比较多一点

**逻辑操作符**

> 你可以使用逻辑操作符，包括`not`、`and`和`only`等，构建复杂的媒体查询。`and`操作符用来把多个媒体属性组合成一条媒体查询，对成链式的特征进行请求，只有当每个属性都为真时，结果才为真。`not`操作符用来对一条媒体查询的结果进行取反。`only`操作符仅在媒体查询匹配成功的情况下被用于应用一个样式，这对于防止让选中的样式在老式浏览器中被应用到。若使用了`not`或`only`操作符，必须明确指定一个媒体类型
>
> 你也可以将多个媒体查询以逗号分隔放在一起；只要其中任何一个为真，整个媒体语句就返回真。相当于`or`操作符。

**not 和 only 应用于整个语法，所以要写在最开头**

```
<link rel="stylesheet" media="not screen and (color)" href="example.css" />
```

```
<link rel="stylesheet" media="only screen and (color)" href="example.css" />
```

**样式表达式**

> 表达式需要用圆括号。没有使用的会引起错误 

用来描述一系列媒体特性，常用的媒体特性如下

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft4w9eyy3zj30e30fk3zx.jpg)

#### 使用

**link标签引入**

`<link rel="stylesheet" media="screen and (max-width: 800px)" href="./index.css"> `

- "screen" 代表 "media type"，"(max-width: 800px)" 代表 "media features" ，整个媒体查询意为 "类型是screen，且设备的宽度不超过800px的媒体"，整个link标签意为 "当满足媒体查询的要求时，才引入 index.css 文件"

**@import引入**

+ 样式文件中通过@import调用别一个样式文件

  ```css
  @import url("example.css") screen and (max-width: 800px); 
  ```

+ 标签中调用

  ```html
  <head>
      <style>
          @import url("example.css") sreen and (max-width: 800px);
      </style>
  </head>
  ```

**@media引入**

+ 在\<head>的\<style>标签中使用

  ```html
  <head>
      <style>
          @media not screen and (max-width: 800px) {
              div {
                  display: none;
  		    }
          }
      </style>
  </head>
  ```

+ css文件中使用

  ```css
  @media all and (max-width: 800px) and (min-width: 600px) {
      ......
  }
  ```

> 实际开发中，最后一种是最常用的

**demo**

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft4x3c9443g311h0bb141.gif)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./index.css">
    <title>Document</title>
</head>
<body>
    <div class="demo"></div>
</body>
</html>
```

index.css文件

```css
.demo {
    width: 100px;
    height: 100px;
    background-color: #000;
}

@media all and (max-width: 500px) {
    .demo {
        background-color: green;
    }
}

@media all and (min-width: 501px) and (max-width: 700px) {
    .demo {
        background-color: red;
    }
}

@media all and (min-width: 900px) {
    .demo {
        background-color: orange;
    }
}
```
