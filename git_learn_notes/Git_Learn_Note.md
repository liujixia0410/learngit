# Git学习

[toc]

## Git简介

### Git诞生

作者：Linus
原因：BitMover公司要收回Linux社区免费使用BitKeeper的权利（Linux社区有人想破解BitKeeper，被BitMover发现了）
时间：2005年，2周时间写出来的
代码：C语言

### 集中式vs分布式

|模式|代表|特点|
|---|---|---|
|集中式|CVS、SVN|1、必须中央服务器</br>2、必须联网才能使用</br>3、中央服务器挂了，大家都歇了|
|分布式|Git、BitKeeper、Bazaar|1、无中央服务器</br>2、每台电脑都是完整仓库</br>3、互相推送各自改动的内容</br>4、互为备份，避免丢失|

## Git安装

### Linux版本安装

- 查看是否已经安装

可以尝试输入git，查看是否已经安装了

```shell
$git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```

像上面的命令，有很多Linux会友好地告诉你Git没有安装，还会告诉你如何安装Git。

- Debian或Ubuntu Linux版本

如果你碰巧用Debian或Ubuntu Linux，通过一条

```shell
sudo apt-get install git
```

就可以直接完成Git的安装，非常简单。

老一点的Debian或Ubuntu Linux，要把命令改为

```shell
sudo apt-get install git-core
```

因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫"git-core"了。由于Git名气实在太大，后来就把GNU Interactive Tools改成"gnuit"，"git-core"正式改为"git"。

- 源码安装

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入以下命令就好了：

```shell
$./config
$make
$sudo make install
```

### Windows版本安装

- 安装

在Windows上使用Git，可以从Git官网直接下载安装程序，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

- 配置

安装完成后，还需要最后一步设置，在命令行输入：

```bash
$git config --global user.name "Your Name"
$git config --global user.email "email@example.com"
```

注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

## 创建版本库repository

可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

- 1、建一个新目录（我起名learngit）

```bash
$cd /z/Git
$mkdir learngit
$cd learngit
$pwd
/z/Git/learngit
```

- 2、通过"git init"命令把这个目录变成Git可以管理的仓库

```bash
$cd /z/Git/learngit
$git init
Initialized empty Git repository in Z:/Git/learngit/.git/
```

Git仓库建好了，而且是一个空的仓库（empty Git repository）.
当前目录（/z/Git/learngit）下多了一个<font color="red">.git</font>的目录（隐藏目录），是Git跟踪管理版本库的，<font color="red">千万不能动</font>。

