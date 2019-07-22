# Laser Odometry and Mapping (Loam)

- [논문](https://www.ri.cmu.edu/pub_files/2014/7/Ji_LidarMapping_RSS2014_v8.pdf), [깃허브](https://github.com/laboshinl/loam_velodyne), [ROS](http://wiki.ros.org/loam_velodyne)
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
PCL : 1.8 추천 (1.7은 `multiScanRegistration error`발생) 

```
# PCL 1.8 설치 Kinetic
apt-get install git build-essential linux-libc-dev cmake cmake-gui libusb-1.0-0-dev libusb-dev libudev-dev mpi-default-dev openmpi-bin openmpi-common libflann1.8 libflann-dev libeigen3-dev libboost-all-dev libvtk5.10-qt4 libvtk5.10 libvtk5-dev libqhull* libgtest-dev freeglut3-dev pkg-config libxmu-dev libxi-dev mono-complete qt-sdk openjdk-8-jdk openjdk-8-jre

git clone https://github.com/PointCloudLibrary/pcl.git

cd pcl && mkdir release && cd release
cmake -DCMAKE_BUILD_TYPE=None -DCMAKE_INSTALL_PREFIX=/usr -DBUILD_GPU=ON -DBUILD_apps=ON -DBUILD_examples=ON -DCMAKE_INSTALL_PREFIX=/usr ..

make -j8
sudo make install

sudo apt-get install ros-kinetic-pcl-conversions ros-kinect-pcl-ros


# Loam compilation and installation
cd ~/catkin_ws/src
git clone https://github.com/laboshinl/loam_velodyne.git

## 설치전 사전 작업 
vi src/lib/LaserMapping.cpp
## 주석 처리 139-153 #https://github.com/laboshinl/loam_velodyne/pull/84/files


# LOAM실행 
roslaunch loam_velodyne loam_velodyne.launch


```

Error handling

1.multiScanRegistration error

If the bag is prompted to multiScanRegistration error after running Loam, the reason is to use apt-get to install the compiled pcl. You need to uninstall PCL according to the second part and download the source code to compile and install PCL. Then you need to restart catkin_make.

2.error: 'downSizeFilterMap' was not declared in this scope error

Errors may appear in catkin_make: 'downSizeFilterMap' was not declared in this scope error, because the source code of Loam has not been modified, refer to https://github.com/laboshinl/loam_velodyne/pull/84/files for   src/lib Comment out the 139-153 lines of /LaserMapping.cpp


---

## [센서 데이터 바로 적용 하기](https://blog.csdn.net/qq_36396941/article/details/83048660)

Vlp16.yaml 준비 
- 다운로드 : https://pan.baidu.com/s/1c327b7IT3M5UTrF02Xua2g Extraction code: m6yr
- xml을 변환 : `$ rosrun velodyne_pointcloud gen_calibration.py ~/Desktop/VLP-16.xml`


```
$ roslaunch velodyne_pointcloud VLP16_points.launch calibration:=/home/xxxx/VLP-16.yaml
$ roslaunch loam_velodyne loam_velodyne.launch
```


---
NSH indoor outdoor : [[Download]](https://pan.baidu.com/s/18ISyr4ky2MfTl7TXJD2W-A), 비번 2yea



[LOAM for point cloud map creation](https://blog.csdn.net/fourier_legend/article/details/88933443)

