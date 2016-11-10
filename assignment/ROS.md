# Lab4: ROS环境配置
*14353173 廖瑶雅*
## 一、ROS
Robot operation system,一套框架，底层提供硬件驱动，软件层 面支持通用的文件格式。毕竟穷，买不起一个150K的激光雷达， 我们主要用它的仿真功能。 这个ROS要在Ubuntu下完成配置，所以在虚拟机中完成的。

## 二、ROS环境配置过程（使用过的是Ubuntu16.04）

1. 设置Ubuntu的下载权限如下图：  
   ![fig1](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/ros1.png)  
   
2. 建立sources.list  
    ```
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```
    
3. 输入密钥  
    ```
    sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
    ```
    
4. 安装    
    ```
    sudo apt-get update
    ```  
    我们需要的是Desktop-Full Install，也就是推荐使用的。  
    ```
    sudo apt-get install ros-kinetic-desktop-full
    ```  
    安装完成以后，查看已安装的可以使用的包  
    ```
    apt-cache search ros-kinetic
    ```
    
5. 对新安装的ROS进行初始化
    当输入`sudo rosdep init`后就会有提示下一步指令为`rosdep update`:  
    ![fig2](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/ros2.png)  
    
6. 环境的配置,此处采用的是长期有效的，不需要每次打开终端都配置一遍环境。因为ROS下的程序有时候需要经常重开终端，所以这样还是比较方便的。  
    ```
    echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
    ```
    
7. 安装rosinstall这个工具，因为这个工具会在ROS使用命令行时经常会被用到，可以方便我们来下载ROS包中的很多源树，因为只需要一条命令即可。  
    ```
    sudo apt-get install python-rosinstall
    ```
    
8. 至此，ROS已经安装完成了。我们就可以跑一个小程序看看是否安装成功了。

9. 我跑的是ROS带有的小海龟程序。重启命令行，输入指令：`$  roscore`,再重启命令行，输入`$  rosrun turtlesim turtlesim_node`。就会出来下面的小海龟，说明ROS安装成功了：  
   ![fig3](https://github.com/liaoyaoya/ES2016_14353173/blob/master/img/ros3.png)  