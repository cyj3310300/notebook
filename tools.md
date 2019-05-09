## git_github安装使用
### 简单使用流程
- 机器绑定github账号
```
git config --global user.name【空格】 "GitHub的用户名"cyj3310300
git config --global user.email【空格】"GitHub的邮箱"1078938243@qq.com
```
使用命令,输出配置的信息,说明配置成功
```
git config --global user.name
git config --global user.email
```
- 创建一个目录，该目录就是一个版本库，里面所有多个小项目（文件夹）都包含在这个库中。为避免遇到各种莫名其妙的问题，目录名（包括父目录）不包含中文。
```
git init
```
表示初始化仓库，这个语句就表示这个仓库建好了，文件夹中出现一个.git的隐藏文件夹就是库文件，不要随便删改。如果出现问题，删了重新来一遍。
- 把添加到缓存区
```
git add  xxx.py //提交文件
git add  dirfile //也可以提交文件夹
``` 
- 把暂缓区文件全部提交到仓库区
```
git commit -m "解释说明性语句" 
```

### 修改文件的名字
```
git mv 原文件名 新文件名
git commit -m "更新了名字"
git push
```
### 删除一个文件
```
git rm xxx.py
git commit -m"删除了xxx.py"
git push origin master # 默认的使用git push 也可以
```
### 分支
- 创建新分支
```
git branch dev # 创建一个新分支dev
git checkout dev # 切换到新分支dev上
git branch # 该命令可查看目前存在的所有分支,及现在在什么分支上
git checkout -b dev表示创建并切换到dev分支上,相当于上面的两个命令
```
- 在分支下的工作
```
git add xxx.py 
git commit -m"dev分支下添加一个文件"
git push origin dev # 将该分支推送到远端,然后在远端就可以看到这个分支了
```
- 分支的合并
```
git checkout master # 合并前先回到主分支
git merge dev # 表示将dev分支合并到master主分支上
```
- 分支的删除
```
git checkout master # 删除分支之前必须先回到主分支
git branch -d dev  # 先删除本地分支
git branch -D dev # 如果分支没有合并,需要用此命令强制删除未合并的分支
git push origin --delete dev　　# 删除远程端的分支
```
## 工作区,暂存区,仓库区概念
- 工作区（working）：电脑磁盘上的那个目录就是工作区。
- 暂存区（Index）：使用git add命令把工作区的文件提交到暂存区。
- 仓库区（HEAD）：使用git commit命令把暂存区的所有文件全部提交到仓库区。
![s](https://github.com/cyj3310300/notebook/blob/master/pic/trees.png?raw=true)
## origin和master原理

> git的服务器端(remote)端包含多个repository，每个repository可以理解为一个项目。而每个repository下有多个branch。"origin"就是指向某一个repository的指针。服务器端的"master"（强调服务器端是因为本地端也有master）就是指向某个repository的一个branch的指针。

这是服务器端(remote)的情况：
![1.png](https://github.com/cyj3310300/notebook/blob/master/pic/1.png?raw=true)

而在本地电脑(local)上：
- "master"就是指向刚刚从remote server传到本地的副本branch。
- ```$git push A B:C```     其中A和C是分别remote端的一个repository的名字和branch的名字，B是本地端branch的名字
意思是把本地的B推送到remotes/A/C下。当B=C时可以直接省略为：git push A B。
- 比如：```"git push origin master:master"``` 可以直接省略为"git push origin master".
- 每个仓库都可以使用origin这个指针名字,不会冲突
---