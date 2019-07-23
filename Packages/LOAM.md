# Laser Odometry and Mapping (Loam)

- [논문](https://www.ri.cmu.edu/pub_files/2014/7/Ji_LidarMapping_RSS2014_v8.pdf), [깃허브](https://github.com/laboshinl/loam_velodyne), [ROS](http://wiki.ros.org/loam_velodyne)
- [저자 홈페이지](https://frc.ri.cmu.edu/~zhangji/), [저자 논문들(Google Scholar)](https://scholar.google.de/citations?user=h-k8LTIAAAAJ&hl=zh-CN&oi=sra)


sing the velodyne 16-line lidar to run the loan-velodyne------ including laser radar and imu calibration](https://www.wandouip.com/t5i166274/)


배경 저장 : rosrun pcl_ros pointcloud_to_pcd input:=/velodyne_cloud_registered

---
## 설치 

OS : 16.04 and 14.04
PCL : 1.8 추천 (1.7은 `multiScanRegistration error`발생) 

```python
# PCL 1.8 설치 Kinetic

$ apt-get install git build-essential linux-libc-dev cmake cmake-gui libusb-1.0-0-dev libusb-dev libudev-dev mpi-default-dev openmpi-bin openmpi-common libflann1.8 libflann-dev libeigen3-dev libboost-all-dev libvtk5.10-qt4 libvtk5.10 libvtk5-dev libqhull* libgtest-dev freeglut3-dev pkg-config libxmu-dev libxi-dev mono-complete qt-sdk openjdk-8-jdk openjdk-8-jre
$ git clone https://github.com/PointCloudLibrary/pcl.git
$ cd pcl && mkdir release && cd release
$ cmake -DCMAKE_BUILD_TYPE=None -DCMAKE_INSTALL_PREFIX=/usr -DBUILD_GPU=ON -DBUILD_apps=ON -DBUILD_examples=ON -DCMAKE_INSTALL_PREFIX=/usr ..
$ make -j8
$ sudo make install
$ sudo apt-get install ros-kinetic-pcl-conversions ros-kinect-pcl-ros


# Loam compilation and installation
$ cd ~
$ mkdir -p catkin_ws/src
$ cd catkin_ws/src
$ catkin_init_workspace

$ cd ~/catkin_ws/src
$ git clone https://github.com/laboshinl/loam_velodyne.git
## 설치전 사전 작업 
$ vi src/lib/LaserMapping.cpp ## 주석 처리 139-153 #https://github.com/laboshinl/loam_velodyne/pull/84/files

$ cd ~/catkin_ws
$ rosdep install --from-paths ./loam_velodyne/ #(옵션)
$ catkin_make  #$ catkin_make -DCMAKE_BUILD_TYPE=Release
$ source ~/catkin_ws/devel/setup.bash 

#Download package
$ wget http://www.aisl.cs.tut.ac.jp/databases/hdl_graph_slam/hdl_400.bag.tar.gz
$ tar -axvf hdl_400.bag.tar.gz

# Run LOAM
$ roslaunch loam_velodyne loam_velodyne.launch
$ rosbap play hdl_400.bag #rosbag play data_file_name.bag -r 0.5 (속도 줄이기)




```

Error handling

1.multiScanRegistration error

If the bag is prompted to multiScanRegistration error after running Loam, the reason is to use apt-get to install the compiled pcl. You need to uninstall PCL according to the second part and download the source code to compile and install PCL. Then you need to restart catkin_make.

2.error: 'downSizeFilterMap' was not declared in this scope error

Errors may appear in catkin_make: 'downSizeFilterMap' was not declared in this scope error, because the source code of Loam has not been modified, refer to https://github.com/laboshinl/loam_velodyne/pull/84/files for   src/lib Comment out the 139-153 lines of /LaserMapping.cpp


---

# [Save and view Loam's 3D point cloud map](https://blog.csdn.net/qq_36396941/article/details/83048415)

지도 정보는 `/laser_cloud_surround`토픽으로 출력.. 이를 수신하여 pcd로 저장 

```
rosbag record -o out /laser_cloud_surround
rosrun pcl_ros bag_to_pcd input.bag /laser_cloud_surround pcd
# 필요시 ply로 변환
pcl_pcd2ply xxxx.pcd
```



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


[배경 저장](https://ishiguro440.wordpress.com/2016/04/05/%E5%82%99%E5%BF%98%E9%8C%B2%E3%80%80ros-loam_velodyne/) : rosrun pcl_ros pointcloud_to_pcd input:=/velodyne_cloud_registered


---

NSH indoor outdoor : [[Download]](https://pan.baidu.com/s/18ISyr4ky2MfTl7TXJD2W-A), 비번 2yea



[LOAM for point cloud map creation](https://blog.csdn.net/fourier_legend/article/details/88933443)

