# multi_drone

## Installation

**Depends on the hector_quadrotor package, you can install from:**
https://github.com/basavarajnavalgund/hector-quadrotor

## Usage

**Launch multiple drones**
```
$ roslaunch multi_drone main.launch
```

**Start drone**
```
$ rosservice call drone1/enable_motors true
$ rosservice call drone2/enable_motors true
```

**Run teleoperation node**
```
$ rosrun teleop_twist_keyboard teleop_twist_keyboard.py cmd_vel:=drone1/cmd_vel
$ rosrun teleop_twist_keyboard teleop_twist_keyboard.py cmd_vel:=drone2/cmd_vel
```

**Launch hector gmapping for each drone**
```
$ ROS_NAMESPACE=drone1 roslaunch multi_drone gmapping.launch drone_name:=drone1
$ ROS_NAMESPACE=drone2 roslaunch multi_drone gmapping.launch drone_name:=drone2
```

**Merge map data**
```
$ roslaunch multi_drone multi_map_merge.launch
```

**Launch rviz**
```
$ rosrun rviz rviz -d `rospack find multi_drone`/rviz/multi_drone_slam.rviz
```

**Send Takeoff messages to drones**
```
$ rostopic pub -r 0.4 drone1/cmd_vel geometry_msgs/Twist  '{linear:  {x: 0, y: 0.0, z: 0.1}, angular: {x: 0.0,y: 0.0,z: 0.0}}'
$ rostopic pub -r 0.4 drone2/cmd_vel geometry_msgs/Twist  '{linear:  {x: 0, y: 0.0, z: 0.1}, angular: {x: 0.0,y: 0.0,z: 0.0}}'
```

**Launch navigation system**
```
$ roslaunch multi_drone navigation.launch
```

**Run rviz navigation**
```
$ rosrun rviz rviz -d `rospack find multi_drone`/rviz/multi_drone_navigation.rviz
```

**Save map**
```
$ rosrun map_server map_saver -f ~/map
```
