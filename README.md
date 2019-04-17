![](https://i.imgur.com/qfwXTbg.png)
```https://arxiv.org/pdf/1607.00470.pdf```

# 로봇의 자율주행을 위해 필요한 기술 

- 지도 : SLAM기술 활용 자동 생성 
- 로봇 자세 계측/추정 기능 : GPS, IMU센서, 추측항법(Dead reckoning)
- 벽, 물체등 장애물 계측 기능 : Lidar, Depth Camera
- 최적 경로를 계산하고 주행 하는 기능 : A*알고리즘, 포텐셜 필드, 파티클 필드, RRT


## SLAM 관련 ROS 패키지 

- gmapping
- cartographer
- rtabmap 


### A majority of SLAM systems share several common components:

- **feature detector** that finds point of interest within the image (features),
- **feature descriptor** that matches tracks features from one image to the next,
- **optimization** backend that uses said correspondences to build a geometry of the scene (map) and find the position of the robot,
- **loop closure detection algorithm** that recognizes previously visited areas and adds constraints to the map.
    - loop closure has the most potential to be solved with DL techniques.
    
> 출처 : [How can Deep Learning help Robotics and SLAM](https://nicolovaligi.com/deep-learning-robotics-slam.html)








--- 

