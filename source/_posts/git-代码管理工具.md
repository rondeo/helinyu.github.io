---
title: git ~ 代码管理工具
date: 2019-03-10 19:06:11
tags: git
categories: 代码管理工具
---

git工具

<font color=red>遇到的问题 </font>
1、经常，我们git管理的项目目录下还会有一个git项目， 这个时候我们上传到github上，展示不出来文件夹，所以要将子目录下面的.git 文件夹以及里面的文件删除掉； 但是，这个时候github上还是没有展示文件夹而是打不开的文件。
PS： 很可能是因为缓存的问题，也就是没有更新到，
—— 这个时候就需要删除掉缓存了；
执行命令：
>git rm -r --cache "文件夹名称"  // 删除缓存
>git push -u origin master // 对应的分支


2、查看某个人写的代码的数量
git log --author="felix" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'

// 或者所有的人：
 git log --format='%aN' | sort -u | while read name; do echo -en "$name\t"; git log --author="$name" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -; done 

 //代码总的函数：
参考链接： https://segmentfault.com/a/119000000854212

3、
Git 的工作需要调用 curl，zlib，openssl，expat，libiconv 等库的代码，所以需要先安装这些依赖工具。
从依赖上面就可以知道git大概做的处理；

4、配置用户信息
```
git config --global user.name "runoob"
$ git config --global user.email test@runoob.com
```
--global : 
1）更改的配置文件就是位于用户目录下的那个，所有的项目将会默认使用这里的配置的用户信息；
2）想在某个特定的项目中使用其他的名字或者邮件，只要去掉--global 这个选项重新配置 ，新的设置保存在当前项目的.git/config 里面；


```
git config --list // 查看配置的信息
vim ~/.gitconfig  上面展示的信息就是在这里；
```

5、git的一般工作流程：
* 克隆 Git 资源作为工作目录。
* 在克隆的资源上添加或修改文件。
* 如果其他人修改了，你可以更新资源。
* 在提交前查看修改。
* 提交修改。
* 在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。

一般的工作提交代码的流程我们已经知道了大概了；

6、Git 工作区、暂存区和版本库
* 工作区：就是你在电脑里能看到的目录。
* 暂存区：英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
* 版本库：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

![git的目录树](../../../../asset/Snip20190318_1.png)
1）图中左侧为工作区，右侧为版本库；
暂存区（stage, index）：标记为 "index" ；
目录树 ： 标记为 "master" 的是 master 分支所代表的目录树。
"HEAD" : 实际是指向 master 分支的一个"游标"。所以图示的命令中出现 HEAD 的地方可以用 master 来替换。
objects : 标识的区域为 Git 的对象库，实际位于 ".git/objects" 目录下，里面包含了创建的各种对象及内容。

git add (命令):在工作区执行git add  命令的时候， 
1）暂存区的目录树被更新；
2）同时工作区修改文件内容被写入到对象库的一个新的对象中；
3）对象的ID被记录到缓存区的索引中。

git commit ：
1）暂存区的目录树写到版本库（对象库）中；
2）master 分支会做相应的更新（master 指向的目录树就是提交时暂存区的目录树）。

git reset HEAD：
1）暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。

git rm --cached <file> ：命令时，会直接从暂存区删除文件，工作区则不做出改变。

git checkout . | git checkout -- <file>：
1）会用暂存区全部或指定的文件替换工作区的文件。
2）！！！这个操作很危险，会清除工作区中未添加到暂存区的改动。

git checkout HEAD . | git checkout HEAD <file>：
1）会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。
2）这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。

6、git创建仓库
>git init 初始化一个仓库, 会自动生成一个.git 目录
git init newrepo 指定目录作为仓库
git add *.c
git add README
git commit -m '初始化项目版本'

git 拷贝项目
git clone <repo>  克隆到当目录下
git clone <repo> <directory>  克隆到指定的目录 repo :git 仓库 directory： 克隆到这里的目录

7、git的基本操作
http://www.runoob.com/git/git-basic-operations.html





