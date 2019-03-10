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
