# Waiteronix11

This package contian simulation of waiteronix robot. 

# gazebo_pkg
this packege contain worlds to test system in such these environments
## Dependencies

* Ununtu 20.04
* ROS Neotic

## Installation(Setup)

follow the instructions below to install the simulation part:
first create your workspace...
```bash
mkdir -p waiteronix_Ws/src
```
then clone the repository...
```bash
git clone https...
```
then excute and source the package
```bash
cd ..
catkin_make
source devel/setup.bash
```

## Run

```bash
roslaunch waiteronix_description gazebo.launch
```

>Note : there is a large block (cube) added on the end of the robot to make robot more balanced

> Note : if you want to add your customized environment , follow these steps :

```
add your world into "gazebo_pkg/worlds
```
```
edit line 13 in "waiteronix_description/launch/gazebo.launch" to add your desired world_name
```
