# Introduction to VSLAM Presentation

> 출처 : [SpaceAnubis](https://www.youtube.com/watch?v=s0W4kW-ZVAg), 2013.07


```
## 1. What is VSLAM
## 2. SfM vs. VSLAM
## 3. Classic Approach : MonoSLAM (EKF-SLAM)
## 4. Current State-of-the-art (2013) : FastSLAM
## 5. Challenge
## 6. DTAM : Dense Tracking and Mapping
```

## 1. What is VSLAM

- Sensor 
    - 모노카메라
    - 스트레오 카메라
    - 키넥트 

- Feature (a.k.a Landmarks
    - point feature
    - Geometric feature (eg. lines, planes)
    - Featureless
    - Object 


![](https://i.imgur.com/c7CX3Gy.png)

```
ROS VSLAM
```

## 2. SfM vs. VSLAM

![](https://i.imgur.com/b9bcnZJ.png)

## 3. Classic Approach : MonoSLAM (EKF-SLAM)

### 3.1 EKF-SLAM:Mono SLAM (Andrew Davision ICCV 2003)
- Maintains full camera and feature covariance
- Limited to Gaussian uncertainty 
- Handheld camera
- Initialized with known target
- Extended kalman filter
    - `Constant velocity` motion model
    - Image patch features with Active Search
    - Automatic Map Measurement
    - Particle Filter for initialization of new feature

> 상세 알고리즘 설명 포함되어 있음, 동영상 참고 




### 3.2 SfM Approach (Nister ICCV 2003)
- RANSAC
- Frame-to-Frame motion only 

## 4. Current State-of-the-art (2013) : FastSLAM

![](https://i.imgur.com/ofNYSnB.png)
