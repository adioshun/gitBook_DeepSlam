# [Point cloud map PCL conversion to octree map octomap](https://blog.csdn.net/LOVE1055259415/article/details/79911653)

> [SLAM picks up (1): octomap](https://www.cnblogs.com/gaoxiang12/p/5041142.html), 




















---


# [Construction Map Bag->Pcd->OctoMap](https://blog.csdn.net/littlethunder/article/details/51955849)


1. ROS 파일에서 PCD파일 추출 : `rosrun pcl_ros bag_to_pcd input.bag /laser_cloud_surround pcd`

2. LOAM으로 생성된 토픽 **/laser_cloud_surround pcd**은 누적되는 포인트 클라우드 이므로 마지막 PCD 사용 

3. PCD를 Octomap(*.bt)으로 변경 : `./pcd2octomap 1.pcd 1.bt` [[코드]](https://github.com/gaoxiang12/octomap_tutor/blob/master/src/pcd2octomap.cpp)

4. [OctoMap](https://github.com/OctoMap/octomap)설치후 생성된 **octovis**툴을 이용하여 시각화 : `./octovis 1.bt`


![](https://i.imgur.com/uWr2sIS.png)