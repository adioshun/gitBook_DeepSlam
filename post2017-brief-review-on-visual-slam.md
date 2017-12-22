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
 - PTAM(Parallel Tracking and Mapping), Georg Klein and David Murray, 2007


- PTAM역시 특징 기반 SLAM이다. `PTAM is also a feature-based SLAM algorithm that tracks and maps many (hundreds of) features to achieve robustness. `

- 베이지안 필터 대신에 키프레임 기반 BA를 사용하여 실시간으로 모션 측정 및 지도 생성(Mapping)을 한다. 
 - Simultaneously, it runs in real-time by creatively parallelizing the motion estimation and mapping tasks and 
 - by relying on efficient keyframe-based **Bundle Adjustment (BA)** instead of Bayesian filtering for pose and map refinement, 
 - which are two main reasons to make PTAM outperform MonoSLAM and the like in both efficiency and precision. 

- PTAM 설계는 AR을 목적으로 하고 작은 책상 공간크기에서만 동작 하고 Global Map을 관리 하지 않지만 주요 아이디어(parallelizing tracking, mapping and keyframe-based map management)들은 최근 비쥬얼 슬램에 많이 적용 되고 있다.
 - ` Although PTAM is designed specifically for AR application and only works well in small desktop space without global map management, its implementation style of parallelizing tracking and mapping and keyframe-based map management is used by most of modern feature based visual SLAM systems (like ORB-SLAM [25]) or VO systems (like SVO [26]).`
  - modern feature based visual SLAM systems (like ORB-SLAM [25]) 
  - VO systems (like SVO [26])


- 사실 키프레임 기반 map를 BA를 이용해 refinement하는것은 **Graph SLAM **기술에 속한다. `In fact, keyframe-based map refinement with BA belongs to so-called Graph SLAM techniques,`
 - 키프레임과 지도 포인트는 그래프이론에서의 노드로 간주되어 측정 에러를 최소화 하기 위한 최적화를 수행 한다. `as keyframes and map points are treated as nodes in a graph and optimized to minimize their measurement errors [27]. `
 
- 그래프 슬램은 EKF 슬램에 비해 그래프상의 sparsity때문에 계산 부하가 적다. 
Graph SLAM is better than EKF SLAM in the sparsity of the graph and thus computational efficiency. 


- 2007년에 그래프 슬램을 위한 정보 필터 기반 방식이 제안 되었다. `Meanwhile in 2007, E. Eade and T. Drummond proposed an information filter based method of graph SLAM [28]. `
 
- 정보필터 방식은 이론적으로는 BA방식과 비슷하다. `Information filter method is essentially similar to BA method in theory,`
 - 그러나 PTAM은 확실히 창의적인 parallel tracking and mapping기법 때문에 기존 비쥬얼 슬램에 많은 영향을 미쳤다. `but PTAM obviously achieved greater influence in visual SLAM research due to its creative implementation of parallel tracking and mapping.`
 
## 4. Effort towards Large Scale Mapping 

- PTAM은 작은 공간에서는 잘 동작 하지만 큰 공간에서는 개선이 필요 하다. `PTAM achieves considerately satisfactory result in small local space, while the problem of large scale mapping remains to be solved. `

- 큰 공간의 지도 해결 방법은 2가지가 있다. `The solution to large scale map management basically includes two parts:`
 - 1) efficient map representation and refinement 
 - 2) and loop closing. 

> Efficient map representation and and refinement is actually a necessary condition for good loop closing.



