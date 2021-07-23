# Git是什么

Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。



## 代码的迭代（版本的迭代）

版本控制(Revision control )是一种在开发的过程中用于管理我们对文件1目录或工程等内容的修改历史，方便查看更改历史记录，备份以便恢复以前的版本的软件工程技术。

* 实现跨区域多人协同开发
* 追踪和记载一个或者多个文件的历史记录
* 组织和保护你的源代码和文档
* 统计工作量
* 并行开发、提高开发效率
* 跟踪记录整个软件的开发过程
* 减轻开发人员的负担，节省时间，同时降低人为错误



**主流的版本控制工具：**

* **Git**（分布式版本控制）
* **SVN**（集中版本控制）
* **CVS**
* **VSS**
* **TFS**
* **Visual Studio Online**

Git现在是最先进的分布式版本控制系统。

## Git安装

Git官网：https://git-scm.com/

一致选择下一步就可，注意安装位置不要默认选择安装在C盘，选择自己的路径安装。

**Git三个工具的介绍：**

![image-20210721211932844](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210721211932844.png)

1. Git Bash：Unix和Linux风格的命令行，使用最多，最推荐使用
2. Git CMD：Windows风格的命令行
3. Git GUI：图形界面的Git，不建议使用，最不建议初学者使用。

### 简单的一些Linux命令

1. cd：切换目录
2. cd..：返回上一级目录
3. pwd：显示当前路径
4. clear：清屏
5. ls：列出当前文件夹下的所有的文件
6. touch：新建文件
7. rm：删除一个文件
8. mkdir：创建一个新的文件夹（目录）
9. rm -r：删除一个文件夹（目录）   rm -rf /  在Linux中代表删除所有文件
10. mv 111 111：移动一个文件到一个文件夹
11. reset：重新加载终端，跟clear效果差不多
12. history：查看历史命令
13. help：帮助
14. exit：退出
15. #表示注释

## Git配置

```bash
# 查看所有的配置文件
git config -l
# 查看系统的config
git config --system --list
# 查看当权用户的config
git config --global --list
```



Git设置用户名以及邮箱

```bash
git config --global user.name "J-ADan" #设置用户名
git config --global user.email 18254874523@163.com #设置邮箱
```



**Git系统级别的配置文件**

G:\Git\Git\etc

**Git用户级别的配置文件**

C:\Users\J-ADan\.gitconfig



## Git的基本理论

**Git的工作区域：**

三个工作区域：工作目录（Working Directory）、暂存区（Stage/Index）、资源库（Repository或者Git Directory）。

如果加上远程的Git仓库（Remote Directory）就可以分为四个工作区域。

**文件在四个工作区域的转换关系**

![image-20210722072202722](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722072202722.png)

* WorkSpace或者Working Directory：工作区域，平时存储代码的地方
* Stage/Index：暂存区，用于临时存放改动，它仅仅是一个文件，保存即将提交的文件列表信息
* Repository或者History：本地仓库（仓库区），安全存放数据的位置，这里有提交的所有版本的数据。HEAD指向最新放仓库的版本。
* Remote：远程仓库，托管代码的服务器，可以简单地认为是一台远程的计算机用于数据交换。



> Git操作

![image-20210722074821610](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722074821610.png)

## Git项目的搭建

**本地仓库的搭建**

* 创建一个新的仓库

```bash
# 在当前目录下创建一个git仓库
git init
```

创建完成后，会出现一个.git文件夹，里面有所有的仓库信息文件

ps：.git文件夹是隐藏文件夹，需要在查看里面打开隐藏文件夹才能看到。

* 克隆一个仓库

它是将远程服务器上的仓库完整的克隆一份在自己的电脑上

一般来说，主要从两个地方克隆，一个就是很著名的GitHub网站，另一个就是中国的Gitee网站。

```bash
# 克隆远程服务器上的仓库
git clone [url]
```

![image-20210722080704995](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722080704995.png)



## Git的文件操作

> Git 文件的四种状态

Git的主要作用就是用于版本控制，要对文件进行修改提交等等操作，要对文件进行操作，就需要文件的状态，不然可能某一个命令提交了不想提交的文件，或者没提交上想要提交的文件。

* Untracked：未跟踪文件。此文件在文件夹中，但是并没有加入git仓库，不参与版本的控制。通过 **git add** 状态转变为 **Staged**
* Unmodify：文件已经入库，但是未修改。即版本库中的文件快照内容与文件夹中完全一致，这种类型的文件有两个去处，如果他被修改，就变为 **Modified** ，如果使用 **git rm** 移出版本库，则会成为 **Untracked**文件
* Modified：文件已经修改，但仅仅被修改，并没有进行其他的操作。这个文件也有两个去处，通过 **git add** 进入**Stage**状态，使用 **git checkout** 则丢弃修改过，恢复到**Unmodify** 状态，这个 **git checkout** 操作即从库中去处文件，覆盖当前的修改。
* Stage：暂存状态。使用 **git commit** 将修改同步到git库中，库中的文件与本地文件变为一致，文件变为 **Unmodify** 状态。使用 **git reset HEAD filename** 取消某个文件的暂存，文件状态为 **Modified**



> Git文件操作

```bash
# 查看所有文件状态
git status
# 查看某个文件的状态
git status filename

# 添加所有文件到暂存区
git add .
# 添加某个文件到暂存区
git add filename

# 提交暂存区到本地仓库
git commit -m "本次提交描述"
```



### 提交文件的忽略

我们并不是所有的项目文件都需要上传，所以我们可以设置忽略文件。

在主目录下设置 **.gitignore** 文件，文件内部书写规则：

1. 或略文件中的空行或以#开始的行会被忽略
2. 可以收用Linux通配符。例如：* 代表任意的多个字符，[abc]代表可选字符的范围，{abc，cde}代表可选字符串。
3. 如果名称前面有一个 ! ，则代表例外规则，不被忽略
4. 如果名称最前面有一个路径分隔符（/），表示要忽略的文件在此目录下，子目录的文件不被忽略
5. 如果名称最后面有一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录而非文件（默认的文件或者目录都忽略）

```bash
# 注释
*.txt		#忽略所有的txt结尾的文件
!lib.txt	#lib.txt 不忽略
/temp		#仅忽略项目根目录下的TODO文件，子目录中的文件不忽略
build/		#忽略build文件目录下的所有文件
doc/*.txt	#会忽略doc下面的txt文件，但不会忽略doc下面文件夹里面的txt文件
```



## 设置GitHub免密登录

**设置ssh公钥：**

```bash
# 检查是否存在ssh公钥
cd ~/.ssh
# 如果没有查询到任何文件即没有设置

# 设置ssh公钥
ssh-keygen -t rsa -C "自己的邮箱地址"
# 然后剩下的一直回车就好，其他的不用设置
```

设置完成后，在C:\Users\J-ADan\.ssh	会存在两个文件

![image-20210722134205507](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722134205507.png)

将	id_rsa.pub	用记事本打开，复制里面的内容

打开github,点击设置

![image-20210722134439429](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722134439429.png)

![image-20210722134520879](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722134520879.png)

设置好名称，直接添加就可。



## 创建GitHub远程仓库

![image-20210722185406679](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722185406679.png)

点击任意一个创建远程仓库

![image-20210722185730514](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722185730514.png)

创建完成后

![image-20210722185804966](C:\Users\J-ADan\AppData\Roaming\Typora\typora-user-images\image-20210722185804966.png)

将仓库克隆到本地仓库

```bash
# 克隆操作
git clone [url]
```



## 连接远程仓库（GitHub）

在上述克隆完毕后，直接在克隆的文件夹内书写自己的项目，这是最快的，最简便的连接方式。

**国内网站Gitee与上述步骤一模一样**



## Git的分支

> 在多人的合作的开发过程中，代码的合并问题，版本更迭问题，代码分散问题都很难受
>
> 所以我们可以利用Git 的分支功能来解决此问题。



```bash
# 列出所有的分支
git branch

# 查看远程分支
git branch -r

# 新建分支,但是仍然会停留在当前分支
git branch name

# 新建分支并切换到该分支
git checkout -b name

# 合并指定分支到当前分支
git merge name

# 删除分支
git branch -d name

# 删除远程分支
git push origin --delete name

# 切换到某一分支
git checkout name
```

