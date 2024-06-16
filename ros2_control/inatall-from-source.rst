源码安装ros2_control
=======================

1.新建ros2Control_ws
------------------------

* 下载所有储存库

.. code-block:: bash

   mkdir -p ~/ros2Control_ws/src
   cd ~/ros2Control_ws/
   wget https://raw.githubusercontent.com/ros-controls/ros2_control_ci/master/ros_controls.humble.repos
   vcs import src < ros_controls.humble.repos

* 安装依赖项

.. code-block:: bash

   rosdep update --rosdistro=humble
   sudo apt-get update
   rosdep install --from-paths src --ignore-src -r -y

.. note::
  
   使用rosdep 需要先 update和init。如果使用rosdep会失败，可以使用国内版本的rosdep-->rosdepc
   使用 ``sudo pip install rosdepc`` 下载。同时相应的需要将 rosdep替换为rosdepc

* 构建一切

.. code-block:: bash

   . /opt/ros/humble/setup.sh
   colcon build --symlink-install

**ros2_control的源代码内提供了一系列的demo实例,编译完成后可以试着运行一下**



.. contents:: Table of Contents
   :depth: 4
   :local: