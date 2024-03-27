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

## 其他

```git config [--global or --local ] -l``` 查看git配置 

删除全局配置

```git config --global --unset user.name ```

```git config --global --unset user.email```

设置全局配置

```git config --global user.name xxx ```

```git config --global user.email``` xxx@xxx.com

### SSH

**在使用Git时配置SSH，首先需要执行以下三个关键步骤：**

1. 利用密钥生成工具生成RSA密钥对（私钥和公钥）。
2. 将生成的RSA公钥添加至代码托管平台。
3. 将RSA私钥添加至SSH代理中，以明确指定SSH客户端使用的密钥文件。

SSH登录的安全性是通过非对称加密来保障的。**在生成密钥时，会同时生成两个密钥，一个是公钥，一个是私钥，在Git中通常命名为id_rsa.pub和id_rsa。**

**如何利用生成的公钥和私钥进行验证呢？**你可以在本地生成一对密钥，将公钥放在远程主机上，而私钥则保存在本地。当本地主机需要登录远程主机时，会发送一个登录请求，远程主机收到请求后会随机生成一个字符串并用公钥加密，然后发送回本地。本地主机使用私钥解密该字符串，再将其发送回远程主机。远程主机会比对解密后的字符串与原始字符串是否相同，如果相同则认证成功。

简而言之，**SSH密钥配置是针对每台主机的。**比如，在某台主机上操作Git和远程仓库，想要在推送代码时无需输入账号密码，只需配置SSH密钥即可。如果更换到另一台主机，想要实现无密码登录，就需要重新配置SSH密钥。

为什么需要配置SSH密钥呢？这样可以避免在推送代码时反复输入GitHub账号密码，更加方便。每次使用新主机都需要配置吗？是的，每次在新主机上进行Git远程操作并实现无密码登录都需要配置。配置了SSH密钥后为什么不需要密码了呢？因为配置时将当前主机的公钥与GitHub账号关联起来，GitHub会认为是该账号的拥有者在操作这台主机，从而信任该主机。这样即使没有登录GitHub，也能直接从本地推送代码到远程仓库。不过需要注意，你只能将代码推送到自己的仓库或者其他有权限的仓库，而不能随意推送到任何仓库。

