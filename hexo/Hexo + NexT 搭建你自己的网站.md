## 概述

参考：[个人博客](http://qht97.com)

### 写在前面

个人爱好，对于新旧知识喜欢通过整理笔记来记录或梳理知识点(主要还是脑子不太好使记不住)，之前一直使用笔记软件记录，从 [oneNote] 转到 [为知笔记] 又转到 [有道云笔记]，不是很喜欢他们的 [markdown] 编辑器，而且 [为知笔记] 还曾经把我的几篇笔记给搞丢了，最后想了想还是搭个自己的博客比较靠谱，既可以打造自己的风格，还能分享交流知识，一举多得。自己的博客还在搭建中，所以暂时使用 [GitHub Pages] 托管。

### 版本

首先将我搭建博客时所使用的环境或者插件的版本摆在前面，以供参考（可略过）

```
- node
	v8.11.3
- git
	v2.17.0.windows.1
- hexo
	v3.7.1
- hexo-cli
	v1.1.0
- NexT
	v6.4.0
```

### 参考

其实利用 [Hexo] 脚手架工具搭建博客相对简单，我们不需要做任何的编码工作，只需要按照自己的需求进行相应的配置，并托管到 [GitHub Pages] 上，至于配置的方法，个人建议参照官方的文档，不仅有详细的说明，还有技术交流社区帮你解决可能遇到的各种错误，我在搭建中参考的官方文档如下，列做参考

+ [NexT](https://theme-next.iissnan.com/getting-started.html)
+ [Hexo](https://hexo.io/zh-cn/docs/)

## 环境

### Node

>  安装 [Hexo] 需要 [Node] 环境，所以首先要安装 [Node]

到 [Node.js] 中文 [官网](http://nodejs.cn/download/) 下载对应操作系统的安装文件，执行安装文件进行安装，持续下一步即可，注意，安装路径可以自定义，但是路径中不要出现中文，安装完成后，在 [cmd] 中使用以下指令查看 [Node] 版本，正确显示版本号则安装成功（因为我们还没有安装 [Git]，所以暂时使用 [cmd] 验证）

```shell
# 查看 Node 版本
node -v
```

### Git

> 整个搭建我们使用 [Git] 命令行终端，使用 [GitHub Pages] 托管也需要使用 [Git] 提交，所以要安装 [Git]

安装方法类似 [node] 安装，[官网](https://git-scm.com/)下载，持续下一步即可，同样注意安装路径中不要出现中文，安装完成后，在你桌面右键，这时出现的菜单中会多出两个选项，[Git GUI Here] 和 [Git Bash Here]，这是两种使用 [Git] 的方式，当然我们选择 [Git Bash Here]，点击后在弹出的 [Git] 终端中输入以下指令，查看你安装的 [Git] 版本，当然我们也可以在在这里查看之前安装的 [Node] 的版本

```shell
# 查看 Git 版本
git version

# 查看 Node 版本
node -v
```

### Hexo

上述环境安装完成后，[Hexo] 所需要的环境以准备完毕，下面可以安装 [Hexo] 了

> 在任意一个文件夹下（桌面即可），右键选择 [Git Bash Here]，使用以下命令全局安装 [Hexo]

```shell
# 全局安装 [Hexo]
npm install hexo-cli -g

# 或者
npm install -g hexo-cli
```

至此，搭建博客的环境需求已安装完毕，接下来就可以愉快的建站了

## 本地站点

在将博客部署到服务器上之前，我们首先要在本地搭建好站点

> 首先，创建本地站点存放的文件目录

```shell
# 新建文件夹，用来存放本地站点，路径自定义，不要使用中文
# 举个例子，为了演示，我在桌面新建了一个博客项目，所以我的博客根路径是 [C:\Users\QHT\Desktop\blog]
# 如果你想在 E 盘根目录下创建 blog 项目也是完全可以，这样你的博客根目录就是 [E:\blog]
```

> 点开你所创建的文件夹，右键选择 [Git Bash Here]，使用以下命令初始化站点，并下载或更新相应的包

```shell
# 初始化站点
hexo init

# 下载相应的资源包
npm install
```

> 编译生成静态文件

```shell
# 生成静态文件
hexo generate

# 简写
hexo g
```

> 在本地服务器预览：启动服务器，将主机（域名+端口号）复制到浏览器地址栏中进行预览

```shell
# 启动服务器
hexo server

# 简写
hexo s
```

> 上面编译生成静态文件和开启本地服务可合并成一步，可单独执行以上两步，或者直接执行这一步

```shell
# 编译并开启服务器(顺序不要写反)
hexo s -g
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8524wc9nj311y0hoakh.jpg)

看到这个界面，是不是有点小激动~

## 部署

当然仅仅创建本地站点无法让别人来访问（不能愉快的和小伙伴那啥），所以我们需要把本地站点部署到服务器上

### 注册 GitHub

[GitHub] 这里就不介绍了，全球最大的 JI 友交流社区，还没有 Gay 友通行证的同学抓紧时间了，[Gay 网传送门](https://github.com/)，注册邮箱一定要正确，不然收不到验证邮件很麻烦，用户名建议自己名字全拼或者简拼，万一哪天就火了呢

### 配置 SSH

[GitHub] 是一个分布式的版本控制系统，可以用来托管我们的代码，它相当于一个远程仓库，那如何将远程仓库和我们的电脑关联起来呢？通过配置 SSH

> 首先在我们电脑任意文件夹下（桌面即可）右键，选择 [Git Bash Here]，输入以下指令

```shell
# 配置 SSH 私钥
ssh-keygen
```

输入以上指令后，命令行会提示你秘钥的路径等信息（记住这个路径），对于所有的提示全部回车选择默认即可，配置完成后，在它默认的文件夹下会生成两个文件，[id_rsa] 和 [id_rsa.pub]，前者是 [SSH私钥]，后者是 [SSH公钥] 

> 执行以下命令将 [SSH公钥] 复制到剪切板中

```shell
# 复制公钥
clip < ~/.ssh/id_rsa.pub
```

> 打开你的 [GitHub]，点击右上角你的头像，下拉菜单中选择 [Settings]

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu86iniijij30770a4a9y.jpg)

> 左侧菜单栏中选择 [SSH and GPG keys]，右侧点击绿色 [New SSH key]

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu86j1giu4j30td0a1gmj.jpg)

> 在弹出的窗口中，[title] 栏输入名称，可自定义，建议写你操作的操作系统，比如 windows；[key] 栏内 `Ctrl + c` 将公钥粘贴进去，完成后点击 [Add SSH key]

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu86j6yq6kj30ub0bp74r.jpg)

### 创建远程博客仓库

在 [GitHub] 上创建一个远程仓库用来部署我们的本地博客仓库，具体步骤如下

> 点击右上角头像，下拉菜单中选择 [Your repositories]

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu86pbd0ulj305m09vgli.jpg)

> 页面跳转后，点击右上角绿色的 [New] 按钮新建仓库

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu86s32ntfj30tl07kdfw.jpg)

> 在设置页面中，填入相应的仓库信息

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu870cga48j30or0gbjsb.jpg)



> 创建完成后，点击你刚刚创建的仓库，将仓库地址复制下来，具体步骤如图

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu875iq8k9j30lb03yjrg.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu87780dzqj30su09qwfa.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu87an1hm3j30sv0aagmb.jpg)

### 安装部署插件

因为我们要把本地站点推送到 [GitHub] 服务器上，所以要先安装相关的插件

> 回到 [Git] 终端，在本地站点根路径下，执行以下命令

```shell
# 安装插件
npm install hexo-deployer-git --save
```

### 本地站点与远程仓库关联

> 找到你创建本地站点的目录，选择根目录下的 [_config.yml] 文件，用记事本打开

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu87dy7wlxj307g05na9v.jpg)

> `Ctrl + f` 定位到 [deploy]，按照以下格式设置

```
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]
```

首先强调格式，[deploy] 没有缩进，[type]、[repo] 等四个属性名缩进两个空格，属性值与属性名之间缩进一个空格，要严格按照格式配置，不然会出错；

[type] 代表部署类型，我们使用 [git] 部署，所以这里填 `git`；[repo] 是你远程仓库的地址，就是我们在 [创建远程博客仓库] 这一步中复制的地址（如果这之间你进行了其他的复制操作，请回到 [GitHub] 中再复制一遍）；[branch] 是分支结构，我们填 `master` 即可；[message] 可以不填，给个样例（填你自己的仓库名，填我的没用）

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu87vcbw92j30dr02w3yb.jpg)

### 编译部署

> 每次部署前，都要执行这一步操作，以清除缓存的静态文件

```shell
# 清除
hexo clean
```

> 编译项目，生成静态文件

```shell
# 编译
hexo g
```

> 部署到服务器上

```shell
# 部署
hexo deploy

# 简写
hexo d
```

> 以上两步可以合并为一步，可单独执行上面两步，也可直接执行这一步

```shell
# 合并写法
hexo g -d

# 或者
hexo d -g
```

### 预览

执行完上述所有的部署操作后，我们的本地站点便部署到了服务器上，这代表我们可以通过域名来访问我们的博客

> 在地址栏中输入你博客的域名，格式如下，将 username 换成你 [GitHub] 的用户名

```
https://username.github.io
```

至此，博客已经搭建完毕，如果没有审美、绑定域名者其他功能的要求，恭喜你，工作结束，学会怎么发表文章就行了

## 本地测试

在进行接下来的一系列改动之前，我们先来介绍一下怎么在本地对所做的改动进行调试，因为我们一次可能做很多的改动，每个小改动后都要看看改动的效果有没有被实现，那不可能我们每次都把代码部署到服务器上，然后在服务器上观察效果，这样不仅将没有意义的代码推到了服务器上，还会消耗很多时间，所以我们应尽量的现在本地服务器中调试，确定没什么问题后，再部署到 [GitHub] 服务器上，大概有两种方法

> 编译静态文件，开启本地服务器测试效果

```shell
# 编译成静态文件
hexo g

# 开启本地服务器
hexo s

# 合并写法，注意顺序，不要写法
hexo s -g
```

在浏览器中通过 `localhost:4000` 进行访问，观察效果

> 在调试模式下，开启本地服务器测试效果

```shell
# 在调试模式下开启本地服务器
hexo s --debug
```

还是一样，在浏览器中通过 `localhost:4000` 进行访问，观察效果；在这种模式下，终端会记录编译以及我们执行各种操作时的调试信息并记录到 [debug.log] 中，我们可以根据调试信息找出找出错误

## 写作

### 三种布局

[Hexo] 有三种内置的布局模式，分别是 `post` (默认)、`draft`、`page`，三种布局代表了创建文章的三种不同的模式，以及文件存储的不同路径



| 布局       | 文章模式     | 存放路径       |
| ---------- | ------------ | -------------- |
| post(默认) | 要发表的文章 | source/_posts  |
| draft      | 草稿         | source/_drafts |
| page       | 单独的页面   | source         |
| 自定义     | -----------  | source/_posts  |

关于自定义布局这里不讲，很少会用到吧，这里内置的三种布局模式的创建方法及区别

### 创建文章

无论哪种布局，创建指令都是一样的，参数不同

```shell
# 创建文章
hexo new [layout] <title>
```

`layout` 代表布局模式，如果省略的话默认是 `post`；`title` 是文章的标题，自定义，这还需要强调的一点是，[Hexo] 中文章格式是 [.md] 的 [markdown] 文档，关于 [markdown] 文档的介绍、语法及使用技巧，会在另外一篇文章中介绍，以供新手参考，这里暂时不提

#### 发表文章

如果我们创建的文章，编辑完以后要直接发表，那么我们可以直接使用 `post` 布局模式创建文章，前面也强调过，这种方法创建的文章都在 [source/_posts] 目录下

```shell
# 创建 post 布局文章
hexo new post <title>

# 可以省略 post 参数，因为默认就是 post 布局
hexo new <title>

# 样例
hexo new "test"
```

以样例为例，如果执行了 `hexo new test` 这条语句，[source/_posts] 文件夹下就会出现一个 [test.md] 文档，这就是我们所创建的文档

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8at3pxkaj30hf03rdfs.jpg)

我们打开这个 [test.md] 这个文档

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8au5i3scj30u5075jr7.jpg)

文档上方有一个配置区域，叫做 [Front-matter]，用于指定当前文件的一些配置信息，默认给出了上图中三项

`title` 表示改文章的题目，默认是文件名，当然你可以改成其他的名字，但如果这里 `title` 没有指定值，那么在博客中显示的标题是 [未命名]；`date` 表示文章被创建的时间，默认即创建文章时的系统时间，`tags` 表示文章的标签，这个后面再提，暂时不用，不理他或者删掉

我们在文章中写一些内容，比如 "谢谢你长得那么好看还看我的博客~"，`Ctrl + s` 保存并退出

> 本地测试

```shell
# 编译并开启本地服务
hexo s -g
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8bqs0jskj310v0g112r.jpg)

可以看到，本地站点中已经添加了我们的文章，以上便是，发表文章的基本流程

#### 草稿

无论我们是在本地测试还是部署到服务器，[source/_posts] 这个文件夹中的内容都会被编译，那么如我们有些文章还没有写完，不适合被发布到博客上，这时我们就要用到另一种布局 `draft` 了，即 [草稿]

> 创建 [草稿] 布局的文章

```shell
# 使用 draft 布局参数
hexo new draft "tmp"
```

前面提到过，`draft` 布局的文章会被保存在 [source/_drafts] 文件夹下，我们打开这个文件夹中刚刚创建的文件

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8c6glzjxj30h502rq2r.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8ceaxf7aj30pq07xdfm.jpg)

[草稿] 文件中也有 [Front-matter] 区域，包含了标题、标签信息，相比 `post` 布局的文章少了 `date` 属性，这是合理的，因为草稿文件不会被编译发布，所以创建时间是无意义的，可以根据实际需要自己配置，保存并退出，我们在本地测试一下，看看这篇 [草稿] 有没有被发布

> 本地测试（这里提醒一下，如果还处于上一次的测试状态中，可以先 `Ctrl + c` 结束）

```shell
# 编译并开启本地服务
hexo s -g
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8cr7749oj30yw0fj47y.jpg)

并没有我们创建的 [草稿] 文件 [tmp]

所以，我们利用 [草稿] 布局来创建一些暂时不需要传到服务器上的文件，如果需要把它当做发表文章时，我们可以使用命令将它移入 [source/_posts] 目录下

```shell
# 移动文件，举例
mv source/_drafts/tmp.md source/_posts
```

当然，我们也可以将 [source/_posts] 目录下暂时不发表的文章，在编译前先移入 [source/_drafts] 目录下

#### 更好的方法？

如果我们不想通过命令的方式来创建一片文章，我们可以现在本地任何一个地方创建 [.md] 文件，编辑结束后，如果需要发布，就把他移入 [blog/source/\_posts] 目录下，这样一来，省去了文章在 [source/\_drafts] 和 [source/_posts] 之间来回一定的麻烦，而且这可能也是最接近我们日常习惯的方法，但是使用这个方法有一点一定要注意，就是要 **手动配置 [Front-matter]**，因为是我们自己创建的文件，所以 [Hexo] 不会帮我们填入初始的 [Fromt-matter] 配置，但这又是我们发表文章必须的（至少 `title` 属性是必须的，因为如果 `title` 没有配置，那么博客中文章的名字将会是 [未命名]，当然，除非你想这么命名）

> 配置 [Front-matter] 区

```
要配置的属性很好写，重点是怎么开辟这块 [Front-matter] 区域，方法是在 [.md] 文档的最上方打三个连续的中划线 "---"（不包括引号），注意一定要是最上方，如果写在其他地方不仅设置不会生效，发布文章后还会出现未知的错误
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8dofi32kg30nf08qjrt.gif)

接下来把它移入到我们博客目录的 [source/_posts] 目录下，进行本地测试，结果如下

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8drhwlo1j30xt0ej7db.jpg)

关于第三种布局方式 `page` ，会在后面 [主题配置] 中讲到，这里暂时不提；至此，博客的搭建、部署、文章发表的讲解已全部结束，如果你满足于博客默认主体的外观，那么可以跳过下一节 [更换主题] 的讲解

## 更换主题

[Hexo] 内置的主题风格算是简约明了，但肯定满足不了骚年们 "花里胡哨" 的想法，所以下面讲解一下更换主题的方法

### 整体思路

[Hexo] 社区中有很多开源的好看的主题，安装方法大同小异，但是每一个主题自己的配置方法有所不同，所以不可能每一套主题都是一个公式进行配置，但可以参考以下整体的配置思路进行配置

```
- 思路
	- 下载主题
	- 应用主题
	- 配置主题
```

> 下载主题

+ 我们打开 [主题社区](https://hexo.io/themes/) 选择一个主题，点击进入博客页面

+ 进入后一般是开发者使用这个主题的博客模板，这个我们不用关心，我们找到作者的 [GitHub] 链接

+ 进入作者 [GitHub] 主页，找到对应主题的仓库

+ 点击进入此仓库，复制仓库地址

+ 回到 [Git] 终端中，把仓库克隆到本地博客目录下 [themes] 目录下

  ```shell
  # 如果 [Git] 当前的路径在你博客的根路径下，执行下面命令
  git clone <repository> themes/<filename>
  
  # <repository> 主题仓库名称
  # <filename> 是主题保存在本地的文件名，一般取为主题名称
  ```

  ```shell
  # 也可以先进入 [themes] 目录下，或者你的 [Git] 当前路径就在 [themes] 路径下，执行下面路径
  git clone <repository> <filename>
  ```

+ 操作完成后，博客根目录下的 [themes] 会多出一个以 \<filename> 命名的存放主题文件的路径

> 应用主题

+ 打开博客根目录下的 [_config.yml] 文件，`Ctrl + f` 定位到 `theme`，将名称修改为 [themes] 路径下，你想应用的主题的 \<filename>，还是一定要注意之前提到的格式的问题

+ `Ctrl + s` 保存退出后，重新编译并打开本地服务器测试

  ```shell
  # 本地测试
  hexo s -g
  ```

> 配置主题

每一个主题都有各自不同风格和功能，配置方法也就不尽相同，每个主题 [GitHub] 仓库中都有一份 [README.md] 文旦，这份文档介绍了该主题的配置方法，可参考该文档进行配置

### 使用 NexT

介绍了更换主题的整体思路，可能大家还是不会自己去配置，这里以我个人博客使用的 [NexT] 主题为例，带大家一步一步的配置一下，熟悉了这个主题的配置，其他主题配置起来也就得心应手了

#### 两个配置文件

再开始之前，先强调一下下面要用到的两个配置文件，一个是博客根目录下的 [_config.yml] 文件，我们称为 [站点配置文件]；另一个是 [themes/next] 路径下的 [\_config.yml] 文件，我们称为 [主题配置文件]；两者的文件名都一样，但是在不同的目录下，需要配置的内容也不同，后面的阅读中一定要注意是在哪个配置文件中进行配置

#### 下载主题

```shell
# 下载 NexT 主题到本地站点
# 保证 [Git] 当前路径在你的博客的根路径下，执行以下命令
git clone https://github.com/theme-next/hexo-theme-next.git themes/next
```

下载完成后，[themes] 文件夹下会出现我们下载的主题

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8jjic0u3j30if05lq2t.jpg)

#### 应用主题

在 [站点配置文件] 中，`Ctrl + f` 定位到 `theme` 属性，将属性值修改为 `next`

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8jlmokp9j30eb02f742.jpg)

#### 验证主题

```shell
# 本地调试
hexo s -g
```

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8k2971exj311k0hna9z.jpg)

这时再访问 `localhost:4000`，博客的主题已经变成了 [NexT] 主题的样子，应用成功

#### 排版风格

[NexT] 主题中内置了四种博客界面排版的风格，通过修改 [主题配置文件] 中的 `scheme ` 属性来更换排版风格

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8kczb9jqj30jq047glh.jpg)

本地测试，验证主题

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu8kfvuel9j30yx0fut8q.jpg)

现在博客的排版变成了这样样子，emmmm感觉比默认的要好看一点~

#### 站点描述

观察你现在的博客，无论是博客的名称还是作者的名称，都不属于你，虽然这博客是你搭建的，但现在还不属于你，你需要将这些信息修改为与你相关。在 [站点配置文件] 中， `Ctrl + f` 定位到 `site` 属性，配置信息如下



| 参数          | 描述                           |
| ------------- | ------------------------------ |
| `title`       | 网站标题                       |
| `subtitle`    | 网站副标题                     |
| `description` | 网站描述                       |
| `keywords`    | 搜索关键字                     |
| `author`      | 作者                           |
| `language`    | 网站使用的语言                 |
| `timezone`    | 网站时区，默认使用电脑的时区。 |

举例：

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu927agjshj30em03p743.jpg)

注意：

1. `keywords` 作为网站搜索关键字，用作 SEO，后续会另写一篇文章介绍 SEO，这里暂时可以先不写

2. `language` 作为网站所采用的语言，这个设定是一定要注意，官网或者网上的很多其他文章给出的属性值时 `zh-Hans`，可能是因为版本不一样，有一些更新，官网的文旦还没有跟上，其实这个属性我们可以自己查看，在 [themes/next/languages] 目录下，找到你想设置的文件对应哪个文件名即可

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu92flwnn5j30hr0a1q39.jpg)

3. `timezone` 是时区设置，默认跟随系统时间的时区，不填即可

4. 最后在强调一下格式问题（嗯前面好像说过好多次了），属性名和属性值之间用 ": "（冒号加一个空格分开）

#### 设置头像

在 [主题配置文件中]，`Ctrl + f` 定位到 `avatar` 字段，修改相应的属性，给个样例

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu937eftrpj30k105jdfw.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu93swvzq7j30dz0ev74g.jpg)

#### 第三方服务

既然是分享性质的博客，自然少不了 Gay 友们亲切的交流，[Hexo] 作为搭建博客的脚手架不提供像评论、搜索或者统计这样的服务，需要使用第三方服务，[NexT] 内置集成了许多实用的第三方服务，下面以 [不蒜子]，[来必力]，[Local Search] 为例介绍

##### 不蒜子统计服务

在 [主题配置文件] 中，`Ctrl + f` 定位到 `busuanzi_count`，将 `enable` 属性值改为 `true` 即可打开 [不蒜子] 统计服务，下面的三个值 `total_visitors`、`total_views`、`post_views`，分别代表 [站点总访客量]、[站点总阅读量]、[文章的阅读量]，默认值全部是 `true` ，即全部开启状态，保持默认即可

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu93rqrcggj307o03zjr6.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu93v2xfpgj30k8015jr5.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu93v945s6j30g103fglf.jpg)

##### 来必力评论服务

1. 首先到 [来必力官网](http://www.laibili.com.cn/) 注册账号

2. 注册成功后登录，选择顶部栏中的 [安装]，选择中间的 [免费] 版本即可，点击 [现在安装]

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu940hzx98j30wr0fyq48.jpg)

3. 在弹出的界面中，输入相应的数据，比如博客名称你可以写 `xxx'blog`，博客地址写你的 `https://username.github.io`，因为我已经安装过了，不会在弹出这个界面了，所以不能给你们截图了，但其实很好写，而且这里的设置在后台管理都可以修改，不要紧张哈~

4. 填写完成后就可以进入到后台管理界面了，点击左侧菜单栏中的 [代码管理]，右侧代码中第二行 `data-uid` 中的值复制

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu94cchonqj30k80ei3z2.jpg)

5. 回到 [主题配置文件] 中，`Ctrl + f` 定位到 `livere_uid ` 属性，将属性值修改为刚刚复制的值

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu94eusdypj30iz01zjr7.jpg)

6. 本地测试，点开一篇文章，你就可以看到文章底部的评论区了（可能要加载一会哦~）

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu94huh2n7j30o509bwef.jpg)

##### Local Search 搜索服务

在博客的根路径下，[Git] 终端中输入以下指令下载搜索服务插件

```shell
# 下载搜索服务插件
npm install hexo-generator-searchdb --save
```

在 [站点配置文件] 任意位置，添加以下配置：

```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

在 [主题配置文件] 中开启搜索服务

```
# Local search
local_search:
  enable: true
```

重新编译测试

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu94uy1lqxj30pr07bglj.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu94vnjdkej30rw0fdt90.jpg)

### 新建页

在 [写作] 这一节中我们介绍过文章一共有三种内置的布局，[发布文章] `post` ，[草稿] `draft`，[单独的页面] `page`，前两个我们已经讲过了，接下我们讲一下关于 [单独页面] 的用法

[单独页面] 的意思就是开辟一个新的页面，这个页面是专门为了解决一个功能而诞生的，比如 [标签页]、[分类页]、[关于页]，他们的添加方法基本相同，下面以这三种页面为例，介绍添加方法

> 在博客根目录下使用 [Git] 终端，输入以下指令

```shell
# 新建 [标签页]
hexo new page tags

# 新建 [分类与]
hexo new page categories

# 新建 [关于页]
hexo new page about
```

这时再 [source] 路径下就会多出三个我们新建的文件夹

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu95he0te0j30ip06gdft.jpg)

每个文件夹中都有一个 [index.md] 文件，这个文件就是最终要显示在我们博客中的一个单独的页

> 配置 [index.md] 文件夹

初始配置是这样的，只有页面的名称和创建时间

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu95lh55wmj30n202nmwx.jpg)

我们给页面添加类型描述，如果希望当前页面不被评论的话，还可以添加 `comments` 设置

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu95pfoar3j30mj03gjr6.jpg)

同理，可配置 [分类] 和 [关于] 页面

> 修改 [主题配置文件]

新建这些页面以后，我们可以把页面的添加到左侧的菜单栏中显示，在 [主题配置文件] 中，定位到 `menu`，将下面属性中对应的 `tags`、`categories`、`about` 前面的 ’#‘ 去掉以打开注释，保存退出，进行本地测试

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu95vn11zkj30qv09x0sn.jpg)

至此，这三个页面就添加成功了，但是你一定会点进去看一下的，看了以后发现，除了标题以外好像什么东西也没有，比如我们点进 [标签页] 中

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu95yng63aj30p508e0sl.jpg)

显示，暂无标签，那我们该怎么给这些页面添加内容呢？

对于 [关于页] 来说，直接在 [source/about] 路径下的 [index.md] 文件中，添加你想要展示的内容，比如说自我介绍，即可显示在博客中；而对于 [标签页] 和 [分类页] 来说，我们要在 [发布文章] 中的 [Front-matter] 区域添加`tags` 和 `categories` 属性，这里添加的属性值将会作为 [标签页] 和 [分类页] 内容的依据

比如，我们在[Hexo] 自带的 [hello-world] 文章中添加这些设置

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu9687rlbbj30n604y3yb.jpg)

进行本地测试

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu96bqfb3zj30tc063wec.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu96bj973dj30sg06ot8l.jpg)

两个页面中都有了我们设置的内容

### 添加社交链接

把你的一些其他网站的链接添加到博客中，有助于大家更多的了解你，也能分享更多的知识方法很简单

在 [主题配置文件] 中，`Ctrl + f` 定位到 `social` 属性，将前面的 `#` 去掉以取消注释打开此功能，在下面的链接选项中，把你想要添加的社交链接前面的 `#` 去掉，然后将后面 `url` 中 `yourname` 部分替换成你该社交链接相应的用户名，以 `GitHub` 为例

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu96p08by3j30g4055q2v.jpg)

这时博客中，就出现了对应的链接图标，点击图标即可访问链接

![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu96pz89eyj306c098wek.jpg)

至此，[Hexo] 使用 [NexT] 主题的基本介绍就全部完成了，除了文章中介绍的功能外，还有很多功能大家可以去探索，参考 [官方文档](https://theme-next.iissnan.com/getting-started.html) 或者其他的博文

### 部署到服务器

最后，别忘了你刚刚所做的修改都只是针对本地站点，还没有把它部署到服务器上，记得把它部署上去，然后通过你的域名 `https://yourname.github.io` 访问哦，部署方法文章开始便讲过了，这里给个提示

```shell
# 清除
hexo clean
# 编译部署
hexo g -d

# 合并写法
hexo clean && g -d
```

## 绑定个人域名

如果只能通过 `https://yourname.github.io` 形式的域名进行访问，总感觉不够酷，毕竟域名中除了自己的名字外还带了其他的名字，如果你想通过你心怡的专属的域名访问，那么你就需要进行接下来的绑定域名的操作了

### 说明

这里要提前说明的是，我个人的域名是在一年前买的，当时年级小不懂事，没有好好对比就选择了 [Godaddy] 平台，虽然入手叫便宜，但是续费的价钱比一般平台都要高，而且最可气的是，[Godaddy] 平台的隐私保护较差，如果不买他的隐私保护，你的个人信息将会暴露在网上，有可能收到各种各样的垃圾邮件或者短信，意思就是强制你买它的隐私保护套餐，这样一来，和其他平台相比就不是很划算了；现在想想也是悔不当初，最近已经打算把域名转到 [阿里云] 了，但因为博客搭建绑定域名时还在 [Godaddy]，所以下面的讲解就以此为参考，如果你手里有现成的 [Godaddy]，可以参考接下来的介绍，如果你正打算买域名来绑定，那建议选择 [阿里云] 或者 [Namesilo]

### 注册域名

参考上述说明

### 域名解析并绑定链接

推荐在 [DNSPod](https://www.dnspod.cn/) 进行解析，速度较快

1. 首先进入，[DNSPod](https://www.dnspod.cn/) 官网，登录或者注册

2. 成功登录后，在菜单栏选择 [域名解析] 并进入

3. 点击页面中绿色的 [添加域名] 按钮，并填入你的域名

4. 添加成功后会有这条域名的记录，点击进入

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu97w3z7npj30ly04gt8n.jpg)

5. 在进入的页面中，点击绿色 [添加记录] 按钮

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu97yh5ebkj30lo03ugll.jpg)

   主机记录：建议填 '@'

   记录值：在 cmd 中 ping 一下你的网站的网址（`https://yourname.github.io`），将 ip 值填入此

6. 保存记录，返回到 [Godaddy] 中进入 [DNS] 设置

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu984rd9iwj30yu06t0ss.jpg)

7. 更改域名服务器

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu9869p1vkj30i30h6t8t.jpg)

8. 在域名服务器修改页面，按照下图修改，保存

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu987dq51wj30r308l0sn.jpg)

9. 在本地博客根目录下的 [source] 路径下，新建一个 [CNAME] 文件，没有后缀，用记事本打开，写一行内容，即你的域名

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu98bdgwhrj308f05ndfn.jpg)

   ![](https://ws1.sinaimg.cn/large/006eYMu7ly1fu98bp51p6j309a02imwx.jpg)

10. 部署一下

  ```shell
  hexo clean
  hexo g -d
  ```

11. 如果域名正常解析的话，这时你就可以通过，你的域名愉快的访问你的博客了