# 

> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [aimuch.com](https://aimuch.com/2019/03/21/git%E6%95%99%E7%A8%8B/#more)

[](#配置git环境 "配置git环境")配置 git 环境
===============================

[](#添加配置 "添加配置")添加配置
--------------------

<table><tbody><tr><td class="gutter"><pre>1<br>2<br></pre></td><td class="code"><pre>git config [--local | --global | --system] user.name 'Your name'<br>git config [--local | --global | --system] user.email 'Your email'<br></pre></td></tr></tbody></table>复制

[](#查看配置 "查看配置")查看配置
--------------------

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git config --list [--local | --global | --system]<br></pre></td></tr></tbody></table>复制

[](#区别 "区别")区别
--------------

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br></pre></td><td class="code"><pre>local：区域为本仓库<br>global: 当前用户的所有仓库<br>system: 本系统的所有用户<br></pre></td></tr></tbody></table>复制

[](#git-add-和-git-add-u区别 "git add . 和 git add -u区别")`git add .` 和 `git add -u` 区别
==================================================================================

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br>10<br>11<br>12<br></pre></td><td class="code"><pre>git add . ：将工作空间新增和被修改的文件添加的暂存区<br>git add -u :将工作空间被修改和被删除的文件添加到暂存区(不包含没有纳入Git管理的新增文件)<br>```    <br><br># 创建仓库<br>```bash<br>git init [project folder name]  初始化 git 仓库<br>git add [fileName]  把文件从工作目录添加到暂存区<br>git commit -m'some information'  用于提交暂存区的文件<br>git commit -am'Some information' 用于提交跟踪过的文件<br>git log  查看历史<br>git status  查看状态<br></pre></td></tr></tbody></table>复制

**额外**  
git add -u 可以添加所有已经被 git 控制的文件到暂存区  
以前删除文件夹只会用 「-rf」，今天学到了 「-r」，并得知它们两个区别：「-r」 有时候会提示是否确认删除。

[](#clone时指定文件夹名字 "clone时指定文件夹名字")clone 时指定文件夹名字
================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git clone https://github.com/repository_NAME PATH/new_folder<br></pre></td></tr></tbody></table>复制

[](#给文件重命名的简便方法 "给文件重命名的简便方法")给文件重命名的简便方法
=========================================

<table><tbody><tr><td class="gutter"><pre>1<br>2<br></pre></td><td class="code"><pre>git  mv  [old file name]  [new file name]<br>git commit -m 'some information'<br></pre></td></tr></tbody></table>复制

[](#Tag标签 "Tag标签")Tag 标签
========================

**显示已有标签**

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git tag<br></pre></td></tr></tbody></table>复制

**新建标签**  
_创建一个含附注类型的标签非常简单，用 -a （译注：取 annotated 的首字母）指定标签名字即可_

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git tag -a tag_name -m 'Some Messages'<br></pre></td></tr></tbody></table>复制

**删除标签**  
删除本地标签:

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git tag -d tag_name<br></pre></td></tr></tbody></table>复制

删除 `remote` 标签 :

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git push --delete origin tag_name<br></pre></td></tr></tbody></table>复制

**推送标签到 github**  
将本地**所有**标签推送到 `remote`:

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git push origin --tags<br></pre></td></tr></tbody></table>复制

[](#在Github上面创建Release "在Github上面创建Release")在 Github 上面创建 Release
=================================================================

1.  在当前 `repository` 下点击 **release** 标签:  
    [![github release](/2019/03/21/git教程/github-release1.png)](/2019/03/21/git教程/github-release1.png "github release")
    
    [github release](/2019/03/21/git教程/github-release1.png "github release")
    
2.  点击 **Draft a new release** 按钮:  
    [![github release](/2019/03/21/git教程/github-release2.png)](/2019/03/21/git教程/github-release2.png "github release")
    
    [github release](/2019/03/21/git教程/github-release2.png "github release")
    
3.  在跳转后的界面下填写 `Tag version` 、 `Release title` 和 `描述`  
    [![github release](/2019/03/21/git教程/github-release3.png)](/2019/03/21/git教程/github-release3.png "github release")
    
    [github release](/2019/03/21/git教程/github-release3.png "github release")
    
      
    如下图:  
    [![github release](/2019/03/21/git教程/github-release4.png)
    
    github release
    
    ](/2019/03/21/git教程/github-release4.png "github release")
    
4.  点击 `Update release` 按钮提交即可，提交后效果:  
    [![github release](/2019/03/21/git教程/github-release5.png)](/2019/03/21/git教程/github-release5.png "github release")
    
    [github release](/2019/03/21/git教程/github-release5.png "github release")
    

[](#通过git-log查看版本演变历史 "通过git log查看版本演变历史")通过 `git log` 查看版本演变历史
===============================================================

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br></pre></td><td class="code"><pre>git log --all 查看所有分支的历史<br>git log --all --graph 查看图形化的 log 地址<br>git log --oneline 查看单行的简洁历史。<br>git log --oneline -n4 查看最近的4条简洁历史。<br>git log --oneline --all -n4 --graph 查看所有分支最近4条单行的图形化历史。<br>git help --web log 跳转到git log 的帮助文档网页<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git branch -v 查看本地有多少分支<br></pre></td></tr></tbody></table>复制

[](#通过图形界面工具来查看版本历史 "通过图形界面工具来查看版本历史")通过图形界面工具来查看版本历史
=====================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>gitk<br></pre></td></tr></tbody></table>复制

[](#探密-git目录 "探密.git目录")探密`.git` 目录
===================================

查看`.git` 文件夹下的内容：

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>ls .git/ -al<br></pre></td></tr></tbody></table>复制

如下:

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br>10<br>11<br>12<br>13<br>14<br></pre></td><td class="code"><pre>drwxr-xr-x 1 Andy 197609   0 12月 17 22:38 ./<br>drwxr-xr-x 1 Andy 197609   0 12月 17 21:50 ../<br>-rw-r--r-- 1 Andy 197609   7 12月 17 22:38 COMMIT_EDITMSG<br>-rw-r--r-- 1 Andy 197609 301 12月 12 22:55 config<br>-rw-r--r-- 1 Andy 197609  73 12月 12 22:55 description<br>-rw-r--r-- 1 Andy 197609  96 12月 19 00:00 FETCH_HEAD<br>-rw-r--r-- 1 Andy 197609  23 12月 12 22:55 HEAD<br>drwxr-xr-x 1 Andy 197609   0 12月 12 22:55 hooks/<br>-rw-r--r-- 1 Andy 197609 249 12月 17 22:38 index<br>drwxr-xr-x 1 Andy 197609   0 12月 12 22:55 info/<br>drwxr-xr-x 1 Andy 197609   0 12月 12 22:55 logs/<br>drwxr-xr-x 1 Andy 197609   0 12月 17 22:38 objects/<br>-rw-r--r-- 1 Andy 197609 114 12月 12 22:55 packed-refs<br>drwxr-xr-x 1 Andy 197609   0 12月 12 22:55 refs/<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br></pre></td><td class="code"><pre>cat命令主要用来查看文件内容，创建文件，文件合并，追加文件内容等功能。<br>cat HEAD 查看HEAD文件的内容<br>git cat-file 命令 显示版本库对象的内容、类型及大小信息。<br>git cat-file -t b44dd71d62a5a8ed3 显示版本库对象的类型<br>git cat-file -s b44dd71d62a5a8ed3 显示版本库对象的大小<br>git cat-file -p b44dd71d62a5a8ed3 显示版本库对象的内容<br></pre></td></tr></tbody></table>复制

`.git` 里几个常用的如下：

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br></pre></td><td class="code"><pre>HEAD：指向当前的工作路径<br>config：存放本地仓库（local）相关的配置信息。<br>refs/heads: 存放分支<br>refs/heads/master/: 指向master分支最后一次commit<br>refs/tags: 存放tag，又叫里程牌 （当这次commit是具有里程碑意义的 比如项目1.0的时候 就可以打tag）<br>objects：核心文件，存储文件<br></pre></td></tr></tbody></table>复制

.git/objects/ 存放所有的 git 对象，对象哈希值前 2 位作为文件夹名称，后 38 位作为对象文件名，可通过 git cat-file -p 命令，拼接文件夹名称 + 文件名查看。

[](#commit、tree和blob三个对象之间的关系 "commit、tree和blob三个对象之间的关系")`commit`、`tree` 和 `blob` 三个对象之间的关系
============================================================================================

[![tree](/2019/03/21/git教程/img1.jpg)](/2019/03/21/git教程/img1.jpg "tree")

[tree](/2019/03/21/git教程/img1.jpg "tree")

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br></pre></td><td class="code"><pre>commit: 提交时的镜像<br>tree: 文件夹<br>blob: 文件<br></pre></td></tr></tbody></table>复制

**【同学问题】** 每次 commit，git 都会将当前项目的所有文件夹及文件快照保存到 objects 目录，如果项目文件比较大，不断迭代，commit 无数次后，objects 目录中文件大小是不是会变得无限大？  
**【老师解答】** Git 对于内容相同的文件只会存一个 blob，不同的 commit 的区别是 commit、tree 和有差异的 blob，多数未变更的文件对应的 blob 都是相同的，这么设计对于版本管理系统来说可以省很多存储空间。其次，Git 还有增量存储的机制，我估计是对于差异很小的 blob 设计的吧。

[](#分离头指针情况下的注意事项 "分离头指针情况下的注意事项")分离头指针情况下的注意事项
===============================================

detached HEAD

[](#进一步理解HEAD和branch "进一步理解HEAD和branch")进一步理解 `HEAD` 和 `branch`
===============================================================

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br>10<br>11<br></pre></td><td class="code"><pre>git checkout -b new_branch [具体分支 或 commit] 创建新分支并切换到新分支<br>git diff HEAD HEAD~1 比较最近两次提交<br>git diff HEAD HEAD~2 比较最近和倒数第三次提交<br>git diff HEAD HEAD^  比较最近两次提交<br>git diff HEAD HEAD^^ 比较最近和倒数第三次提交<br>```   <br><br># 怎么删除不需要的分支？<br>查看分支：   <br>```bash<br>git branch -av<br></pre></td></tr></tbody></table>复制

删除分支命令：

<table><tbody><tr><td class="gutter"><pre>1<br>2<br></pre></td><td class="code"><pre>git branch -d [branch name]  #删除<br>git branch -D [branch name]  #强制删除<br></pre></td></tr></tbody></table>复制

[](#怎么修改最新commit的message "怎么修改最新commit的message")怎么修改最新 commit 的 message
=======================================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git commit --amend  对最近一次的commit信息进行修改<br></pre></td></tr></tbody></table>复制

[](#怎么修改老旧commit的message "怎么修改老旧commit的message")怎么修改老旧 commit 的 message
=======================================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git rebase -i [要更改的commit的上一级commit]<br></pre></td></tr></tbody></table>复制

接下来就是一个交互过程…  
这期间会产生一个 detached HEAD，然后将改好的 commit 指向该 detached HEAD，如下图所示：  
[![rebase](/2019/03/21/git教程/img2.jpg)](/2019/03/21/git教程/img2.jpg "rebase")

[rebase](/2019/03/21/git教程/img2.jpg "rebase")

**git rebase 工作的过程中，就是用了分离头指针。rebase 意味着基于新 base 的 commit 来变更部分 commits。它处理的时候，把 HEAD 指向 base 的 commit，此时如果该 commit 没有对应 branch，就处于分离头指针的状态，然后重新一个一个生成新的 commit，当 rebase 创建完最后一个 commit 后，结束分离头状态，Git 让变完基的分支名指向 HEAD。**

[](#怎样把连续的多个commit整理成1个 "怎样把连续的多个commit整理成1个")怎样把连续的多个 commit 整理成 1 个
=====================================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git rebase -i [要更改的commit的上一级commit]<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br>10<br>11<br>12<br>13<br>14<br>15<br>16<br>17<br>18<br>19<br>20<br>21<br>22<br>23<br>24<br>25<br>26<br>27<br>28<br>29<br>30<br></pre></td><td class="code"><pre>$ git log --graph<br>* commit 7d3386842a2168ae630b65f687364243139c893c (HEAD -&gt; master, origin/master, origin/HEAD)<br>| Author: aimuch &lt;anetspace@gmail.com&gt;<br>| Date:   Thu Dec 20 23:34:18 2018 +0800<br>|<br>|     update<br>|<br>* commit 9eb3188bbc63cae1bfed5f9dfc1593019e360a6a<br>| Author: aimuch &lt;anetspace@gmail.com&gt;<br>| Date:   Wed Dec 19 20:30:14 2018 +0800<br>|<br>|     update<br>|<br>* commit bbe6d53e2b477f2d2aa402af7f315ecdfc63459e<br>| Author: aimuch &lt;anetspace@gmail.com&gt;<br>| Date:   Wed Dec 19 20:12:29 2018 +0800<br>|<br>|     update<br>|<br>* commit 7735d66ded7f98adeca93d96fb7be12ffb67c76a<br>| Author: aimuch &lt;anetspace@gmail.com&gt;<br>| Date:   Wed Dec 19 00:27:00 2018 +0800<br>|<br>|     update<br>|<br>* commit d9f9d115fab425b5654f8ccfec6a996aef35b76b<br>| Author: aimuch &lt;anetspace@gmail.com&gt;<br>| Date:   Wed Dec 19 00:23:36 2018 +0800<br>|<br>|     update<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br>10<br>11<br>12<br>13<br>14<br>15<br>16<br>17<br>18<br>19<br>20<br>21<br></pre></td><td class="code"><pre>pick   7735d66 update #合并到该commit上<br>squash bbe6d53 update<br>squash 9eb3188 update<br>squash 7d33868 update<br># Rebase d9f9d11..7d33868 onto d9f9d11 (4 commands)<br>#<br># Commands:<br># p, pick &lt;commit&gt; = use commit<br># r, reword &lt;commit&gt; = use commit, but edit the commit message<br># e, edit &lt;commit&gt; = use commit, but stop for amending<br># s, squash &lt;commit&gt; = use commit, but meld into previous commit<br># f, fixup &lt;commit&gt; = like "squash", but discard this commit's log message<br># x, exec &lt;command&gt; = run command (the rest of the line) using shell<br># b, break = stop here (continue rebase later with 'git rebase --continue')<br># d, drop &lt;commit&gt; = remove commit<br># l, label &lt;label&gt; = label current HEAD with a name<br># t, reset &lt;label&gt; = reset HEAD to a label<br># m, merge [-C &lt;commit&gt; | -c &lt;commit&gt;] &lt;label&gt; [# &lt;oneline&gt;]<br># .       create a merge commit using the original merge commit's<br># .       message (or the oneline, if no original merge commit was<br># .       specified). Use -c &lt;commit&gt; to reword the commit message.<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br>10<br>11<br>12<br>13<br>14<br>15<br>16<br></pre></td><td class="code"><pre># This is a combination of 4 commits.<br># This is the 1st commit message:<br><br>update<br><br># This is the commit message #2:<br><br>update<br><br># This is the commit message #3:<br><br>update<br><br># This is the commit message #4:<br><br>update<br></pre></td></tr></tbody></table>复制

[](#添加忽略配置文件gitignore "添加忽略配置文件gitignore")添加忽略配置文件 gitignore
============================================================

在 git 中如果想忽略掉某个文件， 不让这个文件提交到版本库中，可以使用修改 .gitignore 文件的方法。  
这个文件每一行保存了一个匹配的规则，可以用正则表达式来描述，例如:

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br></pre></td><td class="code"><pre># 此为注释 – 将被 Git 忽略<br>*.a       # 忽略所有 .a 结尾的文件<br>!lib.a    # 但 lib.a 除外<br>/TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO<br>build/    # 忽略 build/ 目录下的所有文件<br>doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt<br>*ignore/  # 忽略名称中末尾为ignore的文件夹<br>*ignore*/ # 忽略名称中间包含ignore的文件夹<br></pre></td></tr></tbody></table>复制

通用的模板:

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br>10<br>11<br>12<br>13<br>14<br>15<br>16<br>17<br>18<br>19<br>20<br>21<br>22<br>23<br>24<br>25<br>26<br>27<br>28<br>29<br>30<br>31<br>32<br>33<br>34<br>35<br>36<br>37<br>38<br></pre></td><td class="code"><pre># Compiled source #<br>###################<br>*.com<br>*.class<br>*.dll<br>*.exe<br>*.o<br>*.so<br><br># Packages #<br>############<br># it's better to unpack these files and commit the raw source<br># git has its own built in compression methods<br>*.7z<br>*.dmg<br>*.gz<br>*.iso<br>*.jar<br>*.rar<br>*.tar<br>*.zip<br><br># Logs and databases #<br>######################<br>*.log<br>*.sql<br>*.sqlite<br><br># OS generated files #<br>######################<br>.DS_Store<br>.DS_Store?<br>._*<br>.Spotlight-V100<br>.Trashes<br>Icon?<br>ehthumbs.db<br>Thumbs.db<br></pre></td></tr></tbody></table>复制

更详细的介绍请看 **GitHub** 官网给出的例子: `https://github.com/github/gitignore`

[](#Git修改gitignore后生效 "Git修改gitignore后生效")Git 修改 gitignore 后生效
==============================================================

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br></pre></td><td class="code"><pre>git rm -r --cached .    #清除缓存<br>git add .               #重新trace file<br>git commit -m "update .gitignore" #提交和注释<br>git push origin master  #可选，如果需要同步到remote上的话<br></pre></td></tr></tbody></table>复制

[](#寻找并删除Git记录中的大文件 "寻找并删除Git记录中的大文件")寻找并删除 Git 记录中的大文件
=======================================================

本文来介绍查找和重写 Git 记录的命令：`git rev-list` , `git filter-branch` 。生产环境请考虑使用 [bfg](https://github.com/rtyley/bfg-repo-cleaner) 等效率工具。

首先通过 rev-list 来找到仓库记录中的大文件：

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git rev-list --objects --all | grep "$(git verify-pack -v .git/objects/pack/*.idx | sort -k 3 -n | tail -5 | awk '{print$1}')"<br></pre></td></tr></tbody></table>复制

然后通过 `filter-branch` 来重写这些大文件涉及到的所有提交（重写历史记录）：

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git filter-branch -f --prune-empty --index-filter 'git rm -rf --cached --ignore-unmatch your-file-name' --tag-name-filter cat -- --all<br></pre></td></tr></tbody></table>复制

[](#Git仓库的存储方式 "Git仓库的存储方式")Git 仓库的存储方式
---------------------------------------

_如果你熟知 Git 的存储方式，跳过此节。_

Git 仓库位于项目根目录的 `.git` 文件夹，其中保存了从仓库建立（`git init`）以来所有的代码增删。 每一个提交（`Commit`）相当于一个 Patch 应用在之前的项目上，借此一个项目可以回到任何一次提交时的文件状态。

于是在 Git 中删除一个文件时，Git 只是记录了该删除操作，该记录作为一个 Patch 存储在 `.git` 中。 删除前的文件仍然在 Git 仓库中保存着。直接删除文件并提交起不到给 Git 仓库瘦身的效果。

在 Git 仓库彻底删除一个文件只有一种办法：重写（`Rewrite`）涉及该文件的所有提交。 幸运的是借助 `git filter-branch` 便可以重写历史提交，当然这也是 Git 中最危险的操作。 可以说比 `rm -rf *` 危险一万倍。

[](#从所有提交中删除一个文件 "从所有提交中删除一个文件")从所有提交中删除一个文件
--------------------------------------------

如果清楚地记得曾提交过名为 `recent-badge.psd` 的文件。这是一个很大的 PhotoShop 文件，要把它删掉。 `filter-branch` 命令可以用来重写 Git 仓库中的提交， 利用 `filter-branch` 的 `--index-filter` 参数便能把它从所有 Git 提交中删除。

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br></pre></td><td class="code"><pre>$ git filter-branch -f --prune-empty --index-filter 'git rm -rf --cached --ignore-unmatch assets/img/recent-badge.psd' --tag-name-filter cat -- --all<br>Rewrite 2771f50d45a0293668a30af77983d87886441640 (264/982)rm 'assets/img/recent-badge.psd'<br>Rewrite 1a98ecb3f39e1f200e31754714eec18bc92848ce (265/982)rm 'assets/img/recent-badge.psd'<br>Rewrite d4e61cfb1d88187b0561d283e663b81b738df2c7 (270/982)rm 'assets/img/recent-badge.psd'<br>Rewrite 4ba0df06b26cf86fd39c2cda6b012c521cbc4dc1 (271/982)rm 'assets/img/recent-badge.psd'<br>Rewrite 242ae98060c77863f5e826ba7e1ec47<br></pre></td></tr></tbody></table>复制

*   `filter-branch` 是让 git 重写每一个分支；
*   `--prune-empty` 选项告诉 git，如果因为重写导致某些 commit 变成了空（比如修改的文件全部被删除），那么忽略掉这个 commit;
*   `--index-filter` 参数用来指定一条 Bash 命令，然后 Git 会检出（`checkout`）所有的提交， 执行该命令，然后重新提交。我们在提交前移除了 `recent-badge.psd` 文件， 这个文件便从 Git 的所有记录中完全消失了；
*   `--tag-name-filter` 表示对每一个 tag 如何重命名，重命名的命令紧跟在后面，当前的 tag 名会从标注输入送给后面的命令，用 cat 就表示保持 tag 名不变；
*   紧跟着的 `--` 表示分割符；
*   `--all` 参数告诉 Git 我们需要重写所有分支（或引用）。

[](#寻找大文件的ID "寻找大文件的ID")寻找大文件的 ID
---------------------------------

删掉了 `recent-badge.psd` 后我仍不满足，我要找到所有的大文件，并把它删掉。 `verify-pack` 命令用来验证 Git 打包的归档文件，我们用它来找到那些大文件。 例如：

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br></pre></td><td class="code"><pre>$ git verify-pack -v .git/objects/pack/*.idx<br>8fa15d279de33ce28a3289fd33951374084231e4 tree   135 137 144088922<br>a44a50b2ffb1f8283c8e64aafb8e7628249d7453 tree   33 43 144089059<br>b57d99f38fe22491e4a2d30c2b081ecb7bbb329c tree   99 97 144089102<br>2d4ffaffc11758d561ea1a6d57dd8ee17ee1d836 blob   644952 644959 144089199<br>8cf81ebfeec409f19e7a47a76517317f3bfa268d blob   695898 695871 144734158<br>...<br></pre></td></tr></tbody></table>复制

*   `-v`（verbose）参数是打印详细信息。

输出的第一列是文件 ID，第二列表示文件（blob）或目录（tree），第三列是文件大小。 现在得到了所有的文件 ID 及其大小，需要写一点 Bash 了！

先按照第三列排序，并取最大的 5 条，然后打印出每项的第一列（这一列是文件 ID）：

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br></pre></td><td class="code"><pre>$ git verify-pack -v .git/objects/pack/*.idx | sort -k 3 -n | tail -10 | awk '{print$1}')"<br>f846f156d16f74243b67e3dabec58a3128744352 <br>4a1546e732b2e2a352b7bf220c1a22ad859abf89 <br>f72d04efe6d0b41b067f9fbbc62455f28d3670d2 <br>49bdf300ddf57d1946bc9c6570d94a38ac9d6a50 <br>9c073d4177af5d2e43ada41f92efb18d9462a536<br></pre></td></tr></tbody></table>复制

现在变得到了最大的 5 个文件的 ID，而我需要文件名才能用 `filter-branch` 移除它。 我现在需要文件 ID 和文件名的映射关系。

[](#文件名与ID映射 "文件名与ID映射")文件名与 ID 映射
----------------------------------

`rev-list` 命令用来列出 Git 仓库中的提交，我们用它来列出所有提交中涉及的文件名及其 ID。 该命令可以指定只显示某个引用（或分支）的上下游的提交。例如：

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git rev-list foo bar ^baz<br></pre></td></tr></tbody></table>复制

将会列出所有从 `foo` 和 `bar` 可到达，但从 baz 不可到达的提交。我们将会用到 `rev-list` 的两个参数：

*   `--objects`：列出该提交涉及的所有文件 ID。
*   `--all`：所有分支的提交，相当于指定了位于 /refs 下的所有引用。

我们看看这条命令的输出：

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br></pre></td><td class="code"><pre>$ git rev-list --objects --all<br>c252878ac09a3979a80520b82a71dc2dae4529f9<br>7bc7d05c6097063f531580ba4c32921464a6c456 _drafts<br>dcce26ed53fbb869dc7d5b71742d2f9e523bfe42 _layouts<br>414186c794a0d58695abb75c548bdbfec1de2763 _layouts/default.html<br>1934eeffe3d242375510dff28cffa6de6b3de367 _layouts/post.html<br>5f14647875f2177a6d37b8bfbcdb4629af595b64 _posts<br>6cdbb293d453ced07e6a07e0aa6e580e6a5538f4 _posts/2013-10-12-2.md<br>...<br></pre></td></tr></tbody></table>复制

现在就得到了**文件名**（如`_posts/2013-10-12-2.md`）和 **ID**（如 `6cdbb293d453ced07e6a07e0aa6e580e6a5538f4` ）的映射关系。

[](#得到文件名列表 "得到文件名列表")得到文件名列表
-----------------------------

前面我们通过 `rev-list` 得到了**文件名 - ID** 的对应关系，通过 `verify-pack` 得到了最大的 5 个文件 ID。 用后者筛选前者便能得到最大的 5 个文件的文件名：

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br></pre></td><td class="code"><pre>$ git rev-list --objects --all | grep "$(git verify-pack -v .git/objects/pack/*.idx | sort -k 3 -n | tail -5 | awk '{print$1}')"<br>#$ git rev-list --objects --all | grep "$(git verify-pack -v .git/objects/pack/*.idx | sort -k 3 -n | tail -5 | awk '{print$1}')" &gt; large-files.txt<br>f846f156d16f74243b67e3dabec58a3128744352 assets/img/recent-badge.psd<br>4a1546e732b2e2a352b7bf220c1a22ad859abf89 assets/img/album/me/IMG_0276.JPG<br>f72d04efe6d0b41b067f9fbbc62455f28d3670d2 assets/img/album/me/IMG_0389.JPG<br>49bdf300ddf57d1946bc9c6570d94a38ac9d6a50 assets/img/album/me/IMG_0813.JPG<br>9c073d4177af5d2e43ada41f92efb18d9462a536 assets/img/album/me/IMG_0891.JPG<br></pre></td></tr></tbody></table>复制

先把上面输出存到 `large-files.txt` 中。还记得吗？`--tree-filter` 参数中我们需要给出一行的文件名列表。上述列表我们需要处理一下：

<table><tbody><tr><td class="gutter"><pre>1<br>2<br></pre></td><td class="code"><pre>$ cat large-files.txt| awk '{print $2}' | tr '\n' ' '<br>assets/img/recent-badge.psd assets/img/album/me/IMG_0276.JPG assets/img/album/me/IMG_0389.JPG assets/img/album/me/IMG_0813.JPG assets/img/album/me/IMG_0891.JPG<br></pre></td></tr></tbody></table>复制

现在便得到了一行的文件列表。把它存到 `large-files-inline.txt` 中。

[](#删除所有大文件 "删除所有大文件")删除所有大文件
-----------------------------

现在得到了要删除的大文件列表 `large-files-inline.txt`，把它传入到 `--tree-filter` 中即可：

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git filter-branch -f --prune-empty --index-filter "git rm -rf --cached --ignore-unmatch `cat large-files-inline.txt`" --tag-name-filter cat -- --all<br></pre></td></tr></tbody></table>复制

注意这里 `--index-filter` 的参数要用双引号，因为 `cat large-files-inline.txt` 还需要 Bash 的解析。

至此已经干掉了那些大文件，来看看瘦身了多少吧！ 注意 filter-branch 之后.git 目录下会有大量的备份。

当然到此为止我们更改的都是本地仓库，现在把这些改变 Push 到远程仓库中去！

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git push origin --force --all<br></pre></td></tr></tbody></table>复制

因为不是 fast forward，所以需要指定 `--force` 参数。

这里的 `--all` 会将所有分支都推送到 `origin` 上。当然你也可以只推送 `master` 分支：`git push origin master --force`。但是！如果其它远程分支有那些大文件提交的话，仍然没有瘦身！

[](#怎么比较暂存区和HEAD所含文件的差异？ "怎么比较暂存区和HEAD所含文件的差异？")怎么比较暂存区和 HEAD 所含文件的差异？
======================================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git diff --cached<br></pre></td></tr></tbody></table>复制

或者

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git diff --staged<br></pre></td></tr></tbody></table>复制

[](#怎么比较工作区和暂存区所含文件的差异？ "怎么比较工作区和暂存区所含文件的差异？")怎么比较工作区和暂存区所含文件的差异？
=================================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git diff<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git diff -- [filename/pathname] #比较具体的文件或者路径<br></pre></td></tr></tbody></table>复制

[](#如何让暂存区恢复成和HEAD的一样？ "如何让暂存区恢复成和HEAD的一样？")如何让暂存区恢复成和 HEAD 的一样？
================================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git reset HEAD<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br></pre></td><td class="code"><pre>git reset 有三个参数<br>--soft 这个只是把 HEAD 指向的 commit 恢复到你指定的 commit，暂存区 工作区不变<br>--hard 这个是 把 HEAD， 暂存区， 工作区 都修改为 你指定的 commit 的时候的文件状态<br>--mixed 这个是不加时候的默认参数，把 HEAD，暂存区 修改为 你指定的 commit 的时候的文件状态，工作区保持不变<br></pre></td></tr></tbody></table>复制

[](#如何让工作区的文件恢复为和暂存区一样？ "如何让工作区的文件恢复为和暂存区一样？")如何让工作区的文件恢复为和暂存区一样？
=================================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git checkout -- &lt;file&gt;...<br></pre></td></tr></tbody></table>复制

**恢复工作区用 checkout，恢复暂存区用 reset。**

[](#怎样取消暂存区部分文件的更改？ "怎样取消暂存区部分文件的更改？")怎样取消暂存区部分文件的更改？
=====================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git reset HEAD -- &lt;file&gt;...<br></pre></td></tr></tbody></table>复制

[](#看看不同提交的指定文件的差异 "看看不同提交的指定文件的差异")看看不同提交的指定文件的差异
==================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git diff commit-id1 commit-id2 -- &lt;file&gt;...<br></pre></td></tr></tbody></table>复制

[](#正确删除文件的方法 "正确删除文件的方法")正确删除文件的方法
===================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git rm &lt;file&gt;<br></pre></td></tr></tbody></table>复制

[](#开发中临时加塞了紧急任务怎么处理？ "开发中临时加塞了紧急任务怎么处理？")开发中临时加塞了紧急任务怎么处理？
===========================================================

<table><tbody><tr><td class="gutter"><pre>1<br>2<br></pre></td><td class="code"><pre>git stash list #查看stash中存放的信息<br>git stash #将当前工作区内容存放到"堆栈"中<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git stash apply #把"堆栈"里面的内容弹出到工作区中，同时"堆栈"中信息还在<br></pre></td></tr></tbody></table>复制<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git stash pop #把"堆栈"里面的内容弹出到工作区中，同时丢弃"堆栈"中最新的信息<br></pre></td></tr></tbody></table>复制

[](#如何指定不需要Git管理的文件？ "如何指定不需要Git管理的文件？")如何指定不需要 Git 管理的文件？
==========================================================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>.gitignore<br></pre></td></tr></tbody></table>复制

**【同学提问】** 如果提交 commit 后，想再忽略一些已经提交的文件，怎么处理。  
**【老师回答】** The problem is that .gitignore ignores just files that weren’t tracked before (by git add). Run git reset name_of_file to unstage the file and keep it. In case you want to also remove given file from the repository (after pushing), use git rm –cached name_of_file.  
把想忽略的文件添加到 .gitignore ；然后通过 git rm – cached name_of_file 的方式删除掉 git 仓库里面无需跟踪的文件。

[](#添加远程仓库 "添加远程仓库")添加远程仓库
==========================

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git remote add [shortname] [url]<br></pre></td></tr></tbody></table>复制

[](#配置公私钥 "配置公私钥")配置公私钥
=======================

[](#检查是否已存在相应的ssh-key "检查是否已存在相应的ssh key:")检查是否已存在相应的 `ssh key`:
----------------------------------------------------------------

打开终端，输入:

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>ls -al ~/.ssh<br></pre></td></tr></tbody></table>复制

核对列出来的 ssh key 是否有已存在的，假如你没有看到列出的公私钥对，或是不想再用之前的公私钥对，你可以选择下面的步骤生成新的公私钥对.

[](#生成新的ssh-key-并添加至ssh-agent "生成新的ssh key,并添加至ssh-agent:")生成新的 `ssh key`, 并添加至 `ssh-agent`:
--------------------------------------------------------------------------------------------

### [](#打开终端-使用ssh-key生成命令： "打开终端, 使用ssh key生成命令：")打开终端，使用 `ssh key` 生成命令：

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>ssh-keygen -t rsa -b 4096 -C "your_email@example.com"<br></pre></td></tr></tbody></table>复制

**注意** ：后面的邮箱对应相应账号的邮箱，假如是 github 的账号，且注册账号的邮箱为 `xxx@gmail.com`，则命令行为：

<table><tbody><tr><td class="gutter"><pre>1<br>2<br>3<br>4<br>5<br>6<br>7<br></pre></td><td class="code"><pre>ssh-keygen -t rsa -b 4096 -C "xxx@gmail.com"`。    <br>```   <br><br>### 接下来会提示你保存的`ssh key`的名称以及路径。    <br>默认路径是`/home/you/.ssh/id_rsa`(`you`为用户个人目录)即`~/.ssh/id_rsa`。这一步很重要，如果你使用默认的，且下一个账号也是使用默认的路径和文件名，那么之前的`ssh key`就会被后来生成的`ssh key`重写，从而导致之前的账号不可用。因此，正确的做法是给它命名，最后以应用名进行命名，因为更容易区分。以下是我个人配的：    <br>```shell<br>/home/andy/.ssh/github_rsa<br></pre></td></tr></tbody></table>复制

### [](#接下来会提示设置ssh安全密码。 "接下来会提示设置ssh安全密码。")接下来会提示设置 ssh 安全密码。

这一步可以使用默认的（即不设置密码），直接按回车即可。  
这里会生成 `xxx_rsa` 和 `xxx_rsa.pub` 两个文件，`xxx_rsa` 是生成的 `ssh key` 的私钥名，`xxx_rsa.pub` 是生成的 `ssh key` 的公钥名，私钥要放在本地，公钥要放在服务器或 github 的 Settings->SSHand GPG keys->New SSH key 上。  
[![git key](/2019/03/21/git教程/git-key.png)](/2019/03/21/git教程/git-key.png "git key")

[git key](/2019/03/21/git教程/git-key.png "git key")

### [](#ssh-key生成后，接下来需要为ssh-key添加代理。 "ssh key生成后，接下来需要为ssh key添加代理。")`ssh key` 生成后，接下来需要为 `ssh key` 添加代理。

这是为了让请求自动对应相应的账号。网上很多文章写到需要另外配置 `config` 文件，经本人亲测，其实是不需要的，在生成了 `ssh key` 后，通过为生成的 `ssh key` 添加代理即可，为 `ssh key` 添加代理命令:**`ssh-add ~/.ssh/xxx_rsa`**， `xxx_rsa` 是你生成的 `ssh key` 的私钥名，我的设置为:

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>ssh-add ~/.ssh/github_rsa<br></pre></td></tr></tbody></table>复制

这里有可能会提示以下错误:  
[![ssh-add key error](/2019/03/21/git教程/git-sshkey-error.png)](/2019/03/21/git教程/git-sshkey-error.png "ssh-add key error")

[ssh-add key error](/2019/03/21/git教程/git-sshkey-error.png "ssh-add key error")

  
解决方法:  
_需要 ssh-agent 启动 bash，或者说把 bash 挂到 ssh-agent 下面_

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>ssh-agent bash --login -i<br></pre></td></tr></tbody></table>复制

[](#将生成的xxx-rsa-pub公钥内容添加到GitHub的SSH-keys页面上。 "将生成的xxx_rsa.pub公钥内容添加到GitHub的SSH keys页面上。")将生成的 `xxx_rsa.pub` 公钥内容添加到 GitHub 的 SSH keys 页面上。
-------------------------------------------------------------------------------------------------------------------------------------------

[![github ssh](/2019/03/21/git教程/github-ssh.png)](/2019/03/21/git教程/github-ssh.png "github ssh")

[github ssh](/2019/03/21/git教程/github-ssh.png "github ssh")

[](#连接测试 "连接测试")连接测试
--------------------

接下来我们测试是否配置成功，打开终端，输入:

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>ssh -T git@github.com<br></pre></td></tr></tbody></table>复制

[![git test](/2019/03/21/git教程/git-test.png)](/2019/03/21/git教程/git-test.png "git test")

[git test](/2019/03/21/git教程/git-test.png "git test")

[](#怎么快速淘到感兴趣的开源项目 "怎么快速淘到感兴趣的开源项目")怎么快速淘到感兴趣的开源项目
==================================================

**UI 界面高级搜索**： [https://github.com/search/advanced](https://github.com/search/advanced)

**命令高级搜索**：

<table><tbody><tr><td class="gutter"><pre>1<br></pre></td><td class="code"><pre>git 最好 学习 资料 in:readme stars:&gt;1000 language:c<br></pre></td></tr></tbody></table>复制

上述命令的意思是搜索 reademe 中包含 `git、最好、学习、资料`” 且 `star大于1000` 的，用 `C语言编写`的仓库。

* * *

[](#参考资料 "参考资料")参考资料
====================

> 1.  [git-cheat-sheet](https://github.com/arslanbilal/git-cheat-sheet)
> 2.  [寻找并删除 Git 记录中的大文件](https://harttle.land/2016/03/22/purge-large-files-in-gitrepo.html)
> 3.  [GitHub 官网给出的例子](https://github.com/github/gitignore)
