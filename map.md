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
    
### 1.2 ooo

## 2. Map 생성 방법 

