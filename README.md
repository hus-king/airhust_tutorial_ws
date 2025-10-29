# 操作指南

## 一、准备工作
先克隆本仓库到~下
```bash
cd ～
git clone https://github.com/hus-king/airhust_tutorial_ws.git
```

再编译本工作空间
```bash
cd airhust_tutorial_ws
catkin_make
```
把`source ~/airhust_tutorial_ws/devel/setup.bash`加到~/.bashrc文件的末尾

## 二、配置地图
```bash
cd ~/airhust_tutorial_ws/src/sim_task
mkdir -p ~/.gazebo/models
mv models/* ~/.gazebo/models
```

## 三、打开地图并起飞
```bash
roslaunch sim_task task.launch
```
打开另一个窗口，运行
```bash
roslaunch template template.launch
```
