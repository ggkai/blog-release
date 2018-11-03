---
title: git初学
date: 2018-11-03 22:58:18
tags:
---
用githubPages+hexo写博客，用pycharm学习写代码，需要在多台电脑同步，所以学了一些简单的git的技巧。BON
<!-- more -->
# 一、基本概念
1. 仓库repository  
emote repository：公共的仓库  
local repository：本地文件夹

2. 工作流程  
untracked-unmodified-modified-staged  
第一步，在工作目录，创建实际文件  
第二步，git add添加文件到缓存区（Index），临时保存改动  
第三步，git commit提交本地改变到HEAD  
第四步，git push从本地仓库的HEAD推送到远程仓库  

3. 分支  
master 是“默认的”分支

# 二、常用技巧
git --version #查看git版本号  
which git#查看git路径  
git config --list查看user和name  
git clone /path/to/repository#本地仓库的克隆版本  
git clone username@host:/path/to/repository#远程仓库克隆

git init#创建本地仓库，生成.git隐藏文件  
git add file#添加文件  
git add file1 file2#添加多个文件  
git add -all#添加所有文件，或者add .  
git status#查看文件状态  
git commit -m 'add test.sh'#提交到仓库，并添加注释  
git cmmit -am ''#对已有的文件add并commit  
git remote add origin https://github.com/uername/repository.git#关联远程仓库  
git push origin master#主分支提交到远程  
git pull origin master#从远程拉数据  

git branch#查看分支  
git branch -r#查看分支，详细  
git branch <branch> #创建新分支  
git checkout -b <branch>#创建分支并切换  
git checkout master#切换到主分支  
git branch -d <branch>#删除分支  
git mer dev#在master状态下，分支合并到master  
git merge  --no--ff -m ''   <branch>#在master状态下，从分支改变合并到master，保留merge信息  
git push origin <branch>#推送分支到远程仓库  

git show hash值#根据hash值查看详细提交日志  
git log#提交日志  
git log --name-only#提交日志，详细  
git log --name-status#查看文件改变  
git log --oneline#commit ID和commit描述一行显示  
git log --oneline --graph#画commit分支结构  

git reset file#对某个文件回到add之前  
git reset --hard HEAD#回退到上个commit  
git reset --hard <commit ID号> #回退到某个commit版本  
git checkout -- <filename>#从head覆盖到工作目录的文件  
git checkout id -- file #回到某个commit版本的文件  
git fetch origin+git reset --hard   origin/master#远程覆盖本地  


# 三、遇到问题
1. git 报错：missing xcrun  
需要重新安装：xcode-select --install
2. github仓库重命名  
github进入setting中修改，仓库名可以和本地文件名不一样
3. xcode更新后git报错:Can't start Git:/usr/bin/git  
需要重新安装：xcode-select --install，安装并重启xcode
4. git警告：core.autocrlf  
系统换行符不一致导致

# 四、参考
[图解Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)  
[git book](https://git-scm.com/book/zh/v2)