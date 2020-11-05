# LiDAR-lifelong-SLAM-dataset
This is the open LiDAR dataset for lifelong SLAM, please refer to the following paper: `A General Framework for Lifelong Localization and Mapping in Changing Environment.`

# Requirements
To dataset is recorded by ROS recoder, and tested by the following ROS version:
- indigo
- kinetic
- melodic

# Data Name Format
year-month-date-hour-minute-second_index.bag_filtered.bag
Exp: 2020-10-31-6-7-27_176.bag_filtered.bag is recorded on 2020/10/31, 6:7:27. The index of the bag is 176.

# How to Get Dataset
Download files from Baidu Pan: https://pan.baidu.com/s/1JTTo76MEJGODd_T-HitPBw (code: ef3h)

# Topic of Dataset
These bags include such topics:
- poses under `world` frame: /localization/current_pose or /v5_current_pose
- odometry fused by IMU and wheel encoder under `base_odom ` frame: /odom
- static transform between `base_laser` and `base_link`: /tf_static
- dynamic transform between `world` and `base_odom`: /tf
- pre denoised 2D LiDAR scan under `base_laser`: /scan
- raw denoised 2D LiDAR scan under `base_laser`: /raw_scan
- the IMU topic: /gyro
- compressed 3D LiDAR pointclouds:  /rslidar_packets and /rslidar_packets_difop

# How to Check World Pose in Map
Step 1: Install ROS map_server: 
```
sudo apt-get install ros-<version>-map-server
```

Step 2:  Launch ROS and map server: 
```
roscore
rosrun map_server map_server map.yaml _frame_id:="world"
```

Step 3: Play the bags:
```
rosbag play **.bag --clock
```
Note: For ease of use, we recommend you to use launch file:
```
roslaunch test_2D.launch
```

# How to Get the original 3D pointclouds:
Step1 : Install RS-LIDAR driver:
```
cp ros_rslidar  ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_make
```

Step 2: Launch driver:
```
roslaunch test_3D.launch
```

Step 3: Play ros bag:
```
rosbag play *.bag --clock
```

# Acknowledgements
we will upload our new data collected from our robots in real world timelessly! ^_^
