---
title: Git常用语句
date: 2019-04-18 11:29:50
tags: Git
description: 最近又在作死研究Git，发现自己一些常用的基本语法根本记不住，所以就写在这里，以防万一。本人是个萌新，如有错误请回.....emmmmmmm   好像没开评论，算了算了，有时间再说吧。大多数都是我从Git官网和一些大佬博客上总结（抄）出来的。
---
# 首先配置账号和邮箱
 - 具体为什么要配我也不是记得很清楚,反正很重要就是了
 1. `$ git config --global user.name "账号"`
 2. `$ git config --global user.email "邮箱"`

# 正常流程
1. 创建仓库
2. 创建或修改文件
3. 使用`git add`命令添加新创建或修改的文件到本地的缓存区（Index）
> 如果是刚创建首先将文件添加到跟踪文件内
4. 使用`git commit`命令提交到本地代码库
5. （可选，有的时候并没有可以同步的远端代码库）使用`git push`命令将本地代码库同步到远端代码库

## 1. 创建仓库
- Git有两种仓库形式，一种是用clone克隆下来，另外一种是用代码直接创建一个
1. `$ git init`    
> 这个语句会在你所执行的目录下面创建一个.Git的隐藏文件夹，所有Git需要的数据和资源都存放在这个目录中，不过现在，仅仅是按照既有的结构框架初始化好了里边所有的文件和目录
2. `$ git clone git://github.com/schacon/grit.git`
> 上边clone后面的参数是你自己远程仓库的url，和`Git init`一样，会在目录下创建一个.Git的隐藏文件夹


## 2. 检查文件
- 首先要确定哪些文件当前处于什么状态
`$ git status`
> 如果在克隆仓库之后立即执行此命令，会看到类似这样的输出：
```
$ git status
On branch master
nothing to commit, working directory clean
```
这说明你现在的工作目录相当干净。换句话说，所有已跟踪文件在上次提交后都未被更改过。此外，上面的信息还表明，当前目录下没有出现任何处于未跟踪的新文件，否则 Git 会在这里列出来。最后，该命令还显示了当前所在的分支是 master，这是默认的分支名称，实际是可以修改的，现在先不用考虑。

## 3. 添加文件到本地缓存区
- 修改或创建文件后运行 `$ git status` 会看到该文件出现在未跟踪文件列表中：
```
$ vim README
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        README

nothing added to commit but untracked files present (use "git add" to track)
```
- 这句话表示你创建了一个名叫README的文件，并且没有跟踪文件，这里需要你手动进行跟踪，Git不会自动帮你。（修改也是一样，在改后需要手动跟踪一下）
- 只要是出现在 `Untracked files:`这句话下面的文件就是没有被Git追踪的，下次将不会提交
> 这里的跟踪文件表示Git会帮你监控文件夹的变化，比如你创建了什么文件或者删除添加了代码以及各种文件变化

`$ git add 文件名`
> 这句代码可以将文件加入到跟踪文件内，下次将一并提交。没有在跟踪目录内的文件Git将会忽略

> 也可以将文件名改成绝对路径的目录，如：`$ git add c:/git/`,将这个目录下所有文件添加到跟踪文件

- 这个时候再`$ git status`下：
```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   README
```
- 只要在 “Changes to be committed” 这行下面的，就说明是已暂存状态。可以提交了。
- 可以在将文件加入到追踪文件夹之后修改文件，这时候Git会列出所有被追踪而且被更改的文件
比如：

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
```
> 只要是出现在 `Changes to be committed:`下面的文件就表示文件已经被追踪而且被修改了，这时候需要再将文件`$ git add README`一次，将文件添加到暂存文件中。

*注：*
- Git官网上还提到了一种特殊的情况：如果你现在在`README`中修改了代码，会发什么什么呢？
```
$ vim README
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README
```
> 怎么回事？ `README` 文件出现了两次！一次算未暂存，一次算已暂存，这怎么可能呢？好吧，实际上 Git 只不过暂存了你运行 `$ git add` 命令时的版本，如果现在提交，那么提交的是添加注释前的版本，而非当前工作目录中的版本。所以，运行了 `$ git add` 之后又作了修订的文件，需要重新运行 `$ git add` 把最新版本重新暂存起来：
```
$ git add README
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
 
        modified:   README
```

## 4. 提交到本地代码库
  一切就绪，准备提交
> `$ git commit -m "你想在提交时写的信息"`
 - 如果你关联了远程代码库这时候就可以推送数据到远程端代码库了

## 5. 推送数据到远程仓库
`$ git push origin hexo`
> 其中的hexo是我的远程代码分支，改成你自己的分支或者去掉变成默认


# <center>完</center>