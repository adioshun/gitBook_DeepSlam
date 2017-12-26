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