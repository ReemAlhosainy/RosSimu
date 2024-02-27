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