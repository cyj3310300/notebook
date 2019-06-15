# ubuntu使用经验
### 系统python
- ubuntu18.04默认安装了python3.x和python2.x
- 但是默认使用的好像是python2.x，可以终端执行python看下
- 当需要使用python3.x时候，要显示的调用python3。
- 给python3.x安装包的时候也需要使用pip3

### sogou输入法输入中文时，若候选栏显示乱码、无法显示中文，可按如下方式处理：
```
cd ~/.config
rm -rf SogouPY* sogou*
```
然后重启后登录即可。
### vim 的使用
- 新建一个test.txt文件并用vim打开
```
vim test.txt
```
- i 键输入模式，输入结束后，esc键退出输入模式，输入：进入底线命令模式，然后有下面几种命令，输入以enter键结束
```
:q   不保存退出
:q! 强制退出
:wq 保存退出
:set number 显示行号
:set nonumber 隐藏行号
```

### 文件权限
- ls -l中显示的内容如下：
```
-rwxrw-r‐-1 root root 1213 Feb 2 09:39 abc
-rwxrw-r‐-   10个字符确定不同用户能对文件干什么
```
	- 第一个字符代表文件（-）、目录（d），链接（l）
	- 其余字符每3个一组（rwx），读（r）、写（w）、执行（x）
	- 第一组rwx：文件所有者的权限是读、写和执行
	- 第二组rw-：与文件所有者同一组的用户的权限是读、写但不能执行
	- 第三组r--：不与文件所有者同组的其他用户的权限是读不能写和执行, 也可用数字表示为：r=4，w=2，x=1  因此rwx=4+2+1=7
	- 1 表示连接的文件数
	- root 表示用户
	- root表示用户所在的组
	- 1213 表示文件大小（字节）
	- Feb 2 09:39 表示最后修改日期
	- abc 表示文件名

- 改变权限的命令
```
chmod 改变文件或目录的权限
chmod 755 abc：赋予abc权限rwxr-xr-x
chmod u=rwx，g=rx，o=rx abc：同上u=用户权限，g=组权限，o=不同组其他用户权限
chmod u-x，g+w abc：给abc去除用户执行的权限，增加组写的权限
chmod a+r abc：给所有用户添加读的权限
```

### ubuntu远程win
目前该方法只适用于在同一个局域网内可实现.
- - 首先安装rdesktop
```
sudo apt install rdesktop
```
- win端设置
	- 我的电脑->属性->远程->远程协助(打钩)&远程桌面(允许,下面不要钩)
- 全屏连接
```
   rdesktop -f -a 16  192.168.1.112
   
   -f 全屏模式,从全屏模式切换出来按Ctrl+Alt+Enter,是最大的窗口模式
   -a 连接颜色深度（最高到16位），一般选16才会显示真彩色（window7支持32位）
```
- 窗口模式
```
rdesktop -g 800*600 -a 16 192.168.0.101
-g 桌面大小
以800*600（W＊H）窗口大小、真彩色、打开远程192.168.0.101
```

### 浏览器安装flash
```
sudo apt install adobe-flashplugin
```