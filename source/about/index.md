---
title: 关于自己
date: 2018-09-18 13:25:49
type: "about"
---

开发中涉及到的一些笔记，eg：iOS等。

有关的内容进行实现的过程是怎么样的？

```
1> 分类： 是从业务上进行分类
2> 标签： 是从编程语言上进行分类
```

注意事项； hexo 这个日志一定要使用系统自带的，
nvm list 列出对应的npm版本 (看到有system的分类)
nvm use system  使用系统的版本

太久没有用了，可能出现的问题：
Please make sure you have the correct access rights and the repository exists. FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html Error: Permission denied (publickey). fatal: Could not read from remote repository. Please make sure you have the correct access rights and the repository exists.

这个很可能就是ssh的key出现了问题，过期等等
在自己的本地主机中的.ssh/id_rsa.pub 拷贝添加到github上面的项目中，注意消息名字要对
然后执行： hexo clean && hexo g && hexo d

