---
title: git、svn之我用
date: 2019-03-27 16:36:13
tags:
categories: [工具使用]
---

git和svn的命令这么多，脑袋不够记怎么办，不如使用`git help`和`svn help`来帮你吧

`git tag`不会用，试试看`git help tag`，`git bisect`不会用，试试看`git help bisect`。
同样的，`svn patch`不会用，试试看`svn help patch`，`svn revert`不会用，试试看`svn help revert`。

具体的命令不会用时，别急着先去Google或者百度，不妨先看看它的help，以下是我整理的常用的命令：

<!--more-->
### Git常用命令列表

| 命令 | 解释 |
| --- | --- |
| git config [--global] -l | 查看配置信息 |
| git config --global user.name xxx | 配置用户名 |
| git config --global user.email xxx | 配置邮箱地址 |
| git config --global commit.template ~/git.commit.template| 配置提交模板 |
| git config --global core.editor vi | 设置使用的文本编辑器 |
| git config --global color.ui auto | 设置输出为彩色 |
| git init | 把当前的目录变成可以管理的git仓库 |
| git clone xxx | clone某个仓库到本地 |
| git add xxx | 把xxx文件添加到暂存区 |
| git rm xxx | 删除xxx文件 |
| git clean -dfx | 清除本地修改文件 |
| git commit  files  –m “xxx” | 提交文件 –m 后面的是注释 |
| git commit -a files | 使用提交模板提交文件|
| git commit –-amend | 修改提交的信息或文件 |
| git status [-uno] | 查看仓库状态 |
| git diff xxx [--cached]| 查看xxx文件修改了那些内容 |
| git log [--grep=] | 查看历史记录 （-p 显示具体修改）|
| git reflog | 查看所有历史 包括回退历史 |
| git merge dev | 在当前的分支上合并dev分支 |
| git branch | 查看当前所有的分支 （-r 查看远程分支） |
| git branch –d dev | 删除dev分支 |
| git branch name | 创建分支 |
| git branch -a --contains <commit> | 根据 commit 查找 git 分支名 |
| git stash [show&#124; pop&#124; apply&#124; clear] | 把当前的工作隐藏起来 等以后恢复现场后继续工作 （git help stash） |
| git remote | 查看远程库的信息(-v 详细信息) |
| git checkout -b <branch> | 创建并切换到新分支 |
| git checkout -- xxx | 丢弃xxx文件工作区的改动 |
| git checkout master | 切换到master分支  （git checkout -b 创建并切换） |
| git reset --hard <commit> | 回到删除的版本位置  |
| git reset HEAD xxx | 撤出暂存区 |
| git revert <commit> [-n]| 重置一个提交 |
| git cherry-pick <commit>  | 合并某次提交（-n 只合并）|
| git apply xxx.patch | 打入patch |
| git push origin HEAD:refs/for/refs/heads/branchName | 把master分支推送到远程库对应的分支上 |
| git push <remote> --delete <branch> | 删除远程端分支 |
| git pull [-r]  | 将服务器上的代码同步到本地 |
| git fetch | 下载远程端版本，但不合并到HEAD中 |
| git rebase HEAD~3 -i | 修改已commit的信息 |
| git blame xxx [-L50，100] | 文件xxx每行的修改记录 |
| git grep $regexp $(git rev-list --all)| 查找修改记录 |
| git tag –a <标签名> -m “标签说明” | tag的用法 git help tag |
| git push origin refs/tags/<标签名> | 推送tag到中央仓库 |
| git checkout refs/tags/<标签名> | 切换到tag |
| git tag -d <标签名><br>git push origin :refs/tags/<标签名> | 删除tag |


### svn常用命令列表

| 命令 | 解释 |
| --- | --- |
| svnadmin create | svn仓库的创建/删除 |
| htpasswd [-cmdpsD] passwordfile username | svn 用户添加/修改/删除 |
| svn co url | 从服务器上下载代码 |
| svn co --depth=empty url  work_dir <br>cd work_dir; svn up xxxx | 从服务器checkout出单个文件 |
| svn add [delete &#124;rename] | 文件增删 改名 |
| svn ci files -m "log" | 将files上传到服务器，"xxx"为修改日志 |
| svn up -r <versionNum> | 更新到指定版本号 |
| svn st [-q] | 查看当前文件状态 |
| svn revert * -R | 恢复本目录下的文件 |
| svn diff xxx | 查看文件的修改内容 |
| svn cleanup | 清除锁定的文件 |
| svn log [-v .] -r <versionNum> &#124;less | 查看某个版本号修改了哪些文件及日志 |
| svn info | 查看svn的版本号、服务器地址等信息 |
| svn st &#124; grep '^?' &#124; awk '{print $2}' &#124; xargs rm -rf | 删除某些文件 |
| svn diff -r5452:5476 > a.patch<br>svn patch a.patch | svn 合并某一版本提交的代码 |
| svn merge xxx@versionNum yyy . | 合并某一分支versionNum以后的修改 |
| svn merge dev@100 dev@101 . | 合并dev分支的101修改到本目录 |
| svn sw --relocate oldIP/dir newIP/dir | linux下修改svn的URL |
