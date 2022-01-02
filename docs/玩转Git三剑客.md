# 玩转Git三剑客

[TOC]

# 前言

课程：https://time.geekbang.org/course/intro/100021601?tab=catalog

课件下载地址：https://gitee.com/geektime-geekbang/Git-Learning



# 第一章



## 01 课程综述

### VCS 出现前

用目录拷贝区别不同版本

公共文件容易被覆盖

成员沟通成本高，代码集成效率低下



### 集中式 VSC

有集中式的版本管理服务器



可是客户端必须时刻和服务器相连



### 分布式 VSC



服务端和客户端都有完整的版本库

脱离服务端，客户端照样可以管理版本



#### Git

最优的存储能力

非凡的性能

开源

容易备份

支持离线操作

很容易定制工作流



##### Git

官网地址：https://git-scm.com



##### Github



##### GitLab



## 02 安装 Git

Git 官方文档地址：

极客时间版权所有: https://time.geekbang.org/course/detail/100021601-71677



安装：https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git



### 在 Windows 上安装

在 Windows 上安装 Git 也有几种安装方法。 官方版本可以在 Git 官方网站下载。 打开 https://git-scm.com/download/win，下载会自动开始。 要注意这是一个名为 Git for Windows 的项目（也叫做 msysGit），和 Git 是分别独立的项目；更多信息请访问 http://msysgit.github.io/。

要进行自动安装，你可以使用 [Git Chocolatey 包](https://chocolatey.org/packages/git)。 注意 Chocolatey 包是由社区维护的。

另一个简单的方法是安装 GitHub Desktop。 该安装程序包含图形化和命令行版本的 Git。 它也能支持 Powershell，提供了稳定的凭证缓存和健全的换行设置。 稍后我们会对这方面有更多了解，现在只要一句话就够了，这些都是你所需要的。 你可以在 GitHub for Windows 网站下载，网址为 [GitHub Desktop 网站](https://desktop.github.com/)。





推荐安装方式： https://git-scm.com/download/win

检查安装是否成功

```powershell
> git --version
git version 2.29.2.windows.3
```

输出了版本号，说明安装成功了



### 更多帮助：git help 命令名 [--web]

```powershell
git help log
git help --web log # 打开浏览器
```

<img src="玩转Git三剑客/images/1640688693326.png" alt="1640688693326" style="zoom:80%;" />





## 03  使用Git之前需要做的最小配置

### 配置 user.name 和 user.email

```powershell
git config --global user.name 'your_name'
git config --global user.email 'your_email@domain.com'
```

示例：

```powershell
>git config --global user.name 'Artisan-K'
>git config --global user.email '836439285@qq.com'
```



### 显示配置：git config --list

```powershell
git config --list --loccal # 只对某个仓储有效
git config --list --global # 对当前用户的所有仓储有效
git config --list --system # 对系统所有登录的用户的有效
```

示例：

```powershell
>git config --list --global
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
user.name='Artisan-K'
user.email='836439285@qq.com'
```



## 04 建 Git 仓库

两种创建场景：

1. 把已有的项目代码纳入Git管理

   ```powershell
   cd 项目代码所在文件
   git init
   ```

   

2. 新建的项目直接用Git管理

   ```powershell
   cd 某个文件
   git init your_project #会在当期路径下创建和项目名称同名的文件夹
   cd your_project
   ```



### 创建

```powershell
$ git init git_learning
```

会在当期文件夹床一个名为 **git_learning** 的文件夹

进入文件夹

```pow
$ cd git_learning/
$ ls -al
total 4
drwxr-xr-x 1 wei 197121 0 Dec 28 16:39 ./
drwxr-xr-x 1 wei 197121 0 Dec 28 16:39 ../
drwxr-xr-x 1 wei 197121 0 Dec 28 16:39 .git/
```
查看当期配置

```powershell
git_learning>git config --global --list

filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
user.name='Artisan-K'
user.email='836439285@qq.com'
```



设置当期仓储的配置

```powershell
git_learning>git config --local user.name 'weikai'
git_learning>git config --local user.email '277898160@qq.com'
git_learning>git config --local --list

core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
user.name='weikai'
user.email='277898160@qq.com'

```



### 添加文件

<img src="玩转Git三剑客/images/1640681708791.png" alt="1640681708791"  />

```powershell
$ cp ../0-material/readme .
$  git commit -m 'add readme'
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        readme

nothing added to commit but untracked files present (use "git add" to track)
```

错误：是表示 readme 文件没有加入仓储

```powershell
$ git add readme
warning: LF will be replaced by CRLF in readme.
The file will have its original line endings in your working directory

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   readme

```

上述输出，表示文件还在暂存区，执行如下命令进行提交

```powershell
$ git commit -m 'add readme'
[master (root-commit) 86f5cad] add readme
 1 file changed, 2 insertions(+)
 create mode 100644 readme

```

查看日志：

```powershell
$ git log
commit 86f5cad49e27ff8c97924fdbae7506a5c12a85b6 (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:02:00 2021 +0800

    add readme

```



## 05 通过几次commit来认识工作区和暂存区

往仓库⾥添加⽂件 ，

**1.** **加⼊** **index.html** **和** **git-logo**  

**2.** **加⼊** **style.css**  

**3.** **加⼊** **script.js**  

**4.** **修改** **index.html** **和** **style.css** 



![1640682547440](玩转Git三剑客/images/1640682547440.png)



### 添加文件

拷贝一个现有的文件到当期项目文件

```powershell
$ cp ../0-material/index.html.01 index.html # 添加文件
$ cp -r ../0-material/images/ . # 添加文件夹
$ ls -al
total 9
drwxr-xr-x 1 wei 197121    0 Dec 28 17:13 ./
drwxr-xr-x 1 wei 197121    0 Dec 28 16:54 ../
drwxr-xr-x 1 wei 197121    0 Dec 28 17:02 .git/
-rw-r--r-- 1 wei 197121 1303 Dec 28 17:13 index.html
-rw-r--r-- 1 wei 197121   51 Dec 28 16:56 readme

$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        images/
        index.html

nothing added to commit but untracked files present (use "git add" to track) ## 说明还没被跟踪管理

```

### 加入暂存区 git add

```powershell
$ git add index.html images
warning: LF will be replaced by CRLF in index.html.
The file will have its original line endings in your working directory

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   images/git-logo.png
        new file:   index.html

```



### 提交 git commit

```powershell
$ git commit -m 'add index + logo'
[master 9ccc1e2] add index + logo
 2 files changed, 49 insertions(+)
 create mode 100644 images/git-logo.png
 create mode 100644 index.html

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git log
commit 9ccc1e2ee4c4663e6e616bdf4290a41e2bc59d0f (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:24:02 2021 +0800

    add index + logo

commit 86f5cad49e27ff8c97924fdbae7506a5c12a85b6
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:02:00 2021 +0800

    add readme

```



### 添加 css 文件

![1640683272365](玩转Git三剑客/images/1640683272365.png)

页面不太好看，我们添加样式文件

```powershell
$ mkdir styles
$ cp ../0-material/styles/style.css.01  styles/style.css
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        styles/

nothing added to commit but untracked files present (use "git add" to track)

```

页面修改效果：

<img src="玩转Git三剑客/images/1640683750207.png" alt="1640683750207" style="zoom:67%;" />



是我们想要的结果，把它加入暂存区

```powershell
$ git add styles
warning: LF will be replaced by CRLF in styles/style.css.
The file will have its original line endings in your working directory

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   styles/style.css

```

提交

```powershell
$ git commit -m 'Add style.css'
[master 43d68f3] Add style.css
 1 file changed, 50 insertions(+)
 create mode 100644 styles/style.css

$ git log
commit 43d68f36467e961a71a176c0faba03c006e4e7f5 (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:32:05 2021 +0800

    Add style.css

commit 9ccc1e2ee4c4663e6e616bdf4290a41e2bc59d0f
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:24:02 2021 +0800

    add index + logo

commit 86f5cad49e27ff8c97924fdbae7506a5c12a85b6
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:02:00 2021 +0800

    add readme

```



### 添加 js 文件

```powershell
$ cp -r ../0-material/js .

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ ls
images/  index.html  js/  readme  styles/

```

<img src="玩转Git三剑客/images/1640684234989.png" alt="1640684234989" style="zoom:80%;" />

加入暂存区和提交

```powershell
# 加入暂存区
$ git add js
warning: LF will be replaced by CRLF in js/script.js.
The file will have its original line endings in your working directory

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   js/script.js

# 提交代码
$ git commit -m 'Add js'
[master 8cd64a3] Add js
 1 file changed, 15 insertions(+)
 create mode 100644 js/script.js

$ git log
commit 8cd64a399acc93b11a70caf12da26374b6bc5fe7 (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:38:58 2021 +0800

    Add js
commit 43d68f36467e961a71a176c0faba03c006e4e7f5
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:32:05 2021 +0800

    Add style.css

commit 9ccc1e2ee4c4663e6e616bdf4290a41e2bc59d0f
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:24:02 2021 +0800

    add index + logo

commit 86f5cad49e27ff8c97924fdbae7506a5c12a85b6
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:02:00 2021 +0800

    add readme

```



### 修改

修改 idnex.html 和  style.css 文件

 idnex.html 追加如下代码

```html
    <footer>
        <p>
            <a href="https://github.com/TTN-js/unforGITtable">参考项目01</a> 
        </p>
    </footer>
```

style.css 文件，追加如下代码

```Css
footer{
  right: 0;
  bottom: 0;
  position: relative;
  padding: 10px 1rem 10px 0;
  margin-top: 50px;
  font-size: 0.7em;
  text-align: right;
}

footer p{
  margin-bottom:0;
}

```

![1640684958227](玩转Git三剑客/images/1640684958227.png)

查看状态：
```powershell
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html
        modified:   styles/style.css

no changes added to commit (use "git add" and/or "git commit -a")

```



### 一起加入暂存区 git add -u

新命令参数 **git add -u 表示已经被管理的文件，一起提交到暂存区**

而不用一个一个指定文件

```powershell
$ git add -u # 一起提交到暂存区
warning: LF will be replaced by CRLF in index.html.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in styles/style.css.
The file will have its original line endings in your working directory

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html
        modified:   styles/style.css

```

### 提交

```powershell
$ git commit -m 'modified index: refering projects'
[master 8ecc643] modified index: refering projects
 2 files changed, 19 insertions(+), 1 deletion(-)

$ git log
commit 8ecc6430cb6aaf9a43333e7703a2893ae8f891cc (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:55:13 2021 +0800

    modified index: refering projects

commit 8cd64a399acc93b11a70caf12da26374b6bc5fe7
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:38:58 2021 +0800

    Add js

commit 43d68f36467e961a71a176c0faba03c006e4e7f5
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:32:05 2021 +0800

    Add style.css

commit 9ccc1e2ee4c4663e6e616bdf4290a41e2bc59d0f
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:24:02 2021 +0800

    add index + logo

commit 86f5cad49e27ff8c97924fdbae7506a5c12a85b6
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:02:00 2021 +0800

    add readme

```



## 06 给文件重命名的简便方法 git mv

#### 常规操作

```powershell
$ mv readme readme.md # 重命名文件

$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    readme

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        readme.md

no changes added to commit (use "git add" and/or "git commit -a")

$ git add readme.md # 加入暂存区
$ git rm readme     # 移除旧的文件
rm 'readme'

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    readme -> readme.md # git推断出你要重命名

```



#### 回退(到某个commit) : git reset --hard

```powershell
# 先回退刚才的操作
$ git reset --hard
HEAD is now at 8ecc643 modified index: refering projects
$ git status
On branch master
nothing to commit, working tree clean

```



#### 重命名简便方式：git mv xxx yyy

```powershell
$ git mv readme readme.md
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    readme -> readme.md

$ git commit -m 'Move readme to readme.md'
[master 2dd3481] Move readme to readme.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename readme => readme.md (100%)

$ git status
On branch master
nothing to commit, working tree clean

$ git log
commit 2dd34814dd5dcda70b85cae031856ff1f05a423d (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 18:10:22 2021 +0800

    Move readme to readme.md

commit 8ecc6430cb6aaf9a43333e7703a2893ae8f891cc
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:55:13 2021 +0800

    modified index: refering projects

commit 8cd64a399acc93b11a70caf12da26374b6bc5fe7
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:38:58 2021 +0800

    Add js

commit 43d68f36467e961a71a176c0faba03c006e4e7f5
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:32:05 2021 +0800

    Add style.css

commit 9ccc1e2ee4c4663e6e616bdf4290a41e2bc59d0f
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:24:02 2021 +0800

    add index + logo

commit 86f5cad49e27ff8c97924fdbae7506a5c12a85b6
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:02:00 2021 +0800

    add readme


```



## 07 通过 git log 查看版本演变历史

### git log --oneline

```powershell
$ git log --oneline
2dd3481 (HEAD -> master) Move readme to readme.md
8ecc643 modified index: refering projects
8cd64a3 Add js
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme

```



### git log -n？

查看最近的几次

```powershell
$ git log -n2
commit 2dd34814dd5dcda70b85cae031856ff1f05a423d (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 18:10:22 2021 +0800

    Move readme to readme.md

commit 8ecc6430cb6aaf9a43333e7703a2893ae8f891cc
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:55:13 2021 +0800

    modified index: refering projects

```

也可以和其它参数组合使用

```powershell
$ git log -n2 --oneline
2dd3481 (HEAD -> master) Move readme to readme.md
8ecc643 modified index: refering projects
```



### 分支相关命令: git log

```powershell

git_learning (master)
$ git log -n2 --oneline
2dd3481 (HEAD -> master) Move readme to readme.md
8ecc643 modified index: refering projects

git_learning (master)
$ git branch -v #查看分支
* master 2dd3481 Move readme to readme.md

git_learning (master)
# 以版本号【8ecc643】创建一个名为【temp】的分支
$ git checkout -b temp 8ecc643
Switched to a new branch 'temp'

git_learning (temp) ## 注意：已经切换到了temp分支
$ vi readme
# 修改下 readme

git_learning (temp) ## -am 用于提交跟踪过的文件
$ git commit -am 'Add temp branch test'
[temp 3a92237] Add temp branch test
 1 file changed, 2 insertions(+)

git_learning (temp)
$ git branch -av  # 查看有多少个分支
  master 2dd3481 Move readme to readme.md
* temp   3a92237 Add temp branch test

```

### 查看当前分支log: git log

```powershell
## 存在多分支，只查看当期分支的log
git_learning (temp)  
$  git log --oneline
3a92237 (HEAD -> temp) Add temp branch test
8ecc643 modified index: refering projects
8cd64a3 Add js
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme
```



### 查看所有分支的log 

#### git log --all

```powershell
## 存在多分支，只查看当期分支的log
git_learning (temp)  
$  git log --all  --oneline
3a92237 (HEAD -> temp) Add temp branch test
2dd3481 (master) Move readme to readme.md
8ecc643 modified index: refering projects
8cd64a3 Add js
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme

```



#### git log --all --graph ：图形化查看

![1640688119468](玩转Git三剑客/images/1640688119468.png)

```powershell
$  git log --all  --graph
* commit 3a92237b5e09f9a6f28e445356e42315f4273bc7 (HEAD -> temp)
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 18:25:43 2021 +0800
|
|     Add temp branch test
|
| * commit 2dd34814dd5dcda70b85cae031856ff1f05a423d (master)
|/  Author: weikai <277898160@qq.com>
|   Date:   Tue Dec 28 18:10:22 2021 +0800
|
|       Move readme to readme.md
|
* commit 8ecc6430cb6aaf9a43333e7703a2893ae8f891cc
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 17:55:13 2021 +0800
|
|     modified index: refering projects
|
* commit 8cd64a399acc93b11a70caf12da26374b6bc5fe7
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 17:38:58 2021 +0800
|
|     Add js
|
* commit 43d68f36467e961a71a176c0faba03c006e4e7f5
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 17:32:05 2021 +0800
|
|     Add style.css
|
* commit 9ccc1e2ee4c4663e6e616bdf4290a41e2bc59d0f
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 17:24:02 2021 +0800
|
|     add index + logo
|
* commit 86f5cad49e27ff8c97924fdbae7506a5c12a85b6
  Author: weikai <277898160@qq.com>
  Date:   Tue Dec 28 17:02:00 2021 +0800

      add readme

```



### 综合使用
最近所有分支中查看最近5个版本,显示一行信息，图片化显示

![1640688423048](玩转Git三剑客/images/1640688423048.png)

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (temp)
$ git log --all -n5 --oneline --graph
* 3a92237 (HEAD -> temp) Add temp branch test
| * 2dd3481 (master) Move readme to readme.md
|/
* 8ecc643 modified index: refering projects
* 8cd64a3 Add js
* 43d68f3 Add style.css

```



### 创建分支：git branch或 git checkout -b

```powershell
$ git branch 新分支名
或者
$ git checkout -b 新分支名
   -b <branch> create and checkout a new branch
示例：
$ git checkout -b fix_readme fix_css #基于分支fix_css创建新分支 fix_readme
```



### 查看分支: git brach

```powershell
## 显示本地的所有分支
$ git branch -v
  master
* temp

## 查看所有分支，如果有远程分支，也会显示远程分支
$ git branch -av 
  master
* temp
```





### 切换分支: git checkout

将当前分支的temp 切换会master 分支

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (temp)
$ git branch -a
  master
* temp

## 查看当前使用分支(结果列表中前面标*号的表示当前使用分支)
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (temp)
$ git branch
  master
* temp

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (temp)
$ git checkout master
Switched to branch 'master'




```



## 08 gitk: 通过图形界面工具来查看

### 打开 gitk

```powershell
git_learning (master)
$ gitk

```

![1640689314908](玩转Git三剑客/images/1640689314908.png)



### 选择显示版本: gitk --all

菜单【view | new view】

![1640689877987](玩转Git三剑客/images/1640689877987.png)

勾选【All refs】,查看所有分支<img src="玩转Git三剑客/images/1640689927401.png" alt="1640689927401" style="zoom:80%;" />

或者执行

```powershell
gitk --all
```



### Tag[里程碑？]

可以为某个版本添加 Tag，方便筛选

创建方法：点击某个版本，右键菜单【Create Tag】

<img src="玩转Git三剑客/images/1640690182954.png" alt="1640690182954" />

![1640690257777](玩转Git三剑客/images/1640690257777.png)



## 09 探秘 .git 目录

### 包含的文件

```powershell
$ cd .git

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git (GIT_DIR!)
$ ls -al
total 23
drwxr-xr-x 1 wei 197121   0 Dec 28 19:01 ./
drwxr-xr-x 1 wei 197121   0 Dec 28 18:56 ../
-rw-r--r-- 1 wei 197121  21 Dec 28 18:25 COMMIT_EDITMSG
-rw-r--r-- 1 wei 197121  23 Dec 28 18:56 HEAD
-rw-r--r-- 1 wei 197121  41 Dec 28 18:05 ORIG_HEAD
-rw-r--r-- 1 wei 197121 182 Dec 28 16:51 config
-rw-r--r-- 1 wei 197121  73 Dec 28 16:39 description
-rw-r--r-- 1 wei 197121 505 Dec 28 19:01 gitk.cache
drwxr-xr-x 1 wei 197121   0 Dec 28 16:39 hooks/
-rw-r--r-- 1 wei 197121 554 Dec 28 18:56 index
drwxr-xr-x 1 wei 197121   0 Dec 28 16:39 info/
drwxr-xr-x 1 wei 197121   0 Dec 28 17:02 logs/
drwxr-xr-x 1 wei 197121   0 Dec 28 19:17 objects/
drwxr-xr-x 1 wei 197121   0 Dec 28 16:39 refs/
```





### 当前分支 ref: refs/heads

```powershell

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git (GIT_DIR!)
$ cat HEAD
ref: refs/heads/master # 表示当前分支

## 切换到 temp 分支

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git (GIT_DIR!)
$ git checkout temp
fatal: this operation must be run in a work tree
# 错误：要求切换到工作目录

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git (GIT_DIR!)
$ cd ..

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git checkout temp
Switched to branch 'temp'

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (temp)
$ cat .git/HEAD
ref: refs/heads/temp # 表示当前分支为temp
```



### config

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (temp)
$ cat .git/config
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[user]
        name = 'weikai'
        email = '277898160@qq.com'

```

修改config文件



<img src="玩转Git三剑客/images/1640691076208.png" alt="1640691076208" style="zoom: 67%;" />

<img src="玩转Git三剑客/images/1640691132667.png" alt="1640691132667" style="zoom:80%;" />

```powershell
$ vi .git/config
i->修改use.name\mail -> :wq!

$ git config --local --list
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
user.name='Artisan-K'
user.email='836439285@qq.com'
```



### refs

```
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (temp)
$ cd .git

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git (GIT_DIR!)
$ cd refs

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git/refs (GIT_DIR!)
$ ls
heads/  tags/
```

tags： 有些书翻译为：里程碑

```powershell
$ cd tags/
$ ls
JS

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git/refs/tags (GIT_DIR!)
$ ls -al
total 1
drwxr-xr-x 1 wei 197121  0 Dec 28 19:17 ./
drwxr-xr-x 1 wei 197121  0 Dec 28 16:39 ../
-rw-r--r-- 1 wei 197121 41 Dec 28 19:17 JS

```



heads：就是所谓的分支，开辟出新的空间，互不影响

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git/refs/tags (GIT_DIR!)
$ cd ../heads

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git/refs/heads (GIT_DIR!)
$ ls -all
total 2
drwxr-xr-x 1 wei 197121  0 Dec 28 18:25 ./
drwxr-xr-x 1 wei 197121  0 Dec 28 16:39 ../
-rw-r--r-- 1 wei 197121 41 Dec 28 18:10 master
-rw-r--r-- 1 wei 197121 41 Dec 28 18:25 temp


wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git/refs/heads (GIT_DIR!)
$ cat master
2dd34814dd5dcda70b85cae031856ff1f05a423d

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git/refs/heads (GIT_DIR!)
$ git cat-file -t 2dd34814dd5dcda # 查看文件类型
commit

$ git branch -av
  #分支master 当前指向 【2dd3481】这个 commit
  master 2dd3481 Move readme to readme.md 
* temp   3a92237 Add temp branch test


```



### objects

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git (GIT_DIR!)
$ cd objects/

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git/objects (GIT_DIR!)
$ ls -al
total 8
drwxr-xr-x 1 wei 197121 0 Dec 28 19:17 ./
drwxr-xr-x 1 wei 197121 0 Dec 28 19:32 ../
drwxr-xr-x 1 wei 197121 0 Dec 28 17:24 01/
drwxr-xr-x 1 wei 197121 0 Dec 28 18:10 2d/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:02 31/
drwxr-xr-x 1 wei 197121 0 Dec 28 18:25 3a/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:32 43/
drwxr-xr-x 1 wei 197121 0 Dec 28 16:57 4b/
drwxr-xr-x 1 wei 197121 0 Dec 28 19:17 5a/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:19 6a/
drwxr-xr-x 1 wei 197121 0 Dec 28 16:59 7c/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:02 86/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:38 87/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:38 8c/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:55 8e/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:55 91/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:24 96/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:24 9c/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:53 a3/
drwxr-xr-x 1 wei 197121 0 Dec 28 18:25 ab/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:32 ae/
drwxr-xr-x 1 wei 197121 0 Dec 28 18:10 af/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:38 b7/
drwxr-xr-x 1 wei 197121 0 Dec 28 18:25 ce/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:19 da/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:30 ef/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:53 fe/
drwxr-xr-x 1 wei 197121 0 Dec 28 17:55 ff/
drwxr-xr-x 1 wei 197121 0 Dec 28 16:39 info/
drwxr-xr-x 1 wei 197121 0 Dec 28 16:39 pack/


# 随便进入一个文件夹
$ cd ff

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning/.git/objects/ff (GIT_DIR!)
$ ls -al
total 5
drwxr-xr-x 1 wei 197121  0 Dec 28 17:55 ./
drwxr-xr-x 1 wei 197121  0 Dec 28 19:17 ../
-r--r--r-- 1 wei 197121 54 Dec 28 17:55 f96d5ab474cef7c4e4cd5ffc1ec57cc4178032

# 看类型 -t  【tree:ff+ 文件名:f96d5ab474cef7c4e4cd5ffc1ec57cc4178032】
$ git cat-file -t fff96d5ab474cef7c4e4cd5ffc1ec57cc4178032
tree # 是tree类型

# 看内容 -p
$ git cat-file -p fff96d5ab474cef7c4e4cd5ffc1ec57cc4178032
100644 blob a38cb8a5d39ffd87603333865ef9eddf7c308656    style.css

## blob:文件类型
$ git cat-file -t  a38cb8a5d
blob

# 查看blog文件：a38cb8a5d 的内容
$ git cat-file -p a38cb8a5d
body{
  background-color: orange;
  font-family: 'Monaco', sans-serif;
  color: white;
}

body a{
  color: white;
}

header{
  text-align: center;
  margin-top: 50px;
}

h3{
  color: red;
}

header-img{
  width: 400px;
}

header-words{
  line-height: 10px;
  font-size: 50px;
  font-family: 'Monaco', sans-serif;
  margin-bottom: 75px;
}

section{
  padding: 0 50px 0px 50px;
  text-align: left;
}

div.accordion {
  cursor: pointer;
  border: none;
  outline: none;
}

div.accordion.active, div.accordion:hover {
  background-color: white;
  color: #1D2031;
}

div.panel {
  padding: 0 18px 0 0;
  display: none;
}

footer{
  right: 0;
  bottom: 0;
  position: relative;
  padding: 10px 1rem 10px 0;
  margin-top: 50px;
  font-size: 0.7em;
  text-align: right;
}

footer p{
  margin-bottom:0;
}



```



## 10 commit、tree、blob 三个对象之间的关系

![1640694783255](玩转Git三剑客/images/1640694783255.png)

git commit 创建一个 commit对象，一个 commit对象有一个tree（文件夹）



查看结构

```powershell
$ git branch -av
* master 2dd3481 Move readme to readme.md
  temp   3a92237 Add temp branch test

$ git log --oneline
2dd3481 (HEAD -> master) Move readme to readme.md
8ecc643 modified index: refering projects
8cd64a3 (tag: JS) Add js
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme

$ git cat-file -p 8cd64a3
tree b7f16a0faff7eec017ceae4fbd036854601a3a69
parent 43d68f36467e961a71a176c0faba03c006e4e7f5
author weikai <277898160@qq.com> 1640684338 +0800
committer weikai <277898160@qq.com> 1640684338 +0800

Add js


$ git cat-file -p b7f16a0faf
040000 tree 96b67e399c8496ec36cbbbcb776eb924fad7f9a7    images
100644 blob 6ad4c68d567a1a5b415dcfce2010fce1a60b245f    index.html
040000 tree 87b3e92f70e7dfa555f141afeae28a2bc4a343b6    js
100644 blob 7c2bad210b150a75f2734035454e60cde30b5c33    readme
040000 tree aee37060401d19e7bd9f80b7b33920a000e96b5b    styles

$ git cat-file -p 6ad4c68d567
<!DOCTYPE html>
<html>
<head>
    <title>Git Demo</title>
    <link rel="stylesheet" type="text/css" href="styles/style.css">
</head>
<body>
    <header>
        <img id="header-img" src="images/git-logo.png">
        <h1 id='header-words'>We are learning Git.</h1>
    </header>

    <section>
        <div class="accordion"><h1>Terminologys</h1></div>
            <div class="panel">
                <ol>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                </ol>
            </div>
        <div class="accordion"><h1>Basic Commands</h1></div>
            <div class="panel">
                <ol>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                    <li></li>
                </ol>
            </div>
        </div>
    </section>

    <script src="js/script.js"></script>
</body>
</html>

$ git cat-file -p b7f16a0faf
040000 tree 96b67e399c8496ec36cbbbcb776eb924fad7f9a7    images
100644 blob 6ad4c68d567a1a5b415dcfce2010fce1a60b245f    index.html
040000 tree 87b3e92f70e7dfa555f141afeae28a2bc4a343b6    js
100644 blob 7c2bad210b150a75f2734035454e60cde30b5c33    readme
040000 tree aee37060401d19e7bd9f80b7b33920a000e96b5b    styles

$ git cat-file -p 96b67e399c
100644 blob daf480669aa9256fa18b5c28e467af816f16482d    git-logo.png

```



## 11 小练习：数一数tree的个数

<img src="玩转Git三剑客/images/1640695173214.png" alt="1640695173214" style="zoom:80%;" />



## 12 分离头指针情况下的注意事项

git checkout 分支名，不小心输入了一个commit

```powershell
$ git log --oneline
2dd3481 (HEAD -> master, log) Move readme to readme.md
8ecc643 modified index: refering projects
8cd64a3 (tag: JS) Add js
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git checkout 43d68f3  #不小checkout 一个commit
Note: switching to '43d68f3'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 43d68f3 Add style.css

```

You are in 'detached HEAD' state. 处在分离头指针状态，在这个状态下，你可以开发，继续产生commit，而且不影响其它分支。

本质上是，现在正处在没有分支的状态下，没有对应任何分支，这时产生的commit，

当你切换到某个分支进行修改，**之前处在分离状态下的commit就会被清除**，这是一个很危险的结果。

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning ((43d68f3...))
$ ls -al
total 13
drwxr-xr-x 1 wei 197121    0 Dec 28 21:04 ./
drwxr-xr-x 1 wei 197121    0 Dec 28 16:54 ../
drwxr-xr-x 1 wei 197121    0 Dec 28 21:04 .git/
drwxr-xr-x 1 wei 197121    0 Dec 28 17:16 images/
-rw-r--r-- 1 wei 197121 1352 Dec 28 21:04 index.html
-rw-r--r-- 1 wei 197121   53 Dec 28 21:04 readme
drwxr-xr-x 1 wei 197121    0 Dec 28 21:04 styles/

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning ((43d68f3...))
$ vi styles/style.css
背景色改成绿色： orange -> green
Esc->:wq!


```

<img src="玩转Git三剑客/images/1640697412966.png" alt="1640697412966" style="zoom: 33%;" />

```powershell
$ git status
HEAD detached at 43d68f3   ##Head 没有指向任何分支，指向的是一个commit
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   styles/style.css

no changes added to commit (use "git add" and/or "git commit -a")

$ git commit -am 'Backgroud to green' ##不加入暂存区，直接commit
[detached HEAD 58af574] Backgroud to green
 1 file changed, 1 insertion(+), 1 deletion(-)

$ git log --oneline
58af574 (HEAD) Backgroud to green ## (HEAD)指向的是commit，而不是分支
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme

$ git branch -av
* (HEAD detached from 43d68f3) 58af574 Backgroud to green
  log                          2dd3481 Move readme to readme.md
  master                       2dd3481 Move readme to readme.md
  temp                         3a92237 Add temp branch test

## master分支有个bug，紧急切换到master分支进行修复
$ git checkout master
Warning: you are leaving 1 commit behind, not connected to
any of your branches:  ## 警告有个commit没有和任何分支关联

  58af574 Backgroud to green

If you want to keep it by creating a new branch, this may be a good time
to do so with:  ## 问下要不要给这个commit创建个分支

 git branch <new-branch-name> 58af574

Switched to branch 'master'

$ gitk --all

```

<img src="玩转Git三剑客/images/1640698212716.png" alt="1640698212716" style="zoom:80%;" />

这个commit不在分支中

这时突然意识到，这个commit很重要，需要保留

```powershell
$ git branch fix_css 58af574
$ gitk --all
```

<img src="玩转Git三剑客/images/1640698371315.png" alt="1640698371315" style="zoom:80%;" />



## 13 进一步理解HEAD 和 branch

### HEAD 本质上指向一个commit

```powershell
$ git checkout -b fix_readme fix_css #基于分支fix_css创建新分支 fix_readme
Switched to a new branch 'fix_readme'

$ git log --oneline
58af574 (HEAD -> fix_readme, fix_css) Backgroud to green
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme

$ gitk --all

$ cat .git/HEAD
ref: refs/heads/fix_readme

```

<img src="玩转Git三剑客/images/1640699186686.png" alt="1640699186686" style="zoom:80%;" />

**HEAD 可以指向分支，也可以指向某个 commit**, 

**当HEAD指定分支，本质也是指向某个commit**，见如下分析：

```powershell
$ cat .git/HEAD
ref: refs/heads/fix_readme #指向分支

$ cat .git/refs/heads/fix_readme # 指向分支的内容
58af57466c39dd9932753133aa74a887d645781c

$ git cat-file -t 58af57466 ## 指向分支的内容的类型
commit #本质还是commit

```



### 比较两个commit : git diff x1 x2

```powershell
$ git log --oneline
58af574 (HEAD -> fix_readme, fix_css) Backgroud to green
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme

$ git diff 58af574  43d68f3
diff --git a/styles/style.css b/styles/style.css
index 4c6bc45..ef3f137 100644
--- a/styles/style.css
+++ b/styles/style.css
@@ -1,5 +1,5 @@
 body{
-  background-color: green;
+  background-color: orange;
   font-family: 'Monaco', sans-serif;
   color: white;
 }

```

<img src="玩转Git三剑客/images/1640699887462.png" alt="1640699887462" style="zoom:80%;" />



### HEAD^ 或 HEAD~n

HEAD的父亲: HEAD^或HEAD~1

HEAD的爷爷： HEAD^^或HEAD~2

```powershell
$ git diff HEAD HEAD^
diff --git a/styles/style.css b/styles/style.css
index 4c6bc45..ef3f137 100644
--- a/styles/style.css
+++ b/styles/style.css
@@ -1,5 +1,5 @@
 body{
-  background-color: green;
+  background-color: orange;
   font-family: 'Monaco', sans-serif;
   color: white;
 }

$ git diff HEAD HEAD~2
diff --git a/styles/style.css b/styles/style.css
deleted file mode 100644
index 4c6bc45..0000000
--- a/styles/style.css
+++ /dev/null
@@ -1,50 +0,0 @@
-body{
-  background-color: green;
-  font-family: 'Monaco', sans-serif;
-  color: white;
-}
-
-body a{
-  color: white;
-}
-
-header{
-  text-align: center;
-  margin-top: 50px;
-}
-
-h3{
-  color: red;
-}
-
-header-img{
-  width: 400px;
-}

```



# 第二章

## 14 怎么删除不需要的分支：git branch -d/-D

```powershell
git branch -d/-D 分支名
```

```powershell
gitk --all
```

<img src="玩转Git三剑客/images/1640700755973.png" alt="1640700755973" style="zoom: 80%;" />

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (fix_readme)
$ git checkout master #切换到master分支
Switched to branch 'master'

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git branch -d fix_readme ## -d 删除分支，失败
error: The branch 'fix_readme' is not fully merged.
If you are sure you want to delete it, run 'git branch -D fix_readme'.

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git branch -D fix_readme  ## -D 强制删除分支
Deleted branch fix_readme (was 58af574).

```

<img src="玩转Git三剑客/images/1640700984439.png" alt="1640700984439" style="zoom:80%;" />

```powershell
$ git branch -D fix_css
Deleted branch fix_css (was 58af574).
```

<img src="玩转Git三剑客/images/1640701117776.png" alt="1640701117776" style="zoom:80%;" />

## 15 怎么修改最新的commit的message: --amend

修改最新一次commit的message

```powershell
$ git log -1
commit 2dd34814dd5dcda70b85cae031856ff1f05a423d (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 18:10:22 2021 +0800

    Move readme to readme.md

$ git commit --amend
[master 27d2787] Move file readme to readme.md
 Author: weikai <277898160@qq.com>
 Date: Tue Dec 28 18:10:22 2021 +0800
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename readme => readme.md (100%)

```

![1640701317927](玩转Git三剑客/images/1640701317927.png)

输入i, 修改message，按ESC，：wq

```powershell
$ git log -1
commit 27d27879f92b01d922bbf49801fe77c6a7b17ee6 (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 18:10:22 2021 +0800

    Move file readme to readme.md

```



## 16 怎么修改老旧Commit的message：git rebase

```shell
git rebase -i 被修改commit的父亲
```

- -i ：交互式

特别注意，此操作最好是在自己本地的分支，还没有集成到团队的分支上，否则影响到团队的其它开发人员 

```powershell
$ git log -3
commit 27d27879f92b01d922bbf49801fe77c6a7b17ee6 (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 18:10:22 2021 +0800

    Move file readme to readme.md

commit 8ecc6430cb6aaf9a43333e7703a2893ae8f891cc
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:55:13 2021 +0800

    modified index: refering projects

commit 8cd64a399acc93b11a70caf12da26374b6bc5fe7 (tag: JS)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:38:58 2021 +0800


```

<img src="玩转Git三剑客/images/1640701964210.png" alt="1640701964210" style="zoom:80%;" />

<img src="玩转Git三剑客/images/1640702027338.png" alt="1640702027338" style="zoom:80%;" />

输入i,进入修改模式，编辑：

![1640702389524](玩转Git三剑客/images/1640702389524.png)

按Esc键，:wq! 保存退出,又弹出一个交互界面

![1640702561334](玩转Git三剑客/images/1640702561334.png)

显然，上一步的修改的message没有生效，得在这个界面修改，输入i,进入修改模式，编辑

<img src="玩转Git三剑客/images/1640702667445.png" alt="1640702667445"  />

```powershell
$ git rebase -i 8cd64a399

## 使用了分离头指针
[detached HEAD c5503dc] modified index.html: add a link for refering project
 Author: weikai <277898160@qq.com>
 Date: Tue Dec 28 17:55:13 2021 +0800
 2 files changed, 19 insertions(+), 1 deletion(-)
Successfully rebased and updated refs/heads/master.

$ git log -3
commit 7c35f196779f4ab67720d42358f369c4070fafda (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 18:10:22 2021 +0800

    Move file readme to readme.md

## 产生了新的commit
commit c5503dc82aca17eeea116a920b8bdb89b08faa4f
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:55:13 2021 +0800

    modified index.html: add a link for refering project

commit 8cd64a399acc93b11a70caf12da26374b6bc5fe7 (tag: JS)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:38:58 2021 +0800

    Add js

```

注意到没有，旧的commit已被抛弃

```powershell
commit 8ecc6430cb6aaf9a43333e7703a2893ae8f891cc
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:55:13 2021 +0800

    modified index: refering projects
```

产生了新的commit

```powershell
## 产生了新的commit
commit c5503dc82aca17eeea116a920b8bdb89b08faa4f
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:55:13 2021 +0800

    modified index.html: add a link for refering project
```



## 17 怎么把连续的多个commit整理成1个:git rebase

```powershell
$ git branch -av
* master 7c35f19 Move file readme to readme.md
  temp   3a92237 Add temp branch test

$ git log
commit 7c35f196779f4ab67720d42358f369c4070fafda (HEAD -> master)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 18:10:22 2021 +0800

    Move file readme to readme.md

commit c5503dc82aca17eeea116a920b8bdb89b08faa4f
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:55:13 2021 +0800

    modified index.html: add a link for refering project

commit 8cd64a399acc93b11a70caf12da26374b6bc5fe7 (tag: JS)
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:38:58 2021 +0800

    Add js

commit 43d68f36467e961a71a176c0faba03c006e4e7f5
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:32:05 2021 +0800

    Add style.css

commit 9ccc1e2ee4c4663e6e616bdf4290a41e2bc59d0f
Author: weikai <277898160@qq.com>
Date:   Tue Dec 28 17:24:02 2021 +0800

    add index + logo

$ git rebase -i  9ccc1e2ee

```

<img src="玩转Git三剑客/images/1640703740481.png" alt="1640703740481" style="zoom:80%;" />

截图有误，应该是合并三个

<img src="玩转Git三剑客/images/1640703740481.png" alt="1640703740481" style="zoom:80%;" />![1640704028169](玩转Git三剑客/images/1640704028169.png)

![1640704042225](玩转Git三剑客/images/1640704042225.png)

Esc, :wq!

然后，新增一些说明：

```powershell
Create a complete web page
```



![1640704213643](玩转Git三剑客/images/1640704213643.png)

Esc, :wq!

```powershell
$ git rebase -i  9ccc1e2ee
[detached HEAD 12fd153] Create a complete web page
 Author: weikai <277898160@qq.com>
 Date: Tue Dec 28 17:32:05 2021 +0800
 3 files changed, 84 insertions(+), 1 deletion(-)
 create mode 100644 js/script.js
 create mode 100644 styles/style.css
Successfully rebased and updated refs/heads/master.

```

查看下日志

```powershell
$ git log --graph
* commit 2b0bf6a618f08cc188ad64082c66520bfd27896f (HEAD -> master)
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 18:10:22 2021 +0800
|
|     Move file readme to readme.md
|
* commit 12fd153bc350a02904b9b68f75e50452b02b918a
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 17:32:05 2021 +0800
|
|     Create a complete web page
|
|     Add style.css
|
|     Add js
|
|     modified index.html: add a link for refering project
|
* commit 9ccc1e2ee4c4663e6e616bdf4290a41e2bc59d0f
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 17:24:02 2021 +0800
|
|     add index + logo
|
* commit 86f5cad49e27ff8c97924fdbae7506a5c12a85b6
  Author: weikai <277898160@qq.com>
  Date:   Tue Dec 28 17:02:00 2021 +0800

      add readme

```



## 18 怎么把间隔的几个commit整理成1个commit : git rebase

![1640704679940](玩转Git三剑客/images/1640704679940.png)

```powershell
git rebase -i 86f5cad
```

![1640704781514](玩转Git三剑客/images/1640704781514.png)

```powershell
pick 9ccc1e2 add index + logo
pick 12fd153 Create a complete web page
pick 2b0bf6a Move file readme to readme.md
```
增加一个pick,

```powershell
pick 86f5cad  ##增加pick，使用commit
s 2b0bf6a Move file readme to readme.md #s,即squash，融合到之前的commit
pick 9ccc1e2 add index + logo
pick 12fd153 Create a complete web page
pick 2b0bf6a Move file readme to readme.md #删除这行
```

![1640705341810](玩转Git三剑客/images/1640705341810.png)

Esc, :wq!

```powershell
$ git rebase -i  86f5cad49e
interactive rebase in progress; onto 86f5cad
Last command done (1 command done):
   pick 86f5cad
Next commands to do (3 remaining commands):
   squash 2b0bf6a Move file readme to readme.md
   pick 9ccc1e2 add index + logo
  (use "git rebase --edit-todo" to view and edit)
You are currently rebasing branch 'master' on '86f5cad'.
  (all conflicts fixed: run "git rebase --continue")

nothing to commit, working tree clean
The previous cherry-pick is now empty, possibly due to conflict resolution.
If you wish to commit it anyway, use:

    git commit --allow-empty

Otherwise, please use 'git rebase --skip'
Could not apply 86f5cad...


$ git status
interactive rebase in progress; onto 86f5cad
Last command done (1 command done):
   pick 86f5cad
Next commands to do (3 remaining commands):
   squash 2b0bf6a Move file readme to readme.md
   pick 9ccc1e2 add index + logo
  (use "git rebase --edit-todo" to view and edit)
You are currently rebasing branch 'master' on '86f5cad'.
  (all conflicts fixed: run "git rebase --continue")

nothing to commit, working tree clean

$ git rebase --continue

```

![1640705509076](玩转Git三剑客/images/1640705509076.png)
添加一些message

![1640705635971](玩转Git三剑客/images/1640705635971.png)

Esc, :wq!

```powershell
$ git rebase --continue
[detached HEAD 7b07d4f] Add readme.md
 Author: weikai <277898160@qq.com>
 Date: Tue Dec 28 17:02:00 2021 +0800
 1 file changed, 2 insertions(+)
 create mode 100644 readme.md
Successfully rebased and updated refs/heads/master.

```

查看log:

```powershell
$ git log --graph
* commit bef58ea896250322855ea704d3ba2d5b77646733 (HEAD -> master)
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 17:32:05 2021 +0800
|
|     Create a complete web page
|
|     Add style.css
|
|     Add js
|
|     modified index.html: add a link for refering project
|
* commit a9f44d2c54295e9eab053a32ce4a7bd44dd6df17
| Author: weikai <277898160@qq.com>
| Date:   Tue Dec 28 17:24:02 2021 +0800
|
|     add index + logo
|
* commit 7b07d4fab520c7ec36428b6a728e6889682aca1f
  Author: weikai <277898160@qq.com>
  Date:   Tue Dec 28 17:02:00 2021 +0800

      Add readme.md

      add readme

      Move file readme to readme.md
$ gitk -all
```

![1640706070351](玩转Git三剑客/images/1640706070351.png)

特别注意：

**现在已经存在两个独立的树**



## 19 怎么比较暂存区和HEAD所含文件的差异

命令：查看暂存区和HEAD的区别

```powershell
$ git diff --cached
```



```powershell
$ git status
On branch master
nothing to commit, working tree clean

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ vi index.html
```

<img src="玩转Git三剑客/images/1640706412539.png" alt="1640706412539" style="zoom:80%;" />

```powershell
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

$ git add index.htm #加入暂存区
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html

```


查看暂存区和HEAD的区别，

```powershell
$ git diff --cached
diff --git a/index.html b/index.html
index feccfe5..452f17f 100644
--- a/index.html
+++ b/index.html
@@ -29,7 +29,7 @@
         <div class="accordion"><h1>Basic Commands</h1></div>
             <div class="panel">
                 <ol>
-                    <li></li>
+                    <li>add</li>
                     <li></li>
                     <li></li>
                     <li></li>

```

在还没生成commit之前，还可以修改

```powershell
$ vi index.html
```

![1640706815940](玩转Git三剑客/images/1640706815940.png)

```powershell
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

$ git add index.html #把第二次修改加入暂存区
$ git diff --cached
diff --git a/index.html b/index.html
index feccfe5..3f58dc9 100644
--- a/index.html
+++ b/index.html
@@ -29,7 +29,7 @@
         <div class="accordion"><h1>Basic Commands</h1></div>
             <div class="panel">
                 <ol>
-                    <li></li>
+                    <li>cofing</li>
                     <li></li>
                     <li></li>
                     <li></li>



```

提交commit

```powershell
$ git commit -m 'Add the first git command with config'
[master 70ef4a1] Add the first git command with config
 1 file changed, 1 insertion(+), 1 deletion(-)
 
$ git log --oneline
70ef4a1 (HEAD -> master) Add the first git command with config
bef58ea Create a complete web page
a9f44d2 add index + logo
7b07d4f Add readme.md

```



## 20 怎么比较工作区和暂存区所含文件的差异

命令：工作区和暂存区所含文件的差异

```powershell
$ git diff #全部文件
$ git diff -- styles/style.css ## 指定某个文件比较
$ git diff -- readme.md styles/style.css ## 指定多个文件比较
```



示例：

```powershell
$ vi index.html
```

<img src="玩转Git三剑客/images/1640707360866.png" alt="1640707360866" style="zoom:80%;" />

<img src="玩转Git三剑客/images/1640707407802.png" alt="1640707407802" style="zoom:33%;" />

```powershell
$ vi styles/style.css
```

![1640707521473](玩转Git三剑客/images/1640707521473.png)

<img src="玩转Git三剑客/images/1640707554727.png" alt="1640707554727" style="zoom:80%;" />



查看工作区和暂存区所含文件的差异：

```powershell
$ git add index.html ##修改index.html 加入了暂存区
$ git diff
diff --git a/styles/style.css b/styles/style.css
index a38cb8a..7479a7c 100644
--- a/styles/style.css
+++ b/styles/style.css
@@ -1,7 +1,7 @@
 body{
   background-color: orange;
   font-family: 'Monaco', sans-serif;
-  color: white; ## 暂存区还是这个
+  color: black; ## 工作区已经修改为这个
 }

 body a{
@@ -61,4 +61,4 @@ footer{

 footer p{
   margin-bottom:0;
-}
\ No newline at end of file
+}

$ git add styles/style.css

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html
        modified:   styles/style.css
$ git diff

```



## 21 如何让暂存区恢复和HEAD一样

```powershell
git reset HEAD <file>...
```

-  <file>... 一个文件或者多个文件
- 不写 <file>...，就指所有文件

```powershell
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html
        modified:   styles/style.css

$ git reset HEAD
Unstaged changes after reset:
M       index.html
M       styles/style.css

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html
        modified:   styles/style.css

no changes added to commit (use "git add" and/or "git commit -a")

$ git diff --cached 
##暂存区和HEAD一致
```



## 22 如何让工作区的文件恢复为和暂存区一样

命令：

```powershell
git checkout -- <file>...

示例：
git checkout -- index.html##恢复为暂存区
git diff index.html ##检查工作区与暂存区的不同
```







```powershell
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html
        modified:   styles/style.css

no changes added to commit (use "git add" and/or "git commit -a")

$ git add index.html ## 加入暂存区
$ git diff --cached
diff --git a/index.html b/index.html
index 3f58dc9..f792dfa 100644
--- a/index.html
+++ b/index.html
@@ -14,7 +14,7 @@
         <div class="accordion"><h1>Terminologys</h1></div>
             <div class="panel">
                 <ol>
-                    <li></li>
+                    <li>bare repository</li>
                     <li></li>
                     <li></li>
                     <li></li>
                     
$ vi index.html ##修改工作区，将英文改成中文

```

<img src="玩转Git三剑客/images/1640709199449.png" alt="1640709199449" style="zoom:80%;" />

```powershell
$ git diff index.html ##比较工作区和暂存区的异同
diff --git a/index.html b/index.html
index f792dfa..0a70d73 100644
--- a/index.html
+++ b/index.html
@@ -14,7 +14,7 @@
         <div class="accordion"><h1>Terminologys</h1></div>
             <div class="panel">
                 <ol>
-                    <li>bare repository</li>
+                    <li>裸仓库</li>
                     <li></li>
                     <li></li>
                     <li></li>

## 后来又想了下，还是恢复为英文吧，即:恢复为暂存区的内容
$ git checkout -- index.html
$ git diff index.html
$ vi index.html
```

<img src="玩转Git三剑客/images/1640709627675.png" alt="1640709627675" style="zoom: 80%;" />



## 23 怎么取消暂存区部分文件的变更

命名：

```powershell
git reset HEAD -- <file>...
示例：
git reset HEAD -- styles/style.css
git status
```



演示：

```powershell
$ vi readme.md
+ Say Hello word
$ git add .

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html
        modified:   readme.md
        modified:   styles/style.css

$ git reset HEAD -- styles/style.css
Unstaged changes after reset:
M       styles/style.css


$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html
        modified:   readme.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   styles/style.css


## 多个文件撤销暂存区的变更
$ git reset HEAD -- index.html readme.md
Unstaged changes after reset:
M       index.html
M       readme.md
M       styles/style.css

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html
        modified:   readme.md
        modified:   styles/style.css

no changes added to commit (use "git add" and/or "git commit -a")

$ $ git status
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html
        modified:   readme.md
        modified:   styles/style.css

no changes added to commit (use "git add" and/or "git commit -a")

```



## 24 消除最近的几次提交

命令：

```powershell
git reset --hard commit哈希值（指定commit）
示例：
git reset --hard 8cd64a3
```

这条命令要慎用，因为会导致commit永久丢失，不可恢复



```powershell
gitk -all
```

<img src="玩转Git三剑客/images/1640711042997.png" alt="1640711042997" style="zoom:80%;" />

让temp分支回到 Add js 这个commit

```powershell
$ git commit -m '3 files changed'
$ git status
On branch master
nothing to commit, working tree clean


$ git checkout temp #切换到temp分支

Switched to branch 'temp'

$ git branch
  master
* temp #当前分支

$ gitk --all

```

<img src="玩转Git三剑客/images/1640711784373.png" alt="1640711784373" style="zoom: 80%;" />

```powershell
$ git log --oneline
3a92237 (HEAD -> temp) Add temp branch test
8ecc643 modified index: refering projects
8cd64a3 (tag: JS) Add js
43d68f3 Add style.css
9ccc1e2 add index + logo
86f5cad add readme

#temp 分支回到【8cd64a3】commit上
$ git reset --hard 8cd64a3
HEAD is now at 8cd64a3 Add js
$ gitk --all

```

<img src="玩转Git三剑客/images/1640712137996.png" alt="1640712137996" style="zoom:80%;" />

<img src="玩转Git三剑客/images/1640712223793.png" alt="1640712223793" style="zoom:80%;" />

```powershell
$ git checkout master #切换到master分支
Switched to branch 'master'

$ git log --oneline
70aa453 (HEAD -> master) 3 files changed
70ef4a1 Add the first git command with config
bef58ea Create a complete web page
a9f44d2 add index + logo
7b07d4f Add readme.md

```

<img src="玩转Git三剑客/images/1640712346369.png" alt="1640712346369" style="zoom:50%;" />

<img src="玩转Git三剑客/images/1640712471122.png" alt="1640712471122" style="zoom:80%;" />

## 25 看看不同提交的指定文件的差异

比较master和temp分支

```powershell
 git diff temp master ## 全部文件
 git diff temp master -- index.html ## 单个文件
 
 git diff comitId1 comitId2 ## 全部文件
 git diff comitId1 comitId2 -- index.html ## 单个文件
```



演示：

```powershell
$ git log --all --oneline --graph
* 70aa453 (HEAD -> master) 3 files changed
* 70ef4a1 Add the first git command with config
* bef58ea Create a complete web page
* a9f44d2 add index + logo
* 7b07d4f Add readme.md
* 8cd64a3 (tag: JS, temp) Add js
* 43d68f3 Add style.css
* 9ccc1e2 add index + logo
* 86f5cad add readme

$ git diff temp master ## 全部文件
diff --git a/index.html b/index.html
index 6ad4c68..f792dfa 100644
--- a/index.html
+++ b/index.html
@@ -14,7 +14,7 @@
         <div class="accordion"><h1>Terminologys</h1></div>
             <div class="panel">
                 <ol>
-                    <li></li>
+                    <li>bare repository</li>
                     <li></li>
                     <li></li>
                     <li></li>
@@ -29,7 +29,7 @@
         <div class="accordion"><h1>Basic Commands</h1></div>
             <div class="panel">
                 <ol>
-                    <li></li>
+                    <li>cofing</li>
                     <li></li>
                     <li></li>
                     <li></li>
@@ -43,7 +43,11 @@
             </div>
         </div>
     </section>
-
+     <footer>
+        <p>
+            <a href="https://github.com/TTN-js/unforGITtable">参考项目01</a>
+        </p>
+    </footer>
     <script src="js/script.js"></script>
 </body>
 </html>
diff --git a/readme b/readme.md
similarity index 77%
rename from readme
rename to readme.md
index 7c2bad2..6804675 100644
--- a/readme
+++ b/readme.md


$ git diff temp master -- index.html
...
```



## 26 正确删除文件的方法

比如要删除readme.md 文件

### 方式一：在工作区删，再 git rm

```powershell
$ ls -al
total 13
drwxr-xr-x 1 wei 197121    0 Dec 29 01:24 ./
drwxr-xr-x 1 wei 197121    0 Dec 28 16:54 ../
drwxr-xr-x 1 wei 197121    0 Dec 29 01:24 .git/
drwxr-xr-x 1 wei 197121    0 Dec 28 23:34 images/
-rw-r--r-- 1 wei 197121 1506 Dec 29 01:24 index.html
drwxr-xr-x 1 wei 197121    0 Dec 28 23:34 js/
-rw-r--r-- 1 wei 197121   69 Dec 29 01:24 readme.md
drwxr-xr-x 1 wei 197121    0 Dec 29 01:24 styles/

$ rm readme.md # 工作区删除

$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    readme.md

no changes added to commit (use "git add" and/or "git commit -a")

$ git rm readme.md #暂存区删除
rm 'readme.md'

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    readme.md

```



### 方式二：git rm 文件名

```powershell
#先撤销多次commit
$ git reset --hard HEAD
HEAD is now at 70aa453 3 files changed

$ git status
On branch master
nothing to commit, working tree clean

$ ls -al
total 13
drwxr-xr-x 1 wei 197121    0 Dec 29 09:47 ./
drwxr-xr-x 1 wei 197121    0 Dec 28 16:54 ../
drwxr-xr-x 1 wei 197121    0 Dec 29 09:47 .git/
drwxr-xr-x 1 wei 197121    0 Dec 28 23:34 images/
-rw-r--r-- 1 wei 197121 1506 Dec 29 01:24 index.html
drwxr-xr-x 1 wei 197121    0 Dec 28 23:34 js/
-rw-r--r-- 1 wei 197121   69 Dec 29 09:47 readme.md #文件回来了
drwxr-xr-x 1 wei 197121    0 Dec 29 01:24 styles/

$ git rm readme.md
rm 'readme.md'

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    readme.md

$ ls -al
total 12
drwxr-xr-x 1 wei 197121    0 Dec 29 09:49 ./
drwxr-xr-x 1 wei 197121    0 Dec 28 16:54 ../
drwxr-xr-x 1 wei 197121    0 Dec 29 09:49 .git/
drwxr-xr-x 1 wei 197121    0 Dec 28 23:34 images/
-rw-r--r-- 1 wei 197121 1506 Dec 29 01:24 index.html
drwxr-xr-x 1 wei 197121    0 Dec 28 23:34 js/
drwxr-xr-x 1 wei 197121    0 Dec 29 01:24 styles/

```



## 27 开发中临时加塞紧急任务怎么处理

命令：

```powershell
git stash #独立保存工作区内容
git stash apply #搞回来
$ git stash list #查看 stash 列表，内容还保存
stash@{0}: WIP on master: 70aa453 3 files changed

git stash pop  # 搞回来，区别于apply 是，不再保存
$ git stash list

```



```powershell
# 先恢复上一节的 remove readme.md
$ git reset --hard HEAD
HEAD is now at 70aa453 3 files changed

$ git status
On branch master
nothing to commit, working tree clean
```



### 临时插入任务模拟

假设，现在正在正常开发

```powershell
vi index.html
```

<img src="玩转Git三剑客/images/1640743048382.png" alt="1640743048382" style="zoom:80%;" />

```powershell
$ git status  
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html  ##做的修改没有加入暂存区

no changes added to commit (use "git add" and/or "git commit -a")

$ git diff ## 比较工作区与暂存区的不同
diff --git a/index.html b/index.html
index f792dfa..cd55fd7 100644
--- a/index.html
+++ b/index.html
@@ -14,12 +14,12 @@
         <div class="accordion"><h1>Terminologys</h1></div>
             <div class="panel">
                 <ol>
-                    <li>bare repository</li>
-                    <li></li>
-                    <li></li>
                     <li></li>
                     <li></li>
                     <li></li>
+                    <li>stage</li>
+                    <li>working area</li>
+                    <li>'detached Head' state</li>
                     <li></li>
                     <li></li>
                     <li></li>

##老板临时要修改线上的bug
##把目前在工作区的内容先保存起来
$ git stash
Saved working directory and index state WIP on master: 70aa453 3 files changed

$ git stash list
stash@{0}: WIP on master: 70aa453 3 files changed

$ git status
On branch master
nothing to commit, working tree clean

$ git diff
## 无输出，说明工作区和暂存区一样

$ vi index.html #修复bug
```

<img src="玩转Git三剑客/images/1640743521312.png" alt="1640743521312" style="zoom:80%;" />

```powershell
$ git add index.html

#提交bug修复
$ git commit -m 'Bug:fix bug index.html'
[master 03f1da9] Bug:fix bug index.html
 1 file changed, 1 insertion(+), 1 deletion(-)
 
$ git status
On branch master
nothing to commit, working tree clean
```



### git stash apply

```powershell

## 把修改bug之前的工作区内容拿回来
$ git stash apply
Auto-merging index.html ## 自动合并
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

$ vi index.html
```

<img src="玩转Git三剑客/images/1640743860449.png" alt="1640743860449" style="zoom:80%;" />

看到文件进行了**自动合并**，既有之前工作区的内容，也有修复bug的内容。

```powershell
## 查看 stash list ，内容还在
$ git stash list
stash@{0}: WIP on master: 70aa453 3 files changed
```



### git stash pop

为了测试，恢复为与HEAD一样

```powershell
$ git reset --hard HEAD
HEAD is now at 03f1da9 Bug:fix bug index.html

$ git status
On branch master
nothing to commit, working tree clean

$ vi index.html
```

<img src="玩转Git三剑客/images/1640744584098.png" alt="1640744584098" style="zoom:80%;" />

git stash pop的的结果：

```powershell
$ git stash pop
Auto-merging index.html
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (8c6f9a858da8b2865b1e17842a81ab43ea55e6d5) ## Dropped 丢掉

$ git stash list
##无输出
```

文件也自动合并：

```powershell
$ vi index.html
```

<img src="玩转Git三剑客/images/1640744736807.png" alt="1640744736807" style="zoom:80%;" />



## 28 如何指定不需要Git管理的文件

不需要的git管理的文件，

git列举了常见的工程的.gitignore

https://github.com/github/gitignore

特别注意：文件名必须是 **.gitignore**，不能是别的



```powershell
## 恢复上一节的内容，以便往下测试
$ git reset --hard HEAD
HEAD is now at 03f1da9 Bug:fix bug index.html
```

新建doc/readhim

```powershell
$ mkdir doc
$ echo 'hi' > doc/readhim

$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        doc/

```

创建 .gitignore 文件

```powershell
$ vi .gitignore
doc

$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
## doc 文件夹已经不包含在git管控目标中

# doc/也同样
$ vi .gitignore # doc/也同样
doc/

$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore


```



### 假设 doc 是文件而不是文件夹

.gitignore 写 doc 和 doc/ 有什么区别

```powershell
$ rm -rf doc #删除doc文件夹和里面的文件
```

doc: 表示doc文件和doc文件夹下的文件都不管

doc/:表示doc文件管，但是doc文件夹下的文件不管

```powershell
(master)
$ ls
images/  index.html  js/  readme.md  styles/
$ vi doc
doc

$ cat doc
I‘m a file
$ ls -al
total 15
drwxr-xr-x 1 wei 197121    0 Dec 29 11:13 ./
drwxr-xr-x 1 wei 197121    0 Dec 28 16:54 ../
drwxr-xr-x 1 wei 197121    0 Dec 29 11:13 .git/
-rw-r--r-- 1 wei 197121    5 Dec 29 11:13 .gitignore
-rw-r--r-- 1 wei 197121   13 Dec 29 11:10 doc
drwxr-xr-x 1 wei 197121    0 Dec 28 23:34 images/
-rw-r--r-- 1 wei 197121 1513 Dec 29 10:43 index.html
drwxr-xr-x 1 wei 197121    0 Dec 28 23:34 js/
-rw-r--r-- 1 wei 197121   69 Dec 29 09:53 readme.md
drwxr-xr-x 1 wei 197121    0 Dec 29 01:24 styles/



$ cat .gitignore
doc

$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)

$ vi .gitignore
doc/
$ cat .gitignore
doc/
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        doc #管文件，不管doc文件夹

nothing added to commit but untracked files present (use "git add" to track)

```

commit

```powershell
$ rm doc

$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)


$ git add .gitignore
warning: LF will be replaced by CRLF in .gitignore.
The file will have its original line endings in your working directory

$ git commit -m 'Add .gitignore'
[master 19cacff] Add .gitignore
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore

```







## 29 如何将Git仓库备份到本地

命令：

```powershell
git remote
```



<img src="玩转Git三剑客/images/1640748777201.png" alt="1640748777201" style="zoom:80%;" />

哑协议与智能协议 

**直观区别：**哑协议传输进度不可⻅；智能协议传输可⻅。 

**传输速度：**智能协议⽐哑协议传输速度快。



备份特点

多点备份

<img src="玩转Git三剑客/images/1640748913684.png" alt="1640748913684" style="zoom:80%;" />

git clone --mirror和git clone --bare之间的区别是什么

> https://www.imooc.com/wenda/detail/579025
>
> git clone --bare origin-url：您将获得全部复制的标签，地方分支机构master (HEAD)，next，pu，和maint，没有远程跟踪分支。也就是说，所有分支都按原样复制，并且它设置为完全独立，不期望再次获取。任何远程分支（在克隆的远程中）和其他引用都被完全忽略。
>
> 不带工作区的clone



创建一个新的文件夹

```pow
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ cd ..

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src
$ mkdir mybackup

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src
$ cd mybackup/

# 使用哑协议备份 ，没有进度条
$ git clone --bare ../git_learning/.git ya.git
Cloning into bare repository 'ya.git'...
done.

## 使用只能协议：有进度条，打包压缩，传输更快
$ git clone --bare file://../git_learning/.git zn.git
Cloning into bare repository 'zn.git'...
fatal: '//../git_learning/.git' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.


$ cd ya.git/
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/mybackup/ya.git (BARE:master)
$ git remote -v
origin  E:/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/mybackup/../git_learning/.git (fetch)
origin  E:/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/mybackup/../git_learning/.git (push)

$ git remote add  ya.git
fatal: not a git repository (or any of the parent directories): .git

```



# 第三章 Git 与 GitHub 的简单同步

## 30 注册一个GitHub 账号

注册一个 github账号

https://github.com/



## 31 配置公钥

通过SSH 连接远程仓储

https://docs.github.com/cn?query=SSH

 [Connecting to GitHub with SSH - GitHub Docs](https://docs.github.com/cn/authentication/connecting-to-github-with-ssh) 



### 检查现有的SSH秘钥

 [Checking for existing SSH keys - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys) 

Windows 系统

> **注意：**GitHub 通过删除较旧的、不安全的密钥类型来提高安全性。
>
> 不再支持 DSA 密钥 （）。现有密钥将继续运行，直到 2022 年 3 月 15 日。您无法在 GitHub.com 上向用户帐户添加新的 DSA 密钥。`ssh-dss`
>
> 2021 年 11 月 2 日之前的 RSA 密钥 （） 可以继续使用任何签名算法。在该日期之后生成的 RSA 密钥必须使用 SHA-2 签名算法。某些较旧的客户端可能需要升级才能使用 SHA-2 签名。`ssh-rsa``valid_after`

1. 打开Git Bash。

2. 输入以查看是否存在现有的 SSH 密钥。`ls -al ~/.ssh`

   ```shell
   $ ls -al ~/.ssh
   # Lists the files in your .ssh directory, if they exist
   ```

3. 检查目录列表以查看是否已具有公有 SSH 密钥。默认情况下，GitHub 支持的公钥的文件名为以下文件名之一。

   - *id_rsa.pub*
   - *id_ecdsa.pub*
   - *id_ed25519.pub*

   **提示**： 如果您收到*~/.ssh*不存在的错误，则默认位置中没有现有的 SSH 密钥对。您可以在下一步中创建新的 SSH 密钥对。

4. 生成新的 SSH 密钥或上传现有密钥。

   - 如果您没有受支持的公钥和私钥对，或者不希望使用任何可用的密钥对，请生成新的 SSH 密钥。

   - 如果您看到列出了要用于连接到 GitHub 的现有公钥和私钥对（例如*，id_rsa.pub*和*id_rsa），*则可以将密钥添加到 ssh-agent。

     有关生成新的 SSH 密钥或向 ssh 代理添加现有密钥的详细信息，请参阅"[生成新的 SSH 密钥并将其添加到 ssh 代理](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)"。



实践

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 ~/Desktop
$ ls -al ~/.ssh
ls: cannot access '/c/Users/wei/.ssh': No such file or directory

## 如果您收到~/.ssh不存在的错误，则默认位置中没有现有的 SSH 密钥对。
## 您可以在下一步中创建新的 SSH 密钥对


```



### 生成新的 SSH 密钥并将其添加到 ssh 代理

 [生成新的 SSH 密钥并将其添加到 ssh 代理 - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) 

粘贴以下文本，替换您的 GitHub 电子邮件地址。

```shell
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

**注意：**如果您使用的是不支持 Ed25519 算法的旧系统，请使用：

```shell
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```



实操：

打开 Git Bash

```powershell
$ ssh-keygen -t ed25519 -C "836439285@qq.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/wei/.ssh/id_ed25519):#回车
Created directory '/c/Users/wei/.ssh'.
Enter passphrase (empty for no passphrase):#回车
Enter same passphrase again:#回车
Your identification has been saved in /c/Users/wei/.ssh/id_ed25519
Your public key has been saved in /c/Users/wei/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:Ut8ULqiZhxNz39UdV2FWKhb8UmUk+clFDwEQaLZJiCw 836439285@qq.com
The key's randomart image is:
+--[ED25519 256]--+
|   . . . .o++.+@%|
|  E o . =. ..o=**|
|   .  o++o. =o+.*|
|       Xoo *.o.o.|
|      B S o o.   |
|       +         |
|                 |
|                 |
|                 |
+----[SHA256]-----+

$ ls -al ~/.ssh
total 26
drwxr-xr-x 1 wei 197121   0 Dec 29 12:49 ./
drwxr-xr-x 1 wei 197121   0 Dec 29 12:48 ../
-rw-r--r-- 1 wei 197121 411 Dec 29 12:49 id_ed25519 #私钥
-rw-r--r-- 1 wei 197121  98 Dec 29 12:49 id_ed25519.pub #公钥 


```



### 将新的SSH添加到GitHub账户

 [将新的 SSH 密钥添加到您的 GitHub 帐户 - GitHub 文档](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) 

**SSH的好处就是，把本地的仓储 push 到Github 上，不再需要填写GitHub的账号和密码了**



```powershell
$ cat ~/.ssh/id_ed25519.pub #私钥内容
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQ
。。。。。。
H+OrB+h5lNryxqnmyzNbXFa/10hCSmp
dCJLFE8/ksZZSHETncCJAAAAEDgzNjQzOTI4NUBxcS5jb20BAgMEBQ==
-----END OPENSSH PRIVATE KEY-----
```

拷贝公钥内容

打开github账户头像--Settings->SSH and GPG keys

点击【New SSH Key】



<img src="玩转Git三剑客/images/1640754157224.png" alt="1640754157224" style="zoom:80%;" />

1. 在"标题"字段中，为新键添加描述性标签。例如，如果您使用的是个人 Mac，则可以将此密钥称为"个人 MacBook Air"。
2. 将密钥粘贴到"密钥"字段中。

<img src="玩转Git三剑客/images/1640754296807.png" alt="1640754296807" style="zoom:80%;" />

点击【Add SSH key】

 如果出现提示，请确认您的 GitHub 密码。 

<img src="玩转Git三剑客/images/1640754395321.png" alt="1640754395321" style="zoom:80%;" /> Key is invalid. You 

```powershell
must supply a key in OpenSSH public key format 
```

<img src="玩转Git三剑客/images/1640754942489.png" alt="1640754942489" style="zoom:80%;" />

看来不支持 Ed加密，改用

```shell
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

重复上述步骤

![1640755258032](玩转Git三剑客/images/1640755258032.png)

添加成功

![1640755282695](玩转Git三剑客/images/1640755282695.png)



## 32 在GitHub上创建个人仓库

创建个人仓库：

https://github.com/new

<img src="玩转Git三剑客/images/1640761432938.png" alt="1640761432938" style="zoom: 50%;" />



## 33 把本地仓库同步到GitHub

### git remote add github

注意到，GitHub上的仓库，已经有另一个文件 LICENSE

<img src="玩转Git三剑客/images/1640761950658.png" alt="1640761950658" style="zoom:67%;" />

本地没有这个文件，Push会有什么问题？





<img src="玩转Git三剑客/images/1640762200654.png" alt="1640762200654" style="zoom: 50%;" />

这里我们选择SSH方式

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git remote -v #查看管理的远程仓库

$ git remote github git@github.com:K-Artisan/git-leaning.git
error: Unknown subcommand: github
usage: git remote [-v | --verbose]
   or: git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
   or: git remote rename <old> <new>
   or: git remote remove <name>
   or: git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
   or: git remote [-v | --verbose] show [-n] <name>
   or: git remote prune [-n | --dry-run] <name>
   or: git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
   or: git remote set-branches [--add] <name> <branch>...
   or: git remote get-url [--push] [--all] <name>
   or: git remote set-url [--push] <name> <newurl> [<oldurl>]
   or: git remote set-url --add <name> <newurl>
   or: git remote set-url --delete <name> <url>

    -v, --verbose         be verbose; must be placed before a subcommand

# add github表示：创建一个子命令：github，代表git仓库：git@github.com:K-Artisan/git-leaning.git
$ git remote add github git@github.com:K-Artisan/git-leaning.git

$ git remote -v
github  git@github.com:K-Artisan/git-leaning.git (fetch)
github  git@github.com:K-Artisan/git-leaning.git (push)

## push 到 github仓库
$ git push github --all
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])? y
Please type 'yes', 'no' or the fingerprint: yes
Warning: Permanently added 'github.com,20.205.243.166' (ECDSA) to the list of known hosts.
Enumerating objects: 40, done.
Counting objects: 100% (40/40), done.
Delta compression using up to 8 threads
Compressing objects: 100% (32/32), done.
Writing objects: 100% (40/40), 23.17 KiB | 1.10 MiB/s, done.
Total 40 (delta 13), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (13/13), done.
To github.com:K-Artisan/git-leaning.git
 * [new branch]      master -> master
 * [new branch]      temp -> temp



```

Push成功后，在GitHub看到了上传的版本

![1640762745834](玩转Git三剑客/images/1640762745834.png)![1640762816325](玩转Git三剑客/images/1640762816325.png)

```powershell
$gitk --all
```



<img src="玩转Git三剑客/images/1640763049345.png" alt="1640763049345" style="zoom:80%;" />

假设 GitHub 也有一个分支 叫**main**，并里面已经存在了文件，我们要把它合并到本地的master分支，

这时，我们需要先 fetch到本地

> fetch 只是拉取到本地，不会与本地产生关联



### fetch **github**/main

现在的问题：

因为 本地的master 少了 **github/main** 分支上的 **LICESE 文件**

我们的目标是，把 **github/main** 分支上的 LICESE 文件 **拉取（fetch）**到**本地的master**分支上，

然后进行**合并（merge）**，

最后把本地的master分支 **推到（push）**到 **github/maste**r分支上。

打算以后废弃**github/main**分支





这里我们拉取有github上的main分支,

```powershell
$ git fetch github main
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 1.17 KiB | 7.00 KiB/s, done.
From github.com:K-Artisan/git-leaning
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> github/main

$ gitk --all
```

<img src="玩转Git三剑客/images/1640763547859.png" alt="1640763547859" style="zoom:80%;" />

多出来一个分支，现在有3棵树

```powershell
$ git branch -av
* master                19cacff Add .gitignore
  temp                  8cd64a3 Add js
  remotes/github/main   93bda36 Initial commit
  remotes/github/master 19cacff Add .gitignore
  remotes/github/temp   8cd64a3 Add js

```

<img src="玩转Git三剑客/images/1640763547859.png" alt="1640763547859" style="zoom:80%;" />



### 本地master -> **git** merge github/main

github/main 和本地的master 分支是独立的不在一棵树上，merge失败

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (main)
$ git checkout master
Switched to branch 'master'

$  git merge github/main
fatal: refusing to merge unrelated histories
#合并失败，两个分支两者是独立的，没有关联，不在一棵树上。

$ git merge -h
usage: git merge [<options>] [<commit>...]
    --allow-unrelated-histories
                          allow merging unrelated histories 允许不相关的历史（不在一棵树上）的分支合并，
 ...
 
$ git merge --allow-unrelated-histories github/main
#在弹出下图的界面不做修改，直接ESC，:wq

Merge made by the 'recursive' strategy.
 LICENSE | 21 +++++++++++++++++++++
 1 file changed, 21 insertions(+)
 create mode 100644 LICENSE

```

![1640764431602](玩转Git三剑客/images/1640764431602.png)

```powershell
$ gitk --all
```

<img src="玩转Git三剑客/images/1640764658884.png" alt="1640764658884" style="zoom: 80%;" />

在**本地**，基于 github/main 又生成了一个本地的 master

这时，**本地的master有两个父亲**。

<img src="玩转Git三剑客/images/1640764961809.png" alt="1640764961809" style="zoom: 80%;" />

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ ls -al
total 18
drwxr-xr-x 1 wei 197121    0 Dec 29 15:53 ./
drwxr-xr-x 1 wei 197121    0 Dec 29 11:45 ../
drwxr-xr-x 1 wei 197121    0 Dec 29 15:54 .git/
-rw-r--r-- 1 wei 197121    6 Dec 29 15:46 .gitignore
-rw-r--r-- 1 wei 197121 1087 Dec 29 15:53 LICENSE   # github/main 也被合并进来了
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 images/
-rw-r--r-- 1 wei 197121 1513 Dec 29 15:46 index.html
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 js/
-rw-r--r-- 1 wei 197121   69 Dec 29 15:46 readme.md
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 styles/

```

这时，**GitHub上的main分支还只有一个文件**

<img src="玩转Git三剑客/images/1640765129320.png" alt="1640765129320" style="zoom:50%;" />

### 本地master-> git push github master

这时，**github/maste**r 分支上的还没有缺少的 LICENSE文件

```powershell
# 上传到 github/main 失败，没有上传流
$ git push github/main
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream github/main master

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git push --set-upstream github/main master
fatal: 'github/main' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

## 那就上传到 GitHub/master 上
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ git push github master
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 311 bytes | 155.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:K-Artisan/git-leaning.git
   19cacff..9f13e73  master -> master

```

这时，**github/master** 分支上的 有了原来缺少的 LICENSE文件，

并且 **commit数由7变成了8**

<img src="玩转Git三剑客/images/1640765862595.png" alt="1640765862595" style="zoom:67%;" />

```powershell
$ gitk --all
```

<img src="玩转Git三剑客/images/1640765960498.png" alt="1640765960498" style="zoom:80%;" />

**最后，将 github/main 分支废弃即可**



# 第四章 Git 多人单分支集成协作时常见场景

## 34 不同人修改了不同的文件如何处理

### 模拟多人工作场景

基于**master**分支创建一个新的分支 **feature/add_git_commands**

<img src="玩转Git三剑客/images/1640842157902.png" alt="1640842157902" style="zoom:50%;" />

#### git clone

然后为第二个人在本地新建工作目录

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ cd ..

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src
$ pwd
/e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src
$ ll
total 4
drwxr-xr-x 1 wei 197121 0 Dec 28 16:54 0-material/
drwxr-xr-x 1 wei 197121 0 Dec 29 15:53 git_learning/
drwxr-xr-x 1 wei 197121 0 Dec 29 11:55 mybackup/

## 使用SS协议拷贝Github上的仓库，新工作目录是 git_learning02
$ git clone git@github.com:K-Artisan/git-leaning.git git_learning02
Cloning into 'git_learning02'...
remote: Enumerating objects: 45, done.
remote: Counting objects: 100% (45/45), done.
remote: Compressing objects: 100% (22/22), done.
remote: Total 45 (delta 14), reused 42 (delta 14), pack-reused 0
Receiving objects: 100% (45/45), 24.59 KiB | 2.73 MiB/s, done.
Resolving deltas: 100% (14/14), done.

## 新工作目录是 git_learning02
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src
$ ll
total 4
drwxr-xr-x 1 wei 197121 0 Dec 28 16:54 0-material/
drwxr-xr-x 1 wei 197121 0 Dec 29 15:53 git_learning/
drwxr-xr-x 1 wei 197121 0 Dec 30 13:41 git_learning02/
drwxr-xr-x 1 wei 197121 0 Dec 29 11:55 mybackup/

```



#### 设置仓库的local账户【账号2】

```pow
$ cd git_learning02
$ git config --add --local user.name 'Keasy5'
$ git config --add --local user.email '277898160@qq.com'

$ git config --local --list
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
remote.origin.url=git@github.com:K-Artisan/git-leaning.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.main.remote=origin
branch.main.merge=refs/heads/main
user.name=Keasy5
user.email=277898160@qq.com
```



### 创建本地分支

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (main)
$ git branch -av
* main                                    93bda36 Initial commit
  remotes/origin/HEAD                     -> origin/main
  remotes/origin/feature/add_git_commands 9f13e73 Merge remote-tracking branch 'github/main'
  remotes/origin/main                     93bda36 Initial commit
  remotes/origin/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/origin/temp                     8cd64a3 Add js

## 基于远程分支origin/feature/add_git_commands 创建本地分支 feature/add_git_commands
$ git checkout -b feature/add_git_commands origin/feature/add_git_commands
Switched to a new branch 'feature/add_git_commands'
Branch 'feature/add_git_commands' set up to track remote branch 'feature/add_git_commands' from 'origin'.


wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)
$ git branch -av
* feature/add_git_commands                9f13e73 Merge remote-tracking branch 'github/main'
  main                                    93bda36 Initial commit
  remotes/origin/HEAD                     -> origin/main
  remotes/origin/feature/add_git_commands 9f13e73 Merge remote-tracking branch 'github/main'
  remotes/origin/main                     93bda36 Initial commit
  remotes/origin/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/origin/temp                     8cd64a3 Add js

```

![1640843988372](玩转Git三剑客/images/1640843988372.png)



### 开始修改本地 readme 代码然后push

```powershell
$ vi readme.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

+ We are going to record some git commands here

# add
$ git add -u 

$ git status
On branch feature/add_git_commands
Your branch is up to date with 'origin/feature/add_git_commands'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   readme.md

## commit
$ git commit -m 'Add git commands descriptions in readme'
[feature/add_git_commands 42187d7] Add git commands descriptions in readme
 1 file changed, 2 insertions(+)

## push
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 393 bytes | 393.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:K-Artisan/git-leaning.git
   9f13e73..42187d7  feature/add_git_commands -> feature/add_git_commands

```

远程GitHub 已经修改

<img src="玩转Git三剑客/images/1640844938221.png" alt="1640844938221" style="zoom:80%;" />

### 另一个账号修改【账号1】

#### 切换其它账号

```pow
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)
$ cd ../git_learning

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (master)
$ pwd
/e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning

$ git config --local

$ git config --local --list
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true

user.name='Artisan-K'
user.email='836439285@qq.com'

remote.github.url=git@github.com:K-Artisan/git-leaning.git
remote.github.fetch=+refs/heads/*:refs/remotes/github/*
branch.main.remote=github
branch.main.merge=refs/heads/main

```



#### 拉取（fetch）最新代码

```powershell
$ git branch -av
  main                  93bda36 Initial commit
* master                9f13e73 Merge remote-tracking branch 'github/main'
  temp                  8cd64a3 Add js
  remotes/github/main   93bda36 Initial commit
  remotes/github/master 9f13e73 Merge remote-tracking branch 'github/main'
  remotes/github/temp   8cd64a3 Add js
## 还没有feature/add_git_commands 分支

$ git fetch github
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), 373 bytes | 1024 bytes/s, done.
From github.com:K-Artisan/git-leaning
 * [new branch]      feature/add_git_commands -> github/feature/add_git_commands

$ git branch -av
  main                                    93bda36 Initial commit
* master                                  9f13e73 Merge remote-tracking branch 'github/main'
  temp                                    8cd64a3 Add js
  
  ## fetch 到最新分支
  remotes/github/feature/add_git_commands 42187d7 Add git commands descriptions in readme
  
  remotes/github/main                     93bda36 Initial commit
  remotes/github/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/github/temp                     8cd64a3 Add js

```



#### 创建本地分支 feature/add_git_commands

```powershell
$ git checkout -b feature/add_git_commands github/feature/add_git_commands
Switched to a new branch 'feature/add_git_commands'
Branch 'feature/add_git_commands' set up to track remote branch 'feature/add_git_commands' from 'github'.

$ git branch -av

## 创建本地分支 feature/add_git_commands
* feature/add_git_commands                42187d7 Add git commands descriptions in readme
  main                                    93bda36 Initial commit
  master                                  9f13e73 Merge remote-tracking branch 'github/main'
  temp                                    8cd64a3 Add js
  remotes/github/feature/add_git_commands 42187d7 Add git commands descriptions in readme
  remotes/github/main                     93bda36 Initial commit
  remotes/github/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/github/temp                     8cd64a3 Add js

```



#### 修改不同的文件 Index.html

这里修改下 index.html

```powershell
$ vi index.html
```

<img src="玩转Git三剑客/images/1640845831234.png" alt="1640845831234" style="zoom:67%;" />

```powershell
$ git add -u
$ git commit -m 'Add git add in index.html'
[feature/add_git_commands 75fba30] Add git add in index.html
 1 file changed, 1 insertion(+), 1 deletion(-)
 
$ gitk --all
```

还没有Push之前

<img src="玩转Git三剑客/images/1640846027135.png" alt="1640846027135" style="zoom:80%;" />



### 账号1没Push，账号2修改readme

```powershell
# 切换到账号2 的工作目录
$ cd ../git_learning02

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)
$ pwd
/e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02

# 修改 readme.md 文件
$ vi readme.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

+ We are going to record some git commands here,eg add and son

# add and commit
$ git commit -am 'Fix readme'
[feature/add_git_commands 8f014ff] Fix readme
 1 file changed, 1 insertion(+), 1 deletion(-)

#push
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 323 bytes | 107.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:K-Artisan/git-leaning.git
   42187d7..8f014ff  feature/add_git_commands -> feature/add_git_commands

```



### 账号2push后，账号1 push 失败！

#### push 失败

```powershell
$ git push
To github.com:K-Artisan/git-leaning.git
 ! [rejected]        feature/add_git_commands -> feature/add_git_commands (fetch first)
error: failed to push some refs to 'github.com:K-Artisan/git-leaning.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```

账号2 push 失败。

现在怎么办？

#### fetch 远端

```powershell
$ git branch -av
  main                                    93bda36 Initial commit
* master                                  9f13e73 Merge remote-tracking branch 'github/main'
  temp                                    8cd64a3 Add js
  remotes/github/feature/add_git_commands 42187d7 Add git commands descriptions in readme
  remotes/github/main                     93bda36 Initial commit
  remotes/github/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/github/temp                     8cd64a3 Add js

-------------
$ git fetch github
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 2), reused 3 (delta 2), pack-reused 0
Unpacking objects: 100% (3/3), 303 bytes | 3.00 KiB/s, done.
From github.com:K-Artisan/git-leaning
   42187d7..8f014ff  feature/add_git_commands -> github/feature/add_git_commands

## 42187d7..8f014ff 

--
$ git branch -av
                                  ## ahead 1：本地比GitHub多一个commit
                                  ## behind 1：本地比GitHub少一个commit
* feature/add_git_commands                75fba30 [ahead 1, behind 1] Add git add in index.html
  main                                    93bda36 Initial commit
  master                                  9f13e73 Merge remote-tracking branch 'github/main'
  temp                                    8cd64a3 Add js
  remotes/github/feature/add_git_commands 8f014ff Fix readme


```

对其fetch前后：

```powershell
                                  ## ahead 1：本地比GitHub多一个commit
                                  ## behind 1：本地比GitHub少一个commit
* feature/add_git_commands                75fba30 [ahead 1, behind 1] Add git add in 
```

<img src="玩转Git三剑客/images/1640850435341.png" alt="1640850435341" style="zoom: 80%;" />

#### merge

```powershell
$ git merge github/feature/add_git_commands
Merge made by the 'recursive' strategy.
 readme.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

<img src="玩转Git三剑客/images/1640850550324.png" alt="1640850550324" style="zoom:80%;" />

再查看 readme，确实是账号2修改后的内容：

```powershell
$ cat readme.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

We are going to record some git commands here,eg add and son

```



#### push

```powershell
$ git push
Enumerating objects: 9, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 8 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 599 bytes | 199.00 KiB/s, done.
Total 5 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To github.com:K-Artisan/git-leaning.git
   8f014ff..e67e474  feature/add_git_commands -> feature/add_git_commands

```

这时候，账号1的push成功了



## 35 不同人修改同文件不同区域如何处理？

### 同时修改 readme 文件

账号01修改

```powershell
$ vi readme.md

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)
$ cat readme.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

We are going to record some git commands here,eg add and son

+ fix by Account01

```

同时，账号02修改

```powershell
$ vi readme.md

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)
$ cat readme.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

We are going to record some git commands here,eg add and son

+ fix by Account02

```



### 账号1 先Push 到GitHub

```powershell
$ git commit -am 'Add readme fix01'
[feature/add_git_commands a921462] Add readme fix01
 1 file changed, 2 insertions(+)

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 331 bytes | 165.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:K-Artisan/git-leaning.git
   e67e474..a921462  feature/add_git_commands -> feature/add_git_commands

```



### 账号2 push 失败

```powershell
$ git commit -am 'Add fix readme Account02'
[feature/add_git_commands 4ebc982] Add fix readme Account02
 1 file changed, 2 insertions(+)

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)
$ git branch -av
                                          ##显示比远程的多一个commit
* feature/add_git_commands                4ebc982 [ahead 1] Add fix readme Account02
  main                                    93bda36 Initial commit
  remotes/origin/HEAD                     -> origin/main
  remotes/origin/feature/add_git_commands 8f014ff Fix readme
  remotes/origin/main                     93bda36 Initial commit
  remotes/origin/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/origin/temp                     8cd64a3 Add js

# push 失败
$ git push
To github.com:K-Artisan/git-leaning.git
 ! [rejected]        feature/add_git_commands -> feature/add_git_commands (fetch first)
error: failed to push some refs to 'github.com:K-Artisan/git-leaning.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```



### 账号2 fetch

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)
$ git fetch
remote: Enumerating objects: 14, done.
remote: Counting objects: 100% (13/13), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 8 (delta 5), reused 7 (delta 4), pack-reused 0
Unpacking objects: 100% (8/8), 859 bytes | 2.00 KiB/s, done.
From github.com:K-Artisan/git-leaning
   8f014ff..a921462  feature/add_git_commands -> origin/feature/add_git_commands



```



### 账号2 merge

```powershell
$ git branch -av
* feature/add_git_commands                4ebc982 [ahead 1, behind 3] Add fix readme Account02
  ......
  remotes/origin/feature/add_git_commands a921462 Add readme fix01
 
## 合并
$ git merge origin/feature/add_git_commands
Auto-merging readme.md


## 如果修改的不是同文件同区域，这里合并直接成功。


```



## 36 不同人修改了同文件的同一区域如何处理

先决条件：重复 **35 不同人修改同文件不同区域如何处理？**的操作，并且保证修改的同文件（readme.md）同区域，这时就会产生冲突。

### 账号2：fetch + merger 发生冲突

```powershell
$ git branch -av
* feature/add_git_commands                4ebc982 [ahead 1, behind 3] Add fix readme Account02
  ......
  remotes/origin/feature/add_git_commands a921462 Add readme fix01
 
## 合并
$ git merge origin/feature/add_git_commands
Auto-merging readme.md
CONFLICT (content): Merge conflict in readme.md
Automatic merge failed; fix conflicts and then commit the result.

## 比较，找到冲突的地方
$ git diff origin/feature/add_git_commands
diff --git a/readme.md b/readme.md
index 84ddb5c..dbce380 100644
--- a/readme.md
+++ b/readme.md
@@ -4,4 +4,8 @@ Have a good time!

 We are going to record some git commands here,eg add and son

+<<<<<<< HEAD    
+fix by Account02      ##当前账号的代码
+=======
 fix by Account01      ## 非当前账号的代码
+>>>>>>> origin/feature/add_git_commands
```



### 账号2：如何解决合并冲突

 出现了 Git 无法自动处理的冲突，那为了解决这种冲突，只能手动进行处理
此时打开 readme 文件，

```powershell
 vi readme.md
```

![1640862271529](玩转Git三剑客/images/1640862271529.png)

发现文件内容入下： 

```powershell
Say Hello word
Hi,we are learning Git together.
Have a good time!

We are going to record some git commands here,eg add and son

<<<<<<< HEAD
fix by Account02
=======
fix by Account01
>>>>>>> origin/feature/add_git_commands

```

这里我们把两个账号的修改**都保留**下来

<img src="玩转Git三剑客/images/1640862663851.png" alt="1640862663851" style="zoom:80%;" />

```powershell
$ vi readme.md

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands|MERGING)
$ cat readme.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

We are going to record some git commands here,eg add and son


fix by Account02

fix by Account01

```

### 账号2：提交解决冲突后的代码

```powershell
$ git commit -am 'mergr readme and fix conflicts'
[feature/add_git_commands bcd3859] mergr readme and fix conflicts

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)
$ git push
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 8 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 655 bytes | 327.00 KiB/s, done.
Total 6 (delta 4), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (4/4), completed with 3 local objects.
To github.com:K-Artisan/git-leaning.git
   a921462..bcd3859  feature/add_git_commands -> feature/add_git_commands

## 查看版本信息
$ git branch -av
* feature/add_git_commands                bcd3859 mergr readme and fix conflicts
  main                                    93bda36 Initial commit
  remotes/origin/HEAD                     -> origin/main
  remotes/origin/feature/add_git_commands bcd3859 mergr readme and fix conflicts
  remotes/origin/main                     93bda36 Initial commit
  remotes/origin/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/origin/temp                     8cd64a3 Add js


```



### 账号1：拉取（pull）解决冲突后的代码

命名说明：

```powershell
git pull 拉取并自动合并 = git fetch(拉取) + git merge（合并）

```

账号1：获取解决冲突后的代码

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)

$ git pull
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 6 (delta 4), reused 6 (delta 4), pack-reused 0
Unpacking objects: 100% (6/6), 635 bytes | 3.00 KiB/s, done.
From github.com:K-Artisan/git-leaning
   a921462..bcd3859  feature/add_git_commands -> github/feature/add_git_commands
Updating a921462..bcd3859
Fast-forward
 readme.md | 4 ++++
 1 file changed, 4 insertions(+)

## 账号1:获取到的内容是更新后的内容
$ cat readme.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

We are going to record some git commands here,eg add and son


fix by Account02

fix by Account01

## 查看版本信息
$ git branch -av
* feature/add_git_commands                bcd3859 mergr readme and fix conflicts
  main                                    93bda36 Initial commit
  remotes/origin/HEAD                     -> origin/main
  remotes/origin/feature/add_git_commands bcd3859 mergr readme and fix conflicts
  remotes/origin/main                     93bda36 Initial commit
  remotes/origin/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/origin/temp                     8cd64a3 Add js

```

账号1:获取到的内容是更新后的内容



## 37 同时变更了文件名和文件内容如何处理

为了演示不受干扰，两个账号都进行

```powershell
git pull 
```

并确保都与跟远程GitHub版本一致。

```powershell
$ git pull
Already up to date. #说明最新了
```



### 账号1：变更文件名(commit)

```powershell
$ git mv readme.md readhim.md

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)
$ git status
On branch feature/add_git_commands
Your branch is up to date with 'github/feature/add_git_commands'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    readme.md -> readhim.md


wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)
$ git commit -am 'Mv readme t- readhim'
[feature/add_git_commands 99ebc54] Mv readme t- readhim
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename readme.md => readhim.md (100%)

```



### 账号2：修改文件内容(commit)

```powershell
$ vi readme.md
```

<img src="玩转Git三剑客/images/1640865970487.png" alt="1640865970487" style="zoom:80%;" />

```powershell
$ git commit -am 'Add new context'
[feature/add_git_commands fb15289] Add new context
 1 file changed, 1 insertion(+)
```



### 账号1：先push

```powershell
$ git push
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 230 bytes | 230.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:K-Artisan/git-leaning.git
   bcd3859..99ebc54  feature/add_git_commands -> feature/add_git_commands

```



### 账号2：push

```powershell
$ git push
To github.com:K-Artisan/git-leaning.git
  #拒绝了
 ! [rejected]  feature/add_git_commands -> feature/add_git_commands (fetch first)
error: failed to push some refs to 'github.com:K-Artisan/git-leaning.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```



### 账号2：pull

```powershell
$ git pull
```

![1640866378308](玩转Git三剑客/images/1640866378308.png)

直接:q, 退出，不修改

```powershell
$ git pull
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 2 (delta 1), reused 2 (delta 1), pack-reused 0
Unpacking objects: 100% (2/2), 210 bytes | 1024 bytes/s, done.
From github.com:K-Artisan/git-leaning
   bcd3859..99ebc54  feature/add_git_commands -> origin/feature/add_git_commands
Merge made by the 'recursive' strategy. # 合并由“递归”的策略。
 readme.md => readhim.md | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename readme.md => readhim.md (100%)

```

git 自动合并

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)

$ ll
total 9
-rw-r--r-- 1 wei 197121 1087 Dec 30 13:41 LICENSE
drwxr-xr-x 1 wei 197121    0 Dec 30 13:57 images/
-rw-r--r-- 1 wei 197121 1516 Dec 30 18:52 index.html
drwxr-xr-x 1 wei 197121    0 Dec 30 13:57 js/
-rw-r--r-- 1 wei 197121  236 Dec 30 20:12 readhim.md
drwxr-xr-x 1 wei 197121    0 Dec 30 13:57 styles/

$ cat readhim.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

We are going to record some git commands here,eg add and son


fix by Account02

fix by Account01

Add new Content When Account01 Mv readme.md to readhim.md

```



### 账号1：push

```powershell
$ git push
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 8 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 591 bytes | 295.00 KiB/s, done.
Total 5 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 2 local objects.
To github.com:K-Artisan/git-leaning.git
   99ebc54..d4f699c  feature/add_git_commands -> feature/add_git_commands

```



### 账号1：pull

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)
$ git pull
remote: Enumerating objects: 8, done.
remote: Counting objects: 100% (8/8), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 5 (delta 3), reused 5 (delta 3), pack-reused 0
Unpacking objects: 100% (5/5), 571 bytes | 3.00 KiB/s, done.
From github.com:K-Artisan/git-leaning
   99ebc54..d4f699c  feature/add_git_commands -> github/feature/add_git_commands
Updating 99ebc54..d4f699c
Fast-forward
 readhim.md | 1 +
 1 file changed, 1 insertion(+)

$ cat readhim.md
Say Hello word
Hi,we are learning Git together.
Have a good time!

We are going to record some git commands here,eg add and son


fix by Account02

fix by Account01

Add new Content When Account01 Mv readme.md to readhim.md

```



## 38 把同一文件改成不同的文件名如何处理

### 账号2：修改文件名 readhim.md 为：readher.md

```powershell
$ git mv readhim.md readher.md

$ git commit -am 'mv readhim.md tp readher.md'
[feature/add_git_commands 02b7f37] mv readhim.md tp readher.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename readhim.md => readher.md (100%)

$ git push
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 230 bytes | 115.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:K-Artisan/git-leaning.git
   d4f699c..02b7f37  feature/add_git_commands -> feature/add_git_commands

```



### 账号1：修改文件名readhim.md 为：readme.md，但push失败

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)

$ git mv readhim.md readme.md

$ git commit -am 'mv readhim.md to readme.md'
[feature/add_git_commands 99d9130] mv readhim.md to readme.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename readhim.md => readme.md (100%)

$ git push
To github.com:K-Artisan/git-leaning.git
 ## push 被拒绝了
 ! [rejected]        feature/add_git_commands -> feature/add_git_commands (fetch first)
error: failed to push some refs to 'github.com:K-Artisan/git-leaning.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```



### 账号1：如何解决

#### pull : 发现两个文件冲突

```powershell
$ git pull
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 2 (delta 1), reused 2 (delta 1), pack-reused 0
Unpacking objects: 100% (2/2), 210 bytes | 1024 bytes/s, done.
From github.com:K-Artisan/git-leaning
   d4f699c..02b7f37  feature/add_git_commands -> github/feature/add_git_commands
CONFLICT (rename/rename): Rename "readhim.md"->"readme.md" in branch "HEAD" rename "readhim.md"->"readher.md" in "02b7f37dc33500923ca9212eed6207175bd46112"
Automatic merge failed; fix conflicts and then commit the result. ## 提示合并失败了

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands|MERGING)
$ ll
total 10
-rw-r--r-- 1 wei 197121 1087 Dec 29 15:53 LICENSE
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 images/
-rw-r--r-- 1 wei 197121 1516 Dec 30 14:30 index.html
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 js/
-rw-r--r-- 1 wei 197121  236 Dec 30 20:30 readher.md ## 发现两个文件
-rw-r--r-- 1 wei 197121  236 Dec 30 20:30 readme.md  ## 发现两个文件
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 styles/

$ git diff readme.md readher.md
* Unmerged path readher.md ##未合并
* Unmerged path readme.md

```



#### 解决冲突

```powershell
$ ll
total 10
-rw-r--r-- 1 wei 197121 1087 Dec 29 15:53 LICENSE
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 images/
-rw-r--r-- 1 wei 197121 1516 Dec 30 14:30 index.html
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 js/
-rw-r--r-- 1 wei 197121  236 Dec 30 20:30 readher.md ## 发现两个文件
-rw-r--r-- 1 wei 197121  236 Dec 30 20:30 readme.md  ## 发现两个文件
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 styles/

$ git status
On branch feature/add_git_commands
Your branch and 'github/feature/add_git_commands' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add/rm <file>..." as appropriate to mark resolution)
        added by them:   readher.md
        both deleted:    readhim.md
        added by us:     readme.md

no changes added to commit (use "git add" and/or "git commit -a")


```

##### 删除:git rm readhim.md

```powershell
$ git rm readhim.md
rm 'readhim.md'

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands|MERGING)
$ git status
On branch feature/add_git_commands
Your branch and 'github/feature/add_git_commands' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        added by them:   readher.md
        added by us:     readme.md

no changes added to commit (use "git add" and/or "git commit -a")

```



##### 删除:git rm readher.md

```powershell
$ git rm readher.md
rm 'readher.md'

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands|MERGING)
$ git status
On branch feature/add_git_commands
Your branch and 'github/feature/add_git_commands' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        added by us:     readme.md

```



##### 添加：git add readme.md

```powershell
$ git add readme.md

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands|MERGING)
$ git status
On branch feature/add_git_commands
Your branch and 'github/feature/add_git_commands' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

## 提示：冲突已经解决，但是还得commit下
All conflicts fixed but you are still merging. 
  (use "git commit" to conclude merge)

## 这时，冲突的文件只剩下 readme.md
$ ll
total 9
-rw-r--r-- 1 wei 197121 1087 Dec 29 15:53 LICENSE
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 images/
-rw-r--r-- 1 wei 197121 1516 Dec 30 14:30 index.html
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 js/
-rw-r--r-- 1 wei 197121  236 Dec 30 20:30 readme.md
drwxr-xr-x 1 wei 197121    0 Dec 29 15:46 styles/

```



##### commit：修复的文件冲突

```powershell
$ git commit -am 'Decide to mv readhim to readme'
[feature/add_git_commands 1cc4b32] Decide to mv readhim to readme

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)
$ git status
On branch feature/add_git_commands
Your branch is ahead of 'github/feature/add_git_commands' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean


```

<img src="玩转Git三剑客/images/1640869026227.png" alt="1640869026227" style="zoom:80%;" />



##### push 远程GitHub

```powershell
$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 421 bytes | 210.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:K-Artisan/git-leaning.git
   02b7f37..1cc4b32  feature/add_git_commands -> feature/add_git_commands

wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning (feature/add_git_commands)
$ gitk --all
```

<img src="玩转Git三剑客/images/1640869137564.png" alt="1640869137564" style="zoom:80%;" />



#### 账号2：pull

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)

$ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), 401 bytes | 4.00 KiB/s, done.
From github.com:K-Artisan/git-leaning
   02b7f37..1cc4b32  feature/add_git_commands -> origin/feature/add_git_commands
Updating 02b7f37..1cc4b32
Fast-forward
 readher.md => readme.md | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename readher.md => readme.md (100%)


$ ll
total 9
-rw-r--r-- 1 wei 197121 1087 Dec 30 13:41 LICENSE
drwxr-xr-x 1 wei 197121    0 Dec 30 13:57 images/
-rw-r--r-- 1 wei 197121 1516 Dec 30 18:52 index.html
drwxr-xr-x 1 wei 197121    0 Dec 30 13:57 js/
-rw-r--r-- 1 wei 197121  236 Dec 30 21:00 readme.md ##不在是readher.md
drwxr-xr-x 1 wei 197121    0 Dec 30 13:57 styles/

```



# 第五章 Git集成使用禁忌

## 39 禁止向集成分支执行 push -f 操作

强制 **git push -f**  ：强制push，不会报错！！！

```pow
git push -f
git push --force
```

### push -f 的危害

#### 账号2：git reset

```powershell
wei@DESKTOP-Q4DR7HN MINGW64 /e/Kzone/CodeLib/Git/Course/玩转Git三剑客/src/git_learning02 (feature/add_git_commands)

$ git branch -av
* feature/add_git_commands                1cc4b32 Decide to mv readhim to readme
  main                                    93bda36 Initial commit
  remotes/origin/HEAD                     -> origin/main
  remotes/origin/feature/add_git_commands 1cc4b32 Decide to mv readhim to readme
  remotes/origin/main                     93bda36 Initial commit
  remotes/origin/master                   9f13e73 Merge remote-tracking branch 'github/main'
  remotes/origin/temp                     8cd64a3 Add js

$ git log --oneline
1cc4b32 (HEAD -> feature/add_git_commands, origin/feature/add_git_commands) Decide to mv readhim to readme
99d9130 mv readhim.md to readme.md
02b7f37 mv readhim.md tp readher.md
d4f699c Merge branch 'feature/add_git_commands' of github.com:K-Artisan/git-leaning into feature/add_git_commands
fb15289 Add new context
99ebc54 Mv readme t- readhim
bcd3859 mergr readme and fix conflicts
4ebc982 Add fix readme Account02
a921462 Add readme fix01
e67e474 Merge remote-tracking branch 'github/feature/add_git_commands' into feature/add_git_commands
8f014ff Fix readme
75fba30 Add git add in index.html
42187d7 Add git commands descriptions in readme
9f13e73 (origin/master) Merge remote-tracking branch 'github/main'
93bda36 (origin/main, origin/HEAD, main) Initial commit
19cacff Add .gitignore
03f1da9 Bug:fix bug index.html
70aa453 3 files changed
70ef4a1 Add the first git command with config
bef58ea Create a complete web page
a9f44d2 add index + logo
7b07d4f Add readme.md

```

账号2重置HEAD到：commit：bef58ea Create a complete web page

<img src="玩转Git三剑客/images/1640870181543.png" alt="1640870181543" style="zoom:80%;" />

```powershell
$ git reset --hard bef58ea
HEAD is now at bef58ea Create a complete web page

$ git log --oneline
## 其余的日志全没了
bef58ea (HEAD -> feature/add_git_commands) Create a complete web page
a9f44d2 add index + logo
7b07d4f Add readme.md
```



#### 没有git push -f 前

GitHub：1cc4b32

![1640870596565](玩转Git三剑客/images/1640870596565.png)



#### git push -f 后

就在这时候，git push -f

```powershell
$ git push -f
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:K-Artisan/git-leaning.git
 + 1cc4b32...bef58ea feature/add_git_commands -> feature/add_git_commands (forced update)
## -f:强制push，不会报错！！！
```

<img src="玩转Git三剑客/images/1640870726239.png" alt="1640870726239" style="zoom:80%;" />

**所有历史变更都消失了！！！**



## 40 禁止向集成分支执行变更历史的操作

团队的集成分支禁止拉取到本地进行

```powershell
git rebase
```

操作来更改历史，因为团体里其他成员的本地还是旧的历史，

你修改了集成（公共）的变更历史，他们提交就会失败。



# 第六章

## 41 GitHub为什么这么火

###  Git诞生之前

<img src="玩转Git三剑客/images/1640871853052.png" alt="1640871853052" style="zoom: 80%;" />



### Git诞生之后

<img src="玩转Git三剑客/images/1640871998019.png" alt="1640871998019" style="zoom:50%;" />

Git的局限：无法共享代码



### GitHub诞生

<img src="玩转Git三剑客/images/1640872083959.png" alt="1640872083959" style="zoom:80%;" />![1640872249273](玩转Git三剑客/images/1640872249273.png)

### GitHub 成功的因素

<img src="玩转Git三剑客/images/1640872308181.png" alt="1640872308181" style="zoom:80%;" />



## 42 GitHub都有哪些核心功能

<img src="玩转Git三剑客/images/1640872663862.png" alt="1640872663862" style="zoom:50%;" />



### Feature

 [Features | GitHub · GitHub](https://github.com/features) 

代码存放，文档，项目管理、团队管理，集成工具

![1640873181549](玩转Git三剑客/images/1640873181549.png)



### 集成

不同于GitLab，是依靠第三方插件



### 团队管理

个人账号，可以为公司创建团队，以后离职的话，不用上交个人的账号



## 43 如何快速淘到感兴趣的开源项目



https://github.com/search

![1640874474237](玩转Git三剑客/images/1640874474237.png)

高级搜索：https://github.com/search/advanced





<img src="玩转Git三剑客/images/1640874208440.png" alt="1640874208440" style="zoom:50%;" />

create:<2018-12-31



### 一、单条件使用

1. **项目名称**

   仓库名称包含 spring 的项目

   *in:name spring*

2. **项目描述**

   仓库描述中包含 spring 的项目

   *in:description spring*

3. **readme文件**

   readme 中的描述包含 spring 的项目

   *in:readme spring*

4. **star数量**

   star 数量大于 1000 的项目

   *starts: >1000*

   star 数量在 10~20直接的项目

   *stars:10..20*

5. **fork 数量**

   fork 数量大于 1000 的项目

   *fork:>1000*

   fork 数量在 10~20 之间的项目

6. **仓库大小**

   按照仓库大小进行搜索，单位：KB，仓库大于1000kB的项目

   *size:>=1000*

7. **最近更新时间**

   最近一次提交在2019年以后的仓库

   *pushed:>2019-01-01 关键词*

8. **仓库创建时间**

   2019年以后创建的仓库

   *created:>2019-01-01 关键词*

9. **license**

   使用 apache-2.0 协议的仓库

   *license:apache-2.0 关键词*

10. **仓库使用的开发语言**

    用java 语言写的仓库

    *language:java 关键词*

11. **仓库的作者**

    用户google 上传的仓库

    *user:google 关键词*

12. **组织的仓库**

    列出org 的 spring-cloud 仓库

    *org:spring-cloud*

    

### 二、组合条件使用

**1. 搜索名字包含 spring boot ,并且 star 在 1000 以上的项目。**

*in:name spring boot stars:>1000*

**2. 搜索描述中包含 spring boot,并且 star 在1000以上，language 为 java 的项目。**

*in:description spring boot stars:>1000 language:java*

**3. 搜索 readme 中包含关键字【测试自动化框架】，并且 star 在 100 以上，language 是 python 的项目.**

*in:readme 测试自动化框架 stars:>100 language:python*



## 44 如何在GitHub上搭建个人博客

https://blog.csdn.net/u012168038/article/details/77715439

 Liquid语法:https://help.shopify.com/themes/liquid
Jekyll中文网:http://jekyll.com.cn/ 



在GitHub搜索：

```powershell
blog easily start in:readme start:>5000
```

<img src="玩转Git三剑客/images/1640876655022.png" alt="1640876655022" style="zoom:50%;" />

### GitHub Pages是什么？

Github Pages设计的初衷是为托管在GitHub上的项目提供介绍页面,开发者们可以通过GitHub Pages为他们的每一个项目创建一个用于介绍该项目的静态网站,不过由于他的空间免费而且稳定,因此用它搭建一个个人博客网站是再好不过了



### barryclark/jekll-now

https://github.com/barryclark/jekyll-now

jekyll是一个简单的免费的Blog生成工具,将纯文本转化为静态网站和博客;由于咱们的GitHub Pages生成的是静态页面,每次更新博客都需要手动更改HTML,这就使得每次写博客都变得很麻烦,而用了这个工具以后,它会根据预先设置好的格式来生成博客内容,你就无需关心html代码,只需要把重心放在博客的写作上.



 如果想深入学习的同学可以自行学习Jekyll以及Liquid 



### 实操：jekll-now 

#### Fork 项目

打开项目：https://github.com/barryclark/jekyll-now ，

![1640877679796](玩转Git三剑客/images/1640877679796.png)

然后 Fork 到自己的仓库

![1640877784137](玩转Git三剑客/images/1640877784137.png)



#### Settings

点击项目的 **Settings**

<img src="玩转Git三剑客/images/1640877875747.png" alt="1640877875747" style="zoom:80%;" />

修改 Repository Name ：

```powershell
成组织的名称或个人的user.name.github.io 
```

这种形式。这里我改成个人的user.name，即：

```powershell
k-artisan.github.io
```

<img src="玩转Git三剑客/images/1640878179935.png" alt="1640878179935" style="zoom:50%;" />

#### _config.yml

把 name 改了

<img src="玩转Git三剑客/images/1640878464136.png" alt="1640878464136" style="zoom:80%;" />

```yaml
name: K-Artisan Blog
```

点击<img src="玩转Git三剑客/images/1640878544993.png" alt="1640878544993" style="zoom:67%;" />

#### _posts

这个文件存放你要发布的文章，

<img src="玩转Git三剑客/images/1640878812488.png" alt="1640878812488" style="zoom:67%;" />

创建新的文章，文件名格式是：

```powershell
YYYY-MM-DD-文件名.md
例如：2021-12-30-My-First-Blog.md
```

以MarkDown的格式编写文章

![1640878999271](玩转Git三剑客/images/1640878999271.png)

点击【Commit new file】。



#### GitHub Pages

查看 GitHub Pages 已经设置好了

<img src="玩转Git三剑客/images/1640879243965.png" alt="1640879243965" style="zoom:50%;" />

GitHub Pages 地址就是： https://k-artisan.github.io/ 

<img src="玩转Git三剑客/images/1640879311783.png" alt="1640879311783" style="zoom:80%;" />

文章详情页：https://k-artisan.github.io/My-First-Blog/

![1640879488770](玩转Git三剑客/images/1640879488770.png)



## 45 开源项目怎么保证代码质量

Code review

 <img src="玩转Git三剑客/images/1640879925342.png" alt="1640879925342" style="zoom:50%;" />



<img src="玩转Git三剑客/images/1640880011104.png" alt="1640880011104" style="zoom: 67%;" />



<img src="玩转Git三剑客/images/1640880035370.png" alt="1640880035370" style="zoom:67%;" />



## 46 为何需要组织类型的仓库

点击头像 > my profile，查看个人加入的组织

<img src="玩转Git三剑客/images/1640880351031.png" alt="1640880351031" style="zoom:50%;" />

GitHub提供创建 基于组织（Organizations）的仓库

当一个项目你觉得不适合放在个人仓库，需要几个一起管理，那么就创建一个基于组织（Organizations）的仓库



### 创建基于组织（Organizations）的仓库

点【头像】> Settings > Organizations

<img src="玩转Git三剑客/images/1640880688530.png" alt="1640880688530" style="zoom:50%;" />

点击【New organization】按钮

<img src="玩转Git三剑客/images/1640880854286.png" alt="1640880854286" style="zoom:50%;" />

选择 Join Free

<img src="玩转Git三剑客/images/1640881181671.png" alt="1640881181671" style="zoom:50%;" />

添加组织成员Keasy5

<img src="玩转Git三剑客/images/1640881273657.png" alt="1640881273657" style="zoom:50%;" />

自己的话就不用加了，因为已经是该组织成员了



<img src="玩转Git三剑客/images/1640881339649.png" alt="1640881339649" style="zoom:50%;" />

点击【Complete setup】，要求输入密码：

<img src="玩转Git三剑客/images/1640881434471.png" alt="1640881434471" style="zoom: 33%;" />

会给被邀请的人Keasy5发送邀请邮件

You've invited 1 member. They'll receive their invitation email shortly.

 你邀请1成员。他们很快就会收到他们的邀请邮件。 



K-Artisan 创建完组织，还要填写一些调查资料

<img src="玩转Git三剑客/images/1640881618872.png" alt="1640881618872" style="zoom:50%;" />![1640881702916](玩转Git三剑客/images/1640881702916.png)

创建成功后

<img src="玩转Git三剑客/images/1640881743638.png" alt="1640881743638" style="zoom:80%;" />

### 组织仓库的功能

#### Repositories

仓库



#### Peoples

组织成员



#### Teams

小团队，更精细话的管理。

这里我们添加了两个Team，Dev（开发）和Test（测试），然后就可以往Team里面加Member（队员）

<img src="玩转Git三剑客/images/1640882093481.png" alt="1640882093481" style="zoom:80%;" />

可以以Team为单位，授予不同的权限

<img src="玩转Git三剑客/images/1640882258473.png" alt="1640882258473" style="zoom: 80%;" />



### 创建一个组织仓库

https://github.com/ArtisanGarden/FirstProject

<img src="玩转Git三剑客/images/1640883243448.png" alt="1640883243448" style="zoom:67%;" />



### 被邀请成员加入组织

Keasy5 登录GitHub 设置的邮箱，会见到邀请邮件

<img src="玩转Git三剑客/images/1640882521034.png" alt="1640882521034" style="zoom:67%;" />

成员Keasy5 点击登录Github

<img src="玩转Git三剑客/images/1640882773407.png" alt="1640882773407" style="zoom: 80%;" />

点击【Join ArtisanGarden】后成功加入组织【K-Artisan/ArtidanGarden】

<img src="玩转Git三剑客/images/1640882821888.png" alt="1640882821888" style="zoom:50%;" />





目前被邀请账号 ：Keasy5，虽然没有任何权限，但是他可以看到 Team等信息（其它代码管理工具就做不到这一点，新加入的组织的成员完成不知道Team的相关内容，看不到仓库的任何内容），

既然可以看到 Team， 组织的成员自己可以申请加入某个 Team，

下面是邀请账号 ：Keasy5 登录后所看到的界面：

<img src="玩转Git三剑客/images/1640883558514.png" alt="1640883558514" style="zoom: 67%;" />

发出申请后，管理 K-Artisan 收到 一个Request

<img src="玩转Git三剑客/images/1640884086621.png" alt="1640884086621" style="zoom:67%;" />

 Approve ：批准

Deny：拒绝

点击【Approve】按钮，让成员Keasy5加入【Dev】Team.

<img src="玩转Git三剑客/images/1640884195717.png" alt="1640884195717" style="zoom:67%;" />

成功加入后，Keasy5就立马获得该Team的权限



# 第七章 使用 GitHub 进行团队协作

## 47 创建团队的项目

###  创建团队仓库

<img src="玩转Git三剑客/images/1640929393328.png" alt="1640929393328" style="zoom:50%;" />

https://github.com/ArtisanGarden/app01

<img src="玩转Git三剑客/images/1640929664809.png" alt="1640929664809" style="zoom:50%;" />



### 仓库权限

点击仓库的【Settings】，选择【Manage access】

<img src="玩转Git三剑客/images/1640930019577.png" alt="1640930019577" style="zoom:50%;" />

把人员和Tearm加入，

这里加入Dev Tearm ，并授予【Admin】权限

<img src="玩转Git三剑客/images/1640930138814.png" alt="1640930138814" style="zoom:33%;" />

<img src="玩转Git三剑客/images/1640930175977.png" alt="1640930175977" style="zoom:50%;" />



## 48 怎么选择合适自己团队的工作流

管理团队的工作流程，需要考虑的因素：

- 团队人员的组成
- 研发设计能力
- 输出产品的特征
- 项目难易程度





#### 主干开发

<img src="玩转Git三剑客/images/1640930735326.png" alt="1640930735326" style="zoom:50%;" />



#### Git Flow

<img src="玩转Git三剑客/images/1640930910262.png" alt="1640930910262" style="zoom:67%;" />



特性分支，然后合并



#### GitHub Flow

<img src="玩转Git三剑客/images/1640930997744.png" alt="1640930997744" style="zoom:80%;" />做到随时发布的状态



#### GitLab Flow (带生成分支)

<img src="玩转Git三剑客/images/1640931129541.png" alt="1640931129541" style="zoom:67%;" />



#### GitLab Flow (带环境分支)

<img src="玩转Git三剑客/images/1640931201068.png" alt="1640931201068" style="zoom:67%;" />



#### GitLab Flow （带发布分支）

<img src="玩转Git三剑客/images/1640931282522.png" alt="1640931282522" style="zoom:50%;" />



## 49  如何挑选合适的分支集成策略

<img src="玩转Git三剑客/images/1640933262023.png" alt="1640933262023" style="zoom:50%;" />



### Network

点击仓库的**Insights** ，选择菜单 **Network**

展示整个版本树的演进

<img src="玩转Git三剑客/images/1640933394213.png" alt="1640933394213" style="zoom:67%;" />



  两个特性分支b【Beijing】、S【Shanghai】最终合并到主分支【master】上



### Merge button

入口：【Settings > Merge button】

<img src="玩转Git三剑客/images/1640933681932.png" alt="1640933681932" style="zoom:50%;" />

#### 

如果团队的版本是一条线性的版本，一般选择【Allow rebase merging】

也就是说，从主干master上拉取一个分支（Feat分支），开发完之后，合并是基于主干目前最新commit点进行。这样所有团队的分支（Feat分支）合并进去后，主干master包含所有的（Feat分支），这样所有Feat分支甚至可以删除掉。



假设目前有一个项目的分支情况如下：

```powershell
--------1------------------------m:c1---------------------- master主干分支
        |---A:c1--A:c2--A:c3:featA分支
```



#### Allow merge commits

```powershell
--------1------------------------m:c1-------merge:c2--------------- master主干分支
        |---A:c1--A:c2--A:c3:featA分支-------|
```

featA分支的3个commit 合并到master主干分支上的一个commit（merge:c2）上，

这时，出现删除 featA分支的按钮，可以选择某个合适的时间节点，删除featA分支分支。

注意：**此时 featA分支的HEAD指向merge:c2 这个commit**

**master分支有两个父亲**



#### Allow squash merging

```powershell
--------1------------------------m:c1------------merge(A:c1-c3)---------- master主干分支
        |---A:c1---A:c2--A:c3:featA分支
```

把featA分支上的3个commit，合并成一个commit然后合并到 master主干分支上。

**此时 featA分支没有被改动**

**master分支有一个父亲**



#### Allow rebase merging

```powershell
--------1------------------------m:c1------------A:c1---A:c2--A:c3---------- master主干分支
        |---A:c1---A:c2--A:c3:featA分支
```

把featA分支上的3个commit，依次加到master主干分支上，



### Pull requests

创建一个 Pull request ,然后进行代码合并，

合并（Merge）的合并按钮有三种，见上节。





## 50 启用 issue 跟踪需求和任务

默认 issue 功能是打开的，可以使用 issue 提需求任务，提bug，创建一个 issue也相应根据 issue的类型，

提供了issue的模板，打开【Settings > Options > issue】

https://github.com/K-Artisan/git-leaning/settings

<img src="玩转Git三剑客/images/1640942909313.png" alt="1640942909313" style="zoom:67%;" />

预设了3个issue模板

<img src="玩转Git三剑客/images/1640942945449.png" alt="1640942945449" style="zoom:50%;" />



更新一个issue模板，然后提交，仓库下自动生成一个.github 文件夹中，里面有更新后的Issue模板

![1640943270240](玩转Git三剑客/images/1640943270240.png)



## 51 如何用Project管理 Issue

项目的看板

<img src="玩转Git三剑客/images/1640943536263.png" alt="1640943536263" style="zoom:80%;" />

<img src="玩转Git三剑客/images/1640943855009.png" alt="1640943855009" style="zoom:50%;" />



创建一个 Project

<img src="玩转Git三剑客/images/1640943663310.png" alt="1640943663310" style="zoom:33%;" />



## 52 项目内部怎么实施 code review

项目中，做 codereview ，不允许不合格的代码push



打开一个仓库，Settings > Branches

<img src="玩转Git三剑客/images/1640944186131.png" alt="1640944186131" style="zoom:67%;" />

<img src="玩转Git三剑客/images/1640944324195.png" alt="1640944324195" style="zoom:50%;" />



有了rule之后，任何人员提交代码，都得 New pull request，

![1640944444566](玩转Git三剑客/images/1640944444566.png)



![1640944501632](玩转Git三剑客/images/1640944501632.png)

![1640944533362](玩转Git三剑客/images/1640944533362.png)



![1640944556714](玩转Git三剑客/images/1640944556714.png)





<img src="玩转Git三剑客/images/1640944603110.png" alt="1640944603110" style="zoom:50%;" />

审核人员 可以点击 colse 关闭 

![1640944742116](玩转Git三剑客/images/1640944742116.png)





## 53 团队协作时如何做多分支的集成

#### 原始状态

<img src="玩转Git三剑客/images/1640945063487.png" alt="1640945063487" style="zoom:67%;" />

<img src="玩转Git三剑客/images/1640945128894.png" alt="1640945128894" style="zoom:50%;" />

#### merge commits

##### 把Beijing分支集成

把Beijing 分支合并到 master分支

<img src="玩转Git三剑客/images/1640945239018.png" alt="1640945239018" style="zoom:50%;" />

**选择【Create a merge commit】合并方式**

<img src="玩转Git三剑客/images/1640945289441.png" alt="1640945289441" style="zoom:50%;" />

<img src="玩转Git三剑客/images/1640945324882.png" alt="1640945324882" style="zoom:80%;" />







**Beijing分支发生了改变**

**master 分支有两个父亲**



##### 把Shanghai分支集成



<img src="玩转Git三剑客/images/1640945439091.png" alt="1640945439091" style="zoom:50%;" />

![1640945549711](玩转Git三剑客/images/1640945549711.png)



分支Shanghai后Mege到mastr分支，显然这时会发生冲突，点击【Resolve conflicts】可以进行在线解决冲突

<img src="玩转Git三剑客/images/1640945612008.png" alt="1640945612008" style="zoom:50%;" />



两个分支都 保留代码，点击【Marks as resolved】.

<img src="玩转Git三剑客/images/1640945710008.png" alt="1640945710008" style="zoom:67%;" />

再点击【Commit merge】生成一个解决冲突的commit

<img src="玩转Git三剑客/images/1640945795821.png" alt="1640945795821" style="zoom:67%;" />

<img src="玩转Git三剑客/images/1640945867700.png" alt="1640945867700" style="zoom:50%;" />



<img src="玩转Git三剑客/images/1640946021076.png" alt="1640946021076" style="zoom:50%;" />

这时只是产生了一个 merger commit，Shanghai分支还没合并到 master分支上，

所以回到之前的 pull request(#40)，

![1640946205034](玩转Git三剑客/images/1640946205034.png)

把这个解决了冲突的 commit Merge 到master分支上

<img src="玩转Git三剑客/images/1640946274468.png" alt="1640946274468" style="zoom:50%;" />

##### 最终结构

<img src="玩转Git三剑客/images/1640946376022.png" alt="1640946376022" style="zoom:50%;" />

**Beijing和Shanghai分支发生了改变**

**master 分支有两个父亲**



<img src="玩转Git三剑客/images/1640946343842.png" alt="1640946343842" style="zoom:67%;" />







#### squash merging



##### 还要原始状态

回退分支，**还要到原始状态**，以便做对比各个集成策略的不同之处。

 在本地的分支强制 push -f，还原分支状态

<img src="玩转Git三剑客/images/1640946750089.png" alt="1640946750089" style="zoom:50%;" />



<img src="玩转Git三剑客/images/1640946810742.png" alt="1640946810742" style="zoom:50%;" />



<img src="玩转Git三剑客/images/1640946839977.png" alt="1640946839977" style="zoom:67%;" />

<img src="玩转Git三剑客/images/1640946879236.png" alt="1640946879236" style="zoom:67%;" />

##### 把Beijing分支集成

![1640946929697](玩转Git三剑客/images/1640946929697.png)









<img src="玩转Git三剑客/images/1640947021257.png" alt="1640947021257" style="zoom:50%;" />



**选择 【Squash and merge】**

![1640947190405](玩转Git三剑客/images/1640947190405.png)



点就【Squash and merge】> 【Merge】

<img src="玩转Git三剑客/images/1640947355624.png" alt="1640947355624" style="zoom: 67%;" />



<img src="玩转Git三剑客/images/1640947470425.png" alt="1640947470425" style="zoom:67%;" />



<img src="玩转Git三剑客/images/1640947421041.png" alt="1640947421041" style="zoom: 80%;" />

<img src="玩转Git三剑客/images/1640947514418.png" alt="1640947514418" style="zoom:50%;" />

把 Beijing 的3个commit 合并生成一个新的 commit，合并到 master分支

**不会去改动 Beijing分支**



#####  把Shanghai分支集成

<img src="玩转Git三剑客/images/1640947688711.png" alt="1640947688711" style="zoom:80%;" />



有冲突，解决冲突跟上一节相同，都保留两个子分支的内容

<img src="玩转Git三剑客/images/1640948086783.png" alt="1640948086783" style="zoom:80%;" />



<img src="玩转Git三剑客/images/1640948110817.png" alt="1640948110817" style="zoom:67%;" />

<img src="玩转Git三剑客/images/1640948140669.png" alt="1640948140669" style="zoom:50%;" />



回到 pull request（#41），冲突已经解决，就可以 把Shanghai分支 merge 到 master 分支上了

<img src="玩转Git三剑客/images/1640948259383.png" alt="1640948259383" style="zoom:50%;" />![1640948292004](玩转Git三剑客/images/1640948292004.png)



<img src="玩转Git三剑客/images/1640948314566.png" alt="1640948314566" style="zoom:50%;" />



<img src="玩转Git三剑客/images/1640948367701.png" alt="1640948367701" style="zoom:50%;" />



##### 最终结构

![1640949501183](玩转Git三剑客/images/1640949501183.png)

<img src="玩转Git三剑客/images/1640948693035.png" alt="1640948693035" style="zoom:50%;" />



**Beijing  和 Shanghai 分支都没指向 marster**

Shanghai分支指向 Merge 冲突后的 commit。

**master 最终的父亲只有一个**，即：Beijing（#41），见下图所示：

<img src="玩转Git三剑客/images/1640949560630.png" alt="1640949560630" style="zoom:80%;" />



#### rebase merging

##### 还要原始状态

回退分支，**还要到原始状态**，以便做对比各个集成策略的不同之处。

 在本地的分支强制 push -f，还原分支状态

<img src="玩转Git三剑客/images/1640946750089.png" alt="1640946750089" style="zoom:50%;" />



<img src="玩转Git三剑客/images/1640946810742.png" alt="1640946810742" style="zoom: 80%;" />



<img src="玩转Git三剑客/images/1640946839977.png" alt="1640946839977" style="zoom:67%;" />



##### 把Beijing分支集成

同上，New pll request

<img src="玩转Git三剑客/images/1640949974397.png" alt="1640949974397" style="zoom:50%;" />



选择【Rebase an merge】

<img src="玩转Git三剑客/images/1640950018523.png" alt="1640950018523" style="zoom: 67%;" />



原始状态：

<img src="玩转Git三剑客/images/1640950148460.png" alt="1640950148460" style="zoom: 80%;" />

Merge 到master 分支后，Beijing分支的3个commit 依次 加到 master分支上，如下图所示：

<img src="玩转Git三剑客/images/1640950324068.png" alt="1640950324068" style="zoom: 67%;" />



##### Shanghai分支集成

###### Rebase an Merge 失败

操作同上，New pull request，

<img src="玩转Git三剑客/images/1640950757624.png" alt="1640950757624" style="zoom:50%;" />

解决冲突，

<img src="玩转Git三剑客/images/1640950503231.png" alt="1640950503231" style="zoom:50%;" />



Merge出一个新的commit，

<img src="玩转Git三剑客/images/1640950640037.png" alt="1640950640037" style="zoom: 80%;" />



回到 刚才新建的 pull request （#44）

<img src="玩转Git三剑客/images/1640950955232.png" alt="1640950955232" style="zoom:50%;" />



看上图，**不能进行 rebase ！！！**，这时的结构为：

<img src="玩转Git三剑客/images/1640951369796.png" alt="1640951369796" style="zoom:80%;" />

GitHub 不能处理了。得自己人工找方法了。

###### 解决方法

把 Shanghai 分支回退到 s 点所在的commit ，在本地执行如下命令

<img src="玩转Git三剑客/images/1640946839977.png" alt="1640946839977" style="zoom:67%;" />

即：

![1640951607396](玩转Git三剑客/images/1640951607396.png)

<img src="玩转Git三剑客/images/1640951630694.png" alt="1640951630694" style="zoom:67%;" />



基本思路是，在本地基于 marster 分支进行rebase，在push到远程Github。

所有在本地，把 marster 拉取到本地：

`<img src="玩转Git三剑客/images/1640951810575.png" alt="1640951810575" style="zoom:50%;" />

<img src="玩转Git三剑客/images/1640951852852.png" alt="1640951852852" style="zoom: 80%;" />

<img src="玩转Git三剑客/images/1640951962601.png" alt="1640951962601" style="zoom:50%;" />

解决冲突：

![1640952008081](玩转Git三剑客/images/1640952008081.png)

修改为：

![1640952047862](玩转Git三剑客/images/1640952047862.png)

<img src="玩转Git三剑客/images/1640952241765.png" alt="1640952241765" style="zoom:80%;" />





还是 同一个文件 readme 文件发生冲突，解决冲突同上。

直到 status是 clean(干净的)为止。

> 是否有办法不用多次解决反复同一个冲突，见下节【多次解决反复同一个冲突】

<img src="玩转Git三剑客/images/1640952422423.png" alt="1640952422423" style="zoom:80%;" />

<img src="玩转Git三剑客/images/1640952634179.png" alt="1640952634179" style="zoom:67%;" />

把本地的master往远程的GitHub 推送Push

<img src="玩转Git三剑客/images/1640952830957.png" alt="1640952830957" style="zoom:80%;" />

然后由

<img src="玩转Git三剑客/images/1640951630694.png" alt="1640951630694" style="zoom:67%;" />

变成了

<img src="玩转Git三剑客/images/1640956605497.png" alt="1640956605497" style="zoom:80%;" />



这时，pull request（#44）就可以 Rebase And merge 了，见下图：

<img src="玩转Git三剑客/images/1640955274862.png" alt="1640955274862" style="zoom:80%;" />

![1640955376969](玩转Git三剑客/images/1640955376969.png)

<img src="玩转Git三剑客/images/1640955402427.png" alt="1640955402427" style="zoom:50%;" />

<img src="玩转Git三剑客/images/1640955433922.png" alt="1640955433922" style="zoom:50%;" />

<img src="玩转Git三剑客/images/1640955458434.png" alt="1640955458434" style="zoom:80%;" />

###### 

Merge成功后的分支结构：

由

<img src="玩转Git三剑客/images/1640956605497.png" alt="1640956605497" style="zoom:80%;" />

变成了

<img src="玩转Git三剑客/images/1640955717696.png" alt="1640955717696" style="zoom:80%;" />

重新生成了4个新的commit并依次添加（Picke）到 master分支。

为什么还要生成4个新的commit？

如果 master指直接指向Shanghai的最后一个commit，如下图：

<img src="玩转Git三剑客/images/1640956116728.png" alt="1640956116728" style="zoom:80%;" />

这样会把谁接受 push合并的记录高没了

并且

<img src="玩转Git三剑客/images/1640956324009.png" alt="1640956324009" style="zoom:80%;" />

还为了在master分支中加入【接受合并的是账号2】这个信息，而**不丢失Shanghai·分支的代码贡献者是账号1**这个信息。

<img src="玩转Git三剑客/images/1640956891133.png" alt="1640956891133" style="zoom:80%;" />



##### 多次解决反复同一个冲突：git-rerere

 [Git - git-rerere Documentation (git-scm.com)](https://git-scm.com/docs/git-rerere) 

在上一节中，在 git rebase 的时候，得反复的解决同一个文件相同的冲突。

还原本地 **Shanghai**分支到 **remote/origin**

![1640957725507](玩转Git三剑客/images/1640957725507.png)

还原 本地 master 到 原始状态

![1640957934165](玩转Git三剑客/images/1640957934165.png)

然后是git-rerere 生效

![1640957982551](玩转Git三剑客/images/1640957982551.png)

<img src="玩转Git三剑客/images/1640958195190.png" alt="1640958195190" style="zoom:80%;" />

vi readme 文件解决冲突



不看了，马德



## 54 如何保证集成的质量

<img src="玩转Git三剑客/images/1640960038271.png" alt="1640960038271" style="zoom:80%;" />

<img src="玩转Git三剑客/images/1640960076826.png" alt="1640960076826" style="zoom:67%;" />

这些服务区哪里找，到 GitHub的 **Marketplace** 上找

https://github.com/marketplace

![1640960222217](玩转Git三剑客/images/1640960222217.png)



## 55 如何把产品包发布到GitHub上

<img src="玩转Git三剑客/images/1640962118380.png" alt="1640962118380" />

<img src="玩转Git三剑客/images/1640962118380.png" alt="1640962118380" style="zoom:50%;" />





## 56 如何给项目增加详细的指导文档

Wiki

<img src="玩转Git三剑客/images/1640962457820.png" alt="1640962457820" style="zoom:67%;" />



# 第八章 GitLab 实践

[Git，GitHub与GitLab有什么区别](https://zhuanlan.zhihu.com/p/124085062)

 [GitLab官网](https://link.zhihu.com/?target=https%3A//gitlab.com/users/sign_in) 

https://gitee.com



## 57 国内互联网企业为什么喜欢GitLab

公司可以自己搭建代码平台



