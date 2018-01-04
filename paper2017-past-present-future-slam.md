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
    - 이런 알려진 랜드마크를 이용하여 localization이 가능한 시나리오에서는 SLAM이 꼭 필요 하지 않다. `
In such scenarios, SLAM may not be required if localization can be done reliably with respect to the known landmarks.`


- The popularity of the SLAM problem is connected with the emergence of indoor applications of mobile robotics. 
    -     
 
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

- 두번째 대답은 true topology에 관한 것이다. `The second answer regards the true topology of the environment.`

![](https://i.imgur.com/0KbpSfo.png)

```
[Fig. 1: Left:]
- map built from odometry. 
- The map is homotopic to a long corridor that goes from the starting position A to the final position B. 
- Points that are close in reality (e.g., B and C) may be arbitrarily far in the odometric map.

[Fig. 1: Right:]
- map build from SLAM. 
- By leveraging loop closures, SLAM estimates the actual topology of the environment, and “discovers” shortcuts in the map.
```

- odometry를 수행하며 LC를 무시하면 로봇은 세상을 “infinite corridor”로 간주 하게 된다. `A robot performing odometry and neglecting loop closures interprets the world as an “infinite corridor” (Fig. 1-left) in which the robot keeps exploring new areas indefinitely.`


-LC는 로봇에게 corridor가 겹치는걸 알려 준다. `A loop closure event informs the robot that this “corridor”keeps intersecting itself (Fig. 1-right). `

- LC의 장점은 다음과 같다. `The advantage of loopclosure now becomes clear: by finding loop closures,`
    - 토폴로지를 이해 할수있고 `the robot understands the real topology of the environment, `
    - 최단 경로를 계산 할수 있다. `and is able to find shortcuts between locations (e.g., point Band C in the map). `

- 따라서 정확한 토폴로지를 아는게 SLAM의 장점 이라면 왜 metric를 drop하고 단순히 place recognition만 하지 않는 것인가? `Therefore, if getting the right topology of the environment is one of the merits of SLAM, why not simply drop the metric information and just do place recognition? `
    - 답변은 간단하다. Metric정보는 place recognition를 쉽게 하도록 도와 주면 강건성이 증가 한다. `The answer is simple: the metric information makes place recognition much simpler and more robust; `
    - metric reconstruction는 로봇에게 LC가 가능하게 한다. `the metric reconstruction informs the robot about loop closure opportunities and allows discarding spurious loop closures [150].`

- Therefore, while SLAM might be redundant in principle (an oracle place recognition module would suffice for topological mapping), SLAM offers a natural defense against wrong data association and perceptual aliasing, where similarly looking scenes, corresponding to distinct locations in the environment,would deceive place recognition. 

- In this sense, the SLAM map provides a way to predict and validate future measurements:we believe that this mechanism is key to robust operation


##### Q 1.3 

- 세번째 대답은 SLAM은 globally consistent map을 필요로 하는 많은 서비스에 필요로 한다. `The third answer is that SLAM is needed for many applications that, either implicitly or explicitly, do require a globally consistent map. `

- 예를 들어 대부분의 로봇의 목표는 주변을 돌아 다니면서 지도를 사용자에게 전달 하는 것이다. `For instance, in many military and civilian applications, the goal of the robot is to explore an environment and report a map to the human operator, ensuring that full coverage of the environment has been obtained.`

- 또 다른 예로는 구조물에 대한 검사를 하는 롯봇이다. 이 경우에 **globally consistent 3D reconstruction**는 꼭 필요 하다. `Another example is the case in which the robot has to perform structural inspection (of a building, bridge, etc.); also in this case a globally consistent 3D reconstruction is a requirement for successful operation.`

#### Q 2 : is SLAM solved?

- 이 질문은 로보틱스 커뮤니티에서 자주 회자 되는 질문이다. `This question of “is SLAM solved?” is often asked within the robotics community, c.f. [87]. `

- 이 질문은 특정환경/로봇/성능에 따라 다르므로 답변하기 어려운 주제이다. `This question is difficult to answer because SLAM has become such abroad topic that the question is well posed only for a given robot/environment/performance combination. `


- SLAM기술이 완벽한지 평가 하려면 아래 사항들에 대하여 정의 되어야 한다. `In particular,one can evaluate the maturity of the SLAM problem once the following aspects are specified:`
    - robot: 
        - type of motion (e.g., dynamics, maximum speed), 
        - available sensors (e.g., resolution, sampling rate), 
        - avail-able computational resources;
    - environment: 
        - planar or three-dimensional, 
        - presence of natural or artificial landmarks, 
        - amount of dynamic elements, 
        - amount of symmetry and risk of perceptual aliasing. 
        - Note that many of these aspects actually depend on the sensor-environment pair: for instance, two rooms may look identical for a 2D laser scanner (perceptual aliasing), while a camera may discern them from appearance cues;
    - performance requirements: 
        - desired accuracy in the estimation of the state of the robot, 
        - accuracy and type of representation of the environment (e.g., landmark-based or dense), 
        - success rate (percentage of tests in which the accuracy bounds are met), 
        - estimation latency, 
        - maximum operation time, 
        - maximum size of the mapped area

- 예를 들어 아래 상황에 대한 SLAM은 Mature하다고 볼수 있다. 
    - `For instance, mapping a 2D indoor environment with a robot equipped with wheel encoders and a laser scanner,with sufficient accuracy (< 10cm) and sufficient robustness(say, low failure rate), can be considered largely solved (an example of industrial system performing SLAM is the Kuka Navigation Solution [145]). `
    - 비슷한 비젼 기반 SLMA역시 Mature한 연구 결과이다. `Similarly, vision-based SLAM with slowly-moving robots (e.g., Mars rovers [166], domesticrobots [114]), and visual-inertial odometry [94] can be considered mature research fields.`
  
      
- 하지만 다른 상황에 대한 SLAM은 Mature하다고 볼수 없다. `On the other hand,`
    - other robot/environment/performance combinations still deserve a large amount of fundamental research. 


- 오늘날 SLAM알고리즘들은 로봇의 모션이나 환경이 challenging 하면 좋은 성과를 보이지 않는다. `Current SLAM algorithms can be easily induced to fail when either the motion of the robot or the environment are too challenging (e.g., fast robot dynamics, highly dynamic environments); `
    - similarly, SLAM algorithms are often unable to face strict performance requirements, 
        - e.g., high rate estimation for fast closed-loop control. 

###### [2016- : the robust-perception age] 

- 본 논문에서는 SLAM연구가 새로운 전기를 맞이 하고 있다고 본다. `In this paper, we argue that we are entering in a third era for SLAM,` 

- robust-perception age는 아래의 요구사항을 가진다. `the robust-perception age, which is characterized by the following key requirements:`

1. robust performance: 
    - the SLAM system operates with low failure rate for an extended period of time in a broad set of environments; 
    - the system includes fail-safe mechanisms and has self-tuning capabilities[[1]](#11) in that it can adapt the selection of the system parameters to the scenario.

2. high-level understanding: 
    - the SLAM system goes beyond basic geometry reconstruction to obtain a high-level understanding of the environment 
    - (e.g., high-level geometry, **semantics**, physics, affordances);

3. resource awareness: 
    - the SLAM system is tailored to the available sensing and computational resources, and provides means to adjust the computation load depending on the available resources;
    
4. task-driven perception: 
    - the SLAM system is able to select relevant perceptual information and filter out irrelevant sensor data, 
    - in order to support the task the robot has to perform; moreover, the SLAM system produces adaptive map representations, whose complexity may vary depending on the task at hand.

### 논문 구성 

Paper organization. 

- Section II : 공식 및 구조 `The paper starts by presenting a standard formulation and architecture for SLAM `

- Section III : 강건성 `tackles robustness in life-long SLAM. `

- Section IV : 확장성 `deals with scalability. `

- Section V : discusses how to represent the geometry of the environment. 

- Section VI : extends the question of the environment representation to the modeling of semantic information. 

- Section VII : 최근 학문적 성과물 오버뷰 `provides an overview of the current accomplishments on the theoretical aspects of SLAM. `

- Section VIII : 문제점 `broadens the discussion and reviews the active SLAM problem in which decision making is used to improve the quality of the SLAM results. `

- Section IX : 최신 트랜드(센서, 딥러닝) `provides an overview of recent trends in SLAM, including the use of unconventional sensors and deep learning. `

- Section X : 정리 `provides final remarks. `

Throughout the paper, we provide many pointers to related work outside the robotics community. 

Despite its unique traits, SLAM is related to problems addressed in computer vision, computer graphics, and control theory, and cross-fertilization among these fields is a necessary condition to enable fast progress.


- 비 전문가 독자들은 [7, 69]을 먼저 읽어 보길 권한다. `For the non-expert reader, we recommend to read DurrantWhyte and Bailey’s SLAM tutorials [7, 69] before delving in this position paper. `

```
[7] T. Bailey and H. F. Durrant-Whyte. Simultaneous Localisation and Mapping (SLAM): Part II. Robotics and Autonomous Systems (RAS), 13(3):108–117, 2006.

[69] H. F. Durrant-Whyte and T. Bailey. Simultaneous Localisation and Mapping (SLAM): Part I. IEEE Robotics and Automation Magazine, 13(2):99–110, 2006.
```

## II. ANATOMY OF A MODERN SLAM SYSTEM

- The architecture of a SLAM system includes two main components: 
    - the front-end 
    - the back-end. 

![](https://i.imgur.com/ZX089mc.png)
```
[Fig. 2: Front-end and back-end in a typical SLAM system.]
-  The back-end can provide feedback to the front-end for loop closure detection and verification.
```

- **The front-end** abstracts sensor data into models that are amenable for estimation, 

- **The back-end** performs inference on the abstracted data produced by the front-end. 

### 2.1 Maximum a posteriori (MAP) estimation and the SLAM back-end.

- SLAM의 공식들은 [161], [101]을 기반을 두고 있다. `The current de-facto standard formulation of SLAM has its origins in the seminal paper of Lu and Milios [161], followed by the work of Gutmann and Konolige [101].`

- 위 내용을 기반으로 개선된 방식[63, 81, 100, 125, 192, 241]들이 제안 되었다. `Since then, numerous approaches have improved the efficiency and robustness of the optimization underlying the problem[63, 81, 100, 125, 192, 241]. `

All these approaches formulate SLAM as a maximum a posteriori estimation problem, and often use the formalism of factor graphs [143] to reason about the interdependence among variables.

Assume that we want to estimate an unknown variable X ; as mentioned before, in SLAM the variable X typically includes the trajectory of the robot (as a discrete set of poses) and the position of landmarks in the environment. 

We are givena set of measurements Z = {zk : k = 1, . 

. 

. 

, m} such thateach measurement can be expressed as a function of X , i.e.,zk = hk(Xk)+k, where Xk ⊆ X is a subset of the variables,hk(·) is a known function (the measurement or observationmodel), and k is random measurement noise.

### 2.2 Sensor-dependent SLAM front-end



## III. LONG-TERM AUTONOMY I: ROBUSTNESS


## IV. LONG-TERM AUTONOMY II: SCALABILITY


---

<a name="11">[1]</a> The SLAM community has been largely affected by the “curse of manual tuning”, in that satisfactory operation is enabled by expert tuning of the system parameters (e.g., stopping conditions, thresholds for outlier rejection).  <br/>




Indoor operation rules out the use of GPS to bound the localization error; furthermore, SLAM provides an appealing alternative to user-built maps, showing that robot operation is possible in the absence of an ad hoc localization infrastructure.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1NzU5MTc4OV19
-->