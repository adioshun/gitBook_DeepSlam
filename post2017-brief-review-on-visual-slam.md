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

- 그래프 슬램은 불필요한 정보를 줄여 줌으로 큰 지도작업에 강점을 보인다. `Graph SLAM shows its advantages in large scale mapping, since a graph can be easily sparsified to reduce redundant information. `

### 4.1 Square Root SAM (Smoothing and Mapping) [29], iSAM [30] and iSAM2 [31]

- M. Kaess, F. Dellaert et al.’s works, including Square Root SAM (Smoothing and Mapping) [29], iSAM [30] and iSAM2 [31], contributed a lot in theory for this problem. 

- They investigated the theory and performance of graphical model for** map representation** and **matrix factorization** for valuable elimination and graph sparsification. 

### 4.2 FAB-MAP [32]

- Another famous work is FAB-MAP [32] by M. Cummins and P. Newman, 

- which utilizes **visual bag-of-words** to do image retrieval for **loop closure detection**.

### 4.3 loop closure detection

- The problem of loop closure detection is still far from solved, 
 - with challenges mainly in place recognition in long-term SLAM [33], 
 - due to the illumination change, view-point change, dynamic or semi-dynamic objects and many other `pollution’ factors within one scene at different visited moments.
 

## 5. Modern State of Art Systems

- 로봇과 컴퓨터 비젼의 연구 결과가 합쳐지고 있다. 

- 이전 연구 결과물을 기반으로 둘을 합치고 있다. `They are built with many former researchers’ work results as foundation, `

- 예를 들어 `for example `
 - the improved image feature detector and descriptors like ORB [34] provide real-time performance with desktop CPU which SIFT or SURF cannot provide; 
 - some nonlinear least square optimization libraries like g2o [27] provide utilities to do **bundle adjustment**, etc. 
 
- 특히 아래 두 연구는 커뮤니티에 많은 도움이 되었다.  
 - ORB-SLAM [25] by R. Mur-Artal et al. and 
 - LSD-SLAM (Large-Scale Direct Monocular SLAM) [35] by J. Engel et al. 


![](https://i.imgur.com/3QDRVWY.png)

```
Figure 2: State of art visual SLAM systems. 
- Left: result of LSD-SLAM. 
- Right: result of ORB-SLAM.
```

### 5.1 ORB-SLAM 

- ORB-SLAM은 전통적인 특징 기반 시스템이며, PTAM과 유사하다. 하지만 좋은 성능을 보인다. `ORB-SLAM is a more traditional feature based system, and quite similar to PTAM in some way, yet attains much more impressive performance in practice. `

#### A. 장점 `Its main improvement compared to PTAM includes but not limited to: `


- 1) 루프결합 제공 : implement 3 parallel threads, namely tracking, mapping, and loop closing to achieve consistent localization and mapping, 
 - while PTAM does not have loop closing; 


- 2) 초기화 방법 제공 : automatic map initialization with a model selection on two paralleling thread calculating Homography and Fundamental ego-motion with RANSAC, 
 - while PTAM requires manual operation to finish initialization; 


- 3) ORB 특징을 이용하여 강건성 제공 : use **ORB feature** detector and descriptor instead of image patches used in PTAM, improving **robustness** of image tracking and feature matching under scale and orientation change; 


- 4) multi-scale mapping, including local graph for pose bundle adjustment, co-visibility graph for local bundle adjustment, and essential graph for global bundle adjustment after loop closure detection.


### 5.2 LSD-SLAM

- LSD-SLAM은 PTAM이나 ORB-SLAM과는 다르다. `LSD-SLAM is quite different from PTAM or ORB-SLAM. `

- 이 방식은 **direct methods**분류에 속한다. `It should be classified into so-called direct methods`, 
 - 즉, 이미지 특징이 아닌 **픽셀**에서 바로 상태 예측을 수행한다. `that is, doing state estimation based on image pixels directly, rather than relying on image features.`

- 트래킹은 performed by se(3) image alignment using a **coarse-to-fine algorithm** with a **robust Huber loss**. 

- 깊이 측정은 다른 스램과 유사하게 **inverse depth parametrization**을 사용한다. `Depth estimation is just like many other SLAM systems, using an inverse depth parametrization with a bundle of relatively small baseline image pairs.`

- 지도 최적화는 일반적으로 사용되는 **graph optimization**를 사용한다. `Map optimization is also executed in commonly used graph optimization, with existing keyframe poses expressed in sim(3) space just like ORB-SLAM does. `

- LSD-SLAM actually recovers a `semi-dense` map, 
 - since it only estimates depth at pixels solely near image boundaries, 
 - which may be the main reason for it to be the first direct visual SLAM system that can run in real-time on a CPU. 

- 실 적용상황에서는 dense visual SLAM systems(eg.DTAM)같은 모든 픽셀 단위 계산은 계산 부하가 크므로 GPU를 사용한다. `In practice, processing every pixel over all image sequences is very computationally consuming, which is why many dense visual SLAM systems, like DTAM (Dense Tracking and Mapping) [36] by A. Davison’s group, require a GPU to attain real-time performance.`


- 비쥬얼 슬램 기술이 완성되어 감에 따라 상용 제품도 많이 출시 되고 있다: **Google Tango**, **MS Hololens** ` The maturity of visual SLAM can also be reflected from their application in commercial products, among which the Google Tango and Microsoft Hololens attract most interest from the public. It can be predicted that there will be more visual SLAM driven products appear in the near future.`

## 6. What’s Next?

### 6.1 More Semantic Information: From CV to Robotics

- 큰 지도 작성`(large scale mapping)` 부분에서 남은 연구 분야는 공간 인지`(place recognition)` 이다. `As mentioned above, the main challenge in large scale mapping remains in long term visual place recognition. `

- 이 문제는 geometric methods만으로는 어렵다. `This problem is extremely difficult to solve based only on geometric methods, which are what most current visual SLAM systems use. `

- 최근 몇년동안 이미지에 있는 semantic정보를 이용하여 물체를 탐지 하고 공간을 인지 하려는 연구가 진행 되었다. `These several years has seen some effort in utilizing semantic information in image to do object detection for mapping and scene recognition,`
 - such as **SLAM++ [38]** by R. F. Salas-Moreno et al. 

- 공간 인지의 본질적인 어려움으로 인해 비쥬얼 슬램에 시멘틱 정보를 이용하려는 노력은 계속 될것으로 보인다. `Due to complicated nature of place recognition problem, increasing number of researches on the utilization of visual semantic information in visual SLAM is predictable in recent future. `

- 이미 여러 학회에서 이런 연구가 진행 되고 있다. `In fact, this has already been happening, reflected by the frequent appearance of this topic in CVPR, RSS and ICRA workshops in recent years, as shown in Figure 3.`

- 이전에도 비쥬얼 슬램에 대한 로봇연구는 컴퓨터 비젼의 연구 결과의 도움을 많이 받았다. `Historically, robotic researchers on visual SLAM benefited a lot from research work of computer vision community. `

- 최근 딥러닝에 대한 연구가 인기가 있으니 딥러닝이 로보틱스 스램 연구에 적용될수 있다. `These years, as the booming of deep learning in computer vision field, it is also of high possibility that deep learning style methods will soon take their part in visual SLAM or other research fields in robotics. Let’s see.`

### 6.2 More Sensor Fusion: Towards Robustness for Practical Use

- 이와 반대로 비쥬얼 슬램을 위한 geometric methods 역시 완성도가 높아져 가고 있다. 상품에 적용될수로 **강건성**에 대한 이슈가 생길 것이다. `On the other hand, as geometric methods for visual SLAM gradually become mature, the day of its application in civil and industrial environment is approaching (or has approached, in some way, especially in VR/AR), which bring forward the issues of robustness. `

- 앞서 언급한 최근 비쥬얼 슬램 시스템은 모바일 로봇에 적용하기에는 어렵다. `The state of art visual SLAM system mentioned above are far from being truly usable for mobile robot navigation (even if not consider the unrecovered scale problem of monocular vision). `

- 취약한 강건성으로 인한 문제가 발생 할것이다. `The leading limitation lies in their poor robustness. `

- 강건성 문제는 비젼 기반 방식의 본질적 문제점 이다. `Robustness issue is an inherent problem of pure vision-based methods,`
 - due to the fact that image tracking is easy to fail in many motion modes and many environment structures. 

- 따라서 이미지와 다른 센서 정보를 퓨전 하여 강건성을 높이는 방법이 필요 하다. `Therefore, research work on fusing image with other sensors to achieve robust mobile robot navigation is highly demanded.`


---

## References
```
[1] H. Durrant-Whyte and T. Bailey. Simultaneous localization and mapping: part i. Robotics Automation Magazine, IEEE, 13(2):99–110, June 2006.

[2] J. J. Leonard and H. F. Durrant-Whyte. Simultaneous map building and lo- calization for an autonomous mobile robot. In Intelligent Robots and Systems ’91. ’Intelligence for Mechanical Systems, Proceedings IROS ’91. IEEE/RSJ International Workshop on, pages 1442–1447 vol.3, Nov 1991.

[3] J. S. Gutmann and K. Konolige. Incremental mapping of large cyclic envi- ronments. In Computational Intelligence in Robotics and Automation, 1999. CIRA ’99. Proceedings. 1999 IEEE International Symposium on, pages 318– 325, 1999.

[4] S. Thrun, W. Burgard, and D. Fox. A probabilistic approach to concurrent mapping and localization for mobile robots. Autonomous Robots, 5(3-4):253– 271, 1998.

[5] M. W. M. G. Dissanayake, P. Newman, S. Clark, H. F. Durrant-Whyte, and M. Csorba. A solution to the simultaneous localization and map building (slam) problem. IEEE Transactions on Robotics and Automation, 17(3):229– 241, Jun 2001.

[6] S. Thrun, W. Burgard, and D. Fox. Probabilistic robotics. MIT press, 2005.

[7] D. Scaramuzza and F. Fraundorfer. Visual odometry [tutorial]. Robotics & Automation Magazine, IEEE, 18(4):80–92, 2011.

[8] H. P. Moravec. Obstacle avoidance and navigation in the real world by a seeing robot rover. Technical report, DTIC Document, 1980.

[9] S. Lacroix, A. Mallet, R. Chatila, and L. Gallo. Rover self localization in planetary-like environments. In Artificial Intelligence, Robotics and Automa- tion in Space, volume 440, page 433, 1999.

[10] T. Malisiewicz. The Future of Real-Time SLAM and “Deep Learning vs SLAM” . http://www.computervisionblog.com/2016/01/why-slam-matters-future-of-real-time.html, 2016.

[11] A. Fitzgibbon and A. Zisserman. Automatic camera recovery for closed or open image sequences. Computer VisionECCV’98, pages 311–326, 1998.

[12] A. Fitzgibbon, G. Cross, and A. Zisserman. Automatic 3d model construction for turn-table sequences. 3D Structure from Multiple Images of Large-Scale Environments, pages 155–170, 1998.

[13] M. Pollefeys, R. Koch, and L. Van Gool. A simple and efficient rectification method for general motion. In Computer Vision, 1999. The Proceedings of the Seventh IEEE International Conference on, volume 1, pages 496–501. IEEE, 1999.

[14] M. Pollefeys. Self-calibration and metric 3D reconstruction from uncali- brated image sequences. PhD thesis, 1999.

[15] R. Hartley and A. Zisserman. Multiple view geometry in computer vision. Cambridge university press, 2003.

[16] A. J. Davison. Real-time simultaneous localisation and mapping with a single camera. In Computer Vision, 2003. Proceedings. Ninth IEEE International Conference on, pages 1403–1410. IEEE, 2003.

[17] A. J. Davison and D. W. Murray. Simultaneous localization and map-building using active vision. Pattern Analysis and Machine Intelligence, IEEE Trans- actions on, 24(7):865–880, 2002.

[18] A. J. Davison, I. D. Reid, N. D. Molton, and O. Stasse. Monoslam: Real- time single camera slam. Pattern Analysis and Machine Intelligence, IEEE Transactions on, 29(6):1052–1067, 2007.

[19] M. Pupilli and A. Calway. Real-time camera tracking using a particle filter. In BMVC, 2005.

[20] M. Pupilli and A. Calway. Real-time visual slam with resilience to erratic motion. In 2006 IEEE Computer Society Conference on Computer Vision and Pattern Recognition (CVPR’06), volume 1, pages 1244–1249, June 2006.

[21] M. Montemerlo, S. Thrun, D. Koller, B. Wegbreit, et al. Fastslam: A fac- tored solution to the simultaneous localization and mapping problem. In AAAI/IAAI, pages 593–598, 2002.

[22] D. Nister, O. Naroditsky, and J. Bergen. Visual odometry. In Computer Vision and Pattern Recognition, 2004. CVPR 2004. Proceedings of the 2004 IEEE Computer Society Conference on, volume 1, pages I–652–I–659 Vol.1, June 2004.

[23] J. Montiel, J. Civera, and A. J. Davison. Unified inverse depth parametrization for monocular slam. analysis, 9:1, 2006.

[24] G. Klein and D. Murray. Parallel tracking and mapping for small ar workspaces. In Mixed and Augmented Reality, 2007. ISMAR 2007. 6th IEEE and ACM International Symposium on, pages 225–234. IEEE, 2007.

[25] R. Mur-Artal, J. M. M. Montiel, and J. D. Tards. Orb-slam: A versa- tile and accurate monocular slam system. IEEE Transactions on Robotics, 31(5):1147–1163, Oct 2015.

[26] C. Forster, M. Pizzoli, and D. Scaramuzza. Svo: Fast semi-direct monocular visual odometry. In Proc. IEEE Intl. Conf. on Robotics and Automation, 2014.

[27] G. Grisetti, H. Strasdat, K. Konolige, and W. Burgard. g2o: A general frame- work for graph optimization. In IEEE International Conference on Robotics and Automation, 2011.

[28] E. Eade and T. Drummond. Monocular slam as a graph of coalesced obser- vations. In 2007 IEEE 11th International Conference on Computer Vision, pages 1–8, Oct 2007.

[29] F. Dellaert and M. Kaess. Square root sam: Simultaneous localization and mapping via square root information smoothing. The International Journal of Robotics Research, 25(12):1181–1203, 2006.

[30] M. Kaess, A. Ranganathan, and F. Dellaert. isam: Incremental smoothing and mapping. Robotics, IEEE Transactions on, 24(6):1365–1378, Dec 2008.

[31] M. Kaess, H. Johannsson, R. Roberts, V. Ila, J. Leonard, and F. Dellaert. isam2: Incremental smoothing and mapping with fluid relinearization and incremental variable reordering. In Robotics and Automation (ICRA), 2011 IEEE International Conference on, pages 3281–3288, May 2011.

[32] M. Cummins and P. Newman. Fab-map: Probabilistic localization and map- ping in the space of appearance. The International Journal of Robotics Re- search, 27(6):647–665, 2008.

[33] S. Lowry, N. Snderhauf, P. Newman, J. J. Leonard, D. Cox, P. Corke, and M. J. Milford. Visual place recognition: A survey. IEEE Transactions on Robotics, 32(1):1–19, Feb 2016.

[34] E. Rublee, V. Rabaud, K. Konolige, and G. Bradski. Orb: An efficient alter- native to sift or surf. In 2011 International Conference on Computer Vision, pages 2564–2571, Nov 2011.

[35] J. Engel, T. Sch ̈ops, and D. Cremers. Lsd-slam: Large-scale direct monocular slam. In Computer Vision–ECCV 2014, pages 834–849. Springer, 2014.

[36] R. A. Newcombe, S. J. Lovegrove, and A. J. Davison. Dtam: Dense tracking and mapping in real-time. In Computer Vision (ICCV), 2011 IEEE Interna- tional Conference on, pages 2320–2327. IEEE, 2011.

[37] Australian centre for robotic vision public. https://roboticvision.atlassian.net/wiki/display/PUB/RVSS2015+Robotic+ Vision+Summer+School+Presentations, 2016

[38] R. F. Salas-Moreno, R. A. Newcombe, H. Strasdat, P. H. J. Kelly, and A. J. Davison. Slam++: Simultaneous localisation and mapping at the level of objects. In Computer Vision and Pattern Recognition (CVPR), 2013 IEEE Conference on, pages 1352–1359, June 2013.
```