# Map 

## 1. Map의 종류 

### 1.1 Occupancy Grid Map(OGM)

> 일반적으로 많이 사용 

- 2차원 격자 지도
- 0~255의 값으로 표현 = 점유 확률 값(1은 점유, 0은 비 점유)
- ROS msg nav_msgs/OccupancyGrid로 발행 
    - 발행시 점유 확률값(0~1)을 점유도(0~100)으로 변경 
    - 100은 이동 불가(Occupied Area), 0은 이동 가능(Free Area), -1은 미지 영역(unknown area)
- *.pgm 형태로 지도 저장 (Portable graymap format)
- *.yaml형태로 정보 저장
    - image : 지도의 파일명
    - resolution : 해상도 = meter/pixel (eg, 0.05 = 각 픽셀은 5cm)
    - origin : 원점에서의 x,y,yaw (eg. 지도 왼쪽 아래 = -10m, -10m, yaw)
    - negate : 흑백 반전
  
    
– resolution: Resolution of the map, meters / pixel
– origin: The 2-D pose of the lower-left pixel in the map as (x, y, yaw)
– occupied thresh: Pixels with occupancy probability greater than this threshold are considered completely occupied.
– free thresh: Pixels with occupancy probability less than this threshold are considered completely free.  

![](https://user-images.githubusercontent.com/17797922/47696612-ce89a400-dbc4-11e8-93f7-09e12fd6035a.png)



### 1.2 ooo

---

## 2. Map 생성 방법 


![](https://user-images.githubusercontent.com/17797922/47696603-c3367880-dbc4-11e8-9f49-6d2e3fe1af1b.png)

- Scan(sensor_msgs/LaserScan) : 거리값
- tf(tf/tfMessage) : 자세(위치+방향)정보 
- map(nav_msgs/OccupancyGrid)



---

## 3. Map 처리 과정 

![image](https://user-images.githubusercontent.com/17797922/47696736-55d71780-dbc5-11e8-9f86-a7d89a2712a3.png)

### 3.1 Sensor_node
- LDS센서 실행 거리 정보 수집 
- scan정보를 전달

### 3.2 turtlebot3_teleop
- 키보드를 통해 값 수신 (이동 정보)
- turtlebot3_core에 이동속도, 회전 속도등 명령어 전달

### 3.3 turtle3_core
- 로봇 이동 
- 자신의 위치 계측/측정한 정보인 odom정보 전송
- odom전송시 3단계 순서로 각 상대 좌표를 tf형태로 퍼블리시

### 3.4 turtlebot3_slam_gmapping
- 지도 작성 
    - scan 정보 이용 : 거리 정보 
    - tf 정보 이용 : 거리정보를 측정한 센서 위치 정보 


### 3.5 map_saver
- *.pgm / *.yaml 파일 생성 
- 추후 map_server 노드에 위해서 topic형태로 퍼블리쉬된다. 


