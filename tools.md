## git_github安装使用



## git中：关于origin和master

> git的服务器端(remote)端包含多个repository，每个repository可以理解为一个项目。而每个repository下有多个branch。"origin"就是指向某一个repository的指针。服务器端的"master"（强调服务器端是因为本地端也有master）就是指向某个repository的一个branch的指针。

这是服务器端(remote)的情况：
![1.png](https://github.com/cyj3310300/notebook/blob/master/pic/1.png?raw=true)

而在本地电脑(local)上：
- "master"就是指向刚刚从remote server传到本地的副本branch。
- ```$git push A B:C```     其中A和C是分别remote端的一个repository的名字和branch的名字，B是本地端branch的名字
意思是把本地的B推送到remotes/A/C下。当B=C时可以直接省略为：git push A B。
- 比如：```"git push origin master:master"``` 可以直接省略为"git push origin master".
- 
---