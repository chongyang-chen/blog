---
title: git学习笔记
tags:
  - git学习笔记
  - git
categories:
  - git学习笔记
date: 2016-09-25 19:02:39
---
[《git小书》图灵社区](https://www.ituring.com.cn/book/1870)
<!-- more -->

# 介绍
## 安装git
macOS下安装了Xcode,默认是安装了git的。查看git版本：

```
$ git --version
git version 2.24.0
```


如果没有安装git，可以使用下面的命令来安装：

```
$ brew install git
Updating Homebrew...
Warning: git 2.24.0_2 is already installed and up-to-date
To reinstall 2.24.0_2, run `brew reinstall git`
```
我的电脑已经安装了git，所以会显示上面的结果。如果安装过程遇到问题，可以百度查找解决方案，总之电脑要成功安装git，才能开始学习git。



## 配置用户名和邮件

```
git config --global user.name 'cc'
git config --global user.email 'example@xxx.com'
```

## 创建和修改文件

程序员通常使用集成开发工具来创建和修改文件，比如Xcode。这里学习使用终端命令来创建和修改文件。常用echo和sed命令。

### 创建文件

新建一个gitabc的文件夹，在该文件夹里进行git的学习。

```
$ echo Line1 > file
$ echo Line2 >> file
$ echo Line3 >> file
```
上面的代码向file文件写入了三行数据。

file文件：

```
Line1
Line2
Line3
```

### 修改文件
sed可以修改文件，
```
$ sed 's/Line1/LineI/g' file
```
修改后的结果：

```
LineI
Line2
Line3
```
关于echo和sed命名只学习了上面这些内容，以后再具体学习相关知识。接下来开始git的正式学习。

## 创建仓库

在gitabc目录下执行下面命名：

```
$ git init repo
Initialized empty Git repository in /Users/ccyag/gitabc/repo/.git/
```
上面的命令创建了一个.git的隐藏文件。隐藏文件不需要我们关心，git会帮我们处理的。我们只需要创建，修改和删除自己的文件即可。

## 创建文件

```
$ echo line1 > file
```
这里创建了一个file文件，并写入一行数据。使用git status -s
查询git仓库状态。

```
$ git status -s
?? file
```
??表示未跟踪状态，后面是文件名称。

## 跟踪新文件，提交修改

`git add `命令把新文件加入跟踪：

```
$ git add file 
$ git status -s
A  file
```
A 表示状态为已添加，file被加入跟踪。

`git commit` 提交：

```
$ git commit -m "add file"
[master (root-commit) 9326bf0] add file
 1 file changed, 1 insertion(+)
 create mode 100644 file

```
至此完成了新建文件，跟踪文件和提交修改等操作，将文件修改一下，然后暂存并提交。

```
$ echo line2 >> file 
$ git add file 
$ git commit -m "add line2"
```
这一次的git add 与第一次git add 完成的工作并不一样。第一次是把未跟踪的文件加入暂存区，第二次是把修改后的文件加入暂存区。commit命令是把暂存区的文件提交到仓库。总结下来就是创建或者修改文件，加入暂存区，提交到仓库。使用到的命名为：git add， git commit。最后再做一次修改，并提交。

```
$ echo line3 >> file 
$ git add file 
$ git commit -m "add line3"
```
我们一共做了3次commit操作。

## 查看仓库修订

```
$ git log 
commit 01e226420d287c0976063d76fb2346c62a0fb970 (HEAD -> master)
Author: chen chongyang <22377832@qq.com>
Date:   Mon Nov 25 20:26:01 2019 +0800

    add line3

commit 8969434aed2774daa5654b5e7c7e61fa71b767d9
Author: chen chongyang <22377832@qq.com>
Date:   Mon Nov 25 20:18:54 2019 +0800

    add line2

commit 9326bf0877097f70079de0ffa2194a27f259fd4c
Author: chen chongyang <22377832@qq.com>
Date:   Mon Nov 25 20:14:33 2019 +0800

    add file
```
我们可以看到是谁在什么时间做了什么具体的操作。只查看最新的一次提交。

```
$ git log head -1
commit 01e226420d287c0976063d76fb2346c62a0fb970 (HEAD -> master)
Author: chen chongyang <22377832@qq.com>
Date:   Mon Nov 25 20:26:01 2019 +0800

    add line3
```
其中，第一个参数是head，第二个参数-N，N可以使任意正整数。
结果的第一行是一个40位的字符串的标识符，第二行是用户名和邮件地址，这和前面的设置是一样的，下一行是提交的时间，最后是提交时输入的表述信息。所以提交时最好写出都做了哪些修改，让人一目了然。

head~N表示从最近提交开始倒数第N个提交，例如：

```
$ git show head~1 --quiet
commit 8969434aed2774daa5654b5e7c7e61fa71b767d9
Author: chen chongyang <22377832@qq.com>
Date:   Mon Nov 25 20:18:54 2019 +0800

    add line2
$ git show head~2 --quiet
commit 9326bf0877097f70079de0ffa2194a27f259fd4c
Author: chen chongyang <22377832@qq.com>
Date:   Mon Nov 25 20:14:33 2019 +0800

    add file
```
`git show `可以显示一个指定修订的详细情况，如果使用参数就会显示和前一个修订之间的差异。

```
$ git show head
commit 01e226420d287c0976063d76fb2346c62a0fb970 (HEAD -> master)
Author: chen chongyang <22377832@qq.com>
Date:   Mon Nov 25 20:26:01 2019 +0800

    add line3

diff --git a/file b/file
index c0d0fb4..83db48f 100644
--- a/file
+++ b/file
@@ -1,2 +1,3 @@
 line1
 line2
+line3
```
结果有点看不懂，不过不影响继续学习。以后再来看这个结果吧。😂

使用参数`--pretty=oneline`只显示一行信息：

```
$ git log --pretty=oneline
01e226420d287c0976063d76fb2346c62a0fb970 (HEAD -> master) add line3
8969434aed2774daa5654b5e7c7e61fa71b767d9 add line2
9326bf0877097f70079de0ffa2194a27f259fd4c add file
```

## 查看差异
`git diff` 查看文件的差异。

```
$ git diff head~1 head file 
diff --git a/file b/file
index c0d0fb4..83db48f 100644
--- a/file
+++ b/file
@@ -1,2 +1,3 @@
 line1
 line2
+line3
```

## 缩写的修订标识符
`--abbrev-commit` 表示缩写commit的标识符。

```
$ git log --abbrev-commit --pretty=one
01e2264 (HEAD -> master) add line3
8969434 add line2
9326bf0 add file

```
`--oneline`可以实现同样的效果：

```
$ git log --oneline
01e2264 (HEAD -> master) add line3
8969434 add line2
9326bf0 add file
```

## 更简短的log
`--pretty=format:'%s'` 只输出提交消息，前提是提交消息要有意义才行。

```
$ git log --pretty=format:'%s'
add line3
add line2
add file
```

## 命令缩写
创建hist与mist命令缩写

```
$ git config --global alias.hist 'log --pretty=format:"%h %ad |%s%d [%an]" --graph --date=short'
$ git config --global alias.mist 'log --pretty=format:"%s"'
```
查看创建的缩写

```
$ git config --global -l
user.name=chen chongyang
user.email=22377832@qq.com
core.excludesfile=~/.gitignore_global
alias.hist=log --pretty=format:"%h %ad |%s%d [%an]" --graph --date=short
alias.mist=log --pretty=format:"%s"
```
使用上面的命令查看修订信息

```
$ git hist -2
* 01e2264 2019-11-25 |add line3 (HEAD -> master) [chen chongyang]
* 8969434 2019-11-25 |add line2 [chen chongyang]
$ git mist -2
add line3
add line2
```
使用命令缩写可以将一些复杂的难写的git命令，设置成简短的命令。类似于字符替换。

# 暂存区
通过上面的学习，我们知道了要先加入暂存区，再提交至仓库的过程。接下来就来学习一下为什么需要暂存区。

首先要明白一个原则，一次提交尽量包含且只包含一个功能或者一个bug的修正。这样做的好处是不言而喻的。
使用git add将修改加入暂存区，使用git reset从暂存区移除。一个文件往往既有bug的修正，又有新的功能。那就需要用到分批提交。

## Hunk拆分

一个文件的有多个修改的地方，可以拆分后分别暂存，举个例子：
创建新文件并输入:

```
line1
line2
line3
line4
```
完成提交，修改文件为：

```
lineI
line2
line3
lineIIII
```
修改了文件的第一行和第四行。
使用`git add -p`命令将产生下面的结果：

```
git add -p
diff --git a/file b/file
index 84275f9..e375759 100644
--- a/file
+++ b/file
@@ -1,4 +1,4 @@
-line1
+lineI
 line2
 line3
-line4
+lineIIII
(1/1) Stage this hunk [y,n,q,a,d,s,e,?]? 
```
依次输入s,g,1,y,q命令：

```
(1/1) Stage this hunk [y,n,q,a,d,s,e,?]? s
Split into 2 hunks.
@@ -1,3 +1,3 @@
-line1
+lineI
 line2
 line3
(1/2) Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]? g
  1:  -1,3 +1,3          -line1
  2:  -2,3 +2,3          -line4
go to which hunk? 1
@@ -1,3 +1,3 @@
-line1
+lineI
 line2
 line3
(1/2) Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]? y
@@ -2,3 +2,3 @@
 line2
 line3
-line4
+lineIIII
(2/2) Stage this hunk [y,n,q,a,d,K,g,/,e,?]? q
```
查看状态：

```
$ git status -s
MM file
```
提交暂存区：

```
$ git commit -m "feature A" 
```
再次添加修改,输入y命令：

```
$ git add -p
diff --git a/file b/file
index 9080e8c..e375759 100644
--- a/file
+++ b/file
@@ -1,4 +1,4 @@
 lineI
 line2
 line3
-line4
+lineIIII
(1/1) Stage this hunk [y,n,q,a,d,e,?]? y
```
提交暂存区：

```
$ git commit -m "bug fix"
```
使用之前的简洁命令查看历史：

```
$ git mist -3
bug fix
feature A
init
```
学习了将一个文件的不同修改点通过交互模式切分成两次修改，并分别暂存和提交。这是目前为止学习的最麻烦的git命令了，对于每一个字母的命令也不是特别了解，还有很多要学习的地方😔。

## 对git add 的理解
git暂存的是修改而不是文件。

## 简化提交步骤
对于已经跟踪的文件可以使用 `git commit -am` 一起完成暂存和提交。

# 撤销
git可以撤销之前的操作，犯错是人之常情，git可以撤销这些错误，回到之前的状态。

## 撤销工作区文件修改
这里新建一个仓库进行学习，

```
$ git init p1 && cd p1
```
创建三个文件并提交到仓库。

```
$ echo line1 > file1
$ echo line1 > file2
$ echo line1 > file3
$ git status -s
?? file1
?? file2
?? file3
$ git add .
$ git status -s
A  file1
A  file2
A  file3
$ git commit -m "init"
```
上面的代码用到了之前学习的git命令。修改三个文件的内容。

```
$ echo line2 >> file1 
$ echo line2 >> file2
$ echo line2 >> file3
$ git status -s
 M file1
 M file2
 M file3

```
三个文件都显示为修改状态，撤销对file1的修改可以用下面的命令：

```
$ git checkout -- file1
$ git status -s
 M file2
 M file3
$ cat file1 
line1
```
可以看到只有两个文件被修改了，file1还是之前的内容。`git checkout -- `后接文件名称，可以撤销对文件的修改。

## 将文件从暂存区移出

```
$ git rm --cached flie1 
rm 'flie1'
$ git status -s
A  flie2
A  flie3
?? flie1
```
取消`--cached`参数,将产生一个错误，-f将会强制删除文件。

```
$ git status -s
A  flie1
A  flie2
A  flie3
$ git rm flie1
error: the following file has changes staged in the index:
    flie1
(use --cached to keep the file, or -f to force removal)
$ git rm -f flie1
rm 'flie1'
$ ls
flie2	flie3
$ git status -s
A  flie2
A  flie3

```
可以看到使用-f参数，将文件移出暂存区并删除了文件。移除暂存区所有的文件,需要添加 -r参数：

```
$ git rm --cached .
fatal: not removing '.' recursively without -r
$ git rm --cached -r .
rm 'flie2'
rm 'flie3'
$ git status -s
?? flie2
?? flie3
```
## 撤销提交

使用前面的git知识，新建一个仓库并做4次修改和提交：

```
$ git hist 
* 1beb06e 2019-11-26 |r4 (HEAD -> master) [chen chongyang]
* bfeeff3 2019-11-26 |r3 [chen chongyang]
* 50def6a 2019-11-26 |r2 [chen chongyang]
* 37421be 2019-11-26 |r1 [chen chongyang]
```
`git reset`命令会把历史撤销到指定的修订处：

```
$ git reset head~1
Unstaged changes after reset:
M	file1
$ git status -s
 M file1
$ git hist
* bfeeff3 2019-11-26 |r3 (HEAD -> master) [chen chongyang]
* 50def6a 2019-11-26 |r2 [chen chongyang]
* 37421be 2019-11-26 |r1 [chen chongyang]
```
撤销后file1文件处于修改状态，可以加入暂存区或者撤销修改。

## 恢复撤销
`git reflog `列出全部操作：

```
$ git reflog
bfeeff3 (HEAD -> master) HEAD@{0}: reset: moving to head~1
1beb06e HEAD@{1}: commit: r4
bfeeff3 (HEAD -> master) HEAD@{2}: commit: r3
50def6a HEAD@{3}: commit: r2
37421be HEAD@{4}: commit (initial): r1
```
找到要恢复的标识符,使用`git reset `命令：

```
$ git reset 1beb06e
$ git hist
* 1beb06e 2019-11-26 |r4 (HEAD -> master) [chen chongyang]
* bfeeff3 2019-11-26 |r3 [chen chongyang]
* 50def6a 2019-11-26 |r2 [chen chongyang]
* 37421be 2019-11-26 |r1 [chen chongyang]
```
再次回到了之前的位置。

## `--hard` 
使用`--hard`参数撤销提交：

```
$ git reset --hard head~1
HEAD is now at bfeeff3 r3
```
回退到上一个修订处，同时撤销了所有的修改。git reset 只是回退到指定的修订处，保留了修改的内容。通常使用--hard的情况会多一点。

## 撤销提交的部分文件
首先取消整个提交，然后添加需要提交的文件到暂存区，最后提交。
整个过程相当于只撤销了提交的file2文件。
```
$ git reset head~
Unstaged changes after reset:
M	file1
M	file2
$ git add file1 
$ git cimmit -m "r3"
$ git status -s
 M file2
```

#分支
分支就像影分身一样。可以复制出多个本体去做不同的事情，当分身消失的时候，本体知道在分身都做了哪些事情。接下来要学习分支的创建，合并与删除等操作。
## 创建分支

准备工作：

```
$ git init p1 && cd p1
$ echo line1 > file1
$ echo line2 >> file1
$ echo line3 >> file1
$ git add file1 
$ git commit -m "init"
```
查看分支：

```
$ git branch
* master
```
创建并切换到新分支：

```
$ git checkout -b ccy
Switched to a new branch 'ccy'
$ git branch
* ccy
  master
```
在分支上多次修改并提交代码：

```
$ sed -i '' 's/line1/lineI/g' file1 
$ git commit -m "r1" -a
$ sed -i '' 's/line2/lineII/g' file1 
$ git commit -m "r2" -a
$ sed -i '' 's/line3/lineIII/g' file1 
$ git commit -m "r3" -a
$ git hist
* 381cb66 2019-11-26 |r3 (HEAD -> ccy) [chen chongyang]
* 4f2f06b 2019-11-26 |r2 [chen chongyang]
* bb7ccd6 2019-11-26 |r1 [chen chongyang]
* e1c48dd 2019-11-26 |init (master) [chen chongyang]
```

## 切换分支

```
$ git checkout master
Switched to branch 'master'
$ cat file1 
line1
line2
line3
```

master 分支内容并没有改变，现在来合并分支。

```
$ git merge ccy
Updating e1c48dd..381cb66
Fast-forward
 file1 | 6 +++---
 1 file changed, 3 insertions(+), 3 deletions(-)
$ cat file1 
lineI
lineII
lineIII
```

删除分支：

```
$ git branch -d ccy
Deleted branch ccy (was 381cb66).
```

## 解决冲突
冲突是在所难免的，解决冲突并不难，需要一个决策者来做出决定。我们来模拟一次冲突。首先准备一个新的仓库。

```
$ git init p2 && cd p2
Initialized empty Git repository in /Users/ccyag/gitabc/p2/.git/
$ echo line1 > file1
$ echo line2 >> file1
$ cat file1 
line1
line2
$ git add file1 
$ git commit -m "init"
```
新建并切换分支,然后修改文件并提交：

```
$ git branch ccy
$ git branch
  ccy
* master
$ git checkout ccy
Switched to branch 'ccy'
$ sed -i '' 's/line2/lineII/g' file1 
$ git add file1 
$ git commit -m 'r1'
```
返回master分支，也修改文件并提交：

```
$ git checkout master
Switched to branch 'master'
$ sed -i '' 's/line2/lineTwo/g' file1 
$ git commit -m "r2" -a
```
合并分支：

```
$ git merge ccy
Auto-merging file1
CONFLICT (content): Merge conflict in file1
Automatic merge failed; fix conflicts and then commit the result.
```
查看文件：

```
$ cat file1 
line1
<<<<<<< HEAD
lineTwo
=======
lineII
>>>>>>> ccy
```
修改文件后提交,这里使用编辑器修改文件：

```
$ git add file1 
$ git commit -m "conflict solved"
```

## rebase
新建一个仓库，来学习`git rebase`。

```
$ git init p3 && cd p3
$ echo line1 > file1
$ git add .
$ git commit -m "r1"

```
新建一个分支，修改并提交。

```
$ git checkout -b ccy
$ echo lineI > file1 
$ git commit -am "rI"

```
切换master分支，保存并提交。

```
$ git checkout master
$ echo line2 >> file1 
$ git commit -am "r2"
```
查看提交修订。

```
$ git hist
* 01b13d7 2019-11-28 |r2 (HEAD -> master) [chen chongyang]
* 8ab91e1 2019-11-28 |r1 [chen chongyang]
$ git checkout ccy
Switched to branch 'ccy'
$ git hist
* cc5b6a8 2019-11-28 |rI (HEAD -> ccy) [chen chongyang]
* 8ab91e1 2019-11-28 |r1 [chen chongyang]
```
现在要把ccy分支的成果合并到master：

```
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: rI
Using index info to reconstruct a base tree...
M	file1
Falling back to patching base and 3-way merge...
Auto-merging file1
CONFLICT (content): Merge conflict in file1
error: Failed to merge in the changes.
Patch failed at 0001 rI
hint: Use 'git am --show-current-patch' to see the failed patch
Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

```
查看分支，显示没有当前分支，因为`rebase`还没有完成：

```
$ git branch
* (no branch, rebasing ccy)
  ccy
  master
```
解决冲突，使用`--continue`继续`rebase`命名：

```
$ echo line1 >file1 
$ echo line2 >>file1 
$ echo lineI >>file1 
$ git add file1 
$ git rebase --continue
Applying: rI
```
查看历史：

```
$ git mist
rI
r2
r1
```
说明rI的父修订从r1变成了r2，git rebase 会把当前分支的全部修订搬移到指定分支上，两个分支合并成一条单线。

## 撤销`git rebase`
使用git reflog 命令列出全部操作：

```
$ git reflog
a68084d (HEAD -> ccy) HEAD@{0}: rebase finished: returning to refs/heads/ccy
a68084d (HEAD -> ccy) HEAD@{1}: rebase: rI
01b13d7 (master) HEAD@{2}: rebase: checkout master
cc5b6a8 HEAD@{3}: checkout: moving from master to ccy
01b13d7 (master) HEAD@{4}: commit: r2
8ab91e1 HEAD@{5}: checkout: moving from ccy to master
cc5b6a8 HEAD@{6}: commit: rI
8ab91e1 HEAD@{7}: checkout: moving from master to ccy
8ab91e1 HEAD@{8}: commit (initial): r1
```
使用`git reset`命令恢复到`rebase`之前。

```
$ git reset --hard 01b13d7
HEAD is now at 01b13d7 r2
```
`--hard`修改仓库的同时，也会覆盖工作区和暂存区的文件。

查看仓库信息：

```
$ git mist
r2
r1
g$ git branch
* ccy
  master
$ cat file1 
line1
line2

```

# 修订的标识

git采用40位的通过SHA1算法生成的字符串作为基础标识符，使用标识符或者它的缩写可以唯一定位一个修订。此标识符难以阅读和辨识。所以git提供了引用标志符。包括head引用和分支引用。

>1. "^"组合标识。格式为修订标识符+“^”+Number。如果仓库存在分支合并，并导致某个修订有多个父修订的情况下，可以使用此方法指定该修订的第Number父修订。
2. “~”组合标识。格式为修订标识符+“~”+Number。可以使用此方法指定前Number个祖先修订。
3. “@”组合标识。格式为修订标识符+“@”+“{”+Number+"}"。Git会记录所有操作（包括提交、撤销等）数月，这些操作由近及远以渐增数字次序记录。可以使用此方法指定倒数第Number个操作指向的修订。

## 准备环境
为了学习标识符，使用前面学习的知识，构造一个简单的仓库。

```
$ git init p1 && cd p1
Initialized empty Git repository in /Users/ccyag/gitabc/p1/.git/
$ echo line1 > file1
$ git add .
$ git commit -m "r1"
$ echo line2 >> file1 
$ git commit -m "r2" -a
$ git checkout -b ccy
Switched to a new branch 'ccy'
$ echo lineI > file1 
$ git commit -m "rI" -a
$ echo lineII >> file1 
$ git commit -m "rII" -a
cdy:p1 ccyag$ git checkout master
Switched to branch 'master'
$ echo line3 >> file1 
$ git commit -m "r3" -a
$ git merge ccy
$ git commit -m "m1" -a
$ echo line4 >> file1 
$ git commit -m "m2" -a
```
查看仓库历史：

```
$ git hist --graph
* f892dd1 2019-11-28 |m2 (HEAD -> master) [chen chongyang]
*   1cca256 2019-11-28 |m1 [chen chongyang]
|\  
| * c8b8ea0 2019-11-28 |rII (ccy) [chen chongyang]
| * 8ab1b6d 2019-11-28 |rI [chen chongyang]
* | 1c52fb8 2019-11-28 |r3 [chen chongyang]
|/  
* 74ef59d 2019-11-28 |r2 [chen chongyang]
* b8c322a 2019-11-28 |r1 [chen chongyang]
```

## 基础标识符 SHA1标志

```
$ git log --pretty=oneline
f892dd11978faf57444dc6b11b5262eefe3bfe64 (HEAD -> master) m2
1cca256cfbe875654f0c4541a730cd052813d659 m1
1c52fb86fd8c511cd7cf8955c116eaa110dd025a r3
c8b8ea0e54eccfa9293f095f16515bedf05d9678 (ccy) rII
8ab1b6de71c0d0d1d9a8271234952d712ac8e787 rI
74ef59d407d6ec0440f68e799ee98caa9402470a r2
b8c322aa36be8bfb1071cd252d38881e7a547c1e r1
```
显示最后一次的修订信息：

```
$ git show f892dd11978faf57444dc6b11b5262eefe3bfe64
commit f892dd11978faf57444dc6b11b5262eefe3bfe64 (HEAD -> master)
Author: chen chongyang <22377832@qq.com>
Date:   Thu Nov 28 20:22:07 2019 +0800

    m2

diff --git a/file1 b/file1
index 5c51359..9566e72 100644
--- a/file1
+++ b/file1
@@ -6,3 +6,4 @@ line3
 lineI
 lineII
 >>>>>>> ccy
+line4
```

## 缩写的修订标识符
```
$ git log --abbrev-commit --pretty=oneline
f892dd1 (HEAD -> master) m2
1cca256 m1
1c52fb8 r3
c8b8ea0 (ccy) rII
8ab1b6d rI
74ef59d r2
b8c322a r1
```

## 引用标识符：head

```
$ git show head --oneline --quiet
f892dd1 (HEAD -> master) m2
```
head 总是指向当前分支的最近一次修订。

## 引用标识符：分支

```
$ git show master --oneline --quiet
f892dd1 (HEAD -> master) m2
$ git show ccy --oneline --quiet
c8b8ea0 (ccy) rII
```

## "~"标识符

```
$ git show head~3 --oneline --quiet
74ef59d r2
```

## "^"标识符

```
$ git show head~1^1 --oneline --quiet
1c52fb8 r3
$ git show head~1^2 --oneline --quiet
c8b8ea0 (ccy) rII
```

## head变化规律

>1. 提交时，head指向当前分支的最后一次修订。
2. 撤销时，head指向gitreset参数要求的修订。
3. 分支转换时，head指向gitcheckout参数要求的分支的最后一次提交。

# 标签

git标签用于版本标记，比如：

```
$ git tag v1.0.20191127
$ git tag
v1.0.20191127
```

使用标签获取指定的版本：

```
$ git checkout tags/v1.0.20191127
Note: switching to 'tags/v1.0.20191127'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f892dd1 m2
```


