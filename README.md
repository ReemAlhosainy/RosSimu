# RosSimu

## packeges
- ### waiteronix
    - urdf : contain robot description and sensor plugins
    - meshes
- ### gazebo_pkg
    - launch : cantain gazebo.launch
    - worlds : cantain cafe.world


#### Notes 
- urdf : created through solidworks export but this warning appear :

```
[ WARN] [1709066698.122112264]: The root link base_link has an inertia specified in the URDF, but KDL does not support a root link with an inertia.  As a workaround, you can add an extra dummy link to your URDF.
```
so , I added dummy link 
```
 <link name="dummy">
   </link>
   
  <link
    name="base_link">
    ..........
  </link>

<joint name="dummy_joint" type="fixed">
    <parent link="dummy"/>
    <child link="base_link"/>
   </joint>
```

- sensors plugin 
    - camera : https://classic.gazebosim.org/tutorials?tut=ros_gzplugins&cat=connect_ros
    - RPlider a1: https://github.com/joshnewans/articubot_one/blob/545acac87ae215d80ef6b28abe6097eb7281d9ff/description/lidar.xacro

    - imu : https://classic.gazebosim.org/tutorials?tut=ros_gzplugins&cat=connect_ros

### Errors
 ```
 [ERROR] [1709066716.824056, 57.818000]: Spawn service failed. Exiting.
[myrobot_spawn-3] process has died [pid 9498, exit code 1, cmd /opt/ros/noetic/lib/gazebo_ros/spawn_model -urdf -param robot_description -model waiteronix __name:=myrobot_spawn __log:=/home/emanelsayed/.ros/log/0619a3c0-d5b1-11ee-93ee-2fc0cae9f949/myrobot_spawn-3.log].
log file: /home/emanelsayed/.ros/log/0619a3c0-d5b1-11ee-93ee-2fc0cae9f949/myrobot_spawn-3*.log

 ```
### after test it step by step noticed that :
- #### this gazebo.launch is okey but it launch empty environment 
```
<?xml version="1.0" encoding="UTF-8"?>
<launch>

  <!-- custom gazebo arguements-->
  <arg name="world" default="empty"/>
  <arg name="paused" default="false"/>
  <arg name="use_sim_time" default="true"/>
  <arg name="gui" default="true"/>
  <arg name="headless" default="false"/> 
  <arg name="debug" default="false"/>

```
World File
```
  
  
    <include
    file="$(find gazebo_ros)/launch/empty_world.launch">
    <arg name="paused" value="$(arg paused)"/>
    <arg name="use_sim_time" value="$(arg use_sim_time)"/>
    <arg name="gui" value="$(arg gui)"/>
    <arg name="headless" value="$(arg headless)"/>
    <arg name="debug" value="$(arg debug)"/>
  </include>
  
```
```
	<!-- Find my robot Description-->
   <param
    name="robot_description"
    textfile="$(find waiteronix)/urdf/waiteronix.urdf" />
    
   <node
    name="spawn_model"
    pkg="gazebo_ros"
    type="spawn_model"
    args="-file $(find waiteronix)/urdf/waiteronix.urdf -urdf -model waiteronix"
    output="screen" /> 


   
  <!-- Send fake joint values-->

    
  <node name="joint_state_publisher" pkg="joint_state_publisher" type="joint_state_publisher">
    <param name="use_gui" value="false"/>
  </node>

  <!-- Send robot states to tf -->
  <node name="robot_state_publisher" pkg="robot_state_publisher" type="robot_state_publisher" respawn="false" output="screen"/>
   
  <node name="rviz" pkg="rviz" type="rviz" /> 


</launch>
```

- #### afer replace world file with this section , robot fall 
```
  
    <arg name="world_name" value="$(find gazebo_pkg)/worlds/cafe.world"/>
    <include
    file="$(find gazebo_ros)/launch/empty_world.launch">
    <arg name="world_name" value="$(arg world_name)"/>
    <arg name="paused" value="$(arg paused)"/>
    <arg name="use_sim_time" value="$(arg use_sim_time)"/>
    <arg name="gui" value="$(arg gui)"/>
    <arg name="headless" value="$(arg headless)"/>
    <arg name="debug" value="$(arg debug)"/>
  </include>
  ```



