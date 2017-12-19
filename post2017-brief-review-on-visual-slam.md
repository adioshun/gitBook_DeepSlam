# Brief Review on Visual SLAM: A Historical Perspective

> 출처 : [Fan's Farm](http://fzheng.me/2016/05/30/slam-review/), May 30, 2016

## 1. Earlier Inspirations

- 초기 슬램은 works mostly relied on odometry and laser/ultrasonic sensor, 1990

- 로봇 비젼 연구도 활발히 진행 됨 : visual odometry (VO) and structure from motion (SFM)
    - VO : process of estimating the ego-motion of a robot
    - SFM :
    
- 2000년 전까지 SLAM은 로봇틱스에서 SFM은 컴퓨터 비젼 분야에서 따로 연구 되어 왔다. 

> 역사에 대한 설명들 포함 되어 있음, 필요시 재 확인 


## 2. EKF Monocular SLAM

- Davision에 위한 Landmart연구로 인하여 비젼이 SLAM과 연계 되었다. `Landmark work of bringing vision into SLAM came from A. Davison’s Mono-SLAM in early 2000s `

- 모노 슬램은 이미지 feature를 이용하여 랜드마트크를 표현한다. `Mono-SLAM uses image features (local image patches) to represent landmarks in the map,`

 - 반복적으로 연속된 이미지에서 **probability density of the feature depth**를 추출 한다. `iteratively updates the probability density of the feature depth by frame-to-frame matching to recover their 3-D positions and hence initilize feature-based sparse map,`
 
 -  이후 EKF를 사용하여 full state vector를 갱신한다. `and updates the full state vector (robot pose plus feature 3-D locations) within an Extended Kalman Filter (EKF) framework.`
 
 
> 데이빗의 연구는 어떻게 보면 기존의 베이지안 필터 기반으 VSLAM과 유사하다. `Davison’s work in some way set the standard framework for traditional Bayesian filtering based visual SLAM implementation.`