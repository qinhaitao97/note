### 动画与效果

#### animate()

+ 用法

  animate(target, during, speedType, callback)

+ 功能

  使元素获得指定的动画效果

+ 参数

  target: 一个对象，包含想要实现的动画效果

  duration: 指定的动画效果在多长时间内完成

  speedType: 速率函数，表示运动的速率变化方式

  callback: 回调函数

  后面三个参数可以省略

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
              border: 5px solid orange;
          }
      </style>
  </head>
  <body>
      <div class="demo"></div>
      <script type="text/javascript">       
          $('.demo').animate({left: '500px', top: '300px', width: '150px', height: '150px', opacity: '0.5', borderWidth: '10px'}, 1000, 'swing', function () {
              console.log('运动完成');
          });
      </script>
  </body>
  </html>
  ```

  jQuery 提供的 speedStyle 有两种，'swing'  和  'linear'，默认的是 'swing'，如果想用其他的速率变化方式，可以使用一个 'jQuery.easing.js' 插件，插件中包含的速率变化方式及其对应的曲线如下，以供参考

  ![](http://ww1.sinaimg.cn/large/006eYMu7ly1fr8jjrayhqj30ch0hc0to.jpg)

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
      <script src="./js/jquery.easing.1.3.js"></script>
      <style type="text/css">
          .demo {
              position: absolute;
              top: 0px;
              left: 0px;
              width: 100px;
              height: 100px;
              background-color: green;
          }
      </style>
  </head>
  <body>
      <div class="demo"></div>
      <script type="text/javascript">       
          $('.demo').animate({left: '500px', top: '300px'}, 1000, 'easeInOutQuint', function () {
              console.log('运动完成');
          });
      </script>
  </body>
  </html>
  ```

#### stop()

+ 功能

  用来暂停或者停止当前运动

+ 用法

  stop(boolean1, boolean2)

+ 参数

  这里可以写两个参数，都是布尔值

  

  | 参数     | 意义             | true         | false  |
  | -------- | ---------------- | ------------ | ------ |
  | boolean1 | 是否停止后续所有 | 停止后续所有 | 不停止 |
  | boolean2 | 是否立即到达     | 到达         | 不到达 |

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>jQuery</title>
      <script src="./js/jquery-3.3.1.js"></script>
      <script src="./js/jquery.easing.1.3.js"></script>
      <style type="text/css">
          .demo {
              position: absolute;
              top: 0px;
              left: 0px;
              width: 100px;
              height: 100px;
              background-color: green;
          }
      </style>
  </head>
  <body>
      <div class="demo"></div>
      <script type="text/javascript">       
          $('.demo').animate({left: '500px'}, 1000).animate({top: '150px'}, 1000);
   
          $(document).click(function () {
              // $('.demo').stop(true, false);
              // $('.demo').stop(false, false);
              // $('.demo').stop(true, true);
              // $('.demo').stop(false, true);
          });
      </script>
  </body>
  </html>
  ```

  一共四种组合情况，自己查看效果

#### finish()

结束所有运动，并且直接到达最终的目标点

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <script src="./js/jquery.easing.1.3.js"></script>
    <style type="text/css">
        .demo {
            position: absolute;
            top: 0px;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="demo"></div>
    <script type="text/javascript">       
        $('.demo').animate({left: '500px'}, 1000).animate({top: '150px'}, 1000);
 
        $(document).click(function () {
            $('.demo').finish();
        });
    </script>
</body>
</html>
```

#### delay()

当前运动结束之后，经过一段时间的延迟，再进行后续的运行

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <script src="./js/jquery.easing.1.3.js"></script>
    <style type="text/css">
        .demo {
            position: absolute;
            top: 0px;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="demo"></div>
    <script type="text/javascript">       
        $('.demo').animate({left: '500px'}, 1000).delay(1000).animate({top: '150px'}, 1000);
    </script>
</body>
</html>
```

#### slideUp() / slideDown() / slideToggle()

slideUp(): 滑动的将元素隐藏起来

slideDown(): 滑动的将元素展示出来

slideToggle(): 如果元素可见，就将其隐藏；如果不可见就展示

参数：speed（完成时间）、callback（回调函数）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <script src="./js/jquery.easing.1.3.js"></script>
    <style type="text/css">
        .demo {
            /* display: none; */
            position: absolute;
            top: 0px;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="demo"></div>
    <script type="text/javascript">
        // $('.demo').slideUp(1000, function () { console.log('finish'); });
 
        // $('.demo').css('display', 'none').slideDown(2000);
 
        // $(document).click(function () {
        //     $('.demo').slideToggle();
        // });
    </script>
</body>
</html>
```

#### fadeIn() / fadeOut() / fadeToggle()

功能用法与 slideUp() 等方法相同，只不过动画效果不一样，这里的动画效果是淡入淡出

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <script src="./js/jquery-3.3.1.js"></script>
    <script src="./js/jquery.easing.1.3.js"></script>
    <style type="text/css">
        .demo {
            /* display: none; */
            position: absolute;
            top: 0px;
            left: 0px;
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>
</head>
<body>
    <div class="demo"></div>
    <script type="text/javascript">
        // $('.demo').fadeOut(1000, function () { console.log('finish'); });
 
        // $('.demo').css('display', 'none').fadeIn(2000);
 
        // $(document).click(function () {
        //     $('.demo').fadeToggle();
        // });
    </script>
</body>
</html>
```

### 工具方法

我们之前介绍的所有方法都是以类似于 \$('div').xxx 的形式调用的，这种需要先获得 dom 元素，再进行调用的方法叫做 "实例方法"，实例方法是定义在 jQuery 原型上的；接下来要介绍的是 jQuery 中的工具方法，使用工具方法不需要先获取 dom 元素，以 类似于 \$.xxx 的形式调用，工具方法定义在 jQuery 函数上

#### type()

+ 功能

  可以精准的的判断参数的数据类型

+ 原生JS中判断数组和对象的三种方法

  + instanceof

    可以来区分某一变量是数组还是对象，但是无法用来直接判断一个变量到底是数组还是变量(就是说如果明确给到两个变量，让我们区分这两个变量哪个是数组，哪个是对象，这样可以区分；但是如果给一个变量让我们用 instanceof 直接判断它是数组还是变量，这样无法实现)

    ```javascript
    var arr = [1,2];
    var obj = {};
    console.log(arr instanceof Object);
    console.log(obj instanceof Object);
    ```

    两个打印结果都是 true，这就是为什么无法直接判断是数组还是对象的原因，那怎么区分他是数组还是对象呢

    ```javascript
    var arr = [1, 2];
    var obj = {};
    console.log(arr instanceof Array);    // true
    console.log(arr instanceof Object);   // true
    console.log(obj instanceof Array);    // false
    console.log(obj instanceof Object);   // true
    ```

    可以看到，数组属于对象的一种实例，但是对象不属于数组的一种实例，所以用这样的方法可以区分

  + constructor

    这样的写法一般情况下是可以判断是数组还是对象，但是如果涉及到跨域的问题（不知道这样写合不合适，学到跨域再修改吧），这样判断就不准确了

  + Object.prototype.toString.call()

    这样的方法判断数据类型很准确，原生JS中最好使用这样方法判断

    ```javascript
    var arr = [1, 2];
    var obj = {};
    console.log(Object.prototype.toString.call(arr));    "object Array"
    console.log(Object.prototype.toString.call(obj));    "object Object"
    ```

+ type()的用法

  使用 jQuery 中的 type() 方法进行数据类型的判断，结果很准确

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
          var arr = [1, 2];
          var obj = {};
          console.log($.type(arr));    "array"
          console.log($.type(obj));    "object"
      </script>
  </body>
  </html>
  ```

#### trim()

消除字符串头尾两边的空格，不改变原字符串

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
        var str = '  |q  h t|       ';
        console.log($.trim(str));
    </script>
</body>
</html>
```

#### proxy()

+ 功能

  改变this指向

+ 语法

  proxy(fn, obj)

+ 参数

  fn：要改变哪个函数中this的指向

  obj：要让this指向哪个对象

+ 返回值

  返回值是一个函数，这个函数以新的 this 指向调用 fn

+ 使用

  因为返回的是一个函数，所以我们要执行这个函数来使用 proxy() 的功能

  ```javascript
  function test() {
      console.log(this);
  }
  var obj = {};
   
  $.proxy(test, obj)();
  ```

  当然fn可能有参数，我们需要传入参数，传入参数的形式有以下几种：

  ```javascript
  var obj = {};
  function test(a, b) {
      console.log(this);
      console.log(a + ' ' + b);
  }
  $.proxy(test, obj)(1, 2);
   
  $.proxy(test, obj, 1, 2)();
   
  $.proxy(test, obj, 1)(2);
  ```

  可能前两种参数的位置我们还能接受，但是第三种参数位置不禁让人有些困惑，为什么要这样传参？里面一个外面一个，其实允许这样的传参方式主要是为了方便分开传参

  ```javascript
  var obj = {};
  function test(grade, no) {
      console.log(this);
      console.log(grade + ': ' + no);
  }
  var fn = $.proxy(test, obj, 2015);
  fn(201500800529);
  fn(201500800530);
  fn(201500800531);
  fn(201500800532);
  ```

  可以看到，这个函数一共需要两个参数：年级、学号，而现在的数据中年级都是2015级，只有学号不一样，那我们可以在执行 proxy() 方法的时候就把年级先传入进去，后面再传入不同的学号即可，即相同的参数只需传入一次

#### noConflict()

开发时我们可能引用多个 JavaScript 类库，而这些 JavaScript 库可能都使用 \$ 作为一个函数名或者变量名，就像 jQuery 一样。如果我们需要同时使用 jQuery 和其他类库，我们可以把 jQuery中 \$ 的使用权交给其他类库

```javascript
console.log($);
var nquery = $.noConflict();
console.log($);
console.log(nquery);
```

#### parseJSON()

功能同原生js中的 JSON.parse()，解析 JSON 字符串

```javascript
var jsonObj = {
    "name": "qht",
    "age": 20,
    "sex": "male"
}
var str = JSON.stringify(jsonObj);
console.log($.parseJSON(str));
```

#### makeArray()

把类数组转换成数组，相当于原生js中的 Array.prototype.slice()

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
    <script type="text/javascript">
        var oDiv = $('div');
        var arr = $.makeArray(oDiv);
        // var arr = Array.prototype.slice.call(oDiv);
        console.log($.type(oDiv));  // "object"
        console.log($.type(arr));   // "array"     
    </script>
</body>
</html>
```

### jQuery高级方法

#### extend()

+ 插件扩展功能

  当我们需要自定义一些功能方法的时候，就要使用 extend() 方法将这些扩展方法添加到 jQuery 的函数或者原型链上，有两种插件扩展的方式：扩展工具方法、扩展实例方法

  + $.extend()

    扩展工具方法：将扩展的工具方法添加到 jquery 函数上

    ```javascript
    $.extend({
        test: function () {
            console.log('这是一个扩展的工具方法');
        }
    });
    $.test();
    ```

  + $.fn.extend()

    \$.fn = \$.prototype，为了不写比较长的 prototype，做了这样的处理，所以 \$.fn 就相当于是 \$.prototype

    扩展实例方法：将扩展的工具方法添加到 jQuery 对象的原型链上

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>jQuery</title>
        <script src="./js/jquery-3.3.1.js"></script>
    </head>
    <body>
        <div style="width: 100px; height: 100px;"></div>
        <script type="text/javascript">
            $.fn.extend({
                changeBgColor: function (color) {
                    this.css('backgroundColor', color);
                    return this;  // 为了方便后续的链式调用
                }
            });
            $('div').changeBgColor('green');
        </script>
    </body>
    </html>
    ```

  一般不需要选取 dom 进行操作的方法，我们将其扩展为工具方法；需要选取 dom 元素来进行操作的方法我们将其扩展为实例方法

+ 合并对象功能

  \$.extend() 和 \$.fn.extend() 方法都可以用来合并对象

  ```javascript
  var obj = {
      param1: {
          a: 1,
          b: 2
      },
      no: 1
  };
  var obj1 = {
      param2: {
          c: 3,
          d: 4
      },
      no: 2
  }
  console.log(obj);
  ```

  以上代码是将对象 obj1 合并到对象 obj 里面，返回合并后的 obj 对象

  默认情况下，合并对象采用的是浅拷贝:

  ```javascript
  var obj = {
      param1: {
          a: 1,
          b: 2
      },
      no: 1
  };
  var obj1 = {
      param2: {
          c: 3,
          d: 4
      },
      no: 2
  }
  $.extend(obj, obj1);
  obj1.param2.c = 5;
  console.log(obj.param2.c);
  ```

  可以看到，合并完成后，我们修改 obj1 中 param2 对象的参数，obj 中相应的参数也产生了相同的变化，说明这里使用的合并方式是浅拷贝，如果我们需要使用深拷贝，只需要给方法的第一个参数传一个true

  ```javascript
  var obj = {
      param1: {
          a: 1,
          b: 2
      },
      no: 1
  };
  var obj1 = {
      param2: {
          c: 3,
          d: 4
      },
      no: 2
  }
  $.extend(true, obj, obj1);
  obj1.param2.c = 5;
  console.log(obj.param2.c);
  ```


#### Callbacks()

通过构造、使用回调函数对象来管理回调函数队列的方法

+ 用法

  要使用 Callbacks() 方法首先要构造一个回调函数对象

  ```javascript
  var cb = $.Callbacks();
  ```

  使用 add() 方法向回调函数队列中添加需要执行的回调函数，一次可以添加多个回调函数，且可以重复

  ```javascript
  function fn1() {
      console.log('fn1');
  }
   
  function fn2() {
      console.log('fn2');
  }
   
  function fn3() {
      console.log('fn3');
  }
   
  cb.add(fn1, fn1);  // 一次可以添加多个回调函数，且可以重复
  cb.add(fn2);
  cb.add(fn3);
  ```

  使用 **fire()** 函数触发执行回调函数队列(队列是先入先出)，重复执行 cb.fireF()，回调函数队列也会重复被执行

  ```javascript
  cb.fire();
  ```

  完整的测试代码：

  ```javascript
  var cb = $.Callbacks();
   
  function fn1() {
      console.log('fn1');
  }
  function fn2() {
      console.log('fn2');
  }
  function fn3() {
      console.log('fn3');
  }
   
  cb.add(fn1, fn1);  // 可以一次添加多个函数，且可以重复
  cb.add(fn2);
  cb.add(fn3);
   
  cb.fire();
  cb.fire();    // 重复执行cb.fire()，回调函数队列也会重复被执行
  ```

+ 四个参数

  + once

    只执行一次 fire() 方法，即使重复调用也不会重复执行

    ```javascript
    var cb = $.Callbacks('once');
     
    function fn1() {
        console.log('fn1');
    }
    function fn2() {
        console.log('fn2');
    }
    function fn3() {
        console.log('fn3');
    }
     
    cb.add(fn1);
    cb.add(fn2);
    cb.add(fn3);
     
    cb.fire();
    cb.fire();
    ```

  + unique

    回调函数中重复的函数只会执行一次

    ```javascript
    var cb = $.Callbacks('unique');
     
    function fn1() {
        console.log('fn1');
    }
    function fn2() {
        console.log('fn2');
    }
    function fn3() {
        console.log('fn3');
    }
     
    cb.add(fn1, fn1);
    cb.add(fn1);
    cb.add(fn2);
    cb.add(fn3);
     
    cb.fire();
    ```

  + stopOnFalse

    当某一个回调函数的返回值是 false 时，该回调函数队列停止执行，后面的回调函数都不会被执行

    ```javascript
    var cb = $.Callbacks('stopOnFalse');
     
    function fn1() {
        console.log('fn1');
    }
    function fn2() {
        console.log('fn2');
        return false;
    }
    function fn3() {
        console.log('fn3');
    }
     
    cb.add(fn1);
    cb.add(fn2);  // 回调函数fn2返回false，后面的回调函数fn3不会再被执行
    cb.add(fn3);
     
    cb.fire();
    ```

  + memory

    fire() 的调用将会被"记忆"，即使在 fire() 方法执行后再使用 add() 方法添加回调函数，这个回调函数也会被执行

    ```javascript
    var cb = $.Callbacks('memory');
     
    function fn1() {
        console.log('fn1');
    }
    function fn2() {
        console.log('fn2');
    }
    function fn3() {
        console.log('fn3');
    }
     
    cb.add(fn1);
    cb.add(fn2);
     
    cb.fire();
     
    cb.add(fn3);  // 在 fire() 方法后添加，同样会被执行
    ```

  + 参数混合使用

    有时可能不只要满足一个参数的需求，可以同时使用多个参数

    ```javascript
    var cb = $.Callbacks('once unique');
     
    function fn1() {
        console.log('fn1');
    }
    function fn2() {
        console.log('fn2');
    }
    function fn3() {
        console.log('fn3');
    }
     
    cb.add(fn1, fn2);
    cb.add(fn2);
    cb.add(fn3);
     
    cb.fire();
    cb.fire();
    ```

#### Deferred()

用于构造延迟对象，管理回调函数的状态；

相当于是有状态的回调函数

+ 构造延迟对象

  ```javascript
  var dtd = $.Deferred();
  ```

+ 管理函数状态

  ```javascript
  function test(status) {
      if (status == 1) {
          dtd.resolve();
      } else if (status == 2) {
          dtd.reject();
      } else {
          dtd.notify();
      }
  }
  ```

  resolve()、reject()、notify() 三个方法分别代表了函数的三个状态：成功、失败、进行中

+ 执行相应的回调函数

  ```javascript
  dtd.done(function () {
      console.log('成功');
  });
  dtd.fail(function () {
      console.log('失败');
  });
  dtd.progress(function () {
      console.log('进行中');
  });
  ```

+ 调用 test() 进行测试

  ```javascript
  test(1);
  // test(2);
  // test(3);
  ```

+ 以上部分完整代码

  ```javascript
  var dtd = $.Deferred();
   
  function test(status) {
      if (status == 1) {
          dtd.resolve();
      } else if (status == 2) {
          dtd.reject();
      } else {
          dtd.notify();
      }
  }
   
  dtd.done(function () {
      console.log('成功');
  });
  dtd.fail(function () {
      console.log('失败');
  });
  dtd.progress(function () {
      console.log('进行中');
  });
   
  test(1);
  ```

+ 在测试上面的代码时，如果你先使用了 test(1) 或者 test(2) 进行测试，那么在后续的测试中，再使用其他的参数进行测试都不会按照预计的结果执行，如：

  ```javascript
  test(1);
  test(2);
  test(3);
  ```

  打印结果：

  ![](http://ww1.sinaimg.cn/large/006eYMu7gy1frbxe3dkklj30cg051q2q.jpg)

  结果只有一个成功，而没有预想中的 失败 和 进行中，这是为什么呢？

+ 当 **done** 状态的回调函数或者 **fail** 状态的回调函数有一个被触发时，其他的函数就不能再被触发了

  在上面抛出的问题中，首先触发了 done 状态的回调函数，所以后面其他状态的回调函数就不会再被执行了

+ 避免函数状态受到外部因素干扰

  在 test 方法中，我们使用  dtd.resolve()、dtd.reject()、dtd.notify()管理函数的状态，但如果我在函数外部使用同样的方法改变它的状态也是可以的，比如：

  ```javascript
  var dtd = $.Deferred();
   
  function test(status) {
      if (status == 1) {
          dtd.resolve();
      } else if (status == 2) {
          dtd.reject();
      } else {
          dtd.notify();
      }
  }
   
  dtd.done(function () {
      console.log('成功');
  });
  dtd.fail(function () {
      console.log('失败');
  });
  dtd.progress(function () {
      console.log('进行中');
  });
  dtd.resolve();
  test(3);
  ```

  在这组测试代码中，test() 方法的参数是3，本来想让函数的状态修改为"进行中"，但是我在外部使用dtd.resolve() 将函数的状态修改为 resolve，导致打印结果变成 "成功"

+ 如何避免外部因素的干扰

  将 dtd 延迟对象创建于函数中，向外部返回一个不能触发的 dtd 延迟对象

  ```javascript
  function test(status) {
      var dtd = $.Deferred();   // 函数内部构造延迟对象
   
      if (status == 1) {
          dtd.resolve();
      } else if (status == 2) {
          dtd.reject();
      } else {
          dtd.notify();
      }
      return dtd.promise();   // 返回一个不能触发函数(无状态)
  }
  var dtd = test(3);
  // dtd.resolve();           // 会报错，resolve() is not a function
  dtd.done(function () {
      console.log('成功');
  });
  dtd.fail(function () {
      console.log('失败');
  });
  dtd.progress(function () {
      console.log('进行中');
  });
  ```

#### when()

管理多个函数的状态，当所有函数的状态全部是"成功"时，才会触发 done 状态的函数；如过有一个状态为失败，则触发 fail 状态的函数；如果有一个状态为进行中，则什么也不打印(我自己测试的结果是什么也不打印)

```javascript
function test(status) {
    var dtd = $.Deferred();
 
    if (status == 1) {
        dtd.resolve();
    } else if (status == 2) {
        dtd.reject();
    } else {
        dtd.notify();
    }
    return dtd.promise();
}
 
function temp() {
    return $.Deferred().resolve().promise();
}
var dtd = test(1);
var dtd1 = temp();
 
var dtdAll = $.when(dtd, dtd1);
dtdAll.done(function () {
    console.log('成功');
});
dtdAll.fail(function () {
    console.log('失败');
});
dtdAll.progress(function () {
    console.log('进行中');
});
```
#### ajax()

通过HTTP请求加载远程数据

以一个对象作为参数，配置请求的各种属性

##### 属性参数

+ type

  请求方式：get / post / delete ...

+ url

  请求路径

+ data

  请求数据

+ async

  是否异步，默认是true

+ cache

  是否缓存，默认是 true；如果数据要分分钟更新的时候，比如说获取图片验证码时我们就要添加 false，事件上是添加事件戳

+ datatype

  预期服务器返回的数据类型，如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息只能判断，比如 XML MIME 就被识别为 XML。JSON 回生成一个 JavaScript 对象，而 script 会执行这个脚本。随后服务器端返回的数据会根据这个值解析后，传递给回调函数

  - "xml"

     返回 XML 文档，可用 jQuery 处理。

  - "html":

    返回纯文本 HTML 信息；包含的 script 标签会在插入 dom 时执行。

  - "script"

     返回纯文本 JavaScript 代码。不会自动缓存结果。除非设置了 "cache" 参数。注意：在远程请求时(不在同一个域下)，所有 POST 请求都将转为 GET 请求。（因为将使用 DOM 的 script标签来加载）

  - "json"

     返回 JSON 数据 。

  - "jsonp":

    JSONP 格式。使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。

  - "text":

    返回纯文本字符串

  如果指定了 script 或者 jsonp 类型，那么当从服务器接收到数据时，实际上是用了 `<script>` 标签而不是 XMLHttpRequest 对象。这种情况下，$.ajax() 不再返回一个 XMLHttpRequest 对象，并且也不会传递事件处理函数，比如 beforeSend

+ jsonp

  在一个 jsonp 请求中重写回调函数的变量名，用这个值来代替 callback 部分

+ jsonpCallback

  在一个 jsonp 请求中重写回到函数的值，用这个值来代替 jQuery 自动生成的随机函数名

+ crossDomain

  同域请求为 false，跨域请求为 true，如果想用这种方法实现 ajax 跨域，那么需要服务端设置相关的配置支持这种跨域的方法

+ contentType

  发送信息至服务器时，内容编码的类型，默认是 "application/x-www-form-urlencoded"

  默认值适合大多数情况，如果明确传递了一个 content-type 给 ajax，那么他必定会发送给服务器，即使没有数据要发送

+ context

  设置回调函数的执行上下文，就是说，让回调函数内 this 指向某一个对象

##### 方法参数

+ beforeSend

  在发送请求之前调用，并且传入一个 XMLHTTPRequest 对象作为参数

+ success

  请求成功时触发的函数

+ error

  请求失败时触发的函数

+ dataFilter

  在请求成功之后调用，传入返回数据以及 "dataType" 参数的值。并且返回新的数据（可能是处理过的）传递给 success 回调函数

+ complete

  当请求成功后调用这个函数，无论成功或者失败。传入 XMLHTTPRequest 对象，以及一个包含成功或者错误的字符串

##### jsonp

这里详细讲解一下使用 jsonp 发送 ajax 请求时参数中回调函数的问题

前面讲 jsonp 的时候讲过，如果我们要请求 jsonp格 式的数据，我们需要在请求的 url 后面的参数中拼接一个回调函数，用来完成后端到前端的数据传递，比如 http://www.abc.com?q=sth&callback=test 中的 callback = test，这里的 callback 不是固定的，要根据不同请求地址后台自己的规定而定（比如百度是 cb=xx，豆瓣是 callback=xx）。在 jQuery 的 ajax 中，如果我们使用的 dataType 是 jsonp，那么jQuery默认会自动为我们拼接上  "callback=随机函数"，所以如果我们要请求的后台规定的接口是 callback 的话，那我们就不需要在data数据的后面再次拼接 callback=xx；如果不是callback而是其他的像 cb、cbs 这些的话，我们就要单独设置相应的接口

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>ajax</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>
    <script>
        $.ajax({
            type: 'GET',
            url: 'https://api.douban.com/v2/music/search',
            data: 'q=房东的猫',
            dataType: 'JSONP',
            success: function (data) {
                console.log(data);
            }
        });
 
        $.ajax({
            type: 'GET',
            url: 'https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su',
            data: 'wd=房东的猫',
            dataType: 'JSONP',
            jsonp: 'cb',
            success: function () {
                console.log('success');
            }
        });
    </script>
</body>
</html>
```

可以看到，第一个 ajax 请求我们既没有设置 jsonp 属性，也没有设置 jsonpCallback 属性，然后成功的请求到了 jsonp 数据，这是因为上面说到 jQuery 会自动为我们添加上 callback=随机函数，而且豆瓣的后台借口就是使用的 callback，所以请求数据成功，成功的执行了 success 函数；而对于第二个 ajax 请求，百度搜索后台的接口是 cb 不是 callback，所以我们要设置 jsonp 为后台接口给定的形式 cb，但是这里并没有设置 cb等于什么，也就是回调函数的名字，为什么也请求成功了呢？因为只要我们设置 jsonp，在发送 ajax 请求时，jQuery 也会它自动补上一个随机函数名作为回调函数的名字，所以可以请求成功，成功的执行 success函数

也可以将 success 函数定义在外面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>ajax</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>
    <script>
 
        $.ajax({
            type: 'GET',
            url: 'https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su',
            data: 'wd=房东的猫',
            dataType: 'JSONP',
            jsonp: 'cb',
            success: test
 
        });
 
        function test(data) {
            console.log(data);
        }
 
    </script>
</body>
</html>
```

除了执行 success 函数，我们也可以执行自己定义好的函数

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>ajax</title>
    <script src="./js/jquery-3.3.1.js"></script>
</head>
<body>
    <script>
 
        $.ajax({
            type: 'GET',
            url: 'https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su',
            data: 'wd=房东的猫',
            dataType: 'JSONP',
            jsonp: 'cb',
            jsonpCallback: 'test'
 
        });
 
        function test(data) {
            console.log(data);
        }
 
    </script>
</body>
</html>
```