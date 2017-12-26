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




