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

#### 3.2.2 status & diff

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

#### 3.2.3 log & reset & reflog（版本回退）

版本回退需要根据提交本版的日志情况，确定回退到以前的某个版本。

- ***git log***
在实际工作中，我们肯定记不住每次都改了什么内容，所以我们用**git log**命令查看：

```bash
$ git log
commit 0471539bc0556b48a3371101fd98c17aabb0480e (HEAD -> master)
Author: Liujx <liujx@dce.com.cn>
Date:   Wed Jan 13 10:36:10 2021 +0800

    Git Learning note: modified Git_learn_note.md

commit 47fb0e319187d32e1b2796080911f44e6d41a91c
Author: Liujx <liujx@dce.com.cn>
Date:   Wed Jan 13 10:35:19 2021 +0800

    Git Learning note: add images & modified Git_learn_note.md

commit bbd52530c96650b49f27a14b6a09457bb8c528e1
Author: Liujx <liujx@dce.com.cn>
Date:   Wed Jan 13 10:11:10 2021 +0800

    My git learning note, git diff

commit 5284557de44e9f0efc6a932a3a1b81de55dd7bd6
Author: Liujx <liujx@dce.com.cn>
Date:   Mon Jan 11 21:36:09 2021 +0800

    Git learn: add commit status diff

commit d8ca75e78a1c7b06fcadd2bcc4fefdd7a9856c03
Author: Liujx <liujx@dce.com.cn>
Date:   Mon Jan 11 20:38:41 2021 +0800

    First Git Learn, it's my git learning note.
```

**git log**命令显示从最近到最远的提交日志，我们可以看到5次提交，最近的一次是 ***Git Learning note: modified Git_learn_note.md***，上一次是 ***Git Learning note: add images & modified Git_learn_note.md***，最早的一次是 ***First Git Learn, it's my git learning note.*** 。

如果嫌输出信息太多，看得眼花缭乱的，可以试试加上 **--pretty=oneline** 参数：

```bash
$ git log --pretty=oneline
0471539bc0556b48a3371101fd98c17aabb0480e (HEAD -> master) Git Learning note: modified Git_learn_note.md
47fb0e319187d32e1b2796080911f44e6d41a91c Git Learning note: add images & modified Git_learn_note.md
bbd52530c96650b49f27a14b6a09457bb8c528e1 My git learning note, git diff
5284557de44e9f0efc6a932a3a1b81de55dd7bd6 Git learn: add commit status diff
d8ca75e78a1c7b06fcadd2bcc4fefdd7a9856c03 First Git Learn, it's my git learning note.
```

<font color="green">友情提示:
你看到的一大串类似0471539bc...的是commit id（版本号），和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。
为什么commit id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。</font>

- ***git reset***
版本回退时，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交0471539bc...（注意我的提交ID和你的肯定不一样），上一个版本就是<font color="orange">HEAD\^</font>，上上一个版本就是<font color="orange">HEAD\^\^</font>，当然往上100个版本写100个\^是数不过来的，所以写成<font color="orange">HEAD~100</font>。

  - 回退上一版本
为了演示更加清晰，新建一个文件gitversion.txt，文件内容就1行"1st version."。

  - 回退某个版本


- ***git reflog***

## 附录

### Q&A

- ***不在Git仓库管理目录内执行***
  - Q：输入**git add Git_Learn_Note.md**，得到错误：fatal: not a git repository (or any of the parent directories)。
  - A：Git命令必须在Git仓库目录内执行（**git init**除外），在仓库目录外执行是没有意义的。
- ***文件不存在***
  - Q：输入**git add Git_Learn_Note.md**，得到错误fatal: pathspec 'Git_Learn_Note.md' did not match any files。
  - A：添加某个文件时，该文件必须在当前目录下存在。
