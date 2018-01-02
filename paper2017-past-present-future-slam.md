|논문명 |Past, Present, and Future of Simultaneous Localization And Mapping: Towards the Robust-Perception Age |
| --- | --- |
| 저자\(소속\) | Cesar Cadena\( ETH Zurich\), L. Carlone(MIT) \) |
| 학회/년도 | arXiv Jun 2016~Jan 2017, [논문](https://arxiv.org/abs/1606.05830) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 | |
| 관련연구||
| 참고 |[홈페이지](https://slam-future.github.io/) |
| 코드 | |


# Past, Present, and Future of Simultaneous Localization And Mapping


- We survey the current state of SLAM and consider future directions

- We start by presenting what is now the de-facto standard formulation for SLAM. 

- 관련연구 : We then review related work, covering a broad set of topics including 


----------


    - robustness and scalability in long-term mapping, 
    - metric and semantic representations for mapping, 
    - theoretical performance guarantees, 
    - active SLAM and exploration, 
    - and other new frontiers. 

 - 최종 질문 : Do robots need SLAM? and Is SLAM solved?
 
 
 ## I. INTRODUCTION
 
- SLAM comprises the simultaneous  
    - 상태 측정 : estimation of the **state of a robot** equipped with on-board sensors, 
    - 지도 생성 : the construction of a **model (the map)** of the environment that the sensors are perceiving. 

###### In simple instances,

- 로봇 상태는 포즈`(포지션, 방향)`나 기타 정보`(속도, 오차, 파라미터)`로 표현 할수 있다.  : `the robot state is described by `
    - its pose (position and orientation), 
    - although other quantities may be included in the state, 
        - such as robot velocity,sensor biases, and calibration parameters. 


- 지도는 랜드마크/장애물 위치등 관심 영역으로 표현 할수 있다. `The map is a representation of aspects of interest (e.g.,position of landmarks, obstacles) describing the environment in which the robot operates.`


- 지도가 필요한 두가지 이유 `The need to use a map of the environment is two fold.`
    - 첫째 다른 Task에 활용하기 위해  `First, the map is often required to support other tasks; `
        - 예 : 경로 설정,  `for instance, a map can inform path planning or provide an intuitive visualization for a human operator. 
    - 둘째, 로봇의 State측정시 발생하는 에러를 제한 하기 위해 `Second, the map allows limiting the error committed in estimating the state of the robot. `
        - 지도가 없다면, dead-reckoning이 빠르게 확산될것이다. `In the absence of a map, dead-reckoning would quickly drift over time; `
        - 지도가 있다면, 위치 에러를 알려진 지역의 re-visiting를 통해 재설정 가능하다. `on the other hand, using a map, (e.g.,a set of distinguishable landmarks), the robot can “reset” its localization error by re-visiting known areas (so-called loop closure). `

- 따라서 SLMA은 지도가 없어 생성해야 하는 서비스에서도 활용이 가능하다. `Therefore, SLAM finds applications in all scenarios in which a prior map is not available and needs to be built.`

- 일부 환경에서는 랜드마크가 미리 정의되어 있다. `In some robotics applications the location of a set of landmarks is known a priori. `
    - 예를 들어 비콘등을 이용하여 위치 정보를 미리 알려 준다. `For instance, a robot operating on a factory floor can be provided with a manually-built map of artificial beacons in the environment. `
    - 또는 실내지만 GPS를 수신할수 있는 환경도 랜드마크가 알려진것으로 볼수 있다. `Another example is the case in which the robot has access to GPS (the GPS satellites can be considered as moving beacons at known locations). `
    - 이런 알려진 랜드마크를 이용하여 localization이 가능한 시나리오에서는 SLAM이 꼭 필요 하지 않다. `In such scenarios, SLAM may not be required if localization can be done reliably with respect to the known landmarks.`

- The popularity of the SLAM problem is connected with the emergence of indoor applications of mobile robotics. 
    - Indoor operation rules out the use of GPS to bound the localization error; 
    - furthermore, SLAM provides an appealing alternative to user-built maps, showing that robot operation is possible in the absence of an ad hoc localization infrastructure.
    










