# 시각적 주행거리 측정 방법 (Visual Odometry) 

> 출처 : [시각적 주행거리 측정 방법 (Visual Odometry)](https://timefire.blog.me/140189696134)

- 정의 : 카메라 이미지를 분석하여 로봇의 위치와 방향을 결정하는 과정, `VO is the process of incrementally estimating the pose of the vehicle by examining the changes that motion induces on the images of its onboard cameras`

- 장점 : 주행 거리를 추정하기 위해 연속적인 카메라 이미지를 사용하여 상응하는 주행거리 측정 정보를 결정하는 과정
 - Contrary to wheel odometry, VO is not affected by wheel slippage on uneven terrain or other adverse conditions.
 - More accurate trajectory estimates compared to wheel odometry (relative position error 0.1% − 2%)
 - Crucial for flying, walking, and underwater robots
 
- VO Assumption  
 - Sufficient illumination in the environment
 - Dominance of static scene over moving objects
 - Enough texture to allow apparent motion to be extracted
 - Sufficient scene overlap between consecutive frames
 
## 1. 단계 

1. 입력 이미지 습득: 단일 카메라, 스테레오 카메라, 전방향 카메라 등을 사용
2. 이미지 보정: 렌즈 왜곡 제거를 위한 영상 처리 기법을 적용
3. 특성 검출: 관심 연산자를 정의하고 프레임에 걸쳐 일치하는 특성을 찾고 광학 흐름 필드를 구축
 - 3.1 두 이미지의 관련성을 설정하기 위해 상관 관계를 사용하고 장기 특성 추적은 하지 않음
 - 3.2 특성 추출 및 연관성 성립
 - 3.3 광학 흐름 필드 구축

4. 잠재적인 추적 오류를 위해 흐름 필드 벡터를 확인하고 분리물을 제거
5. 광학 흐름으로부터 카메라 움직임을 추정
 - 5.1 선택 1: 상태 추정 배포 유지를 위해 칼만 필터 사용
 - 5.2 선택 2: 두 인접 이미지 사이의 재투영 오류를 기반으로 비용 함수를 최소화하는 기능의 기하학적, 3D 속성을 찾음. 이는 수학적 최소화나 랜덤 샘플링을 통하여 수행될 수 있음

6. 이미지를 통한 적용 범위를 유지하기 위하여 추적점의 주기적인 확인



## 2. History 
- 1980: First known VO real-time implementation on a robot by Hans Moraveck PhD
thesis (NASA/JPL) for Mars rovers using one sliding camera (sliding stereo).

- 1980 to 2000: The VO research was dominated by NASA/JPL in preparation of the 2004 mission to Mars

- 2004: VO was used on a robot on another planet: Mars rovers Spirit and Opportunity
(see seminal paper from NASA/JPL, 2007)

- 2004. VO was revived in the academic environment by David Nister’s «Visual Odometry» paper.
The term VO became popular.

## 주요 연구 결과 

- Scaramuzza, D., Fraundorfer, F., Visual Odometry: Part I - The First 30 Years and
Fundamentals, IEEE Robotics and Automation Magazine, Volume 18, issue 4, 2011. PDF

- raundorfer, F., Scaramuzza, D., Visual Odometry: Part II - Matching, Robustness, and
Applications, IEEE Robotics and Automation Magazine, Volume 19, issue 1, 2012. PDF

- C. Cadena, L. Carlone, H. Carrillo, Y. Latif, D. Scaramuzza, J. Neira, I.D. Reid, J.J. Leonard,
Past, Present, and Future of Simultaneous Localization and Mapping: Toward the RobustPerception
Age, IEEE Transactions on Robotics, Vol. 32, Issue 6, 2016. PDF


![](https://i.imgur.com/bki52pZ.png)

> 참고 [why VO](http://rpg.ifi.uzh.ch/docs/teaching/2017/01_introduction.pdf): 

## SFM & VO

- SFM is more general than VO and tackles the problem of 3D reconstruction and 6DOF pose estimation from unordered image sets

- VO is a particular case of SFM

- VO focuses on estimating the 3D motion of the camera sequentially (as a new frame arrives) and in real time.

- Terminology: sometimes SFM is used as a synonym of VO

## Visual SLAM & VO

- Visual Odometry :Focus on incremental estimation/local consistency

- Visual SLAM: Simultaneous Localization And Mapping
 - Focus on globally consistent estimation
 - Visual SLAM = visual odometry + loop detection + graph optimization
 
- The choice between VO and V-SLAM depends on the tradeoff between performance and consistency, and simplicity of implementation.

- VO trades off consistency for real-time performance, without the need to keep track of all the previous history of the camera


