# LeGO LOAM 

![](https://i.imgur.com/3p4oVYC.png)

> LeGO-LOAM: Lightweight and Ground-Optimized Lidar Odometry and Mapping on Variable Terrain article., IROS 2018 

https://github.com/RobustFieldAutonomyLab/LeGO-LOAM



## 1.

LeGO LOAM은 LOAM에 비해 계산 시간은 줄이고, 루프백(LOOP BACK)을 지원하여 SLAM 안전성을 높인 방법이다. Levenberg–Marquardt algorithm 을 이용해 해 계산 방법을 개선한다. 참고로 LM 알고리즘은 특정 함수에 적합한 커브를 피팅(curve fitting)할 때도 많이 사용된다.
LeGO LOAM 링크를 방문해, 다음과 같이 소스를 다운로드후 빌드를 준비한다. 참고로, LeGO LOAM을 빌드하기 전에 GTSAM(Georgia Tech Smoothing and Mapping library) 패키지를 미리 설치해 놓아야 한다.

> http://daddynkidsmakers.blogspot.com/2019/06/lidar-slam.html

This code is based on LOAM.

comparison between loam and LeGO-LOAM on the i7 4710mq and jetson tx2 platforms
https://www.youtube.com/watch?v=O3tz_ftHV48  

Lightweight and Ground-Optimized Lidar Odometry and Mapping
1) A lightweight, runable on an embedded platform 
2) Point cloud segmentation to remove noise 
3) Real-time 6-degree-of-freedom estimation with ground optimization (using the presence of ground planes in the segmentation and optimization steps) 
4 Loopback detection



## 2. [Installation]()



Ubuntu16.04+ROS kinetic+pcl1.8+gtsam


```python 
# Download the source code of gtsam     
$ git clone https://bitbucket.org/gtborg/gtsam.git
$ cd gtsam && mkdir build && cd build
$ cmake ..
$ sudo make install


# Compilation and installation of LeGO-LOAM
$ cd ~/catkin_ws/src
$ git clone https://github.com/RobustFieldAutonomyLab/LeGO-LOAM.git
$ cd ~/catkin_ws
$ vi ./integration/utility.h # L91 : globalMapVisualizationSearchRadius 
$ catkin_make -j1
$ source ~/devel/setup.bash
```


```python 
$ roslaunch lego_loam run.launch
$ rosbag play *.bag --clock --topic /velodyne_points /imu/data
```

---

https://github.com/TixiaoShan/Stevens-VLP16-Dataset




# [LeGO-LOAM](https://github.com.cnpmjs.org/topics/velodyne)


[lation LeGO-LOAM paper translation (simplified content)](https://blog.csdn.net/wykxwyc/article/details/89605721) : 중국어 

https://blog.csdn.net/Travis_X/article/details/89374013

https://blog.csdn.net/qq_36396941/article/details/83513121


[Unable to locate package ros-kinect-pcl-ros](https://blog.csdn.net/weixin_43211438/article/details/88898544)


http://daddynkidsmakers.blogspot.com/2019/06/lidar-slam.html : 하단 부분에 LeGO-LOAM설명 