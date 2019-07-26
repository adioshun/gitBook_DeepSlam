# [Vehicle Detection and Pose Estimation in Autonomous Convoys](https://brage.bibsys.no/xmlui/bitstream/handle/11250/2455922/Baardseth_Elisabeth.pdf?sequence=1&isAllowed=y)

> 2017, Master Thesis



## Abstract

Autonomous convoys, also known as platooning, are defined as a group of vehicles driving after one another autonomously. 

Acting as one single unit the gap between them can be significant reduced and hence the fuel costs compared to conventional driving.

본 연구에서는 반자율 주행을 다루고 있다. `In this thesis a semi-automatic two-vehicle military convoy is studied. `

첫번째 차는 사람이 운전하고, 두번째 차는 첫번째 차의 거리, 위치, 속도 정보에 기반하여 자율 주행 하는 모델 `Assume the first vehicle remain in control by humans. The second vehicle should then follow it’s track autonomously based on information about the relative distance, position and velocity of the first vehicle.`


논문의 목적은 차량 탐지와 자세 추정 이다. `The purpose of this thesis is to find and test methods for vehicle detection and pose estimation.`

활용 센서는 Lidar와 카메라이다. `The methods are mainly based on 3D point cloud data gathered by a LiDAR, but information from cameras are also used. `

센서 선정 사유 : The LiDAR is chosen because of it’s robustness in shifting light and weather conditions, but also because most of today’s research on the field is based on camera vision.

분류기 : Classifiers based on the leading vehicle’s geometrical properties was found suitable. 

2D/3D정보를 합치는 POSIT방식도 성능 좋음 `Also the POSIT method, which combines the imaging coordinates with the corresponding 3D properties provides good results. `

성능 결과 : Distance error was measured to around 15% and orientation deviation to ±4°. 

For driving that not require millimetre precision the conclusion it that the methods used are well suited. 

They also have room for improvements as there was several sources of uncertainty in this project.


## 1. Introduction

## 2. Background

### 2.1 Previous work


### 2.2 POS(Pose from Orthography and Scaling)/POSIT(POS with Iterations)

물체의 3D모델이 알려져 있다는 가정 하에, POS/POIST기법을 이용하여 변형, 회전 정보를 예측 할수 있다. `Assuming a 3D model of the object is known, i.e. the relative geometry of a set of feature points, the translation and rotation matrices can be approximated by means of the **POS/POSIT method** from a single image.`

기법 제안자는 [21]이다. `The methods POS and POSIT was first presented by DeMenthon et al. in [21]. `

최소 요구 사항안 4개 이상의 3D feature 쌍과 관련 2D 이미지다. `The methods require minimum four known pairs of 3D feature point coordinates and the corresponding 2D image coordinates.`

```
[21] D. F. DeMenthon and L. S. Davis, “Model-based object pose in 25 lines of code,” International Journal of Computer Vision, vol. 15, pp. 123–141, June 1995.
[22] “Aforge.net: 3d pose estimation.” http://www.aforgenet.com/articles/posit/. Accessed: 2017-05-20.
```

Based on perspective projection the POS method generates a linear equation system based on the given feature point coordinate pairs. When solved an approximate of the current rotation and translation matrices of that object in relation to the camera position is estimated. [21] [22]POSIT is an extended version of POS. 

By implementing POS in an iteration loop the results can be used to estimate an even more accurate approximation. 

The number of iteration can be specified according to available processing time. POSIT converges after only a few iterations, see section 16 in [21].



### 2.3 Imaging geometry (3D coordinates -> 2D Coordinates)


Forward projection : the process of converting 3D world coordinates into 2D image pixel coordinates.

**Imaging geometry** and **perspective projection** is used to create a conversion method from LiDAR 3D-coordinates to camera image 2D-coordinates

![](https://i.imgur.com/Aq1ltga.png)

![](https://i.imgur.com/nHl7rFO.png)

### 2.4 RANSAC





---


## 3. Methods



### 3.1 Vehicle detection


#### 3.1.1 Vehicle properties

##### Visual properties

- colour, shape and illumination
- license plate

##### Geometrical properties

3D Lidar, Four general vehicle properties[25] : 다음장 3.1.2에서 상세히 다룸

1. 90 degree requirement (along the z-axis)
2. Smoothness
3. Convexity (xy-plane/ground plane)
4. Negative gradients (along the z-axis)


```
[25] K. J. Steinemann, P. and J. e. a. Dickmann, “Determining the outline contour of vehicles in 3d-lidar-measurements,” IEEE Intelligent Vehicle Symposium (IV), pp. 479–484, 2011.
```

#### 3.1.2 Point cloud detection


5단계로 구성됨 

##### (1) Normal estimation

##### (2) Ground angle computation



##### (3) Object extraction


##### (4) Clustering


##### (5) Vehicle verification


---

### 3.2 Pose estimation


POSIT-Algorithm에 별도 정리 




















