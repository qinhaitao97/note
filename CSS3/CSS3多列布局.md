### 简介

> **CSS多栏布局** 扩展*块布局模式*，以便更容易地定义多列文本。如果 一行太长，人们阅读文本很麻烦; 如果眼睛从一行的终点移动到下一个行的开始需要太长时间，它们就会丢失它们所在的行。因此，为了最大限度地利用大屏幕，作者应该将宽度不等的文本列并排放置，就像报纸一样。
>
> 不幸的是，这是不可能的，使用CSS和HTML，而不是在固定位置强制列分栏，或严重限制文本中允许的标记，或使用英雄脚本。
>
> 糟糕的是如果不使用CSS和HTML在特定的位置强制换行，或者严格限制文本中允许的标记，或者夸张地使用脚本的话，这是不可能实现的。该限制通过从传统的块级布局模块中延伸出来的新的CSS属性得以解决

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft129vemczj30f207kwes.jpg)

### 属性

#### 总览

+ 列数和列宽

  column-count、column-width、columns

+ 列的间距和分列样式

  column-gap、column-rule-width、column-rule-style、column-rule-color、column-rule

+ 跨越列

  column-span

+ 填充列

  column-fill

+ 分栏符

  column-break-before、column-break-after、column-break-inside

#### 列数和列宽

##### column-count

**定义**

> 属性 `column-count` 设置特定数量的列数

**语法**

`column-count: auto || number;`

auto 是该属性默认值，当设置为auto时，元素分栏由其他元素决定，比如 `column-width`；number 是我们要设置的列数，用正整数表示

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        #demo1 {
            width: 500px;
            border: 1px solid #000;
            column-count: 2;
        }
        #demo2 {
            width: 500px;
            border: 1px solid #000;
            column-count: 3;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div id="demo1">
        <p>自己填充文本</p>
    </div>
    <div id="demo2">
        <p>自己填充文本</p>
    </div>
</body>
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft12ncdce2j30e90dk754.jpg)

##### column-width

**定义**

> 属性 column-width 设置期望的最小宽度。如果 column-count 没有设置，那么浏览器就会以合适的宽度尽量显示更多的列

这里来解释一下 “尽量展示更多的列”：假设父元素的宽度为 W，我们设置的列宽为 w，W 不一定能被 w整除，所以我们可能会想，W / w 向下取整就是浏览器能展示的最多的列，但实际情况是这样么？先来看一个例子

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        #demo1 {
            width: 500px;
            border: 1px solid #000;
            column-width: 250px;
        }
    </style>
</head>
<body>
    <div id="demo1">
        <p>自己填充文本</p>
    </div>
</body>
</html>
```

在这个demo中，W = 500px，w = 250px，W / w = 500 / 250 = 2，按照我们的预想，这里会显示两列布局，但实际效果是

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft13awbpqjj30ep06l3ys.jpg)

可以看到，只显示了一列布局，这是为什么呢？我们保持W = 500px 不变，逐渐的缩小 w 的值，当缩小到242px的时候，发现呈现了两列布局

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft13dmvuvkj30ep073t90.jpg)

仔细观察这个效果，发现除了我们预期的两列文字外，中间还有一列空白区域

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft13mn25xoj30ep072tzb.jpg)

就是这个空白区域占据了一定的宽度，导致结果与我们预想的效果不同，我们来计算一下这个空白区域的宽度：W / (w * 2) = 16px，有没有感觉这个16px很眼熟，没错是浏览器默认的字体大小，所以结论是：浏览器能显示的列数除了要看列宽之外，还要考虑列之间的间距，这个间距的大小取决于字体的大小

**PS：**即使是准确的算好了每一列的width，Opera下最好再减1个px，当然如果你是中文的话也最好这样做，减1-2px，至于为什么，只有opera能解释清楚。

**语法**

`column-width: auto || length;`

默认值是auto，当设置为 auto时，列宽由其他属性决定，比如 `column-count`；length 代表我们要设置的列宽，单位可以是 px 或者 em

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        #demo1 {
            width: 500px;
            border: 1px solid #000;
            column-width: 156px; /* (500 - 16*2) / 3 */
        }
    </style>
</head>
<body>
    <div id="demo1">
        <p>自己填充文本</p>
    </div>
</body>
</html>
```

![](http://ww1.sinaimg.cn/large/006eYMu7ly1ft13sndo51j30eg071glw.jpg)

##### columns

**定义**

> 多数时候，网页设计者都会使用 `column-count` 和 `column-width` 的一个. 由于它们的值没有重叠，一般使用简写属性 `columns`

**语法**

```
columns: 2;       /* column-count */
 
columns: 100px;   /* column-width */
 
columns: 2 100px; /* column-count column-width */
```

如果使用了第三种语法，则要注意，因为同时使用了两个属性，对于属性的复合效果要注意，即要知道最终的分栏效果是由哪个属性决定的，分为三种情况：

这里以一个具体的例子说明，不列公式了， 假设父元素的宽度为 500px，字体为默认大小16px

1. `columns: 2 100px;`

   意为分成两栏，每栏的宽度是 100px，经过计算（2 * 100 + 16 * 1 <= 500）结果有效，则可以分栏；我们让 `column-width: 100px;` 属性暂时固定，当 `column-count` 的值取 3、4时计算结果依然是有效的（3 * 100 + 16 * 2 < 500、4 * 100 + 16 * 3 <= 500），结果分别显示 3、4栏；同理，我们让 `column-count: 2;` 固定，当`column-width` 的值在有效范围内逐渐变换（经过计算，有效值范围在1px — 242px），这时显示的栏数始终是2栏；所以结论是

   > 当 `column-count` 与 `column-width` 的计算结果在有效范围内时，结果的分栏数取决于 `column-count` 属性

2. `columns: 3 242px;`

   意为分为三栏，每栏的宽度是242px，经过计算（3 * 242 + 16 * 2 > 500）结果无效，但是依然可以分栏，原因是虽然整体的计算结果无效，但是对于`column-width: 242px;` 属性来说，可以分为两栏（242 * 2 + 16 * 1 = 500），当我们逐渐的缩小 `column-width` 属性时，他会逐渐分成三栏、四栏...；所以结论是

   > 当 `column-count` 与 `column-width` 的计算结果不在有效范围内，且这个无效的结果是因为 `column-count` 的值太大导致的（即仅看`column-width` 属性的话，至少可以分为两栏），那么依然可以分栏，且分栏的结果取决于 `column-width`，与 `column-count` 无关

3. `columns: 3 250px;`

   意为分为三栏，每栏的宽度为250px，经过计算（250 * 3 + 16 * 2）结果无效，不能分栏；原因是这里整体结果无效，且根据 `columns-width` 属性也无法将结果至少分为两栏，所以整个属性无效，结果不能分栏

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        #demo1 {
            width: 500px;
            border: 1px solid #000;
            columns: 2 100px;
            /* columns: 3 100px; */
            /* columns: 4 100px; */
            /* columns: 5 100px; */
            /* columns: 3 242px; */
            /* columns: 3 250px; */
        }
    </style>
</head>
<body>
    <div id="demo1">
        <p>自己填充文本</p>
    </div>
</body>
</html>
```

#### 列的间距和分列样式

##### column-gap

**定义**

> 列之间的间距

**语法**

`column-gap: normal || length;`

默认值为normal，W3C建议值1em。length表示任何非负整数，单位可以是px、em、vw等

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        #demo1 {
            width: 500px;
            border: 1px solid #000;
            columns: 242px;
            column-gap:  normal;  /* 16px */
            /* column-gap: 17px; */
        }
    </style>
</head>
<body>
    <div id="demo1">
        <p></p>
    </div>
</body>
</html>
```

##### column-rule

**定义**

> 用来设置列与列之间边框的宽度、样式、颜色

**语法**

`column-rule: column-rule-width column-rule-style column-rule-color;`

其中 `column-rule-width`、`column-rule-style`、`column-rule-color` 代表三种不同的属性，可以单独设置

+ `column-rule-width`

  边框的宽度，默认值为none，类似于border-width属性

+ `column-rule-style`

  边框的样式，默认值为none，可以设置的值还有

  hidden || dotted || dashed || solid || double || groove || ridge || inset || outset

+ `column-rule-color`

  边框的颜色，类似于border-color属性，可以设置为透明色（transparent）

注意，**column-rule 所设置的边框不会占用空间位置**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        #demo1 {
            width: 500px;
            border: 1px solid #000;
            columns: 242px;
            column-gap:  normal;
            column-rule: 2px dashed red;
            /* column-rule: 30px dashed red; */  /* 并没有把盒子撑开，不占据空间位置 */
        }
    </style>
</head>
<body>
    <div id="demo1">
        <p>自己填充文本</p>
    </div>
</body>
</html>
```

#### 跨越列

##### column-span

**定义**

指定某个**子元素**跨越多少列

**语法**

`column-span: none/1 || all;`

+ none

  >  元素不跨多个列

+ all

  > 元素横跨所有列。元素出现之前，出现在元素之前的正常流中的内容在所有列之间自动平衡。该元素建立一个新的块格式上下文

**demo**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <style>
        #demo1 {
            width: 500px;
            border: 1px solid #000;
            columns: 242px;
            column-gap:  normal;
            column-rule: 2px dashed red;
        }
        h1 {
            /* column-span: none;  */  /* 不跨列 */
            column-span: all;
        }
    </style>
</head>
<body>
    <div id="demo1">
        <h1>标题</h1>
        <p>文本自己填充</p>
    </div>
</body>
</html>
```

#### 填充列

##### column-fill

 

#### 分栏符

##### column-break-before

##### column-break-after

##### column-break-inside

### 兼容性

注意不是所有的浏览器都支持不带前缀的属性名。为了在大多数现代浏览器中应用这种特性，每个属性必须写三次： 一次用 -moz 前缀，一次用 -webkit前缀，一次不使用前缀

```html
{
    -moz-column-count: 2;
    -webkit-column-count: 2;
    column-count: 2;
}
```
### 参考

[MDN]('https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Using_multi-column_layouts')

[浅谈CSS3多列布局]('http://imweb.io/topic/5828601d6f3c6d4940e525d5')