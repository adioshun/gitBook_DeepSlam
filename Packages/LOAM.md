# Laser Odometry and Mapping (Loam)

- [논문](https://www.ri.cmu.edu/pub_files/2014/7/Ji_LidarMapping_RSS2014_v8.pdf), [깃허브](https://github.com/laboshinl/loam_velodyne)
- [저자 홈페이지](https://frc.ri.cmu.edu/~zhangji/), [저자 논문들(Google Scholar)](https://scholar.google.de/citations?user=h-k8LTIAAAAJ&hl=zh-CN&oi=sra)





- 목적 :  Build a low drift odometer -> 3D Point Cloud Map (Loop Closure는 고려 안함)


![](https://i.imgur.com/ENEOPGp.png)

Mainly through the following steps

- Point Cloud Registration - Receives laser data, completes point cloud registration and feature point cloud (edge ​​and face) extraction.
- Lidar Odometry - Issues an odometer at 10hz by matching a feature point cloud. The accuracy of the odometer at this time is not high.
- Lidar Mapping - Receives odometer information and current point cloud data, performs fine matching based on the rough matching odometer pose, registers the point cloud to the map according to the estimated pose, and publishes the updated pose according to 1hz.
- Transform Integration - Receives pose information published by lidar odometry and lidar mapping, and publishes odometer information at 10hz.



## LOAM mapping practice

```python
# Create your ROS Workspace
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make
$ source devel/setup.bash

#Download LOAM Package
$ cd ~/catkin_ws/src
$ git clone https://github.com/laboshinl/loam_velodyne.git 
$ cd ..
$ catkin_make -DCMAKE_BUILD_TYPE=Release
$ source ~/catkin_ws/devel/setup.bash     

#Download package
$ wget http://www.aisl.cs.tut.ac.jp/databases/hdl_graph_slam/hdl_400.bag.tar.gz
$ tar -axvf hdl_400.bag.tar.gz

# Run LOAM
$ roslaunch loam_velodyne loam_velodyne.launch
$ rosbap play hdl_400.bag

```