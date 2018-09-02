# what

npm 是一个包管理工具，大致由三部分组成

+ 网站

  开发者查找包（package）、设置参数以及管理 npm 使用体验的主要途径

+ 注册表（registry）

  *注册表* 是一个巨大的数据库，保存了每个包（package）的信息，我们在 cli 中使用 `npm install` 或者 `npm update` 等操作时，都会先访问 registry 查找包的相关信息，然后根据这些信息到网站执行对应操作

+ cli

  you know，where we use it

# install

安装 node 环境，node 环境中集成了 npm 包管理工具

# install method

+ `npm install <package> -g`

  全局安装，安装的包在 node 路径下的 [node modules] 中

+ `npm install <package>`

  + 本地安装，安装的包在项目目录下的 [node modules] 中
  + 不会被写入项目的 [package.json] 文件中，使用 `npm install` 安装项目依赖时不被安装

+ `npm install <package> --save`

  + 本地安装，安装的包在项目目录下的 [node modules] 中

  + 会被写入项目的 [package.json] 文件中的 `dependencies` 对象中，使用 `npm install` 安装项目依赖时会被安装
  + 发布时依赖，即项目发布仍需要使用的包

+ `npm install <package> --save-dev`

  - 本地安装，安装的包在项目目录下的 [node modules] 中

  - 会被写入项目的 [package.json] 文件中的 `devDependencies` 对象中，使用 `npm install` 安装项目依赖时会被安装
  - 开发时依赖，即项目开发、构建时所以依赖的包，项目的发布时不需要这些包

要明确不同安装方法的区别，尤其是 `--save` 和 `--save-dev` 的区别，因为如果发布时有一些不必要的开发依赖包，会影响整个项目的体积性能等；一般发布时依赖较少，如 vue，vue-router，vuex 等；开发时依赖较多，如 vue-loader，css-loader，webpack 等