# SLAM for Dummies

- A Tutorial Approach to Simultaneous Localization and Mapping 

- Søren Riisgaard and Morten Rufus Blas 

## 1. 목차 

## 2. Introduction 

- 이 글을 작성한 이유등..

## 3. About SLAM 

- 용어 출처 :  SLAM was originally developed by Hugh Durrant-Whyte and John J. Leonard
[7] based on earlier work by Smith, Self and Cheeseman [6].


- SLAM consists of multiple parts; 
    - Landmark extraction, 
    - data association, 
    - state estimation, 
    - state update 
    - landmark update.
    

> 본 문서는 실내 환경에서 2D motion에 초점을 두었다. 


## 4. The Hardware 

SLAM을 위해 필요한 H/W :  a **mobile robot** and a **range measurement device**

### 4.1 The robot 

- 로봇선정시 주요 고려 요소는 ease of use, **odometry performance**, price이다. 
    - The odometry performance measures how well the robot can estimate its own position, just from the rotation of the wheels. 
    - 오차 범위 2cm 이내여야 한다. 
    
> 본 문서에서는 ER1이란 로봇을 사용하였지만 더이상 팔지 않는다. 

### 4.2 The range measurement device 

#### A. laser scanner

- 일반적으로 많이 사용된다. 

- 장점 : 정확하고 추가적인 데이터 처리가 불필요 하다.  

- 단점 : 비싸고, 환경의 영향을 많이 받는다. 

#### B. sonar

- 상대적으로 저렴하지만 정확도가 좋지 않다. 

#### C. vision

- 과거에는 여러 단점들로 적합하지 않았다. 

- 최근에는 이런 문제를 해결하였으며, stereo카메라를 사용해 Depth측정도 가능하다. 

- 레이져에 비하여 더 풍부한 정보를 제공할수 있다. 

- Vision based range measurement has been successfully used in [8]. 

> 본 문서에서는 laser range finder from SICK [9]를 사용하였다. (오차 5~50mm)

## 5. The SLAM Process 


- SLAM은 여러 절차로 이루어져 있다. `The SLAM process consists of a number of steps. `

- 이러한 절차의 목적은 환경 정보를 이용하여 로봇의 position을 갱신하는 것이다. `The goal of the process is to use the environment to update the position of the robot. `

- position 정보를 제공한는 로봇의 odometry가 정확하지 않기 때문에 이를 바로 사용하지 않고 레이져 스캐너를 이용하여 보정한다.  `Since the odometry of the robot (which gives the robots position) is often erroneous we cannot rely directly on the odometry. We can use laser scans of the environment to correct the position of the robot. `
    - This is accomplished by extracting features from the environment and re-observing when the robot moves around. 


- EKF (Extended Kalman Filter)가 SLAM의 핵심이다. 
    - It is responsible for updating where the robot thinks it is based on these features. 
    - These features are commonly called **landmarks **
    - The EKF keeps track of an estimate of the uncertainty in the robots position and also the uncertainty in these landmarks it has seen in the environment. 

![](https://i.imgur.com/Wk5AWW8.png)



1. When the odometry changes because the robot moves the uncertainty pertaining to the
robots new position is updated in the EKF using Odometry update. 
2. Landmarks are then extracted from the environment from the robots new position. 
3. The robot then attempts to associate these landmarks to observations of landmarks it previously has seen. 
4. Re-observed landmarks are then used to update the robots position in the EKF.
5. Landmarks which have not previously been seen are added to the EKF as new observations so they can be re-observed later. 

> It should be noted that at any point in these steps the EKF will have an estimate of the robots current position. 


||The diagrams below will try to explain this process in more detail: |
|-|-|
|![](https://i.imgur.com/PlWWAoC.png)|- The robot is represented by the triangle. <br>- The stars represent landmarks. <br>- The robot initially measures using its sensors the location of the landmarks (sensor measurements illustrated with lightning). |
|![](https://i.imgur.com/GvMUtTp.png)|- The robot moves so it now thinks it is here. <br>- The distance moved is given by the robots odometry|
|![](https://i.imgur.com/s5bpgKa.png)|- The robot once again measures the location of the landmarks using its sensors but finds out they don’t match with where the robot thinks they should be (given the robots location). <br>- Thus the robot is not where it thinks it is. |
|![](https://i.imgur.com/IEUDxgg.png)|-As the robot believes more its sensors than its odometry it now uses the information gained about where the landmarks actually are to determine where it is (the location the robot originally thought it was at is illustrated by the dashed triangle).|
|![](https://i.imgur.com/Q54DlDx.png)|-  In actual fact the robot is here. <br>- The sensors are not perfect so the robot will not precisely know where it is. <br>- However this estimate is better than relying on odometry alone. <br>- The dotted triangle represents where it thinks it is; the dashed triangle where odometry told it it was; and the last triangle where it actually is. |

## 6. Laser Data 

- SLAM의 첫 단계는 레이져를 이용하여 주변 거리를 측정 하는것이다. `The first step in the SLAM process is to obtain data about the surroundings of the robot`

- 센서의 아웃풋은 다음과 같을것이다. : 2.98, 2.99, 3.00, 3.01, 3.00, 3.49, 3.50, ...., 2.20, 8.17, 2.21 

- 정확한 거리를 측정하지 못할경우에는 아주 큰값을 리턴한다. 본 문서에서는 threshold로 8.1을 잡았다. 

> 본 문서에서 사용된 코드는 `Appendix B: SICK LMS 200 interface code. `를 참고 


## 7. Odometry Data 

- SLAM의 중요한 요소중 하나는 odometry데이터 이다. `An important aspect of SLAM is the odometry data.`

- odometry데이터의 사용 목적은 바퀴 움직임에 따른 대략적인 위치를 측정하는 것이다. `The goal of the odometry data is to provide an approximate position of the robot as measured by the movement of the wheels of the robot, to serve as the initial guess of where the robot might be in the EKF.`

- 어려운 점은 Laser데이터와 Odmometry데이터의 시간 동기화 이다. `The difficult part about the odometry data and the laser data is to get the timing right.`

## 8. Landmarks 

- 랜드마크는 re-observed가능하고 distinguished한 Feature를 의미한다. `Landmarks are features which can easily be re-observed and distinguished from the environment.`

- 랜드마크는 현재 어디에 있는지 알수 있게 한다. `These are used by the robot to find out where it is (to localize itself). `

- 랜드마크가 가져야 하는 성질 `The key points about suitable landmarks are as follows:`
    - Landmarks should be easily re-observable.
    - Individual landmarks should be distinguishable from each other.
    - Landmarks should be plentiful in the environment.
    - Landmarks should be stationary. 

## 9. Landmark Extraction 

- 랜드마크 추출에는 센서 종류와 랜드마크에 따라 여러 알고리즘이 사용가능하다. 

- 본 문서에서는 레이져 센서용 추출 알고리즘인 Spikes와 RANSAC에 대하여 살펴 보겠다. `We will present basic landmark extraction algorithms using a laser scanner. They will use two landmark extraction algorithm called Spikes and RANSAC.`


### 9.1 Spike landmarks 

> 필요시 추후 자세히 살펴 보기 

### 9.2 RANSAC(Random Sampling Consensus)

> 필요시 추후 자세히 살펴 보기 



## 10. DATA ASSOCIATION

- 데이터 ASSOCIATION에서의문제점은 두개의 센서에서 읽은 랜드마크를 matching하는 것이다. `The problem of data association is that of matching observed landmarks from different (laser) scans with each other. `

- We have also referred to this as **re-observing landmarks**. 

```
[예]
- 


## 11. THE EKF


## 12. FINAL REMARKS

## 13. REFERENCES