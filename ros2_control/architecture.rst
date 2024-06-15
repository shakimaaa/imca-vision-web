框架
======

1. 架构图及说明
------------------

**下图为ros2_control的框架架构**

.. image:: images/1.png
   :width: 600 px

1.1 Controllers (控制器)
~~~~~~~~~~~~~~~~~~~~~~~~~~

这里包括三个控制器（Controller A, Controller B, Controller C），它们的职责是：

* 向控制器管理器（Controller Manager）请求接口。
* 一旦接口被授予，控制器可以使用这些接口来执行它们的功能。

1.2 Controller Manager (控制器管理器)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

控制器管理器的职责是：

* 接收控制器的接口请求。
* 将控制器的接口请求传递给资源管理器（Resource Manager）。
* 管理和协调控制器之间的接口请求。

1.3 Resource Manager (资源管理器)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

资源管理器的职责是：

* 管理状态接口（State Interface）和命令接口（Command Interface）。
* 为状态接口和命令接口分配资源。
* 将请求的接口分配给控制器管理器。

1.4 State Interface (状态接口)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

状态接口是只读的接口，负责读取硬件资源的状态信息，例如传感器数据。

1.5 Command Interface (命令接口)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

命令接口是读写接口，负责发送命令给硬件资源，例如向执行器发送控制信号。

1.6 Sensor, System, Actuator (传感器、系统、执行器)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
这些组件负责：

* 传感器：收集环境数据或设备状态。
* 系统：处理和管理传感器数据及执行器命令。
* 执行器：根据命令接口的指令执行具体操作。

1.7 Hardware Resources (硬件资源)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

包括实际的物理设备：

* 传感器硬件（如温度传感器）。
* 执行器硬件（如机械手臂）。

1.8 Transmissions (传动装置)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

传动装置是硬件资源的一部分，可能被系统或执行器使用，用于传递机械运动或其他形式的物理信号。

2. 结合ros2_control项目树的说明
--------------------------------------

.. note:: 

   下面会引入一个 ``decription`` 对模型进行描述。


.. code-block:: none
   
   my_robot_control/
    ├── bringup
    │   ├── config
    │   │   └── controllers.yaml
    │   └── launch
    │       └── my_robot_launch.py
    ├── CMakeLists.txt
    ├── description
    │   ├── launch
    │   │   └── view_robot.launch.py
    │   ├── ros2_control
    │   │   └── my_robot.ros2_control.xacro
    │   ├── rviz
    │   │   └── my_robot.rviz
    │   └── urdf
    │       └── my_robot.urdf.xacro
    ├── hardware
    │   ├── mybot_system.cpp
    │   └── include
    │       └── my_robot_control
    │           └── mybot_system.hpp
    ├── package.xml
    ├── README.md
    ├── my_robot_control.xml
    └── test
        ├── test_urdf_xacro.py
        └── test_view_robot_launch.py

2.1. Controllers (控制器)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 文件位置: bringup/config/controllers.yaml
* 作用: 定义控制器的配置文件，包含控制器类型、控制策略和参数设置等。控制器管理器根据这个文件加载和管理控制器。  

2.2. Controller Manager (控制器管理器)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 文件位置: bringup/launch/my_robot_launch.py(此部分并不是实现Controller Manager 的代码)
* `Controller_Manager示例代码 <https://github.com/ros-controls/ros2_control/blob/master/controller_manager/src/ros2_control_node.cpp>`__
* 作用: 启动文件，用于启动控制器管理器、Gazebo 仿真环境和其他必要的节点。控制器管理器负责加载控制器配置文件并管理控制器的生命周期。

2.3. Resource Manager (资源管理器)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 文件位置: hardware/mybot_system.cpp
* 作用: 管理硬件接口和资源，负责分配状态接口和命令接口。资源管理器从硬件中获取数据并将控制命令发送给硬件。

2.4. State Interface (状态接口) 和 Command Interface (命令接口)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 文件位置: hardware/mybot_system.cpp
* 作用: 实现硬件接口，用于读取传感器数据（状态接口）和发送控制命令（命令接口）到执行器。

2.5. Sensor, System, Actuator (传感器、系统、执行器)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 文件位置: hardware/mybot_system.cpp 和 hardware/include/my_robot_control/mybot_system.hpp
* 作用: 定义系统组件，包含传感器数据读取和执行器控制的逻辑。传感器采集环境数据，系统进行数据处理，执行器根据控制命令执行相应操作。

2.6. Hardware Resources (硬件资源)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 文件位置: description/urdf/my_robot.urdf.xacro 和 description/ros2_control/my_robot.ros2_control.xacro
* 作用: 定义机器人模型，通过 URDF 和 xacro 文件描述机器人各部分的物理特性和控制接口。Gazebo 仿真环境使用这些文件进行模拟，实现虚拟机器人在仿真环境中的操作。

2.7. Gazebo Simulation (Gazebo 仿真)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 文件位置: description/launch/view_robot.launch.py
* 作用: 用于启动 Gazebo 仿真环境和 RViz 可视化工具的启动文件。仿真环境模拟机器人的物理行为和交互，RViz 提供实时的可视化。



.. contents:: Table of Contents
   :depth: 4
   :local:
