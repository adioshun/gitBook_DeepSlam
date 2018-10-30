# [OpenSLAM](https://openslam-org.github.io/)

여러 SLAM알고리즘 정리 

---
# Gmapping

- OpenSLAM에 공개된 SLAM 의 한 종류, ROS에서 패키지로 제공
- 저자: G. Grisetti, C. Stachniss, W. Burgard
- 특징: Rao-Blackwellized 파티클 필터, 파티클 수 감소, 그리드 맵

하드웨어 제약 사항
- X, Y, Theta 속도 이동 명령
    - 차동 구동형 모바일 로봇(differential drive mobile robot)
    - 전 방향 이동 로봇 (omni-wheel robot)
- 주행기록계 (Odometry)
- 계측 센서: 2차 평면 계측 가능 센서( LRF, LiDAR, Kinect, Xtion 등)
- 직사각형 및 원형의 로봇



https://github.com/ROBOTIS-GIT/bags/blob/master/TB3_WAFFLE_SLAM.bag



--- 

# ubuntu 18.4

- [Source code installation method for ROS melodic version map_server, gmapping, etc. in Ubuntu18.04 environment](https://blog.csdn.net/wsc820508/article/details/81561304)

