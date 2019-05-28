# ubuntu软件安装
记录使用ubuntu下的经验、方法、心得体会
### *1.系统安装*
- 如果是只安装一个系统，直接“下一步”安装就好。
- 如果是安装“双系统”
	- Swap（相当于电脑内存）：逻辑分区、大小设置为电脑内存大小，2G，4G；
	- /boot（引导分区）：主分区：大小设置为200M；
	- /home（用户存储数据用）：逻辑分区，要尽可能大，100G空间可以设置为85G，留10G给主分区即可。
	- /.（主分区）：主分区，用于存放系统，相当于win7的C盘，10G即可。
- 软件和更新->下载自->其他站点->中国->mirros.aliyun.com

### *2.安装软件*
#### 使用默认的python3.6
- 安装pip
```
sudo apt install python-pip
sudo apt install python3-pip
```
- 更改下载源。修改 ~/.pip/pip.conf (没有就创建一个文件夹及文件。文件夹要加“.”，表示是隐藏文件夹)
内容如下：
```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host=mirrors.aliyun.com
```
### miniconda3：
- [下载miniconda](https://docs.conda.io/en/latest/miniconda.html)
- 安装:  bash Miniconda3-latest-Linux-x86_64.sh
- 使用这个命令，激活刚才的安装：source ~/.bashrc
- 更改为清华源
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```
- 创建一个新环境：conda create -n python36 python=3.6
- 激活环境：conda activate python36
- 安装需要的包：conda install keras numpy pillow matplotlib

### pycharm
- [下载linux版](https://www.jetbrains.com/pycharm/)
- 解压缩到 /usr/local/目录下
- sh /usr/local/pycharm/bin/pycharm.sh
- 将程序添加快捷方式
	- 第一步：
```
sudo gedit /usr/share/applications/Pycharm.desktop
```
	- 第二步：
```
[Desktop Entry]
Type=Application
Name=Pycharm
GenericName=Pycharm3
Comment=Pycharm3:The Python IDE
Exec=sh ～/Downloads/pycharm-2017.1.4/bin/pycharm.sh
Icon=～/Downloads/pycharm-2017.1.4/bin/pycharm.png
Terminal=pycharm
Categories=Pycharm;
 ```
 
### jupyter notebook
- 安装
```
pip3 install jupyter  # 在python3下安装
pip install jupyter　　＃　在python2下安装
```
- 打开
```
jupyter notebook
```
- 使用

### 微信
```
sudo apt install snapd snapd-xdg-open
sudo snap install electronic-wechat
electronic-wechat
```
### 印象笔记插件
```
sudo add-apt-repository ppa:nixnote/nixnote2-daily
sudo apt update
sudo apt install nixnote2
```
在登录国服时候，输入完邮箱地址一直不会显示密码框，这个时候点击左上角的“印象笔记”链接，然后会打开网页版的印象笔记页面，在里面找到登录页面，正常登录。然后关闭登录框，再从'工具'中的同步进入，这个时候就会看到授权提示了。

### 安装cpu,ram,网速监控插件：
```
sudo add-apt-repository ppa:fossfreedom/indicator-sysmonitor
sudo apt-get update
sudo apt-get install indicator-sysmonitor
indicator-sysmonitor &
```
* Ctrl+C就可以实现后台运行indicator-sysmonitor
* 鼠标右键点击标题栏上图标->弹出菜单->选择首选项->Run on startup开机启动-> Advanced 添加上net:{net}
### 安装moeditor markdown软件
- [下载moeditor](https://github.com/Moeditor/Moeditor/releases/tag/v0.2.0-beta)
```
sudo apt-get -f install    # 安装需要的依赖包
sudo dpkg -i moeditor_0.2.0-1_amd64.deb
```
### 安装wine：
- wine是基于32位架构的，现在计算机基本上都是64位，因此需要启用32位架构，如果计算机是32位的则忽略此步。  
```
sudo dpkg --add-architecture i386
```
- 添加软件源。
```
wget -nc https://dl.winehq.org/wine-builds/Release.key
sudo apt-key add Release.key
sudo apt-add-repository https://dl.winehq.org/wine-builds/ubuntu/
sudo apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ xenial main'
```
- 添加公钥
```
sudo apt-key adv --recv-keys --keyserver keyserver.Ubuntu.com F987672F
```
- 更新软件包。
```
sudo apt-get update
```
- 选择一个wine稳定版或发行版安装。
```
sudo apt install wine-stable 　#稳定版
sudo apt install wine-development　#发行版
```
- 测试是否安装成功
```
wine --version     #如果出现wine的版本则说明安装成功
```
- 使用
	- 将windows下的安装执行文件拷到ubuntu下的某一目录，在命令行下执行 wine xxx.exe,
	- wine程序安装在/opt目录，安装的win软件在~/.wine/drive_c目录下。
	

### 安装opencv
- 更新数据
```
sudo apt-get update
sudo apt-get upgrade
```
安装依赖包
```
sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
```
E: 无法定位软件包 libjasper-dev，使用一下命令安装
```
sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
sudo apt update
sudo apt install libjasper1 libjasper-dev
```

- [下载openc3.4.1数据包](https://github.com/opencv/opencv/releases)
- 解压
```
sudo unzip opencv-3.4.1.zip
cd opencv-3.4.1
sudo mkdir build
cd build
```
- 使用CMAKE安装opencv
```
sudo cmake -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=ON -D WITH_OPENGL=ON ..
```
等一会下载ippicv_2017u3_lnx_intel64_general_20170822.tgz，可手动下载(https://github.com/opencv/opencv_3rdparty/blob/ippicv/master_20170822/ippicv/ippicv_2017u3_lnx_intel64_general_20170822.tgz)
```
sudo cmake ..
sudo apt-get install libgazebo9 libgazebo9-dev    # 如果下一步不行，执行这一步
```
- 进行MAKE创建编译
```
sudo make -j4   # 4表示的是电脑4核，一定要有sudo，否则没权限,这一步有绿色的滚动，有一段时间
```
- 成功后，进行安装
```
sudo make install
```
执行完毕后OpenCV编译过程就结束了，接下来就需要配置一些OpenCV的编译环境。

- 首先将OpenCV的库添加到路径，从而可以让系统找到,在配置之前，由于修改系统配置文件需要权限，请将身份转变成root
```
sudo -s
```
- 修改opencv.conf文件
```
sudo gedit /etc/ld.so.conf.d/opencv.conf
```
- 文本可能为空白，在文本里添加opencv库的安装路径
```
/usr/local/lib
```
- 更新系统共享链接库
```
sudo ldconfig
```
- 再修改bash.bashrc文件
```
sudo gedit /etc/bash.bashrc
```
- 在末尾加入
```
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig  
export PKG_CONFIG_PATH  
```
- 保存退出，然后执行如下命令使得配置生效
```
source /etc/bash.bashrc
```
- 查看opencv版本
```
pkg-config --modversion opencv
```
- 编辑测试程序，测试是否安装成功
	- cd到opencv-3.4.1/samples/cpp/example_cmake目录下，我们可以看到这个目录里官方已经给出了一个cmake的example我们可以拿来测试下，按顺序执行：
```
cmake .
make
./opencv_example
```
- 打开了摄像头，在左上角有一个hello opencv，即表示配置成功


**测试一**：
- 新建一个opencv_demo.cpp文件：
```
#include<iostream>
#include<opencv2/opencv.hpp>
using namespace std;
using namespace cv;
int main()
{
	Mat src = imread("test.png");
	imshow("src",src);
	waitKey(5000);
	return 0;
}
```
- 新建一个CMakeLists.txt
```
cmake_minimum_required(VERSION 3.5)
project(test1)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_executable(${PROJECT_NAME} opencv_demo.cpp)
target_link_libraries(${PROJECT_NAME} opencv_core opencv_highgui opencv_imgcodecs)
```

- 在以上文件目录下：
```
mkdir build # 创建目录
cd build # 进入目录
cmake .. # cmake自动查找父目录下的CMakeLists.txt文件
make # 编译生成test1可执行文件
```
将需要的图片文件放在build目录下
```
./test1 # 运行可执行文件,
```

**vscode中使用：**参考(https://www.jianshu.com/p/6d3f4a30945d)
- 配置好以下c_cpp_properties.json、launch.json、tasks.json 3个文件
	- c_cpp_properties.json
```
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/local/include",     //确保下面是有opencv和opencv2文件夹
                "/usr/include"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "clang-x64"
        }
    ],
    "version": 4
}
```
	- launch.json
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/${fileBasenameNoExtension}.o",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "/usr/bin/gdb",
            "preLaunchTask": "g++",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        },
    ]
}
```
	- tasks.json
```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "command": "g++",
    "args": [
        "-g", "-std=c++11", "${file}", "-o", "${fileBasenameNoExtension}.o",// 设置动态链接库
        "-I", "/usr/local/include",
        "-I", "/usr/local/include/opencv",
        "-I", "/usr/local/include/opencv2",
        "-L", "/usr/local/lib",
        "-l", "opencv_core",
        "-l", "opencv_imgproc",
        "-l", "opencv_imgcodecs",
        "-l", "opencv_video",
        "-l", "opencv_ml",
        "-l", "opencv_highgui",
        "-l", "opencv_objdetect",
        "-l", "opencv_flann",
        "-l", "opencv_imgcodecs",
        "-l", "opencv_photo",
        "-l", "opencv_videoio"
    ],// 编译命令参数
    "problemMatcher":{
        "owner": "cpp",
        "fileLocation":[
            "relative",
            "${workspaceFolder}"
        ],
        "pattern":[
            {
                "regexp": "^([^\\\\s].*)\\\\((\\\\d+,\\\\d+)\\\\):\\\\s*(.*)$",
                "file": 1,
                "location": 2,
                "message": 3
            }
        ]
    },
    "group": {
        "kind": "build",
        "isDefault": true
    }
}
```
- 创建一个opencv_test.cpp文件
```
#include<opencv2/opencv.hpp>
using namespace cv;
int main()
{
	Mat img = imread("test.png");
	imshow("df",img);
	waitKey(5000);
	return 0;
}
```
### 安装使用darknet
```
git clone https://github.com/pjreddie/darknet.git  //下载源码
cd darknet  //cd到该目录下
make　//make以下
wget https://pjreddie.com/media/files/yolov3.weight　　//下载权值文件
./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg　 //测试图片
```
### 安装labelImg
- Python 2 + Qt4
```
sudo apt-get install pyqt4-dev-tools
sudo pip install lxml
git clone https://github.com/tzutalin/labelImg.git
cd labelImg
make all  # 如果不行，执行这个：pyrcc4 -o resources.py resources.qrc 
python labelImg.py  #打开labelImg
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```
- Python 3 + Qt5
```
sudo apt-get install pyqt5-dev-tools
sudo pip3 install lxml
git clone https://github.com/tzutalin/labelImg.git
cd labelImg
make all  # 如果不行，执行这个：pyrcc5 -o resources.py resources.qrc
python3 labelImg.py  #打开labelImg
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```
