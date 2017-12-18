# The Future of Real-Time SLAM and Deep Learning vs SLAM

> 출처 : [Tombone's Computer Vision Blog](http://www.computervisionblog.com/2016/01/why-slam-matters-future-of-real-time.html)


## Part I: Why SLAM Matters

- SLAM is prime example of a what is called a "Geometric Method" in Computer Vision.
- eg. CMU의 computer vision강의 = Learning-based Methods in Vision + Geometry-Based Methods in Vision 로 나누어짐

- SLAM algorithms are complementary to ConvNets and Deep Learning:
- SLAM focuses on geometric problems
- Deep Learning is the master of perception (recognition) problems.

> If you want a robot to go towards your refrigerator without hitting a wall, use SLAM. If you want the robot to identify the items inside your fridge, use ConvNets.


- SLAM is a real-time version of Structure from Motion (SfM)


### - Structure from Motion vs Visual SLAM

- Structure from Motion (SfM) and SLAM are solving a very similar problem, 
    - SfM is traditionally performed in an offline fashion
    - SLAM has been slowly moving towards the low-power / real-time / single RGB camera mode of operation. 


- SfM 문제점 : 큰 구조물은 많은 사진이 필요 하고 처리 하는데 많은 시간이 걸림. 

```
given a large collection of photos of a single outdoor structure (like the Colliseum), construct a 3D model of the structure and determine the camera's poses. The image collection is processed in an offline setting, and large reconstructions can take anywhere between hours and days. 
```

- sfM 관련 소프트웨어 라이브러리 
    - Bundler, an open-source Structure from Motion toolkit
    - Libceres, a non-linear least squares minimizer (useful for bundle adjustment problems)
    - Andrew Zisserman's Multiple-View Geometry MATLAB Functions
    
## Part II: The Future of Real-time SLAM

- MonoSLAM (2003년 Andrew Davison 주도)
- PTAM
- FAB-MAP
- DTAM
- KinectFusion


![](https://3.bp.blogspot.com/-Oh94IZlctLA/VpWlSwN_WEI/AAAAAAAAOdw/fKDBj8KQoGM/s400/robotvision-01.png)


### - Talk 1: Christian Kerl on Continuous Trajectories in SLAM


### - Talk 2: Semi-Dense Direct SLAM by Jakob Engel

> 생략 ...

## Part III: Deep Learning vs SLAM

> workshop presenters agreed that **semantics** are necessary to build bigger and better SLAM systems

### - Integrating semantic information into SLAM

- "Will end-to-end learning dominate SLAM?"





