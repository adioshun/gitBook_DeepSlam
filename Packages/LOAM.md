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




## Analysis of Algorithms
How to select the feature point and the planar point 
The author first defines a formula for measuring the smoothness of the point. The degree of smoothness of the point is measured by measuring the difference in distance between the two points. The point with the largest c value will be the edge point and the point with the smallest cz value will be the plane point. Divide 360 ​​degrees into four regions, each of which produces a maximum of two edge points and four plane points. These edge points and plane points are shown below. 
These extracted points are used as feature points to complete the matching of the front and rear frames to estimate their pose.

After constructing the loss function feature points, convert to the map coordinate system according to the tf relationship, find the nearest edge point and plane point in the map, and construct a transformation matrix by using the two nearest edge points and plane points as corresponding points, (t_x , t_y, t_z, theta), find the Jacobian for the conversion, and use the Gauss-Newton method to narrow the loss function until convergence.

## Algorithm pseudo code

![](https://img-blog.csdnimg.cn/2019040218251192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ZvdXJpZXJfTGVnZW5k,size_16,color_FFFFFF,t_70)


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

---
## 설치 

OS : 16.04 and 14.04
PCL : 1.8 추천 (1.7은 `multiScanRegistration error`발생 : 



---




[LOAM for point cloud map creation](https://blog.csdn.net/fourier_legend/article/details/88933443)