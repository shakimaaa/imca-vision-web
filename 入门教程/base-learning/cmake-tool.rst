cmake安装和基本使用
=====================

1安装cmake
-------------

1.1.指令安装
~~~~~~~~~~~~~~~~

.. code-block:: bash
   
   sudo apt install cmake  #下载版本可能不是最新的

1.2.源码安装
~~~~~~~~~~~~~

* 第一步：卸载原来的cmake版本:

.. code-block:: bash

   sudo apt-get remove cmake

* 第二步：去 `cmake官网 <https://cmake.org/download/>`__ 下载linux版本源码安装包

* 第三步：在cmake源码所在文件夹中打开命令终端，解压文件

.. code-block:: bash

   tar -zxv -f cmake-x.x.x.tar.gz  #'x.x.x.' 是对应的版本

* 第四步：进入解压后的cmake文件，执行：

.. code-block:: bash

   ./bootstrap

* 第五步：编译构建

.. code-block:: bash

   make

* 第六步：安装

.. code-block:: bash

   sudo make install

* 第七步：验证

.. code-block:: bash

   cmake --version









2024.6.3 Shakima

.. contents:: Table of Contents
   :depth: 3
   :local:
