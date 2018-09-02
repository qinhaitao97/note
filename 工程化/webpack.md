## 什么是前端工程化

前端工程化是根据业务特点，将前端开发流程规范化、标准化，它包括了开发流程、技术选型、代码规范、构建发布等，用于提高前端工程师的开发效率和代码质量

一个符合前端工程化要求的方案应该包含以下要素：

```
- 开发规范
- 模块化开发
- 组件化开发
- 组件仓库
- 性能优化
- 部署
- 开发流程
- 开发工具
```

那我们该怎么实现这一系列的工程化需求呢？

## 构建工具

### 自动化构建工具

说到构建工具，我往往会在前面加「自动化」三个字，因为构建工具就是用来让我们不再做机械重复的事情，解放我们的双手的。

要完成前端工程化，少不了工程化工具，requireJS与grunt的出现，改变了业界前端代码的编写习惯，同时他们也是推动前端工程化的一个基础。

requireJS是一伟大的模块加载器，他的出现让javascript制作多人维护的大型项目变成了事实；grunt是一款javascript构建工具，主要完成编译、压缩、合并等一系列工作，后续又出了yeoman、Gulp、webpack等构建工具。

Webpack具有Grunt、Gulp对于静态资源自动化构建的能力，但更重要的是，Webpack弥补了requireJS在模块化方面的缺陷，同时兼容AMD与CMD的模块加载规范，具有更强大的JS模块化的功能。

### 自动化构建工具的两个模式

开发模式

> 开发模式主要就是监听文件变化，自动进行打包、合并等操作

生产模式

> 参考我们的技术栈与需求，我们的静态文件都要发布到 CDN 上，而且必须有 md5 版本号，方便快速发布（CDN 更新机器缓慢，所以更新必须使用新的文件名）
>
> 生产模式主要增加了文件压缩、文件 md5 修改、替换 html 等操作
>
> 这样的好处就是上线非常方便，一个命令即可更新上线，而且不存在缓存问题

### CDN

#### 基本原理

CDN 是构建在网络上内容分发网络，依靠部署在各地的边缘服务器，通过中心平台的负载均衡、调度、内容发布等功能模块，使用户就近的获取所需内容，降低网络拥塞，提高用户的响应速度和命中率；CDN 关键技术主要有 内容存储 和 分发技术

CDN 基本原理是广泛采用各种缓存服务器，将这些缓存服务器分布到用户访问相对集中的地区或网络中，在用户访问网站时，利用全局负载技术将用户的访问指向距离最近的工作正常的缓存服务器，有缓存服务器直接响应用户请求

CDN 网络是在用户和服务器之间增加了 cache 层，如何将用户的请求引导到 cache 上获得服务器的数据，主要是通过接管 DNS 实现的，这就是 CDN 的基本原理

#### 流程

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftwese20vej30d909aq5o.jpg)

1. 用户向浏览器输入 `www.web.com` 这个域名，浏览器第一次发现本地没有 DNS 缓存，则向网站的 DNS 服务器请求
2. 网站的 DNS 域名解析设置了 CNAME，指向了 `www.web.51cdn.com`，请求指向了 CDN 网络中的智能 DNS 负载均衡系统
3. 智能 DNS 负载均衡系统解析域名，把用户响应速度最快的的 IP 节点返回给用户
4. 用户向改 IP 节点（DNS 服务器）发出请求
5. 由于是第一次访问，CDN 服务器会向原 web 站点请求，并缓存内容
6. 请求结果发给用户

## webpack

### 概述

> 本质上，*webpack* 是一个现代 JavaScript 应用程序的*静态模块打包器(module bundler)*。当 webpack 处理应用程序时，它会递归地构建一个*依赖关系图(dependency graph)*，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 *bundle* 

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftxt5vlyfsj30iw07hq41.jpg)



### 安装

**node**

webpack 运行基于 node 环境，在升级到 4.x+ 版本以后，运行环境升级，node-v >= 6.11.5，[官网下载](https://nodejs.org/zh-cn/) 循环下一步安装即可，安装时不要有中文路径，安装完成后可选择性的 [配置环境](https://www.jianshu.com/p/03a76b2e7e00) (不是必须)

```shell
# 查看 node 版本
node -v

# 查看 npm 版本
npm -v
```

**git**

我们打算用 git 来进行指令操作，所以 [官网下载](https://git-scm.com/)，循环下一步安装

如果在 git 中查看 node 版本时出现以下提示，重启电脑即可

```
bash: node: command not found
```

**webpack**

全局安装 webpack，出现 `+ webpack@4.x` 代表安装成功，下同

```shell
# 全局安装 webpack
npm install webpack -g
```

webpack 4.x+ 中，CLI 移到了 webpack-cli 中，需要单独安装

```shell
# 全局安装 webpack-cli
npm install webpack-cli -g
```

安装静态服务 package （不是必须，但是几乎所有项目都要用到，这里一并安装了）

```shell
# 全局安装 webpack-dev-server
npm install webpack-dev-server -g
```

完成了以上操作后，已经在全局安装了 webpack 及 webpack-cli（命令行接口），接下来我们在本一个本地项目中使用 webpack，在本地新建一个文件夹然后右键 `Git Bash Here`

本地局部安装 webpack

```shell
# 局部安装 webpack
npm install webpack
```

本地局部安装 webpack-cli

```shell
# 局部安装 webpack-cli
npm intall webpack-cli --save-dev

# --save-dev 意为在本地开发模式下安装，在 webpack 4.x+ 版本中，它等同于
npm install webpack-cli -D
```

初始化项目，生成 `package.json` 配置文件

```shell
npm init
```

至此，局部 webpack 安装完成，但是如果直接使用 `webpack` 命令，会出现以下错误

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftxstqauisj30pc06qwgh.jpg)

因为 webpack 4.x+ 会默认指定一个入口文件和一个出口文件，这个入口文件需要我们自己创建

```shell
# 在刚刚新建的本地目录下，创建 "src/index.js"
```

这时，我们再使用 webpack 命令，不会报错，而且本地目录下会自动创建 "dist/main.js"，这便是输出；虽然不会报错，但使用这个命令还是会提示警告，类似于

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftxt05s2g5j30pc05vmyp.jpg)

这是因为我们没有配置 webpack 模式，这个后续再提，不影响接下来的操作

### 基本概念

入口[entry]

> **入口起点(entry point)**指示 webpack 应该使用哪个模块，来作为构建其内部*依赖图*的开始。进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的 

出口[output]

> **output** 属性告诉 webpack 在哪里输出它所创建的 *bundles*，以及如何命名这些文件，默认值为 `./dist`。基本上，整个应用程序结构，都会被编译到你指定的输出路径的文件夹中 

loader

> *loader* 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只理解 JavaScript）。loader 可以将所有类型的文件转换为 webpack 能够处理的有效[模块](https://webpack.docschina.org/concepts/modules)，然后你就可以利用 webpack 的打包能力，对它们进行处理

插件[plugins]

> loader 被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量。[插件接口](https://webpack.docschina.org/api/plugins)功能极其强大，可以用来处理各种各样的任务 

模式

> 通过选择 `development` 或 `production` 之中的一个，来设置 `mode` 参数，你可以启用相应模式下的 webpack 内置的优化 

### 基本使用

以上基本概念中提到的属性，均可以在 `webpack.config.js` 中进行配置，下面介绍基本语法

**模式**

方法一：在 webpack.config.js 文件中配置

```js
// 方法一：在 webpack.config.js 文件中配置
module.exports = {
    mode: 'development'
}
```

方法二：从 CLI 参数中传递

```shell
# 方法二：从 CLI 参数中传递
webpack --mode=production

# 或者用空格 ' ' 代替 "="
webpack --mode production
```

方法三：或者在 package.json 文件中的 "scripts" 属性下进行配置，然后配合 npm 指令运行

```json
// 方法三：或者在 package.json 文件中的 "scripts" 属性下进行配置，然后配合 npm 指令运行
"scripts": {
    // ...,
    "dev": "webpack --mode development"
}
```

```shell
# npm指令，配合方法三
npm run dev
```

**入口**

可自定义入口文件，默认是我们创建时所提供的 `src/index.js`

单个入口

```js
const config = {
    entry: './src/entrance.js'
}
module.exports = config;
```

多个入口

```js
const config = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};
```

**输出**

配置 `output` 选项可以控制 webpack 如何向硬盘写入编译文件。注意，即使可以存在多个 `入口` 起点，但只指定一个 `输出` 配置 

在 webpack 中配置 `output` 属性的最低要求是，将它的值设置为一个对象，包括以下两点：

- `filename` 用于输出文件的文件名
- 目标输出目录 `path` 的绝对路径

```js
module.exports = {
  // ...
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
}

// 或者多个入口生成不同文件
module.exports = {
  entry: {
    foo: './src/foo.js',
    bar: './src/bar.js',
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist',
  },
}

// 路径中使用 hash，每次构建时会有一个不同 hash 值，避免发布新版本时线上使用浏览器缓存
module.exports = {
  // ...
  output: {
    filename: '[name].js',
    path: __dirname + '/dist/[hash]',
  },
}
```

**loader**

当我们需要使用不同的 loader 来解析处理不同类型的文件时，我们可以在 `module.rules` 字段下来配置相关的规则，例如使用 Babel 来处理 .js 文件： 

```js
module: {
  // ...
  rules: [
    {
      test: /\.jsx?/, // 匹配文件路径的正则表达式，通常我们都是匹配文件类型后缀
      include: [
        path.resolve(__dirname, 'src') // 指定哪些路径下的文件需要经过 loader 处理
      ],
      use: ['babel-loader'] // 指定使用的 loader
    },
  ]
}
```

使用前需要先下载相应的 loader

```shell
# 下载 babel-loader，要与 babel-loader 一起安装
npm install babel-core babel-loader -D

# 可以一次下载多个 loader
npm install css-loader style-loader -D
```

**插件**

[插件](https://webpack.docschina.org/plugins/)是 webpack 的支柱功能。webpack 自身也是构建于，你在 webpack 配置中用到的**相同的插件系统**之上！

插件目的在于解决 loader 无法实现的**其他事**

```js
const UglifyPlugin = require('uglifyjs-webpack-plugin')

module.exports = {
  plugins: [
    new UglifyPlugin()
  ],
}
```

使用前需要先下载相应的插件

```shell
npm install uglifyjs-webpack-plugin -D

# 可以一次下载多个插件
npm install uglifyjs-webpack-plugin extract-text-webpack-plugin@next -D
```

**模块**

对比 node.js 模块，webpack 模块能够以各种方式表达他们的依赖关系

```
- ES6
	import
- CommonJS
	require
- AMD
	define
	require
- css / sass / less
	@import
- url
	url
	image url
```

### 基本命令

```shell

```

### 搭建基本的前端开发环境

```
- 构建我们发布需要的 HTML、CSS、JS 文件
- 使用 CSS 预处理器来编写样式
- 处理和压缩图片
- 使用 Babel 来支持 ES 新特性
- 本地提供静态服务以方便开发调试
```

### 配置loader

在 `module.rules` 数组中进行 loader 的配置，该数组中每一个对象对应一条 loader 规则

```js
module.exports = {
  // ...
  module: {
    rules: [ 
      {
        test: /\.jsx?/, // 条件
        include: [ 
          path.resolve(__dirname, 'src'),
        ], // 条件
        use: 'babel-loader', // 规则应用结果
      }, // 一个 object 即一条规则
      // ...
    ],
  },
}
```

在每一条规则中，有两种关键配置：匹配条件 和 匹配后的应用

匹配条件：

```
- 匹配特定的条件
	{ test: ... }
- 匹配特定的路径
	{ include: ... }
- 排除特定的路径
	{ and: [...] }
- 匹配数组中任意一个条件
	{ or: [...] }
- 排除匹配数组中所有的条件
	{ not: [...] }
```

通常会结合使用 test / and 和 include & exclude 来进行条件配置

匹配后的应用：

用 module.rules 中的 `use` 属性进行配置，可以是字符串、对象或者数组，可以使用 `optionis` 给对应的 loader 传递一些配置项，可以参见官网对不同 loader 的配置说明

```js
rules: [
  {
    test: /\.less/,
    use: [
      'style-loader', // 直接使用字符串表示 loader
      {
        loader: 'css-loader',
        options: {
          importLoaders: 1
        }
      }, // 用对象表示 loader，可以传递 loader 配置等
      {
        loader: 'less-loader',
        options: {
          noIeCompat: true
        } // 传递 loader 配置
      }
    ]
  },
]
```

loader 应用顺序

对于同一个 `rule` 中的 loader，应用顺序从后向前，对于不同 `rule` 中的 loader，应用顺序是：前置 > 行内 > 普通 > 后置，前置和后置通过 `rule` 中的 `enforce` 字段来设置，行内 loader 是在应用代码中引用依赖时直接声明使用的 loader，如 `const json = require('json-loader!./file.json')` 这种，不建议在应用开发中使用这种 loader。其他的为普通 loader

```js
rules: [
  {
    enforce: 'pre', // 指定为前置类型，post 为后置类型
    test: /\.js$/,
    exclude: /node_modules/,
    loader: "eslint-loader",
  },
]
```

使用 `noParse`

除了 module.rules 字段用于配置 loader 之外，还有一个 module.noParse 字段，可以用于配置哪些模块文件的内容不需要进行解析。对于一些不需要解析依赖（即无依赖） 的第三方大型类库等，可以通过这个字段来配置，以提高整体的构建速度

> 使用 `noParse` 进行忽略的模块文件中不能使用 `import`、`require`、`define` 等导入机制。 

```js
module.exports = {
  // ...
  module: {
    noParse: /jquery|lodash/, // 正则表达式

    // 或者使用 function
    noParse(content) {
      return /jquery|lodash/.test(content)
    },
  }
}
```

### webpack-dev-server

webpack-dev-server 是 webpack 官方提供的一个工具，可以基于当前的 webpack 构建配置快速启动一个静态服务。当 mode 为 development 时，会具备 hot reload 的功能，即当源码文件变化时，会即时更新当前页面，以便你看到最新的效果

安装

```shell
npm install webpack-dev-server -g
```

使用

```shell
webpack-dev-server --mode development
```

建议把 webpack-dev-server 作为开发依赖安装，然后使用 npm scripts 来启动 

```json
// package.json
{
  // ...
  "scripts": {
    // ...
    "start": "webpack-dev-server --mode development"
  }
}
```

webpack-dev-server 默认使用 8080 端口，如果你使用了 html-webpack-plugin 来构建 HTML 文件，并且有一个 index.html 的构建结果，那么直接访问 `http://localhost:8080/` 就可以看到 index.html 页面了。如果没有 HTML 文件的话，那么 webpack-dev-server 会生成一个展示静态资源列表的页面

### 使用 HMR

HMR 全称是 Hot Module Replacement，即模块热替换。在这个概念出来之前，我们使用过 Hot Reloading，当代码变更时通知浏览器刷新页面，以避免频繁手动刷新浏览器页面。HMR 可以理解为增强版的 Hot Reloading，但不用整个页面刷新，而是局部替换掉部分模块代码并且使其生效，可以看到代码变更后的效果。所以，HMR 既避免了频繁手动刷新页面，也减少了页面刷新时的等待，可以极大地提高前端页面开发效率

配置使用

```js
const webpack = require('webpack')

module.exports = {
  // ...
  devServer: {
    hot: true // dev server 的配置要启动 hot，或者在命令行中带参数开启
  },
  plugins: [
    // ...
    new webpack.NamedModulesPlugin(), // 用于启动 HMR 时可以显示模块的相对路径
    new webpack.HotModuleReplacementPlugin(), // Hot Module Replacement 的插件
  ],
}
```

### 优化前端资源加载

#### 图片加载优化和代码压缩

##### CSS Sprites



##### 图片压缩

在一般的项目中，图片资源会占前端资源的很大一部分，既然代码都进行压缩了，占大头的图片就更不用说了。 我们之前提及使用 file-loader 来处理图片文件，在此基础上，我们再添加一个 image-webpack-loader 来压缩图片文件。简单的配置如下：

```js
module.exports = {
  // ...
  module: {
    rules: [
      {
        test: /.*\.(gif|png|jpe?g|svg|webp)$/i,
        use: [
          {
            loader: 'file-loader',
            options: {}
          },
          {
            loader: 'image-webpack-loader',
            options: {
              mozjpeg: { // 压缩 jpeg 的配置
                progressive: true,
                quality: 65
              },
              optipng: { // 使用 imagemin-optipng 压缩 png，enable: false 为关闭
                enabled: false,
              },
              pngquant: { // 使用 imagemin-pngquant 压缩 png
                quality: '65-90',
                speed: 4
              },
              gifsicle: { // 压缩 gif 的配置
                interlaced: false,
              },
              webp: { // 开启 webp，会把 jpg 和 png 图片压缩为 webp 格式
                quality: 75
              },
          },
        ],
      },
    ],
  },
}
```

##### 使用 DataURL

有的时候我们的项目中会有一些很小的图片，因为某些缘故并不想使用 CSS Sprites 的方式来处理（譬如小图片不多，因此引入 CSS Sprites 感觉麻烦），那么我们可以在 webpack 中使用 url-loader 来处理这些很小的图片。 url-loader 和 file-loader 的功能类似，但是在处理文件的时候，可以通过配置指定一个大小，当文件小于这个配置值时，url-loader 会将其转换为一个 base64 编码的 DataURL，配置如下

```js
module.exports = {
  // ...
  module: {
    rules: [
      {
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192, // 单位是 Byte，当文件小于 8KB 时作为 DataURL 处理
            },
          },
        ],
      },
    ],
  },
}
```

##### 代码压缩

对于 HTML 文件，之前介绍的 html-webpack-plugin 插件可以帮助我们生成需要的 HTML 并对其进行压缩 

```js
module.exports = {
  // ...
  plugins: [
    new HtmlWebpackPlugin({
      filename: 'index.html', // 配置输出文件名和路径
      template: 'assets/index.html', // 配置文件模板
      minify: { // 压缩 HTML 的配置
        minifyCSS: true, // 压缩 HTML 中出现的 CSS 代码
        minifyJS: true // 压缩 HTML 中出现的 JS 代码
      }
    }),
  ],
}
```

对于 CSS 文件，我们之前介绍过用来处理 CSS 文件的 css-loader，也提供了压缩 CSS 代码的功能：

```js
module.exports = {
  module: {
    rules: [
      // ...
      {
        test: /\.css/,
        include: [
          path.resolve(__dirname, 'src'),
        ],
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              minimize: true, // 使用 css 的压缩功能
            },
          },
        ],
      },
    ],
  }
}
```

对于 JS 文件，使用 uglifyjs-webpack-plugin 插件进行压缩

```js
const UglifyPlugin = require('uglifyjs-webpack-plugin');
const config = {
    // ...
    plugins: [
        new UglifyPlugin()
        // ...
    ]
}
module.exports = config;
```

### 常见错误

> Error: Cannot find module 'less'

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftyky70xywj30pc01awen.jpg)

```shell
# 原因：less-loader 与 less 是相互依赖的，在使用 less 开发时，两者都要安装
npm install less -D
```

> (node:20256) DeprecationWarning: Tapable.plugin is deprecated. Use new API on `.hooks` instead

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftynwlqhx9j30ra02it9l.jpg)

```shell
# 原因：'extract-text-webpack-plugin' 不支持 webpack 4.x+ 版本
# 使用 alpha 版本
npm install extract-text-webpack-plugin@next -D
# 或者使用支持 webpack 4.x+ 的正式版本，这个具体用法和 extract-text-webpack-plugin 不一样，详细见链接
npm install mini-css-extract-plugin -D
```

[mini-css-extract-plugin](https://github.com/webpack-contrib/mini-css-extract-plugin)

> ERROR in ./src/less/index.less 1:0
> Module parse failed: Unexpected character '@' (1:0)
> You may need an appropriate loader to handle this file type.
>
> > @import 'base.less';
> > |
> > | .wrapper {
> > @ ./src/js/index.js 1:0-29

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftyoq92kpbj30r902ut94.jpg)

出现这样类似的问题，有可能是 `webpack.config.js` 中 `module.rules` 中的 `test` 属性匹配错误（比如正则表达式的错误）