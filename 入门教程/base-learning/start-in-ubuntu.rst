开始使用Ubuntu
==============

ubuntu系统相较于windows的优点
----------------------------------

在windows下使用visual studio开发c++程序时，每创建一个工程都必须不厌其烦的挨个设置每个第三方库的头文件目录、库文件目录、以及库文件名。
在实际大型项目的开发过程中，总是不可避免的会使用到大量的第三方库，而一旦用到第三方库，在windows系统上就会极其繁琐。使用ubuntu系统的一个好处就是开发环境配置方便。

ubuntu基本知识
-----------------

1. ubuntu硬盘与文件目录结构
~~~~~~~~~~~~~~~~~~~~~~~~~
    
   linux下所有硬盘分区要么直接作为根目录，要么是根目录下的一个子目录。如

   硬盘分区1挂载到根目录，即：/

   硬盘分区2挂载到根目录的子目录，如：/data

   在没有其他挂载的情况下，目录：/，下面的所有文件（除了目录：/data）都是保存在硬盘分区1中。而目录：/data，下面的所有文件都是保存在硬盘分区2中。

2. ubuntu常用文件目录及其作用
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  * /home：该目录下保存不同账户的用户文件。假如你的ubuntu有一个叫user的账户，那么 /home/user 下就保存着user账户的用户文件。如果还有一个叫foo的账户，那么 /home/foo 下就保存着foo账户的用户文件。
   
  * /root：该目录下保存着root账户的用户文件。root账户是ubuntu中的一个特殊账户，拥有最高读写权限，类似与windows中的管理员。
   
  * /etc：该目录下保存着各种软件的配置信息。
   
  * /usr：该目录下通常保存用户安装的各个软件、开发包等。
   
  * /proc：该目录下都是虚拟文件，用于监控系统的运行状态。
   
  * /dev：该目录下也是虚拟文件，用于保存各个设备驱动。
   
  * /mnt：该目录下通常保存外部存储设备。如U盘等设备，通常可以在该目录下访问。

3. ubuntu权限管理
~~~~~~~~~~~~~~~~~~

  通常来说，一个文件有9个权限可以设置，而这9个权限可以分为3类，分别是文件所有者权限，组权限和其他用户权限。
  其中这三类中，每类都包含3个权限，即读、写、执行。
  由于读、写、执行可以用三个2进制比特表示，所以这三个权限可以用一个8进制数表示，而一共有3类权限，所以一个文件的权限可以由三个8进制数表示。
  我们可以使用命令ls -l来查看当前目录下所有文件的权限。

  我们可以通过 ``chmod`` 命令修改文件的权限，基本用法是 ``chmod <权限> <文件名>`` ，比如 ``chmod 755 ./run``
  一个文件的权限可以由3个8进制数表示，这里就是一个典型的例子。

  由于有权限限制，在默认的用户权限下，我们通常只能修改目录 ``/home`` 下对应用户文件夹里的文件，而其他地方的文件都是无法修改的。
  为了获取修改任意文件的权限，我们可以使用 ``sudo命令`` 该命令会使得用户获得临时的 ``root权限`` 也就是类似于windows下的 **管理员权限**。这时我们就可以修改那些原本不能修改的文件了。

ubuntu系统常用指令
------------------

使用 ``CTRL + ALT + T`` 打开终端，我们的指令在终端输入运行

.. code-block:: bash

    pwd  #显示当前工作路径

    cd  #改变目录，用于输入需要前往的路径/目录
    cd ..     #directory name
    cd ..     #表示进入上层目录
    cd ../..  #进入上上层目录，后面还可以加更多。
    cd -      #表示返回上一次的目录
    cd ~      #进入home主目录，即/home/用户名的简写

    ls  #显示当前目录下的文件（不包括隐藏文件和缓存文件等）
    ls -a  #列出目录下所有文件

    mkdir  #创建目录，后面接上directory的名字
    mkdir imca  #创建一个名为的“imca”目录

    touch  #创建任意格式的文件 如.cpp .c .hpp等
    touch hello_imca.cpp  #创建hello_imca源代码

    rm  #删除文件
    rm -I <目录名>  #这样做会删除指定目录中的所有子目录和包含的文件

    apt/apt-get  #更推荐使用apt命令而不是apt-get命令，它的命令更精简而且易用
    sudo apt install <软件名>  #安装软件最简单的方式
    sudo apt list             #查看所有已安装的软件列表
    sudo apt search <软件名>   #搜索某个软件
    sudo apt remove <软件名>   #删除某个软件包
    sudo apt purge <软件名>    #删除某个软件包以及配置文件，更彻底
    sudo apt update           #更新相关命令
    sudo apt upgrade          #更新相关命令

    dpkg  #包管理工具
    dpkg -i <.deb后缀的软件名>    #i 表示 install(下载)
    dpkg -r <包的名字>           #r 表示 remove, 此种方法会保留配置文件
    dpkg -P <包的名字>           #直接全删了，配置也不会保留
    dpkg -l                     #查看安装列表
    dpkg -S <包的名字>           #搜索某个包

    <命令名> -h or --help  #如果碰到不会的命令，或者忘记了具体的options（操作选项），可以使用帮助命令

**以上指令根据笔者印象列举，更多可自行搜索**

.. note::
    有时在使用指令的时候需要root权限，需要在指令前加上 ``sudo`` 提升权限

搭建c/c++环境
-----------------

1. **C编译环境配置和使用**

使用以下指令进行C语言的环境的安装

.. code-block:: bash

    # 安装编译环境
    apt-get install gcc 
    # 查看版本
    gcc --version

接下来我们写一个HelloIMCA.c的文件并编译运行

.. code-block:: bash

    vim HelloIMCA.c  #打开终端输入这个指令，使用vim创建编辑c文件

在文件内添加下面内容

.. code-block:: C

    #include<stdio.h>
    int main(void){
    printf("Hello IMCA!\n");
    }

保存好后编译运行

.. code-block:: bash

    gcc HelloIMCA.c -o HelloIMCA  #  编译
    ./HelloIMCA                   #  运行

2. **c++编译环境配置和使用** 

使用指令进行环境安装

.. code-block:: bash

    apt-get install g++
    #  查看版本
    g++ --version
    #  查看该命令所有操作
    g++ --h

然后接下来我们用C++写一个HelloIMCA.cpp,

.. code-block:: bash

    vim HelloWorld.cpp

在文件内添加下面内容

.. code-block:: c++

    #include<iostream>
    using namespace std;
    int main(void){
    cout<<"Hello IMCA!"<<endl;
    }

保存后运行

.. code-block:: bash

    g++ HelloIMCA.cpp -o HelloIMCAcpp  #  编译
    ./HelloIMCAcpp   



2024.3.5 Shakima

.. contents:: Table of Contents
   :depth: 6
   :local: