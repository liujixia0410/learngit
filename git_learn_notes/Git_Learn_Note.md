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

#### 3.2.1 git add & git commit

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

#### 3.2.2 git status & git diff

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

#### 3.2.3 git log & git reset & git reflog（版本回退）

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
你看到的一大串类似0471539bc...的是commit_id（版本号），和SVN不一样，Git的commit_id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit_id和我的肯定不一样，以你自己的为准。
为什么commit_id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。</font>

- ***git reset***
版本回退时，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交0471539bc...（注意我的提交ID和你的肯定不一样），上一个版本就是<font color="orange">HEAD\^</font>，上上一个版本就是<font color="orange">HEAD\^\^</font>，当然往上100个版本写100个\^是数不过来的，所以写成<font color="orange">HEAD~100</font>。

***回退上一版本***
为了演示更加清晰，新建一个文件gitversion.txt，然后进行两次修改提交，总共三个版本，内容分别如下（参考git log模式，时间从后往前排列）：
版本3：1st version. 2nd version. 3th version.
版本2：1st version. 2nd version.
版本1：1st version.

```bash
$ git log --pretty=oneline
a766f4ae555cd9a4a8b9e141da582f1a27ef9ab7 (HEAD -> master) modify gitversion.txt 3th
92a45b1e176eaf979f95935a8c657215e367a787 modify gitversion.txt 2nd
8b59c8d2deb541ee00baae115c512ac27c44bef7 add gitversion.txt
```

从上述log内容看，新建了一个文件，并且修改了两次，当前最新版本是a766f4a...，我们要回退到上一版本92a45b1...，可以通过如下操作执行：

```bash
$ git reset --hard HEAD^
HEAD is now at 92a45b1 modify gitversion.txt 2nd

$ cat gitversion.txt
1st version. 2nd version.

$ git log --pretty=oneline
92a45b1e176eaf979f95935a8c657215e367a787 (HEAD -> master) modify gitversion.txt 2nd
8b59c8d2deb541ee00baae115c512ac27c44bef7 add gitversion.txt
```

通过上述操作看到，果然回退到上一个版本了，并且通过 ***git log*** 看到当前最新版本的commit_id已经是92a45b1...了。

***回退任意版本***

但是，又想回到之前的最后一个版本a766f4a...怎么办？
只要窗口没关掉，或者你能通过任何方法找到版本的commit_id，就可以通过下面的方式，回到某个具体版本。
*<u>版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，就无法确定是哪一个了。</u>*

```bash
$ git reset --hard a766f4a
HEAD is now at a766f4a modify gitversion.txt 3th

$ cat gitversion.txt
1st version. 2nd version. 3th version.

$ git log --pretty=oneline
a766f4ae555cd9a4a8b9e141da582f1a27ef9ab7 (HEAD -> master) modify gitversion.txt 3th
92a45b1e176eaf979f95935a8c657215e367a787 modify gitversion.txt 2nd
8b59c8d2deb541ee00baae115c512ac27c44bef7 add gitversion.txt
```

- ***git reflog***

上述提到的“只要窗口没关掉”，目的是为了找到某个版本的commit_id，只要能找到这个commit_id，窗口关掉几次都没关系，一样可以回退。但是窗口关掉之后，如何找到commit_id呢？

```bash
$ git reflog
a766f4a (HEAD -> master) HEAD@{0}: reset: moving to a766f4a
92a45b1 HEAD@{1}: reset: moving to HEAD^
a766f4a (HEAD -> master) HEAD@{2}: commit: modify gitversion.txt 3th
92a45b1 HEAD@{3}: commit: modify gitversion.txt 2nd
8b59c8d HEAD@{4}: commit: add gitversion.txt
```

Git提供了一个命令 ***git reflog*** 用来记录你每一次执行的命令，有了这个，放心回退吧。

- ***git版本回退原理***

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，Git仅仅是把HEAD从指向到某个版本：

┌────┐
│HEAD│
└────┘
   └──> ○ modify gitversion.txt 3th
　　　│
　　　○ modify gitversion.txt 2nd
　　　│
　　　○ add gitversion.txt

改为指向 modify gitversion.txt 2nd：

┌────┐
│HEAD│
└────┘
   │　　○ append GPL
   │　　│
   └──> ○ add distributed
　　　│
　　　○ wrote a readme file

然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。

#### 3.2.4 工作区 & 暂存区

- **工作区（Working Directory）**
就是在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：

```bash
$ cd /z/Git/learngit
$ ll
total 0
drwxr-xr-x 1 lenovo 197121 0  1月 13 14:59 git_learn_notes/

$ cd git_learn_notes
$ ll
total 17
-rw-r--r-- 1 lenovo 197121 14170  1月 13 16:18 Git_Learn_Note.md
-rw-r--r-- 1 lenovo 197121    40  1月 13 14:59 gitversion.txt
drwxr-xr-x 1 lenovo 197121     0  1月 13 10:42 image/
```

- **版本库（Repository）& 暂存区（stage）**

工作区有一个隐藏目录 *.git*，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
（分支和HEAD的概念后面再说）

![image](.\image\git_repository.png)

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

我们再练习一遍，先对gitversion.txt做个修改，比如加上一行内容：

```txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
```

然后，在工作区新增一个git_test.txt文本文件（内容随便写）。

先用git status查看一下状态：

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git_test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Git非常清楚地告诉我们，gitversion.txt被修改了，而git_test.txt还从来没有被添加过，所以它的状态是Untracked。

现在，使用两次命令git add，把gitversion.txt和git_test.txt都添加后，用git status再查看一下：

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   git_test.txt
        modified:   gitversion.txt
```

现在，暂存区的状态就变成这样了：

![image](.\image\git_stage.png)

所以，***git add*** 命令实际上就是把要提交的所有修改放到 **暂存区（Stage）**，然后，执行 ***git commit*** 就可以一次性把暂存区的所有修改提交到分支。

```bash
$ git commit -m "Git learn: stage"
[master 4af1b44] Git learn: stage
 2 files changed, 1 insertion(+)
 create mode 100644 git_learn_notes/git_test.txt
```

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

现在版本库变成了这样，暂存区就没有任何内容了：

![image](.\image\git_stage_after_commit.png)

#### 3.2.5 管理修改而非文件

**问：为什么Git比其他版本控制系统设计得优秀？**
**答：因为Git跟踪并管理的是<font color="red">修改</font>，而非文件。任何增删改，都是修改**

我们做一个实验，看看Git是如何管理修改，而不是管理文件的。

第一步，对gitversion.txt添加一行(Git tracks changes.)：

```txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
```

第二步，***git add*** 将第一次修改放入暂存区

```bash
$ git add gitversion.txt
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   gitversion.txt
```

第三步，再次修改gitversion.txt，再添加一行(Git tracks changes of files 2nd.)

```txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
```

第四步，***git commit***，然后 ***git status*** 再看状态

```bash
$ git commit -m "Git test: git tracks changes"
[master 652163d] Git test: git tracks changes
 1 file changed, 2 insertions(+), 1 deletion(-)

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

至此，你会发现，**第二次修改没有被提交！第二次修改没有被提交！第二次修改没有被提交！**

原因如下：
第一次修改 -> ***git add*** -> 第二次修改 -> ***git commit***

你看，前面提到了Git管理的是修改，当使用 ***git add*** 命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，***git commit*** 只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

提交后，用 ***git diff*** 命令可以查看工作区和版本库里面最新版本的区别，可见，第二次修改确实没有被提交。

```bash
$ git diff
diff --git a/git_learn_notes/gitversion.txt b/git_learn_notes/gitversion.txt
index 42b2849..fd43f3f 100644
--- a/git_learn_notes/gitversion.txt
+++ b/git_learn_notes/gitversion.txt
@@ -1,3 +1,4 @@
 1st version. 2nd version. 3th version.
 Git has a mutable index called stage.
-Git tracks changes.
\ No newline at end of file
+Git tracks changes.
+Git tracks changes of files 2nd.
\ No newline at end of file
```

#### 3.2.6 撤销修改 git restore

撤销修改分为两类

1. 撤销 ***git add*** 之前的修改内容
2. 撤销 ***git add*** 之后，还未 ***git commit*** 的修改内容

- **git add 之前 撤销**

先对gitversion.txt进行修改，添加一行"Git undo change before add."。

```bash
$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
Git undo change before add.
```

通过 ***git status*** 查看当前状态

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

我们会发现，Git告诉我们，"git restore \<file\>..."可以丢弃工作区的修改，尝试一下：

```bash
$ git restore gitversion.txt

$ git status
On branch master
nothing to commit, working tree clean

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
```

命令 ***git restore gitversion.txt*** 意思就是，把gitversion.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是gitversion.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是gitversion.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次 ***git commit*** 或 ***git add*** 时的状态。
从上述输出看，文件内容果然复原了。

- **git add 之后 撤销**

如果修改后执行了 ***git add*** 怎么办？我们再来操作一下。
先添加一句话"Git undo change after add."，再执行 ***git add***；
执行 ***git commit*** 之前，我们发现这句话错了，***git status***看一下，发现修改只是添加到暂存区，还未提交。

```bash
$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
Git undo change after add.

$ git add gitversion.txt

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   gitversion.txt
```

我们发现，Git同样告诉我们，用命令"git restore --staged \<file\>..."可以把暂存区的修改撤销掉（unstage），重新放回工作区，我们尝试一下：

```bash
$ git restore --staged gitversion.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   gitversion.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
Git undo change after add.
```

我们可以看到，暂存区干净了，工作区还存在文件修改，查看一下文件内容，"Git undo change after add."这句不该存在的内容确实还在。

接下来呢，按照“撤销 ***git add*** 之前的修改”在操作一次就行了。

```bash
$ git restore gitversion.txt

$ git status
On branch master
nothing to commit, working tree clean

$ cat gitversion.txt
1st version. 2nd version. 3th version.
Git has a mutable index called stage.
Git tracks changes.
Git tracks changes of files 2nd.
```

到这里，全干净了，***git status***什么也没有了，查看文件内容，"Git undo change after add."这句确实不存在了，一切都回到了原点。

#### 3.2.7 删除文件 git rm

Git中，删除也被当做一种修改操作来管理。我们试着删除之前曾经提交过的"git_test.txt"文件。

```bash
$ ll
total 29
-rw-r--r-- 1 lenovo 197121 24390  1月 19 19:36 Git_Learn_Note.md
-rw-r--r-- 1 lenovo 197121     0  1月 13 16:40 git_test.txt
-rw-r--r-- 1 lenovo 197121   132  1月 19 19:32 gitversion.txt

$ rm git_test.txt

$ ll
total 29
-rw-r--r-- 1 lenovo 197121 24390  1月 19 19:36 Git_Learn_Note.md
-rw-r--r-- 1 lenovo 197121   132  1月 19 19:32 gitversion.txt
```

此时，Git知道有文件被删除了，工作区和版本库不一致了，***git status***命令会告诉哪些文件被删除了。

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    git_test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

此时可以有两个选择

1. 一是删除错了，要从版本库恢复回来，使用命令 ***git restore***
通过以下执行，可以看到，"git_test.txt"被恢复回来了，***git status*** 也是干净的。

```bash
$ git restore git_test.txt

$ ll
total 29
-rw-r--r-- 1 lenovo 197121 24390  1月 19 19:36 Git_Learn_Note.md
-rw-r--r-- 1 lenovo 197121     0  1月 22 14:00 git_test.txt
-rw-r--r-- 1 lenovo 197121   132  1月 19 19:32 gitversion.txt

$ git status
On branch master
nothing to commit, working tree clean
```

2. 二是确实要从版本库中删除该文件，使用命令 ***git rm*** 删掉，并且 ***git commit***
通过以下执行，可以看到，"git_test.txt"已经不存在了，并且 ***git status*** 也是干净的。

```bash
$ git rm git_test.txt
rm 'git_learn_notes/git_test.txt'

$ git commit -m "Git learn: git rm"
[master 7398e9d] Git learn: git rm
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 git_learn_notes/git_test.txt

$ git status
On branch master
nothing to commit, working tree clean

$ ll
total 29
-rw-r--r-- 1 lenovo 197121 24390  1月 19 19:36 Git_Learn_Note.md
-rw-r--r-- 1 lenovo 197121   132  1月 19 19:32 gitversion.txt
```

## 第四章 远程版本库

GitHub也可以创建Git仓库，并且让GitHub与本地仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作。

### 4.1 添加到远程仓库

首先，注册并登录GitHub，创建一个仓库。我针对Git学习，创建一个叫做learngit的仓库。创建后，仓库是空的。

GitHub给出了很明确的提示，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

GitHub提示信息如下：

![image](.\image\GitHub_new_repo.png)

现在，根据GitHub的提示，在本地的learngit仓库下运行命令：

```bash
$ git remote add origin http://github.com/liujixia0410/learngit.git
```

上面的liujixia0410需要替换成自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

下一步，就可以把本地库的所有内容推送到远程库上：

```bash
$ git push -u origin master
warning: redirecting to https://github.com/liujixia0410/learngit.git/
Enumerating objects: 79, done.
Counting objects: 100% (79/79), done.
Delta compression using up to 8 threads
Compressing objects: 100% (55/55), done.
Writing objects: 100% (79/79), 193.28 KiB | 7.73 MiB/s, done.
Total 79 (delta 16), reused 0 (delta 0)
remote: Resolving deltas: 100% (16/16), done.
To http://github.com/liujixia0410/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

把本地库的内容推送到远程，用 ***git push*** 命令，实际上是把当前分支master推送到远程。

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

推送成功后的Git页面，与本地一样了。

```bash
$ ll
total 33
-rw-r--r-- 1 lenovo 197121 26672  1月 22 15:07 Git_Learn_Note.md
-rw-r--r-- 1 lenovo 197121   132  1月 19 19:32 gitversion.txt
drwxr-xr-x 1 lenovo 197121     0  1月 13 16:50 image/
```

![image](.\image\GitHub_push_01.png)

从现在起，只要本地作了提交，就可以通过命令 ***git push*** 推送到GitHub上。

```bash
$ git push origin master
```

把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

SSH警告
当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。

### 4.2 从远程仓库克隆

## 附录

### Q&A

- ***不在Git仓库管理目录内执行***
  - Q：输入**git add Git_Learn_Note.md**，得到错误：fatal: not a git repository (or any of the parent directories)。
  - A：Git命令必须在Git仓库目录内执行（**git init**除外），在仓库目录外执行是没有意义的。
- ***文件不存在***
  - Q：输入**git add Git_Learn_Note.md**，得到错误fatal: pathspec 'Git_Learn_Note.md' did not match any files。
  - A：添加某个文件时，该文件必须在当前目录下存在。

### Git命令列表

|Commond|说明|
|---|---|
|git add [file_name]|添加一个文件到Git，无论是新文件还是修改文件，都需要通过add之后，才能commit|
|git commit|将git add之后的文件，全部提交，并产生新的commit_id<br>-m "[comment]"：提交时，添加日志<br>-a [file_name]：讲一个没有add的文件，同时执行add和commit|
|git status|查看Git所管理的文件状态，包括哪些没有add，哪些add没有提交，哪些是新建文件，哪些是修改文件等|
|git diff|查看当前修改与Git当前版本之间的差异|
|git log|查看Git管理下的所有日志<br>--pretty=oneline：该参数简化log显示为同一行，方便查看|
|git reset [commit_id]|版本回退|
|git reflog|查看Git管理下所有被记录的操作|
