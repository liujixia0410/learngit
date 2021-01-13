# Git学习

[toc]

## 第一章 Git简介

### 1.1 Git诞生

作者：Linus
原因：BitMover公司要收回Linux社区免费使用BitKeeper的权利（Linux社区有人想破解BitKeeper，被BitMover发现了）
时间：2005年，2周时间写出来的
代码：C语言

### 1.2 集中式vs分布式

|模式|代表|特点|
|---|---|---|
|集中式|CVS、SVN|1、必须中央服务器</br>2、必须联网才能使用</br>3、中央服务器挂了，大家都歇了|
|分布式|Git、BitKeeper、Bazaar|1、无中央服务器</br>2、每台电脑都是完整仓库</br>3、互相推送各自改动的内容</br>4、互为备份，避免丢失|

## 第二章 Git安装

### 2.1 Linux版本安装

- 查看是否已经安装

可以尝试输入 **git**，查看是否已经安装了

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

### 2.2 Windows版本安装（git config）

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

## 第三章 版本库repository管理

### 3.1 创建版本库（git init命令）

可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

- 1、建一个新目录（我起名learngit）

```bash
$cd /z/Git
$mkdir learngit
$cd learngit
$pwd
/z/Git/learngit
```

- 2、通过 **"git init"** 命令把这个目录变成Git可以管理的仓库

```bash
$cd /z/Git/learngit
$git init
Initialized empty Git repository in Z:/Git/learngit/.git/
```

Git仓库建好了，而且是一个空的仓库（empty Git repository）.
当前目录（/z/Git/learngit）下多了一个<font color="red">.git</font>的目录（隐藏目录），是Git跟踪管理版本库的，<font color="red">千万不能动</font>。

### 3.2 版本管理

#### 3.2.1 add & commit

将学习笔记《Git_Learn_Note.md》放到版本控制目录下，即"/z/Git/learngit"下面，子目录也行
<font color="blue">我建了子目录，实际放在"/z/Git/learngit/git_learn_notes"</font>

- ***git add***
第一步，使用 ***git add*** 命令，把文件添加到Git仓库
这步执行之后，是没有任何提示的

```bash
$git add Git_Learn_Note.md
```

- ***git commit***
第二步，使用 ***git commit*** 命令，把文件提交到Git仓库

```bash
$ git commit -m "First Git Learn, it's my git learning note."
[master (root-commit) d8ca75e] First Git Learn, it's my git learning note.
 1 file changed, 108 insertions(+)
 create mode 100644 git_learn_notes/Git_Learn_Note.md
```

***<u>"git add & git commit"说明：***

- *git commit 的"-m"后面，是本次提交的说明，commont*
- *git commit命令执行成功后会告诉你*
  - *1 file changed：1个文件被改动（我们新添加的学习笔记）*
  - *108 insertions：插入了108行内容（该学习笔记当时108行）*</u>
- *<font color="green">关于目录，Git是不进行目录管理的，而是只管理仓库内的文件*
- *git add 可以操作目录（没毛用），git commit 操作目录会提示"nothing to commit"，如下</font>*

```bash
$ git commit -m "First Git Learn, it's learning notes directory."
On branch master

Initial commit

nothing to commit
```

#### 3.2.1 status & diff

可以用来查看接受Git管理的文件的修改状态，以及比较修改内容

- ***git status***
用于查看文件修改的状态，当前Git_Learn_Note.md已经被修改过，我们通过 **git status** 看看会告诉我们什么？

![image](.\image\git_status_01.png)

**git status**命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，Git_Learn_Note.md被修改过了(modified:   Git_Learn_Note.md)，但还没有准备提交的修改(no changes added to commit)。

- ***git diff***
虽然Git告诉我们Git_Learn_Note.md被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你休假两周从国外回来，第一天上班时，已经记不清上次怎么修改的Git_Learn_Note.md，所以，需要用git diff这个命令看看：

![image](.\image\git_diff_01.png)

**git diff** 顾名思义就是查看difference，显示的格式是Unix通用的diff格式，可以从上面的命令输出看到，我们在第186行删除了“疑难解答”四个字。

- ***对于修改的提交***
  - 参考 "3.2.1 add & commit" 章节
  - 1、git add
  - 2、git commit

## 附录

### Q&A

- ***不在Git仓库管理目录内执行***
  - Q：输入**git add Git_Learn_Note.md**，得到错误：fatal: not a git repository (or any of the parent directories)。
  - A：Git命令必须在Git仓库目录内执行（**git init**除外），在仓库目录外执行是没有意义的。
- ***文件不存在***
  - Q：输入**git add Git_Learn_Note.md**，得到错误fatal: pathspec 'Git_Learn_Note.md' did not match any files。
  - A：添加某个文件时，该文件必须在当前目录下存在。
