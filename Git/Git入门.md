## 下载安装

官网下载，循环下一步安装

```
https://git-scm.com/downloads
```

## 基本工作流

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftvcrvzubmj30hr07vdfv.jpg)





## 基本指令

### GitHub账户

```
https://www.github.com
```

登录以上GitHub网站，注册属于你的GitHub账户

### 配置环境

> SSH配置

```shell
ssh-keygen
```

1. 在桌面或者某一个空文件夹下，右键选择 `Git Bash Here`，在打开的命令行中输入以上指令
2. 首先他会询问想要把秘钥存放在本地的路径，这里直接回车选择默认路径即可；后面两步输入回车或者是 `y`
3. 完成后找到第一步选择的路径下 `.ssh` 文件下的 `id_rsa.pub` 文件，用记事本打开，复制其中的公钥
4. 打开你的GitHub网站，点击头像，在下拉菜单中选择 `settings`，在左侧菜单中选择 `SSH and GPG keys`
5. 右侧点击绿色 `New SSH key` 按钮，Title栏中输入自定义名称（一般为当前机器名称，代表给哪台机器配置了 了 SSH 环境），在 Key 栏中粘贴刚才复制的内容
6. 配置完毕

> 本地环境配置

```shell
git config --global user.name <username>

git config --global user.email <useremail>
```

在命令行中输入以上指令，注意尖括号内为自定义内容：

username：GitHub的用户名

useremail：GitHub的邮件地址

> 查看本地配置

```shell
git config --list
```

### 工作目录 & 本地仓库

> 创建工作目录

在本地新建一个文件夹作为**工作目录**

> 初始化本地仓库

```shell
git init
```

在工作目录文件夹，右键鼠标选择 `Git Bash Here`，在打开的命令行窗口中输入以上指令，用来初始化本地仓库，成功之后，在该文件夹会有一个隐藏的 `.git` 文件夹，包含所有的版本信息，这就是我们的**本地仓库**

### 远程仓库

> 创建远程仓库

打开GitHub网站，登录GitHub账号，点击右上角头像，在下拉菜单中选择 `Your repositories`，在打开的页面中，点击右侧绿色的 `New` 按钮，新建一个远程仓库，根据提示输入相关的信息

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftvcm06x80j309s09sa9y.jpg)

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftvcmf4pu3j30l10g674u.jpg)



创建成功之后的界面如下

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftvcp3buvcj30tv0f7dga.jpg)

### 关联

> 本地分支与远程分支建立关联

```shell
git remote add <name> <repository>
```

之前我们已经创建好了本地仓库和远程仓库，那怎么把两者关联起来了呢？使用上述命令进行关联，注意 \<> 内的内容为自定义，其代表的含义如下

name：给要关联的远端仓库起个别名

repository：要关联的远端仓库的地址

别名可以自定义，那这个远端仓库的地址在哪获取呢？步骤如下：

1. 打开GitHub网站，登录后点击头像，选择 `Your repositories`
2. 选择你要关联的远端仓库(如之前教程中创建的test仓库)
3. 点击右侧绿色的 `Clone or download` 按钮，复制下面的地址，此地址即为上面命令中的 \<repository>

> 查看远端仓库的别名

```shell
git remote
```

> 重命名远端仓库

```shell
git remote rename <oldname> <newname>
```

如果想给远程仓库重命名，使用这条指令，注意 \<> 内的内容为自定义，其含义如下

oldname：远端仓库原来的名字

newname：远端仓库新的名字

> 查看远程仓库

```shell
git remote -v
```

查看已关联的远程仓库

### 工作

> 创建或修改工作目录中的文件

完成了创建以及关联的工作后，我们就可以进行工作了，我们的工作区还没有任何的文件，所以我们在工作目录新建一个文件，如 `index.html`

> 查看当前文件状态

```shell
git status
```

如果工作目录中的某一个文件是刚刚创建的或者刚刚被修改过的，那么我们输入这条指令后，会提示我们 `Untracked files`，在这条提示的下面列出了所有的 `Untracked files`，表示这些文件是未被追踪的，即对于本地仓库来说，这些文件是不存在的，所以我们要先把这些文件提交到 **暂存区**，方法如下

> 添加到暂存区

```shell
git add <file>

git add .
```

第一条指令表示要添加哪个文件到暂存区，\<file> 代表文件，第二条指令表示将工作目录中所有文件都添加到暂存区中去；把文件添加到暂存区是为了临时保存，比如在开发过程中临时有事，暂时不能开发，那就先把文件添加到暂存区中，方便后续继续进行修改；如果我们已经确定开发完成，那么就可以把暂存区中的内容提交到本地仓库，方法如下

> 提交到本地仓库

```shell
git commit -m <description>
```

-m 是 message 的意思，代表这次提交的描述信息，比如这是第几次提交、这是第几次修改等等，\<description> 就是用来写这个描述信息

> 提交内容到远程仓库

```shell
git push <remote> <branch>
```

将本地仓库中的内容提交到远程仓库中

remote：被提交的本地仓库

branch：提交到远程仓库中的哪个分支（分支的概念后面介绍，这里我们暂且只有一个 master 分支）

### 撤销

> 撤销工作区修改

```shell
git checkout -- <file>
```

撤销工作区的修改，是相对于暂存区而言的；比如我们将工作区 `index.html` 文件添加到暂存区，然后我们又在工作区对 `index.html` 文件进行了修改，修改了一大堆发现还是不修改比较好，当然这个时候我们可以一步步的 `Ctrl + z` ，但更好的方式是直接使用上述命令，工作区中的该文件直接回退到暂存区中这个文件的版本

> 查看提交日志

```shell
git log
```

查看所有的提交记录，包括 commit信息、作者、时间、描述信息，以及 `HEAD -> branch` 当前指向哪个版本

![](https://ws1.sinaimg.cn/large/006eYMu7ly1ftvhxyo77qj30l90bc0u3.jpg)

> 查看提交id

```shell
git reflog
```

查看所有提交的 `commit ID`，以及 `HEAD -> branch` 当前指向哪个版本

> 版本回退

```shell
git reset (--hard | soft | mixed) (<HEAD~ num> | <commit ID>)
```

1. `--hard`：重置位置的同时，清空工作目录的所有改动
2. `--soft`：重置位置的同时，保留并做目录和暂存区的内容，并把重置 `HEAD` 的位置所导致的新的文件差异放进暂存区
3. `--mixed`：默认参数，重置位置的同时，保留工作目录的内容，并清空暂存区

使用举例：

使用 hard 参数回退一个版本

```shell
git reset --hard HEAD~ 1

git reset --hard HEAD^
```

使用 mixed 参数退回两个版本

```shell
git reset --mixed HEAD~ 2

git reset HEAD~2
```

使用 soft 参数回退一个版本

```shell
git reset --soft HEAD~ 1
```

使用 hard 参数回退到指定版本

```shell
git reset --hard <commit ID>
```

### 差异比较

> 比较工作区和暂存区的内容

```shell
git diff
```

> 比较暂存区和本地仓库最近一次commit内容

```shell
git diff --cached
```

> 比较工作区与本地仓库最近一次commit内容

```shell
git diff HEAD
```

> 比较两个commit之间的差异

```shell
git diff <commit ID> <commit ID>
```

### 分支

不同分支之间互不影响

> 查看分支

```shell
git branch
```

> 创建新分支

```shell
git branch <name>
```

> 切换分支

```shell
git checkout <name>
```

> 创建并切换分支

```shell
git checkout -b <name>
```

> 删除本地分支

```shell
git branch -d <name>
```

> 删除远程分支

```shell
git push -d <remote> <branch>
```

> 合并分支

```shell
git merge <branch>
```

如果有分支冲突，选择保留哪一个分支的设置，然后 `add`、`commit`

> 将本地分支推到远程分支上

```shell
git push <remote> <branch1>:<branch2>
```

branch1：本地分支

branch2：远程分支

### clone

> 克隆GitHub的项目

```shell
git clone <repository>
```


