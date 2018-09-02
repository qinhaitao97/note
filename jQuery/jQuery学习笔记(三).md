### 事件

#### dom.click(function () {})

类似于这种形式，直接为 dom 元素绑定事件

#### on()

+ 语法

  dom.on(event, src, param, function() {});

+ 参数

  event: 需要绑定的事件

  src: 可以执行事件的事件源对象

  param: 需要向事件处理函数中传入的参数

  function: 事件处理函数

+ 实例讲解

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
      <style type="text/css">
          .wrapper {
              width: 300px;
              height: 300px;
              background-color: gray;
          }
          .inner1, .inner2 {
              width: 100px;
              height: 100px;
              background-color: green;
              margin-bottom: 20px;
          }
          .inner2 {
              background-color: orange;
          }
      </style>
  </head>
  <body>
      <div class="wrapper">
          <div class="inner1"></div>
          <div class="inner2"></div>
      </div>
      <script type="text/javascript">
          $('.wrapper').on('click', '.inner1', [1, 2, 3], function (e){
              console.log(e.target);
              console.log(e.data);
          });
      </script>
  </body>
  </html>
  ```

  详解：

  一共构造了三个 dom 元素，wrapper 和他的两个子元素 inner1、inner2，用on给父元素 wrapper 绑定了 'click' 事件；设置事件源对象是 '.inner1'，即只有 wrapper 下的 inner 被点击时才会触发该事件；将数组 [1,2,3] 作为参数传入事件处理函数 function；function 中打印了传入的参数 e.data 和 事件源对象

+ 注意

  事件源对象和传入参数这两个参数可以省略，当这两个参数都省略时没什么，但如果只有一个参数被省略掉时，这个参数的形式可能会引起歧义：如果参数不是字符串形式，那么这个参数会被当做第三个参数即传入参数来看待；如果参数是字符串，那这个参数会被当做事件源对象来看待

#### off()

+ 功能

  取消事件绑定

+ 语法

  dom.off(event, param1, param2...)

+ 参数

  event：需要解除绑定的事件

  param：精确定位某一事件的条件

+ demo

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
      <style type="text/css">
          .wrapper {
              width: 300px;
              height: 300px;
              background-color: gray;
          }
          .inner1, .inner2 {
              width: 100px;
              height: 100px;
              background-color: green;
              margin-bottom: 20px;
          }
          .inner2 {
              background-color: orange;
          }
      </style>
  </head>
  <body>
      <div class="wrapper">
          <div class="inner1"></div>
          <div class="inner2"></div>
      </div>
      <script type="text/javascript">
          $('.wrapper').on('click', '.inner1', [1, 2, 3], function (e){
              console.log(e.target);
              console.log(e.data);
          });
   
          function fn1() {
              console.log('fn1');
          }
   
          function fn2() {
              console.log('fn2');
          }
   
          $('.wrapper').on('click', '.inner2', fn1);
   
          $('.wrapper').on('click', '.inner2', fn2);
   
          // 取消wrapper下所有元素的事件
          // $('.wrapper').off('click');
   
          // 取消wrapper下事件源对象为 inner1 元素的事件
          // $('.wrapper').off('click', '.inner1');
   
          // 取消wrapper下事件源对象为 inner2，且处理函数为 fn1 元素的事件
          $('.wrapper').off('click', '.inner2', fn1);
   
          // 取消wrapper下事件源对象为 inner2，且处理函数为 fn2 元素的事件
          $('.wrapper').off('click', '.inner2', fn2);
      </script>
  </body>
  </html>
  ```

#### one()

+ 功能

  绑定一次性事件

+ 语法

  语法和 on() 相同

+ demo

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
      <style type="text/css">
          div {
              width: 100px;
              height: 100px;
              background-color: green;
          }
      </style>  
  </head>
  <body>
      <div></div>
      <script type="text/javascript">
          $('div').one('click', function () {
              console.log('执行了一次');
          });
      </script>
  </body>
  </html>
  ```

#### 事件对象

##### e.pageY / e.clientY / e.screenY

e.pageY：相对于文档顶部距离（和滚动条相关）

e.clientY：相对于可视区窗口顶部的距离（和滚动条无关）

e.screenY：相对于电脑屏幕顶部的距离（和浏览器的位置相关）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <style type="text/css">
        .null {
            height: 1500px;
        }
    </style>  
</head>
<body>
    <div class="null"></div>
    <script type="text/javascript">    
        $(window).click(function (e) {
            console.log(e.clientY);
            console.log(e.pageY);
            console.log(e.screenY);
        });
    </script>
</body>
</html>
```

##### e.which / e.button

which：对于键盘上的每一个按键都会返回一个值，以此来区分是哪个键；对于鼠标来说，左键的which值是1，右键是3，滚轮是2

button：对于鼠标的三个键，左键是0，右键是2，滚轮是1

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>  
</head>
<body>
    <input type="text">
    <script type="text/javascript">
        $(window).on('contextmenu', function (e) {
            e.preventDefault();
        });
        $('input').on('keydown', function (e) {
            console.log(e.which);
        });
        $('input').on('mousedown', function (e) {
            console.log(e.which);
            console.log(e.button);
        })
    </script>
</body>
</html>
```

##### e.preventDefault()

取消默认事件，jQuery已经封装好了它的兼容性

##### e.stopPropagation()

取消冒泡，jQuery已经封装好了它的兼容性

##### return false

可以取消默认事件，也可以取消冒泡

#### trigger()

+ 功能

  事件触发器，用来在指定的条件下触发事件

+ 用法

  trigger(event, data)

  event: 事件类型

  data: 参数数组，作为参数传递给要触发的事件处理函数

+ 自定义事件

  除了可以触发系统设定的事件外，还可以触发自定义事件

+ demo

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
      <style type="text/css">
          .demo {
              position: absolute;
              top: 0px;
              left: 0px;
              width: 100px;
              height: 100px;
              background-color: green;
          }
          button {
              margin-left: 100px;
          }
      </style>
  </head>
  <body>
      <div class="demo"></div>
      <button class="test1">点我也能触发demo的点击事件</button>
      <button class="test2">点我触发自定义的"move"事件</button>
      <script type="text/javascript">
          $('.demo').on('click', function (e, data1, data2) {
              console.log(data1);
              console.log(data2);
              console.log('触发了demo点击事件');
          });
          $('.test1').on('click', function () {
              $('.demo').trigger('click', ['11', '22']);
          });
   
          $('.demo').on('move', function () {
              console.log('触发了自定义的move事件');
              $(this).animate({top: '300px', left: '300px', opacity: '0.5'}, 1500);
          });
          $('.test2').on('click', function () {
              $('.demo').trigger('move');
          });
      </script>
  </body>
  </html>
  ```

  trigger 的第二个参数是用来向要被触发的事件处理函数传递参数，这里的第二个参数必须是数组的形式；而在事件处理函数接受这些参数时，不能一下接受一个数组，而是一个一个的接受

### 一些方法

#### scrollTop()

滚动条滚动出去的距离

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <style type="text/css">
        div {
            height: 1000px;
        }
    </style>  
</head>
<body>
    <div></div>
    <script type="text/javascript">    
        $(window).scroll(function () {
            console.log($(window).scrollTop());
        });
    </script>
</body>
</html>
```

利用这个方法可以实现 fixed 的效果（fixed在IE中的兼容性不好）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <style type="text/css">
        .null {
            height: 1500px;
            width: 1500px;
        }
        .demo {
            position: absolute;
            top: 100px;
            left: 100px;
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>  
</head>
<body>
    <div class="null"></div>
    <div class="demo"></div>
    <script type="text/javascript">    
        $(window).scroll(function () {
            $('.demo').css({top: $(window).scrollTop() + 100, left: $(window).scrollLeft() + 100});
        });
    </script>
</body>
</html>
```

 

#### width() / innerWidth() / outerWidth()

width()：content

innerWidth()：content + padding

outerWidth()：content + padding + border

outerWidth()：content + padding + border + margin

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <style type="text/css">
        .demo {
            margin: 20px;
            width: 100px;
            height: 100px;
            background-color: green;
            padding: 10px;
            border: 5px solid #000;
        }
    </style>  
</head>
<body>
    <div class="demo"></div>
    <script type="text/javascript">    
        console.log($('.demo').width());
        console.log($('.demo').innerWidth());
        console.log($('.demo').outerWidth());
        console.log($('.demo').outerWidth(true));
    </script>
</body>
</html>
```

#### offset().left/top / position().left/top

offset().left/top：元素相对于文档的坐标

position().left/top：元素相对于最近有定位的父级的坐标（没有就相对于文档）

#### parent() / offsetParent() / parents() / closest()

+ dom.parent(param)

  该 dom 元素的直接父元素，参数可以省略，如果加参数的话，意思是如果该 dom 元素的直接父元素满足参数指定特征才返回这个父元素，否则不返回

+ dom.offsetParent()

  返回距离该 dom 元素最近的有定位的父级元素

+ dom.parents(param)

  返回该 dom 元素所有父元素，可以加参数，结果根据参数再次筛选

+ dom.closest(param)

  返回在该 dom 元素所有的父级元素中，距离它最近的满足参数特征的元素

+ demo

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
   
      <div class="box1" style="position: absolute">
          <p class="box2">
              <span class="box3">
                  <em class="box5"></em>
              </span>
          </p>
      </div>
      <script type="text/javascript">
          console.log($('em').parent());
   
          console.log($('em').parent('box4'));
   
          console.log($('em').offsetParent());
   
          console.log($('em').parents());
   
          console.log($('em').closest('div'));
      </script>
  </body>
  </html>
  ```

  **这里有个问题，如果标签是这样的结构，那么对于这些方法都好理解，但是如果在 em 标签下面在添加一个 p 标签（与 em 标签同级），结果就完全不一样了，按理说与 em 同级的元素不会影响到 em 的父元素是谁啊，为什么会出现这样的结果**

#### val()

和原生 JS 中的 value 属性功能相同

#### each()

+ 功能

  循环遍历jQuery对象

+ 用法

  each(function(index, ele) {})

  这里类似于原生 js 中的 forEach 方法，但是注意回调函数中的参数顺序是先写 index，后写 ele，因为ele 是可写可不写的

+ demo

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
      </ul>
      <script type="text/javascript">
          $('li').each(function (index, ele) {
              console.log(index);
              console.log(ele);
          });
   
          $('li').each(function (index) {
              console.log(index);
              console.log(this);
          });
      </script>
  </body>
  </html>
  ```

  可以看到，每一次的 ele 都可以被 this 代替，所以一般 ele 可以省略掉，只需要用 index，所以 index 参数写在前面（jQuery 类似这种循环遍历的方法，参数的顺序都是这样的）

#### end()

+ 功能

  回退到上一次选择出来的 jQuery 对象

+ 好处

  方便链式调用

+ demo

  ul 下有4个 li，现在要把第二个设为红色，第三个设为绿色

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
      </ul>
      <script type="text/javascript">
          // 一般情况下我们是这样实现的，需要两行代码
          // $('li').eq(1).css('color', 'red');
          // $('li').eq(2).css('color', 'green');
   
          // 使用end() 方法，只需要一行代码
          $('li').eq(1).css('color', 'red').end().eq(2).css('color', 'green');
      </script>
  </body>
  </html>
  ```

+ preObject 属性

  使用上面的 end() 方法简化了代码，但是为什么 end() 具有这样的功能呢，jQuery 中怎么实现的？首先我们先来了解一下 preObject 属性

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
      </ul>
      <script type="text/javascript">
          console.log($('li').eq(1));
      </script>
  </body>
  </html>
  ```

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fr7ml8pxekj30cj07haa1.jpg)

  代码的功能是打印筛选出来的第二个 li，展开这个 li 对象，我们可以看到有一个 prevObject 属性，这个属性就是上一次被选中的 jQuery 对象（通过 $('li') 选中的），end() 方法就是访问这个属性实现回退功能的；每一个备选出来的 jQuery 对象都有这个属性，如果它是直接被选出来的（就像上面的 &('li')）那么他的 prevObject 属性是 document

#### add()

add() 方法是为了集中操作 dom 元素，方便链式调用

现在有两个 ul，每个 ul 下有4个 li，现在要把每个 ul 下的第一个 li 字体设为绿色

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>
    <ul class="first">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
    <ul class="last">
        <li>5</li>
        <li>6</li>
        <li>7</li>
        <li>8</li>
    </ul>
    <script type="text/javascript">       
        $('.first li').eq(0).add($('.last li').eq(0)).css('color', 'red');
    </script>
</body>
</html>
```

#### siblings() / prevAll() / nextAll() /  prevUntil() / nextUntil()

+ dom.siblings()

  该dom元素的所有兄弟元素

+ dom.prevAll()

  该dom元素前面的兄弟元素

+ dom.nextAll()

  该dom元素后面的兄弟元素

+ dom.prevUntil(param)  / dom.nextUntil(param)

  掐头去尾选中元素，传 jQuery 对象或者 dom

+ demo

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
          <li>5</li>
      </ul>
      <script type="text/javascript">
          // siblings()
          // $('li').eq(2).siblings().css('color', 'red');
   
          // prevAll()
          // $('li').eq(2).prevAll().css('color', 'red');
   
          // nextAll()
          // $('li').eq(2).nextAll().css('color', 'red');
   
          // prevUntil()
          // $('li').eq(2).prevUntil($('li').eq(0)).css('color', 'red');
   
          // nextUntil()
          // $('li').eq(2).nextUntil($('li').eq(4)).css('color', 'red');
      </script>
  </body>
  </html>
  ```

#### clone()

克隆节点，参数为 true 时还能克隆节点上的事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <style type="text/css">
        div {
            width: 100px;
            height: 100px;
            background-color: green;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="demo">点我查看有没有点击事件</div>
    <script type="text/javascript">
        $('div').click(function () {
            console.log('点击事件');
        });
 
        var oDiv1 = $('div').clone(),
            oDiv2 = $('div').clone(true);
 
        $('body').append(oDiv1).append(oDiv2);
    </script>
</body>
</html>
```

分别克隆得到的第二个和第三个方块，第二个没有点击事件，第三个有点击事件

#### wrap() / wrapInner() / wrapAll() / unwrap()

+ wrap()

  给选中的 jQuery 对象外面添加一层 wrapper，参数可以 function，用来进行筛选

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
      </ul>
      <script type="text/javascript">
          // 给所有的li添加一层p标签
          // $('li').wrap('<p>');
   
          // 给下标是3的倍数的li添加一层p标签
          // $('li').wrap(function (index) {
          //     if (index % 3 == 0) {
          //         return '<p>'
          //     }
          // });
      </script>
  </body>
  </html>
  ```

+ wrapInner()

  给选中的 jQuery 对象里面添加一层 wrapper，参数可以是 function 进行筛选

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
      </ul>
      <script type="text/javascript">
          // 给所有的li添加一层inner
          // $('li').wrapInner('<p>');
   
          // 给所有下标为3的倍数的li，添加一层inner
          // $('li').wrapInner(function (index) {
          //     if (index % 3 == 0) {
          //         return '<p>';
          //     }
          // });
      </script>
  </body>
  </html>
  ```

+ wrapAll()

  包裹选中的所有元素，一般不使用

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
      </ul>
      <script type="text/javascript">       
          $('li').wrapAll('<div>');
      </script>
  </body>
  </html>
  ```

  上面这个例子看起来就是给所有的li添加了一层 div，并没有体会到破坏结构的感觉，看下面这个例子

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <span></span>
          <li>3</li>
          <li>4</li>
      </ul>
      <li>5</li>
      <script type="text/javascript">       
          $('li').wrapAll('<div>');
      </script>
  </body>
  </html>
  ```

  改变后的 dom 结构

  ![](http://ww1.sinaimg.cn/large/006eYMu7gy1fr8acvwkj2j306s048742.jpg)

  可以看到，原来在 ul 外面的 li 被拿到了 ul 里面，原来 ul 里面的 span 被拿到了 ul 外面，破坏了原有的dom 结构

+ unwrap()

  解除包装，但是结构化的标签不能删除（html、body）

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
      </ul>
      <script type="text/javascript">       
          // 将所有li的包装ul解除了
          $('li').unwrap();
   
          // 结构化标签body不能解除
          $('li').unwrap();
      </script>
  </body>
  </html>
  ```

#### slice()

截取操作，算头不算尾

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
    <script type="text/javascript">       
        console.log($('li').slice(0,2));
    </script>
</body>
</html>
```

#### empty()

清空 jQuery 对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
    <script type="text/javascript">       
        // $('ul').empty();
 
        // 这样也可以实现
        // $('ul').html('');
    </script>
</body>
</html>
```

#### serialize() / serializeArray()

串联表单数据  / 串联数据成数组

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>
    <form action="">
        <input type="text" name="username">
        <input type="password" name="password">
        <input type="submit" value="提交">
    </form>
    <script type="text/javascript">       
        $('input').eq(2).click(function (e) {
            e.preventDefault();
            var str = $('form').serialize();
            console.log(str);
            var strArray = $('form').serializeArray();
            console.log(strArray);
        });
    </script>
</body>
</html>
```

### 创建dom元素

#### 直接创建

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <style type="text/css">
        .demo {
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>  
</head>
<body>
    <script type="text/javascript">    
        $('<div class="demo"></div>').appendTo($('body'));
    </script>
</body>
</html>
```

#### 单标签创建

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <style type="text/css">
        .demo {
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>  
</head>
<body>
    <script type="text/javascript">    
        $('<div class="demo">').appendTo($('body'));
 
        $('<p/>').appendTo($('.demo'));
    </script>
</body>
</html>
```

注意：

第二中单标签写法是 `<div/>` 而不是 `</div>`，且这种写法无法给标签直接写属性

 