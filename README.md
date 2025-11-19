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

## 四、添加下摄像头

编辑文件`~/PX4-Autopilot/Tools/simulation/gazebo/sitl_gazebo/models/iris/iris.sdf`

在其中添加
```xml
      <!-- 添加下视摄像头定义 -->
      <sensor name="downward_camera" type="camera">
        <pose>0 0 -0.1 0 1.57 0</pose> <!-- 位置在底部，朝向下方 -->
        <camera>
          <horizontal_fov>1.386</horizontal_fov> <!-- 水平视场角，根据焦距计算 -->
          <image>
            <width>640</width>
            <height>480</height>
            <format>R8G8B8</format>
          </image>
          <clip>
            <near>0.1</near>
            <far>30</far>
          </clip>
        </camera>
        <plugin name="camera_plugin" filename="libgazebo_ros_camera.so">
          <topicName>camera/image_raw</topicName>
          <frameName>camera_frame</frameName>
          <distortionK1>0.01401476</distortionK1>
          <distortionK2>0.01596416</distortionK2>
          <distortionK3>0.25648364</distortionK3>
          <distortionT1>-0.00489736</distortionT1>
          <distortionT2>0.00298071</distortionT2>
        </plugin>
      </sensor>
```

如下图
![downward_camera](image/downward_camera.png)

之后可获得下视摄像头话题`/image_raw`