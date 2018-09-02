---
title: JSON、XML
date: 2018-05-22 11:23:14
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

这篇主要是简单了解一下 XML 与 JSON 的用途及简单的语法，不进行深入的研究

#### XML

+ XML是一门语言
+ XML是存储和通过因特网传输结构化数据的标准
+ XML可以自定义标签

#### JSON

> 曾经有一段时间，XML 是互联网上传输结构化数据的标准。web 服务的第一次浪潮很大程度上都是建立在XML 之上的，突出的特点是服务器与服务器之间的通信。然而不少人认为 XML 过于繁琐、冗长。为了解决这个问题，涌现了一些方案。
>
> 2006 年，DouglasCrockford 把 JSON (Javascript Object Notation，JavaScript对象表示法) 作为 IETF RFC 4627 提交给 IETF，而 JSON 早在 2001 年就开始被使用了。JSON 是 JavaScript 的一个严格子集，利用JavaScript 中的一些模式来表示结构化数据。与 XML 相比，JSON 是在 JavaScript 中读写结构化数据更好的方式。因为可以把 JSON 直接传给 eval()，而不必创建 DOM 对象。

+ JSON 是一种数据格式，而不是一门编程语言

+ JSON 与 JavaScript 具有相同的语法形式，但是不从属于 JavaScript

+ 并不是只有 JavaScript 才有 JSON，JSON 只是一种数据格式，很多语言都有针对 JSON 的解析器和序列化器。

+ 语法

  JSON 的语法可以表示一下三种类型的值，不支持变量、函数或者对象实例

  + 简单值

    使用与 JavaScript 相同的语法，可以在 JSON 中表示字符串、数值、布尔值、null，不支持 undefined。JSON 中的字符串必须使用双引号，单引号会导致语法错误

  + 对象

    JSON 中的对象与 JavaScript 中的字面量有些不同，先看一个 JavaScript 字面量的例子：

    ```javascript
    var person = {
        name: 'qht',
        age: 20
    };
    ```

    JSON 中的对象是这样的：

    ```javascript
    {
        "name": "qht",
        "age": 20
    }
    ```

    不同点：

    + 没有变量声明(JSON 中没有变量的概念)
    + 文末没有分号(因为这并不是 JavaScript 语句，所以不需要分号)
    + 属性值必须加双引号(JavaScript 中的属性名可以加引号也可以不加引号，如果加引号，可以加单引号也可以见双引号，但是对于 JSON 来说，属性名必须加双引号，单引号回导致语法错误)

  + 数组

    JSON 中的数组采用的就是 JavaScript 中数组字面量的形式，没有变量声明和分号

    ```javascript
    [11, "hello", true]
    ```

+ JSON对象

  早期的 JSON 解析器基本上就是 JavaScript 的 eval() 函数，ECMAScript 5 对解析 JSON 的行为进行了规范，定义了全局的 JSON 对象，支持这个对象的浏览器有IE8+、Firefox3.5+、Safari4+、chrome、Opera10.5+。对于较早版本的浏览器，可以使用一个shim：https://github.com/douglascrockford/JSON-js。在旧版本的浏览器中，使用 eval() 对 JSON 数据结构求值存在风险，可能会执行一些恶意代码。对于不能原生支持 JSON解析的浏览器，使用这个 shim 是最好的选择。

+ 解析与序列化

  JSON 格式的数据进行解析和序列化利用的是 JSON 对象中的两个方法

  + **JSON.stringify()**

    ```javascript
    var obj = {
        name: 'qht',
        age: 20,
        fn: function() {
            console.log('a');
        },
        test: undefined,
    }
    ```

    JSON 序列化的结果是一个**字符串**，默认情况下，这个字符串不包含任何空格或者缩进。

    在序列化 JavaScript 对象时，所有函数、原型成员都会别有意忽略，不体现在结果中，值为 undefined 的任何属性也都会被跳过。结果中的最终值都是值为有效的 JSON 数据类型的实例属性。

  + **JSON.parse()**

    将JSON字符串直接传递给 JSON.parse() 方法，就可以得到相应的 JavaScript 类型的值。如果传递给这个方法的字符串不是有效的 JSON，该方法会抛出错误。

    ```javascript
    var obj = {
        name: 'qht'
    }
    var str = JSON.stringify(obj);
    console.log(JSON.parse(str));
    ```
