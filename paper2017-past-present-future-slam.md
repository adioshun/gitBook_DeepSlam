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
    
 
 ###### [1986-2004 : classical age] 
      
- 20년간의 SLAM 문제 연구에 대한 추천 서베이 논문 : [7, 69]`A thorough historical review of the first 20 years of the SLAM problem is given by Durrant-Whyte and Bailey in two surveys [7, 69]. `


- [7, 69]의 주요 내용은 classical age(1986-2004)에 대한 내용이다. `These mainly cover what we call the classical age (1986-2004); `
    - the classical age saw the introduction of the main probabilistic formulations for SLAM,
    - including approaches based on 
        - Extended Kalman Filters, 
        - RaoBlackwellised Particle Filters, 
        - and maximum likelihood estimation;
    - moreover, it delineated the basic challenges connected to efficiency and robust data association. 


- classical age의 연구의 참고 문헌 들 `Two other excellent references describing the three main SLAM formulations of the classical age are` 
    - the book of Thrun, Burgard, andFox [240] and 
    - the chapter of Stachniss et al. [234, Ch. 46].

###### [2004-2015 : algorithmic-analysis age] 

- 이후의 연구는 algorithmic-analysis age (2004-2015)라고 불리우고 [64]에 잘 설명되어 있다. `The subsequent period is what we call the algorithmic-analysis age (2004-2015), and is partially covered by Dissanayake etal. in [64]. `
    - The algorithmic analysis period saw the study of fundamental properties of SLAM, 
    - including 
        - observability,
        - convergence, and 
        - consistency. 
    - In this period, 
        - the key role of sparsity towards efficient SLAM solvers was also understood,
        - and the main open-source SLAM libraries were developed.





![](https://i.imgur.com/H3wV6eR.png)
- SLAM 서베이 논문들을 표 1에 정리 하였다. 최근 서베이 논문들은 특정 aspects이나 SLMA의 sub-fields에 초점을 두고 있었다. ` We review the main SLAM surveys to date in Table I,observing that most recent surveys only cover specific aspects or sub-fields of SLAM. `


- 지난 30년간 SLAM이 인기 있었던것은 SLAM이 포함하는 aspects 만 봐도 알수 있다. `The popularity of SLAM in the last 30years is not surprising if one thinks about the manifold aspects that SLAM involves. `
    - At the lower level (called the front-end in Section II) SLAM naturally intersects other research fields such as 
        - computer vision and 
        - signal processing; 
    - at the higher level (that we later call the back-end), SLAM is an appealing mix of 
        - geometry, 
        - graph theory, 
        - optimization, 
        - and probabilistic estimation. 
    - Finally, a SLAM expert has to deal with practical aspects ranging 
        - from sensor calibration 
        - to system integration. 


- 최근 논문 들은 SLAM에 대한 오버뷰와 연구 방향을 제시 하고 있다. `The present paper gives a broad overview of the current state of SLAM, and offers the perspective of part of the community on the open problems and future directions for the SLAM research. `

- 우리의 주 관심은 **metric**과 **semantic SLAM**이다. 추천할 만한 서베이논문은 [160]이다. `Our main focus is on metric and semantic SLAM, and we refer the reader to the recent survey by Lowry etal. [160],`
    - 이논문은 비젼 기반 place recognition과 topological SLAM에 대하여 다루고 있다. ` which provides a comprehensive review of vision based place recognition and topological SLAM.`
    
```
[160] S. Lowry, N. Sunderhauf, P. Newman, J. J. Leonard, D. Cox, P. Corke, and M. J. Milford. Visual Place Recognition: A Survey. IEEE Transactions on Robotics (TRO), 32(1):1–19, 2016.

```

### SLAM에 대한 두가지 논의 점 

- 좀더 깊게 들어 가기 전에 아래 두 물음에 대하여 살펴 보자 `Before delving into the paper, we first discuss two questions that often animate discussions during robotics conferences: `
    - (1) do autonomous robots need SLAM? and 
    - (2) is SLAM solved as an academic research endeavor? 
- 이 질문에 대하여서는 후반부에 다시 언급하겠다. `We will revisit these questions at the end of the manuscript.`

####  Q 1 : Do autonomous robots really need SLAM?


- 첫번째 질문에 답변하기 위해서는 무엇이 SLAM을 Unique하게 만드는지 이해 해야 한다. `Answering the question “Do autonomous robots really need SLAM?” requires understanding what makes SLAM unique.`

- 슬램의 목표는 글로벌하고 일관된 representation을 생성 하는것이다. S`LAM aims at building a globally consistent representation of the environment,`
    - leveraging both ego-motion measurements and loop closures. 

- 키워드는 loop closure이다. `The keyword here is “loop closure”:`
    - loop closure를 포기 하면 odometry를 줄일수 있다. `if we sacrifice loop closures, SLAM reduces to odometry. `

- 초창기에는 odometry는 바퀴 인코더를 통해서 얻었다. `In early applications, odometry was obtained by integrating wheel encoders. `

- 바퀴 odometry 로 예측한 Pose는 쉽게 drifts되어 몇미터만 이동하여도 쓸모없게 된다. `The pose estimate obtained from wheel odometry quickly drifts, making the estimate unusable after few meters[128, Ch. 6]; `


- 이것이 스램을 개발하는데 문제점이다. `this was one of the main thrusts behind the development of SLAM:` 
    - 랜드마크를 관찰하는 방법은 이런 trajectory drift를 줄여 주고 보정도 가능하게 한다. `the observation of external landmarks is useful to reduce the trajectory drift and possibly correct it [185]. `
    - 최근의 odometry 알고리즘은 비쥬얼 기반이며 inertial 정보를 사용하여 매우 작은 에러를 가진다. ` However, more recent odometry algorithms are based on visual and inertial information, and have very small drift(< 0.5% of the trajectory length [82]). `

따라서, 첫번째 질문은 다음과 같이 3가지로 legitimate된다. ` Hence the question becomes legitimate: do we really need SLAM? Our answer is three-fold.`

##### Q 1.1

- 최근 10년간의 슬램 연구들은 visual-inertial odometry알고리즘을 itself produced해다. `First of all, we observe that the SLAM research done over the last decade has itself produced the visual-inertial odometry algorithms that currently represent the state of the art, e.g., [163, 175];` 

- 이런 관점에서 VIN은 SLAM이다. `in this sense Visual-Inertial Navigation(VIN) is SLAM:`
    - VIN은 loop closure가 제거된 간소화(Reduced)된 SLAM시스템이다. ` VIN can be considered a reduced SLAM system, in which the loop closure (or place recognition) module is disabled. `

- SLAM은 센서 퓨전에 대한 연구를 이끌어 왔다. `More generally, SLAM has directly led to the study of sensor fusion under more challenging setups (i.e., no GPS, low quality sensors) than previously considered in other literature (e.g., inertial navigation in aerospace engineering).`

##### Q 1.2

The second answer regards the true topology of the environment.A robot performing odometry and neglecting loopclosures interprets the world as an “infinite corridor” (Fig. 1-left) in which the robot keeps exploring new areas indefinitely.A loop closure event informs the robot that this “corridor”keeps intersecting itself (Fig. 

1-right). 

The advantage of loopclosure now becomes clear: by finding loop closures, therobot understands the real topology of the environment, andis able to find shortcuts between locations (e.g., point Band C in the map). 

Therefore, if getting the right topologyof the environment is one of the merits of SLAM, whynot simply drop the metric information and just do placerecognition? The answer is simple: the metric informationmakes place recognition much simpler and more robust; themetric reconstruction informs the robot about loop closure opportunitiesand allows discarding spurious loop closures [150].Therefore, while SLAM might be redundant in principle (anoracle place recognition module would suffice for topologicalmapping), SLAM offers a natural defense against wrong dataassociation and perceptual aliasing, where similarly lookingscenes, corresponding to distinct locations in the environment,would deceive place recognition. 

In this sense, the SLAM mapprovides a way to predict and validate future measurements:we believe that this mechanism is key to robust operation






