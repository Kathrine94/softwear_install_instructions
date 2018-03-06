### 安装搜狗拼音：

网址：blog.csdn.net/iamplane/article/deails/70447517

### 安装teamviewer:

http://www.cnblogs.com/wmr95/p/7574615.html

### ubuntu16.04从源码编译opencv3.4.0

http://blog.csdn.net/cocoaqin/article/details/78163171 

1.官网下载OpenCV的安装包，本教程使用的是OpenCV3.4.0.下载链接http://opencv.org/releases.html，选择sources版本   

2.解压下载下来的zip包 

    unzip opencv-3.4.0.zip

3.进入到解压后的文件包中

4.安装依赖库，如果提醒需要apt-get update，那就先sudo apt-get update然后再执行下面的命令

    sudo apt-get install cmake
    sudo apt-get install build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg.dev libtiff4.dev libswscale-dev libjasper-dev

5.安装完cmake和一些需要的文件之后执行如下命令，创建编译文件夹build, 并进入到build文件夹内。

    mkdir build
    cd build

6.cmake一下，但同时应该将opencv与所指定的Python相关联，不然就是只能在ubuntu系统默认的Python2.7中可使用。(本代码是将OpenCV与anconda安装的Python3.6相关联)

    cmake -DBUILD_opencv_python3=ON -DPYTHON_LIBRARY=/home/test/anaconda3/lib/libpython3.6m.so -DCMAKE_INSTALL_PREFIX=/usr/local ..

期间可能会下载东西需要等一会。

7.进行编译，时间可能会比较长。

    sudo make

8.执行命令

    sudo make install

9.sudo make install 执行完毕后OpenCV编译过程就结束了，下面我们需要将一个.so文件放入python3.6的site-packages中。即将/build/lib/python3中的cv2.cpython-36m-x86_64-linux-gnu.so文件（其中，build文件为步骤5创建的）拷贝至/anaconda3/lib/python3.6/site-packages中。

10.接下来就需要配置一些OpenCV的编译环境，首先将OpenCV的库添加到路径，从而可以让系统找到。

    sudo gedit /etc/ld.so.conf.d/opencv.conf 

执行此命令后打开的可能是一个空白的文件，不需要在意这一点，只需要在文件末尾添加

    /usr/local/lib

11.执行如下命令是的刚才的配置路径生效

    sudo ldconfig

12.配置bash

    sudo gedit /etc/bash.bashrc  

在打开的文件的末尾添加如下内容

    PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig
    export PKG_CONFIG_PATH 

保存之后，执行如下命令是的配置生效

    source /etc/bash.bashrc  

更新

    sudo updatedb  

13.至此所有的配置都已经完成，打开Python输入import cv2若没有报错则成功安装OpenCV。

Ubuntu系统配置Git

http://blog.csdn.net/tina_ttl/article/details/51326684






