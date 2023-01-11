# Workspace for unitree_ros2_real, and unitree_legged_sdk version 3.5.1 ROS2 examples 

You are expected to have both colcon, and ROS2 galactic installed. Checkout the repo, and list the colcon packages as a sanity check 

```
user@dev0:~$ cd 
user@dev0:~$ git clone https://github.com/MAVProxyUser/unitree_ros2_ws.git --recurse-submodules
user@dev0:~$ cd unitree_ros2_ws
user@dev0:~/unitree_ros2_ws$ colcon list
```

If you don't see the following packages, you have a problem
```
ros2_unitree_legged_msgs	src/ros2_unitree_legged_msgs	(ros.ament_cmake)
unitree_legged_real	src/unitree_ros2_to_real	(ros.ament_cmake)
unitree_legged_sdk	src/unitree_legged_sdk	(cmake)
```

If you do see them, go on and source the ROS2 environment, and start to build packages
user@dev0:~/github/unitree_ros2_ws$ source /opt/ros/galactic/setup.sh
user@dev0:~/github/unitree_ros2_ws$ colcon build
```

# Troubleshooting

Don't see any packages? Did you run the wrong git command? Did you forget the submodules? 

```
user@dev0:~$ git clone https://github.com/MAVProxyUser/unitree_ros2_ws.git 
user@dev0:~$ cd unitree_ros2_ws
user@dev0:~/unitree_ros2_ws$ colcon list
```

If you saw nothing on your colcon listing, then you will need to run the following commands from within your unitree_ros2_ws folder.  

user@dev0:~/unitree_ros2_ws$ git submodule update --init --recursive
user@dev0:~/unitree_ros2_ws$ colcon list

Now you should see the packages. 
```
ros2_unitree_legged_msgs	src/ros2_unitree_legged_msgs	(ros.ament_cmake)
unitree_legged_real	src/unitree_ros2_to_real	(ros.ament_cmake)
unitree_legged_sdk	src/unitree_legged_sdk	(cmake)
```

# Running the examples

All examples are hard coded for the Wifi IP address 192.168.12.1, please edit them if you are on Ethernet

Start the high level server
```
user@dev0:~$ cd ~/unitree_ros2_ws
user@dev0:~/unitree_ros2_ws$ source /opt/ros/galactic/setup.sh
user@dev0:~/unitree_ros2_ws$ source install/setup.sh 
user@dev0:~/unitree_ros2_ws$ ros2 run unitree_legged_real ros2_udp highlevel
```

On a second window 
```
user@dev0:~$ cd ~/unitree_ros2_ws
user@dev0:~/unitree_ros2_ws$ source /opt/ros/galactic/setup.sh
user@dev0:~/unitree_ros2_ws$ source install/setup.sh
user@dev0:~/unitree_ros2_ws$ ros2 run unitree_legged_real ros2_walk_example
```
