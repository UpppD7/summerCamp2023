# 雷达

## 如何驱动

建立一个工作空间并下载思岚给的ROS包

（不进入src）编译并source

`roslaunch <project> <launchfilename> //注意对应雷达型号`

启动rviz可观察效果

`ls /dev/tty*` 查看串口文件

雷达的串口文件是ttyUSB

若（电脑或mini PC）第一次连接雷达，要运行scripts文件夹中的脚本文件