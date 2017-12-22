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
 
 
> 데이빗의 연구는 어떻게 보면 기존의 베이지안 필터 기반의 VSLAM과 유사하다. `Davison’s work in some way set the standard framework for traditional Bayesian filtering based visual SLAM implementation.`

### 2.1 2000년대 초반 연구들 

- 가우시안 필터 대신 파티클 필터 사용 하는 방법 `M. Pupilli and A. Calway investigated utilizing particle filter instead of Gaussian filter framework in camera pose tracking and visual SLAM [19] [20]. `
 - Fast SLAM : 비젼 대신 레이져 사용, 파티클 필터의 대표적 방법 `Although more famous work of particle filter based SLAM is FastSLAM proposed by M. Montemerlo et al. [21], they used laser sensors instead of vision. `
 
 
- 비쥬얼 슬램의 Front-end에서 사용되는 **주요 visual odometry 기법** `visual odometry from D. Nister et al. [22], who proposed methodology that sooner became almost ‘golden method’ for feature based VO and SFM, and are still frequently used in front-end of visual SLAM today. `

- Feature 파라미터화의 **주요 기법** : Inverse Depth이용  방법 `Another work that sooner became ‘golden method’ was in feature parameterisations from J. Montiel et al. [23], which used inverse depth instead of depth in feature position filter process.`


## 3. PTAM: New Standard for Local Tracking and Mapping

- 기존 EKF기반 비쥬얼 슬램의 문제점은 지도가 커지면 연산량이 커진다. `The problem of traditional EKF based visual SLAM mainly lies in computation effort as the map grows,` 
 - 랜드마크의 수에 따라 quadratically으로 연산량이 증가 한다. `since computation grows quadratically with the number of landmarks. `

- 모든 랜드마크를 사용하는 방식으로 구현하게 되는것과 huge covariance matrix를 관리하는것은 어렵다. 
 -  ` The implementation of putting all landmarks together with the robot pose in a long state vector and a huge covariance matrix seems not making sense (because not all observed features have direct constraints with each other),`
 - `and, as the covariance matrix is not sparse, computation resource spent on the iterative calculation of the covariance matrix is huge.`


![](https://i.imgur.com/qUfUaab.png)
```
Figure 1: Mono-SLAM vs PTAM. 
- Left: visualized result of MonoSLAM. 
- Middle: visualized result of keyframe-based tracking and mapping with PTAM. 
- Right: demo of PTAM.
```

- 흥미로운 챌리지이지만 이를 해결하기 위한 해결책은 SLAM연구원이 아닌 AR연구원에 의하여 제안 되었다. 












