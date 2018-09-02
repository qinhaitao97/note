### 选择元素

+ 基本形式

  jQuery 选取元素的基本形式是 ---  $();

  '$' 是 'jQuery' 的代替符号，为了更方便书写，jQuery() 就是函数调用

  ()里面可以填写我们想要选取的元素（参数），这个元素允许的形式有很多，在下面介绍；

  通过这种方法选取出来的结果是一个类数组（返回值），这个类数组对象继承的是 jQuery 原型上的方法；

  对于被选取出来的一组元素，jQuery 是一起处理的，省略了循环，这在 js 中是不允许的;

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Document</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>      
      <div class="wrapper">
          <p id="text"></p>
      </div>
      <div class="wrapper"></div>
      <script type="text/javascript">
          $('div').css({width: '100px', height: '100px', backgroundColor: 'green', margin: '5px'});
      </script>
  </body>
  </html>
  ```

  上面这个 demo 体现了统一处理的效果：选取出来一组 dom 元素，没有进行循环遍历，直接对所有的元素赋予样式

+ () 中可以填写元素的形式（参数）

  + css 选择器

    即我们在 css 中选取元素的写法也可以在这里使用

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script src="./js/jquery-3.3.1.js"></script>
    </head>
    <body>      
        <div class="wrapper">
            <p id="text"></p>
        </div>
        <div class="wrapper"></div>
        <script type="text/javascript">
            // 标签选择器
            console.log($('div'));
     
            // 类选择器
            console.log($('.wrapper'));
     
            // ID选择器
            console.log($('#text'));
     
            // 父子选择器
            console.log($('div > p'));
        </script>
    </body>
    </html>
    ```

    > 因为使用 css 选择器选择元素的写法有些复杂(可能会很长)，所以 jQuery 单独封装了一个函数 "sizzle"，用来选择 dom 元素，sizzle 方法中使用正则匹配的方法查找 dom 元素，效率很高；为了给有些在开发中只需要选择 dom 元素的开发者提供便利，sizzle 也单独封装成了一个类库 sizzle.js，如果开发的功能只需要使用到选择 dom 元素，那么直接引入 sizzle.js 即可

  + dom 元素

    一些已经在 js 中被选取出来的 dom 元素，也可以被 jQuery 选取

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script src="./js/jquery-3.3.1.js"></script>
    </head>
    <body>      
        <div class="wrapper">
            <p id="text"></p>
        </div>
        <div class="wrapper"></div>
        <script type="text/javascript">
            var oDiv = document.getElementsByTagName('div'),
                oP = document.getElementById('text');
     
            console.log($(oDiv));
            console.log($(oP));
        </script>
    </body>
    </html>
    ```

    因为在 jQuery 中可以对被选择出来的对象进行统一的操作而不需要进行遍历，这在原生 js 中是不允许的，所以可以利用 jQuery 获取在原生 js 中被选取的 dom 元素，然后进行统一操作；

    **这个方法可以用来将原生的 dom 元素转换成 jQuery 对象**

  + null / undefined

    使用 null 或者 undefined 等选取元素，返回一个空的类数组

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>jQuery</title>
        <script src="./js/jquery-3.3.1.js"></script>
    </head>
    <body>
        <script type="text/javascript">
            console.log($(null));
            console.log($(undefined));
        </script>
    </body>
    </html>
    ```

  + function(){}

    如果 $() ; 选中了一个函数，那么他会把这个函数立即执行一次

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>jQuery</title>
        <script src="./js/jquery-3.3.1.js"></script>
    </head>
    <body>
        <script type="text/javascript">
            $(function (){
                console.log('jQuery');
            });
        </script>
    </body>
    </html>
    ```

  + 两个参数

    $('被选取的元素', '被选取元素的执行期上下文');

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>jQuery</title>
        <script src="./js/jquery-3.3.1.js"></script>
    </head>
    <body>      
        <div class="wrapper">
            <p id="text"></p>
        </div>
        <div class="demo">
            <p></p>
        </div>
        <script type="text/javascript">
            console.log($('p', '.demo'));
        </script>
    </body>
    </html>
    ```

    这里我们想选择类名为 "demo" 的 div 下的 p 标签，所以我们想选择的元素就是 p , 它的执行期上下文就是 .demo

  + 特殊选择方法

    可以按照索引选择一组相同元素中的元素

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
            <li id="1">1</li>
            <li id="2">2</li>
            <li id="3">3</li>
            <li id="4">4</li>
            <li id="5">5</li>
        </ul>
        <script type="text/javascript">
            // 选择ul下的第一个 li
            console.log($('ul>li:first'));
            // 选择ul下的最后一个 li
            console.log($('ul>li:last'));
            // 选择ul下的索引为3的 li（索引是从0开始的）
            console.log($('ul>li:eq(3)'));
            // 选择ul下的索引为偶数的li
            console.log($('ul>li:even'));
            // 选择ul下的索引为奇数的li
            console.log($('ul>li:odd'));
        </script>
    </body>
    </html>
    ```

+ 经过上面的一系列选取方法，最终筛选出一个 dom 类数组，这个类数组还有一些方法可以对结果进行进一步的筛选

  + filter()

    参数可以是字符串或者是函数

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
            <li id="1">1</li>
            <li id="2">2</li>
            <li id="3">3</li>
            <li id="4">4</li>
            <li id="5">5</li>
        </ul>
        <script type="text/javascript">
            var oLi1 = $('li').filter('#1'),
                oLi2 = $('li').filter('[id=2]'),
                oLi3 = $('li').filter(function (index) {
                    if (index % 3 == 0) {
                        return true;
                    }
                });
     
            console.log(oLi1);
            console.log(oLi2);
            console.log(oLi3);
        </script>
    </body>
    </html>
    ```

  + not()

    语法与 filter() 相同，筛选的结果与 filter() 相反

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
            <li id="1">1</li>
            <li id="2">2</li>
            <li id="3">3</li>
            <li id="4">4</li>
            <li id="5">5</li>
        </ul>
        <script type="text/javascript">
            var oLi1 = $('li').not('#1'),
                oLi2 = $('li').not('[id=2]'),
                oLi3 = $('li').not(function (index) {
                    if (index % 3 == 0) {
                        return true;
                    }
                });
     
            console.log(oLi1);
            console.log(oLi2);
            console.log(oLi3);
        </script>
    </body>
    </html>
    ```

  + has()

    筛选某一个元素包含某些特征的子元素（特征可以是标签名、类名、ID名、属性等）

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
            <li id="1">1</li>
            <li id="2">2</li>
            <li id="3">
                <p id="pp">3</p>
            </li>
            <li id="4">4</li>
            <li id="5">5</li>
        </ul>
        <script type="text/javascript">
            var oLi = $('li').has('p'),
                oLi2 = $('li').has('[id=pp]');
            console.log(oLi);
            console.log(oLi2);
        </script>
    </body>
    </html>
    ```

  + find()

    上一个 has() 筛选的是子元素拥有某些特征的父元素，而这个 find() 是直接找到拥有这些特征的子元素

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
            <li id="1">1</li>
            <li id="2">2</li>
            <li id="3">
                <p id="pp">3</p>
            </li>
            <li id="4">4</li>
            <li id="5">5</li>
        </ul>
        <script type="text/javascript">
            var oLi = $('li').find('p'),
                oLi1 = $('li').find('#pp');
            console.log(oLi);
            console.log(oLi1);
        </script>
    </body>
    </html>
    ```

  + eq()

    按照下标索引筛选元素

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
            <li id="1">1</li>
            <li id="2">2</li>
            <li id="3">
                <p id="pp">3</p>
            </li>
            <li id="4">4</li>
            <li id="5">5</li>
        </ul>
        <script type="text/javascript">
            console.log($('li').eq(0));
        </script>
    </body>
    </html>
    ```

  + is()

    判断筛选到的元素是否满足某个特定的特征，返回值是 true / false

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
            <li id="1">1</li>
            <li id="2">2</li>
            <li id="3">
                <p id="pp">3</p>
            </li>
            <li id="4">4</li>
            <li id="5">5</li>
        </ul>
        <script type="text/javascript">
            var oLi = $('li').eq(0).is('#1');
            console.log(oLi);
        </script>
    </body>
    </html>
    ```

### 一些方法

jQuery 操作 dom 都是通过函数调用的方法实现的

#### css()

设置元素的 css 样式

+ 参数是字符串时，可以单独的设置元素的某一个样式
+ 参数是对象是，可以设置元素的一组样式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>      
    <div></div>
    <script type="text/javascript">
        var oDiv = $('div');
        // 设置css样式
        oDiv.css({width: '100px', height: '100px', border: '5px solid black'});
        oDiv.css('backgroundColor', 'green');
 
        // 读取css样式
        console.log(oDiv.css('width'));
    </script>
</body>
</html>
```

css() 取值相当于 getComputed，赋值相当于 dom.style.***;

css() 赋值赋一组，取值取一个（第一个），如果取得值是颜色，会在内部转换成 rgb 值

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>      
    <div></div>
    <div></div>
    <div></div>
    <script type="text/javascript">
        $('div').css({width: '100px', height: '50px', display: 'inline-block'});    // 赋值赋一组
        $('div').eq(0).css('backgroundColor', 'red');
        $('div').eq(1).css('backgroundColor', 'green');
        $('div').eq(2).css('backgroundColor', 'blue');
        console.log($('div').css('backgroundColor'));                             // 取值取第一个
    </script>
</body>
</html>
```

#### html() / text()

功能相当于原生 js 里面的 innerHTML 和 innerText

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>      
    <div>
        <p>文本</p>
    </div>
    <script type="text/javascript">
        // 取值
        console.log($('div').html());
        console.log($('div').text());
 
        // 赋值
        $('p').html('<span></span>');
        $('span').text('更改后的文本');
 
        // 取值
        console.log($('div').html());
 
    </script>
</body>
</html>
```

html() 、text() 没有参数时是取值操作，有参数时是赋值操作；并且和 css() 一样，赋值赋一组，取值取第一个

#### attr() / prop()

这两个方法都是针对标签属性的操作，但是他们有以下几点区别：

+ 回想之前讲过的在原生 js 中对属性的操作，系统中设定存在的属性，我们可以直接通过 dom.attr 取值或者是赋值；但是对于系统中没有设定的、自己定义的一些属性，我们要向取值或者赋值要使用 getAttirbute()、setAttribute() 方法；jQuery 中的这两个方法同样也是这样的区别，对于系统有设定的属性（特性）可以使用prop() 来取值或者赋值；对于系统没有设定的、自己定义的属性就要采用 attr 来取值或者赋值

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>      
      <div class="demo" name="qht" sex="male"></div>
      <script type="text/javascript">
          // 取值
          console.log($('div').prop('class'));  // demo      -- 取值成功
          console.log($('div').prop('name'));   // undefined -- 取值失败
          console.log($('div').attr('sex'));    // male      -- 取值成功
   
          // 赋值
          $('div').prop('class', 'temp');       -- 赋值成功
          $('div').attr('name', 'sb');          -- 赋值成功
          $('div').prop('sex', 'famale');       -- 赋值失败
   
          console.log($('div').attr('class'));
          console.log($('div').attr('name'));
          console.log($('div').attr('sex'));
      </script>
  </body>
  </html>
  ```

+ 关于这两个函数的第二点区别：attr() 只能操作属性，而 prop() 可以获取一些属性的状态，返回 true / false

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
  </head>
  <body>      
      <input type="checkbox" checked>
      <input type="checkbox">
      <script type="text/javascript">
          console.log($('input').attr('checked'));       // checked
          console.log($('input:eq(0)').prop('checked')); // true
          console.log($('input:eq(1)').prop('checked')); // false
      </script>
  </body>
  </html>
  ```

  这样的属性还有selected、disabled等

#### next() / prev() / index()

next(): 下一个兄弟节点

prev(): 上一个兄弟节点

index(): 该节点在兄弟节点中的索引

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
        <li id="demo1"></li>
        <li id="demo2"></li>
        <li id="demo3"></li>
        <li id="demo4"></li>
        <li id="demo5"></li>
    </ul>
    <script type="text/javascript">
        console.log($('li:eq(2)'));
        console.log($('li:eq(2)').prev());
        console.log($('li:eq(2)').next());
        console.log($('li:eq(2)').index());
    </script>
</body>
</html>
```

#### addClass() / removeClass()

为 dom 元素添加 / 删除类名

参数是要添加 / 删除的类名，如果 removeClass() 的参数为空，则将 dom 元素的所有类名都删除

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>  
 
    <div class="name1 name2"></div>
 
    <script type="text/javascript">
        $('div').addClass('name3');
        console.log($('div').prop('class'));
        $('div').removeClass('name2');
        console.log($('div').prop('class'));
        $('div').removeClass();
        console.log($('div').prop('class'));
    </script>
</body>
</html>
```

**除了字符串以外，这两个函数的参数还可以是函数**

这个函数可以实现，当满足某些条件的时候，再进行类名的添加或者删除

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
        $('li').addClass('name');
        $('li').addClass(function (index) {
            if (index % 3 == 0) {
                return 'three';
            }
        });
 
        $('li').removeClass(function (index) {
            if (index % 3 == 0) {
                return 'name';
            }
        });
    </script>
</body>
</html>
```

#### toggleClass()

这个方法的作用是：当一个有指定类名的元素调用这个方法时，这个方法会把它的指定类名删掉；当一个没有指定类名的元素调用这个方法时，这个方法会给这个元素添加一个指定类名

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>    
    <div class="demo temp"></div>
    <script type="text/javascript">
        $('div').toggleClass('demo');
        console.log($('div').prop('class'));
        $('div').toggleClass('demo');
        console.log($('div').prop('class'));
    </script>
</body>
</html>
```

这个方法一般用在一个元素的样式通过某种触发条件反复变换的场景下，灵活运用

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
        .active {
            background-color: orange;
        }
    </style>
</head>
<body>    
    <div class="demo"></div>
    <script type="text/javascript">
        $('.demo').click(function () {
            $(this).toggleClass('active');
        });
    </script>
</body>
</html>
```

#### insertBefore() / before()

A.insertBefore(B) : A 要插到 B 的前面

B.before(A) : B 的前面是 A

两种方法的操作结果相同，都是 A 在 B的前面，但是操作的主体不相同，即返回的对象不同

A.insertBefore(B) :  A 要 插到 B 的前面，A是主动方(主动抢这个位置)，所以A是主体，方法调用的返回值是A

B.before(A) : B 的前面是 A，B 是主动方(主动让出这个位置)，所以B是主体，方法调用的返回值是B

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>    
    <ul class="demo1">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
    <button class="btn1">insertBefore</button>
    <ul class="demo2">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
 
    <button class="btn2">before</button>
    <script type="text/javascript">
        $('.btn1').click(function () {
            $(this).css('display', 'none');
            $('.demo1 li:eq(3)').insertBefore($('.demo1 li:eq(0)')).css('color', 'red');
        });
 
        $('.btn2').click(function () {
            $(this).css('display', 'none');
            $('.demo2 li:eq(0)').before($('.demo2 li:eq(3)')).css('color', 'red');
        });
    </script>
</body>
</html>
```

可以看到，两个 demo 都是把 第四个li 剪切到 第一个 li 前面，但是执行操作的主体不一样，上面的 demo 在执行完剪切操作后，将执行操作的主体颜色变红，这样可以看出来方法调用的返回值是谁（其实 jQuery 这样设置执行操作的不同主体，是为了我们更方便的使用链式调用来操作 dom）

#### insertAfter() / after()

功能用法和 insertBefore() / before() 相同，只不过是把元素剪切到后面

#### appendTo() / append()

A.appendTo(B) : A 元素要添加到 B 元素里面

B.append(A) : B 元素 里面要添加 A

两种方法的操作结果相同，**都是把子元素插入到父元素的最后一个元素后**，但是操作的主体不相同，第一种方法是 A 要添加到 B 里面，A 是操作主体(A主动要这个位置)，方法的返回值是 A；第二种方法是 B 里面要添加 A，B 是操作主体(B主动让出这个位置)，方法的返回值是 B

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <style type="text/css">
        .wrapper1, .wrapper2 {
            width: 200px;
            height: 150px;
            background-color: green;
            margin-top: 20px;
        }
        .inner1, .inner2 {
            width: 100px;
            height: 100px;
            background-color: orange;
        }
 
    </style>
</head>
<body>
    <div class="wrapper1"></div>
    <div class="inner1"></div>
    <button class="btn1">appendTO</button>
 
    <div class="wrapper2"></div>
    <div class="inner2"></div>
    <button class="btn2">append</button>
 
    <script type="text/javascript">
        $('.btn1').click(function () {
            $(this).css('display', 'none');
            $('.inner1').appendTo($('.wrapper1')).css('backgroundColor', 'red');
        });
 
        $('.btn2').click(function () {
            $(this).css('display', 'none');
            $('.wrapper2').append($('.inner2')).css('backgroundColor', 'red');
        });
    </script>
</body>
</html>
```

两个方法操作结束后，都链式调用 css() 方法，将操作主体变成红色；可以看到，两次变红的主体不同，这是他们的区别所在

**append() 方法的实现同原生JS中的 appendChild() 方法相同**

> 小技巧：同上面的insertBefore() 一样，谁在前面谁是操作主体，方法的返回值是谁

#### prependTo() / prepend()

功能用法同 appendTo() / append() 相同，只不过是把子元素插入到父元素的第一个元素之前

#### remove() / detach()

+ 功能

  删除元素，并返回被删除的元素

+ 区别

  都能删除元素，都能返回被删除的元素，但是这个返回的被删除的元素有所不同：用 remove() 方法删除元素返回元素不包含之前给其绑定的任何事件，而用 detach 方法删除元素返回的元素依然包含之前给元素绑定的任何事件

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
      <button>恢复</button>
      <script type="text/javascript">
          $('.inner1').click(function () {
              item1 = $(this).remove();
          });
          $('.inner2').click(function () {
              item2 = $(this).detach();
          });
          $('button').click(function () {
              $('.wrapper').append(item1).append(item2);
          });
      </script>
  </body>
  </html>
  ```

  分别点击橘色和绿色方块，将这两个元素进行删除，用 item1 和 item2 将删除的元素记录下来，点击 button后，将这两个元素用 append() 方法再添加到 wrapper 里面去；然后再分别点击橘色和绿色方块，发现只有橘色方块可以被删除，绿色方块无法被删除，原因就是使用 remove() 方法删除的元素，它的返回元素不在包含之前绑定的事件，所以后面点击就不在有事件响应了

  还有一个知识点：就是点击 button 是将被删除的两个方块在添加到 wrapper 中，每点击一次就添加两个方块，可是为什么重复点击，始终只有这两个方块呢？因为每次添加的 dom 元素都相同，所以后面添加的会把前面的 dom 元素替换，所以始终是这两个元素