---
title: Date对象、计时器
date: 2018-05-16 10:13:31
updated:
categories:
  - JavaScript
tags:
  - JavaScript
top: false
comments:
keywords:
description: " "
---

### Date对象的常用方法

#### 1. Date()

返回当前的日期和时间

```javascript
console.log(Date());
```

#### 2. getDate()

从Date对象返回一个月中的某一天(1~31)

```javascript
var date = new Date().getDate();
```

#### 3. getDay()

从Date方法返回一周中的某一天(0~6，周日是0)

```javascript
var date = new Date().getDay();
```

#### 4. getMonth()

从Date对象返回月份(0~11，一月是0)

```javascript
var date = new Date().getMonth();
```

#### 5. getFullYear()

+ 从Date对象以四位数字返回年份

+ 返回年份一开始使用的是 getYear() 这个方法，但是这个方法会造成 '千年重'的问题

  JavaScript是上世纪诞生的，当时对于年份的称谓是80年、90年这样，没有考虑跨世纪的问题，所以当时年份仅仅返回两位数字来表示，这样到了新的世纪以后就无法表示了，所以现在不使用这个方法了，虽然这个方法现在已经不仅仅是返回两位数了，但也不能直观的表示年份，所以不使用这个方法

```javascript
var date = new Date().getFullYear();
```

#### 6. getHours()

返回Date对象的小时(0~23)

```javascript
var date = new Date().getHours();
```

#### 7. getMinutes()

返回Date对象的分钟(0~59)

```javascript
var date = new Date().getMinutes();
```

#### 8. getSeconds()

返回Date对象的秒(0~59)

```javascript
var date = new Date().getSeconds();
```

#### 9. getMilliseconds()

返回Date对象的毫秒(0~999)

```javascript
var date = new Date().getMilliseconds();
```

#### 10. getTime()

+ 时间戳
+ 返回1970年1月1日（计算机纪元时间）至今的毫秒数
+ 求某一段时间的事件差可以用这个方法
+ 利用时间戳的唯一性可以唯一标记某一个时间

```javascript
var date = new Date().getTime();
```

#### 11. setDate()

设置Date对象中月的某一天(1~31)

```javascript
var date = new Date();
date.setDate(1);
```

#### 12. setMonth()

设置Date对象中的某一个月(0~11)

```javascript
var date = new Date();
date.setMonth(0);  // 一月
```

#### 13. setFullYear()

设置Date对象中的某一年(4为数字)

```javascript
var date = new Date();
date.setFullYear(1997);
```

#### 14. setHours()

设置Date对象中的某个小时(0~23)

```javascript
var date = new Date();
date.setHours(23);
```

#### 15. setMinutes()

设置Date对象的某一分钟(0~59)

```javascript
var date = new Date();
date.setMinutes(59);
```

#### 16. setSecons()

设置Date对象的某一秒(0~59)

```javascript
var date = new Date();
date.setSeconds(0);
```

#### 17. setTime()

```javascript
var date = new Date();
date.setTime(1000000000000);
```

#### 18. toString()

```javascript
var date = new Date();
var str = date.toString();
```

#### 19. toDateString()

```javascript
var date = new Date();
var str = date.toDateString();
```

### JS定时器

以下的所有方法都是window上的方法，内部的指针指向window

#### 1. setInterval()

```javascript
var time = 1000;
setInterval(function() {
    console.log('a');
}, time);
```

+ 功能

  每隔一段设定的时间(time)，执行一次函数(function)

+ 时间间隔

  + time一旦确定放到setInterval中去执行的时候，这个值就不会再改变了，后面再修改time也不会影响到这个时间间隔

  + 这个时间间隔是很准确的么？

    ```javascript
    <script type="text/javascript">
        var firstTime = new Date().getTime(),
            lastTime;
        setInterval(function() {
            lastTime = new Date().getTime();
            console.log(lastTime - firstTime);
            firstTime = new Date().getTime();
        }, 1000);
    </script>
    ```

    通过打印结果来看，这个时间差是不太精确的，具体原因与js的执行机制以及setInterval的内部原理有关

    可参考文章：https://jeffjade.com/2016/01/10/2016-01-10-javaScript-setInterval

+ 另一个用法

  ```javascript
  setInterval('str', time);
  ```

  如果第一个参数是字符串的话，setInterval会执行引号内的代码，但是一般不这样用

#### 2. clearInterval()

+ 功能：让循环停下来
+ 原理：setInterval()方法有一个返回值，这个返回值可以唯一标识一个计时器，通过这个标识可以让setInterval停下来

```javascript
<script type="text/javascript">
    var timer;
    timer = setInterval(function() {
        console.log('a');
    }, 1000);
    clearInterval(timer);
</script>
```

#### 3. setTimeout()

隔一段时间后执行一个函数，且只执行一次

``` javascript
<script type="text/javascript">
    setTimeout(function () {
        console.log('a');
    }, 1000);
</script>
```

#### 4. clearTimeout()

```javascript
<script type="text/javascript">
var timer;
    timer = setTimeout(function () {
        console.log('a');
    }, 1000);
    clearTimeout(timer);
</script>
```
