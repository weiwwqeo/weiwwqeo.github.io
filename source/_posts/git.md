---
title: Git
categories: '-计算机'
date: 2024-2-16
abbrlink: 69c3279c
---

# Git

ref:[14.GUI工具_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1HM411377j) by GeekHour

##### 一些教程

* <https://www.runoob.com/manual/git-guide/>

## 什么是Git

* Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

## git速成

### 创建仓库

`git init` 将当前文件夹新建为仓库\
`git clone /path/to/repository` 创建一个本地仓库的克隆版本\
`git clone username@host:/path/to/repository` 克隆远程仓库

### 常见指代

* `HEAD`指代分支的最新提交节点
* `HEAD~` / `HEAR^` 指上一个版本
* `HEAD~3` 上第三个版本

### 工作流

<img src="/img/git_learn/workflow.jpg" style="zoom:70%;" />

<img src="/img/git_learn/workflow1.jpg" style="zoom:70%;" />

<img src="/img/git_learn/workflow2.jpg" style="zoom:70%;" />

* `git status` #查看仓库状态
* `git add <filename>` / `git add *` #添加文件到暂存区
* `git commit -m "代码提交信息"` #提交代码到本地仓库
* `git remote add origin <server>` #将本地仓库链接到远程仓库
* `git push origin master` #提交到远程仓库，branch为master，可以改成别的branch
* `git log` / `git log --oneline` #查看提交历史，可以获取提交版本ID。 --oneline可以让显示更简洁
* `git tag 1.0.0 1b2e1d63ff` #指定版本标签1.0.0, 1b2e1d63ff是版本ID的前10位
* `git ls-files` #查看暂存区文件 注，直接ls是查看工作区文件

```bash
~/git/git_learn master ❯ echo "这是第一个文件">file1.txt

~/git/git_learn master ?1 ❯ git status                                          
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file1.txt
nothing added to commit but untracked files present (use "git add" to track)

~/git/git_learn master ?1 ❯ git add file1.txt

~/git/git_learn master +1 ❯ git status                                            
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   file1.txt

~/git/git_learn master +1 ❯ git commit -m "the first commit"                                           
[master (root-commit) da89405] the first commit
 1 file changed, 1 insertion(+)
 create mode 100644 file1.txt

~/git/git_learn master ❯ git status                                            
On branch master
nothing to commit, working tree clean 
```

### 回退版本reset

<img src="/img/git_learn/reset.jpg" style="zoom:70%;" />
`git reset [--options] version` version处是版本号

### git diff

<img src="/img/git_learn/diff0.jpg" style="zoom:70%;" />

* `git diff`比较工作区与暂存区的文件
* `git diff HEAD` 比较工作区域本地仓库的内容
* `git diff --cache` 比较暂存区与本地仓库内容
* `git diff verID1 verID2` 比较两个版本间的差异

<img src="/img/git_learn/diff.jpg" style="zoom:70%;" />

### 删除文件 rm / git rm

<img src="/img/git_learn/rm.jpg" style="zoom:70%;" />

### .gitignore

忽略一些不用出现在版本库中的文件
直接用vim或别的编辑器打开.gitignore就好
一下是.gitignore

```
*.log #忽略所有日志文件
temp/ #忽略名为temp的文件夹
```

<img src="/img/git_learn/ignore.jpg" style="zoom:70%;" />
<img src="/img/git_learn/ignore1.jpg" style="zoom:70%;" />

## git分支与更新
列出分支：
`git branch`
创建一个叫做“feature_x”的分支，并切换过去：
`git checkout -b feature_x`  
切换回主分支：
`git checkout master`  
再把新建的分支删掉：
`git branch -d feature_x`  
将分支推送到远端仓库：
`git push origin <branch>`  
更新本地仓库`git pull`  
要合并其他分支到你的当前分支（例如 master），执行：
`git merge <branch>`  
在这两种情况下，git 都会尝试去自动合并改动。遗憾的是，这可能并非每次都成功，并可能出现冲突（conflicts）。 这时候就需要你修改这些文件来手动合并这些冲突（conflicts）。改完之后，你需要执行如下命令以将它们标记为合并成功：
`git add <filename>`  
在合并改动之前，你可以使用如下命令预览差异:  
`git diff <source_branch> <target_branch>`  

### SSH

*ref:<https://blog.csdn.net/weixin_42310154/article/details/118340458>*
git使用SSH配置， 初始需要以下三个步骤

* 使用秘钥生成工具生成rsa秘钥和公钥
* 将rsa公钥添加到代码托管平台
* 将rsa秘钥添加到ssh-agent中，为ssh client指定使用的秘钥文件

**SSH登录安全性由非对称加密保证，产生密钥时，一次产生两个密钥，一个公钥，一个私钥，在git中一般命名为id_rsa.pub, id_rsa。**

**那么如何使用生成的一个私钥一个公钥进行验证呢？**

本地生成一个密钥对，其中公钥放到远程主机，私钥保存在本地
当本地主机需要登录远程主机时，本地主机向远程主机发送一个登录请求，远程收到消息后，随机生成一个字符串并用公钥加密，发回给本地。本地拿到该字符串，用存放在本地的私钥进行解密，再次发送到远程，远程比对该解密后的字符串与源字符串是否等同，如果等同则认证成功。
通俗解释！！
**重点来了：一定要知道ssh key的配置是针对每台主机的！**，比如我在某台主机上操作git和我的远程仓库，想要push时不输入账号密码，走ssh协议，就需要配置ssh key，放上去的key是当前主机的ssh公钥。那么如果我换了一台其他主机，想要实现无密登录，也就需要重新配置。

下面解释开头提出的问题：
**（1）为什么要配？**
配了才能实现push代码的时候不需要反复输入自己的github账号密码，更方便
**（2）每使用一台主机都要配？**
是的，每使用一台新主机进行git远程操作，想要实现无密，都需要配置。并不是说每个账号配一次就够了，而是每一台主机都需要配。
**（3）配了为啥就不用密码了？**
因为配置的时候是把当前主机的公钥放到了你的github账号下，相当于当前主机和你的账号做了一个关联，你在这台主机上已经登录了你的账号，此时此刻github认为是该账号主人在操作这台主机，在配置ssh后就信任该主机了。所以下次在使用git的时候即使没有登录github，也能直接从本地push代码到远程了。当然这里不要混淆了，你不能随意push你的代码到任何仓库，你只能push到你自己的仓库或者其他你有权限的仓库！