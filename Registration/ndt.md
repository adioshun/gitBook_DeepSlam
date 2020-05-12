# NDP 

ICP가 고전적인 알고리즘 이다. `The most classic point cloud accurate registration technology is the iterative closest point (ICP) algorithm. `

ICP는 단점이 있음, NDP추천 `However, because ICP is used to find the corresponding point using the nearest neighbor search, the operation is too long, and the initial position of the point cloud is too high, so the normal distributions transform (NDT) algorithm is the main precision Quasi-technical research.`

#### A. History 

- The NDT algorithm was proposed in 2003 by Biber et al. [11]. 

- In 2006, Martin Magnusson [12] summarized 2D-NDT and extended it to the registration of 3D data through 3D-NDT. 
    - Magnusson’s algorithm is faster than the current standard for 3D registration and is often more accurate. 

- In 2011, Cihan [13] proposed a multilayered normal distribution transformation algorithm called MLNDT. 
    - The algorithm divides a point cloud into 8n cells, where n is the number of layers, 
    - replaces the original Gaussian probability function with the Mahalanobis distance function as a fractional function, 
    - and uses the Newton and Levenberg-Marquardt (LM) optimization method to optimize the fractional function, with better registration speed than the previous NDT algorithm. 
    
- In 2013, Cihan [14] further explained the MLNDT algorithm. 

- In 2015, Hyunki Hong and B.H. Lee [15] proposed the key-layered normal distributions transform algorithm (KLNDT) based on the key layer normal distribution transformation; it has a good success rate and accuracy. 

- In 2016, Hyunki Hong and B.H. Lee [16] proposed to convert the reference point cloud into a disk-like distribution suitable for the point cloud structure to improve the registration accuracy of the NDT algorithm. 

- Zhang Xiao [17] performed a feature point search based on the speeded up robust features (SURF) algorithm, an improvement of the 3D-NDT algorithm. 

- Hu Xiuxiang [18] proposed the normal aligned radial feature (NARF) algorithm, which improved NDT. 

- Chen Qingyan [19, 20] study is based on curvature feature of NDT registration method; Zheng Fen [21] et al. 

- improved 3D scale invariant feature transform (3DSIFT) algorithm and 3D-NDT algorithm. 

- 위 여러 연구들은 모두 NDT알고리즘을 정확도와 속도 측면에서 향상 시키는 방안 들이다. `The above methods all improve the original NDT algorithm in different ways, with various accuracy and time advantages. `
    - 이둘은 항상 트레이드 오프다 `However, it has always been a challenge to obtain a balance between time and accuracy when registering large amounts of point cloud data. `

- 본 논문의 제안 `The registration algorithm in this paper improves the normal distribution transformation INDT algorithm in the accurate registration stage, improves the speed of the registration algorithm, and ensures good registration accuracy.`


> 레퍼런스는 여기서 ; https://www.hindawi.com/journals/mpe/2018/7352691/

---




NDT (normal distributions transform)은 정규분포 집합으로 공간을 표현하는 방식을 말한다. 

거리 센서로 수집한 점군이 주어졌을 때, NDT는 일정한 크기의 격자를 설정하고, 각 격자 속의 점의 위치 벡터에 대해 정규분포로 변환하기 위한 평균 벡터와 공분산 행렬을 구한다.
NDT는 점들의 개수에 비해 월등히 적은 분포로 공간을 표현하기 때문에 메모리 효율을 보장하고 저장 공간의 효율을 보장한다 [1]. 

또한, 이 때문에 2개의 다른 위치에서 수집한 점군을 정합하여 그 사이의 위상차를 구할 때에도 NDT는 ICP (iterative closest point)에 비해 대응 쌍 검색의 소요시간이 짧다는 장점이 있다 [2]. 

NDT를 이용한 정합은 대상 점군과 참조 점군을 모두 NDT로 변환하여 정합하므로써 그 효율성이 더 높아졌다 [3].

> 확률적 Normal Distributions Transform 간 다해상도 정합 기법, 홍현기, ICROS2018

[1] M. Magnusson, “The three-dimensional normaldistributions transform: an efficient representation for registration, surface analysis, and loop detection,” Ph.D. dissertation, Orebro universitet, 2009.
[2] M. Magnusson, A. Nuchter, C. Lorken, A. J. Lilienthal, and J. Hertzberg, “Evaluation of 3d registration reliability and speed-a comparison of icp and ndt,” Proc. of IEEE Int. Conf. Robotics and Automation (ICRA), pp. 3907–3912, 2009.
[3] C. Ulas¸ and H. Temeltas¸, “3d multi-layered normal distribution transform for fast and long range scan matching,” Journal of Intelligent & Robotic Systems, pp. 1–24, 2013.


---

# The Normal Distributions Transform: A New Approach to Laser Scan Matching, IROS 2003

> https://ieeexplore.ieee.org/document/1249285

Matching 2D range scans is a basic component of many localization and mapping algorithms. 

Most scan match algorithms require finding correspondences between the used features, i.e. points or lines. 

We propose an alternative representation for a range scan, the normal distributions transform. 

Similar to an occupancy grid, we subdivide the 2D plane into cells. To each cell, we assign a normal distribution, which locally models the probability of measuring a point. 

The result of the transform is a piecewise continuous and differentiable probability density, that can be used to match another scan using Newton's algorithm. 

Thereby, no explicit correspondences have to be established. 

We present the algorithm in detail and show the application to relative position tracking and simultaneous localization and map building (SLAM). 

First results on real data demonstrate, that the algorithm is capable to map unmodified indoor environments reliable and in real time, even without using odometry data.

--- 

# [Supervoxel Segmentation기반의 Normal Distributions Transform을 이용한 3차원 스캔 정합 기술](http://s-space.snu.ac.kr/handle/10371/123138)


2.2 Scan registration 

Scan registration algorithms allow robots to collect more information about the surrounding environment by integrating two scans taken at different times or places. 

## 분류 
Scan registration algorithms can be broadly categorized into local methods and global methods. 
### Local 
- Local methods conduct a scan registration by iteratively optimizing a cost function which represents the registration error between two scans. 
	- Given that the cost function has local minima, in most cases, the results from local methods depend on the initial transformation. 
	- The initial transformation can be obtained by odometry, an inertial measurement unit (IMU), or a GPS if this type of system is available. 
	- If the initial transformation is sufficiently close to the ground truth, local methods can estimate the relative transformation finely compared to global methods. 

There are various algorithms used with **local methods**, 
- such as the iterative closest point (ICP) [45, 46, 47], 
- the normal distributions transform (NDT) [1], 
- and the polar scan matching (PSM) [48]. 

### Global 

Global methods undertake scan registration with the distinct local geometrical features of each scan. 
They vary depending on their means of **extracting features** 
- such as the Hough transform [49, 50], 
- the fast point feature histogram (FPFH) [51], 
- the phase only matched filtering (POMF) [52], 
- and other methods.

## 상세 

### ICP 
One of the most popular scan registration algorithms is the ICP algorithm. 

The ICP algorithm is a point-to-point algorithm that estimates the optimal transformation to overlap two scans, a model and a data scan, by iteratively minimizing the sum of the squared Euclidean distances between the corresponding points. 

The ICP algorithm regards the closest points in different scans as corresponding points. 

Because a closed-form solution exists for optimizing the sum of the squared Euclidean distances between associated pairs, the ICP is easily implemented. 

단점 해결 방안 : Although the nearest neighbor search is a bottleneck when using the ICP due to the high computational cost, using the k-d tree [53] or approximate k-d tree [54] can mitigate this problem. 

However, the assumption that the closest points in different scans are the corresponding points is satisfied well only when the relative rotation difference between the two scans is small. 

Given a large relative rotation difference, points that are far from the sensor move far away, with many of these points not associated correctly as a result. 

For this reason, 
- iterative dual correspondence (IDC) [55] generates corresponding points for rotation and translation separately and alternatively minimizes the sum of the squared Euclidean distances. 
- Metric-based ICP (MbICP) [56, 57] establishes correspondences between two scans with a new metric which takes into account rotation as well as translation. Every scan is composed of the closest surfaces in the surroundings to the sensor. 
- Generalized-ICP (G-ICP) [58] uses local surface structures while retaining the simplicity of the ICP. 
- The G-ICP models the vicinity of each point as a locally planar surface by means of a covariance matrix and applies this information to the cost function to decrease the effect of incorrectly associated points.

### NDP 

Another algorithm for scan registration is the NDT algorithm. 

The NDT algorithm was initially proposed as a 2-D scan registration algorithm and was later extended to three dimensions [59]. 

The 3-D NDT algorithm is not a point-to-point method which performs registration between two scans directly but is instead a point-to-distribution method that carries out registration between the data scan and a set of distributions generated from the model scan. 

장점 : Because the NDT does not need to search for the closest points or store the raw data from the model scan, it has low computational complexity and can greatly reduce the amount of memory required. 

In addition, the gradient vector and the Hessian matrix of its score function have analytic forms, allowing the simple use of standard nonlinear optimization methods to estimate the optimal transformation. 

문제점 : However, the use of a regular grid by the NDT causes several fundamental problems. 
- 첫번째 문제 : The first is the discontinuity of the score function. 
	- When a data scan point passes one of its cell boundaries, the value of the score function jumps. 
	- Because this can cause a problem, a method using trilinear interpolation between distributions within neighboring voxels, which relieves the effects of discontinuities [60], was proposed. 
	- Furthermore, an alternative method was suggested that modifies the score function so that it becomes continuous [61]. 
	- Because this method employs greedy clustering to partition the scan, there are few distributions. 
	- Thus, the modified score function includes the scores of all of the normal distributions for each point in the data scan. 
	- In addition, a distribution-to-distribution registration approach was proposed which transforms the data scan as well as the model scan into normal distributions [62]. 
- 두번째 문제 : The second fundamental problem is that the registration performance relies on the cell size of the regular grid. 
	- In one study [63], the cell size of each cell was made to vary with the distance from the sensor in an effort to solve this problem. 
	- In addition, the use of multi-layered NDT (ML-NDT) [64] changes the cell size from large to small during the iterative optimization process. 
- 세번째 문제 : A more serious problem, though, is that a normal distribution in each voxel does not represent the local structure of the point subset within the voxel accurately because the regular grid does not take into account the structures of the model scan. 
	- When part of the scan data, i.e., that composed of surfaces, is modeled by a normal distribution, the shape of the point subset which minimizes information loss is a plane. 
	- Thus, in order to utilize the merits of the NDT and minimize the loss of information, the model scan should be divided into locally planar surfaces by means of segmentation techniques.

---

# [A Point Cloud Registration Algorithm Based on Feature Extraction and Matching](https://www.hindawi.com/journals/mpe/2018/7352691/)

## 3. Rough Registration of Point Clouds

The main ideas of the initial algorithm are as follows. 
- First, the feature points are extracted from the source point cloud and the target point cloud, respectively, reducing the number of points involved in registration and removing the redundant points and thus greatly reducing the registration time. 
- Second, the high dimensional descriptor FPFH is used not only as a standard, but also the Moorhouse multihusband distance to further determine the correspondence between points. 
- The RANSAC algorithm is then used to remove the corresponding pairs of errors. 
- Finally, we use singular value decomposition (SVD) to solve the coordinate transformation matrix and apply it to the source point cloud to complete the coarse registration. 
- Next, we introduce the main links of the rough registration algorithm.

##### 3.1. Feature Point Extraction

The extraction of feature points reduces the number of point sets involved in registration, thereby improving the speed of registration. 

With fewer point cloud data points, the introduction of feature points greatly improves the algorithms speed. 

But a large volume of point cloud data will increase the running time of feature point extraction. 

This can easily burden the entire registration algorithm, which leads to long running time. 

To solve this problem, we judge the retention points before judging the feature points. The judgment of reserved points cannot only remove obvious outliers but can improve the efficiency of the whole feature point extraction algorithm. 

Moreover, the more point cloud data the greater the time advantage of the feature point extraction algorithm.

The method of extracting feature points in this paper is divided into two steps:  
- removing some points according to the mean curvature of the point, i.e., selecting the reservation point, 
- and  determining the feature points by the concave and convex points, as described below.

The first step is the judgment of the reservation point. The mean curvature of each point in the point cloud is calculated, and the mean  and variance  of the point average mean curvature are calculated. 

Second, the points with average curvature greater than  are chosen as reservation points to remove the other points in the point cloud. Among them,  is the proportional coefficient, whose value controls the number of reserved points. When  is large, there are fewer reserved points, and vice versa.

Curvature generally includes the principal, normal, mean, and Gaussian curvature. We use the mean curvature to filter feature points. The normal curvature measures the degree of curvature of a surface in a certain direction, and the principal curvature represents the extreme value of the normal curvature. Gaussian curvature is an intrinsic measure of curvature; i.e., its value depends on how the distance on the surface is measured, rather than how the surface is embedded in space. Average curvature is an “external” bending measurement standard, which describes the curvature of a surface embedded in the surrounding space locally. Therefore, it can better reflect the degree of change and particularity of the current point, so in this paper, average curvature is used as the measure of screening feature points.

The second step is the judgment of the concave and convex points.


##### 3.2. Corresponding Point Pair Lookup Based on FPFH and Hausdorff Distance

To find the corresponding point is to find the nearest point of the query point in another point cloud. 

If we calculate the Euclidean distance from each point in the other point cloud to the query point, we will find the corresponding point pair, but this requires extensive calculation with little accuracy in the results. 

The accuracy of the corresponding point pairs directly affects the registration effect of point clouds. 

In this paper, the robust FPFH descriptor is added to the corresponding point pair search algorithm. 

The fast point feature histogram (FPFH) is based on the relationship between the sampling point and the neighborhood point normal, which is represented by 33 dimensional descriptors. 

In addition, to find the corresponding points more accurately and reduce the effect of error correspondences, the Hausdorff distance is introduced to the algorithm.

We use FPFH points and Hausdorff distances to find corresponding points. 
- First, the feature points set in the source point cloud and target point cloud are described by FPFH. 
- Next, we find the point of minimum difference between the FPFH points of each point of the source point cloud feature point through the nearest neighbor search in the target point cloud feature point set. 
- Finally, we calculate the Hausdorff distance; if it is less than the threshold value, then the two are corresponding points.

##### 3.3. RANSAC Culling Error Corresponding Point Pair

The corresponding error pairs will affect the estimation of the final rigid transformation matrix, thus affecting the point cloud registration. 

Therefore, wrong corresponding point pairs must be eliminated. 

By finding the corresponding points based on FPFH and the Hausdorff distance in the previous section, we obtained a corresponding point pair with a higher matching degree, however, with a certain gap in the actual application of the distance point cloud registration. 

This is mainly due to noise in the gathering process of the point cloud, which leads to the topology of the point cloud data of the two times of obtaining the same area being not completely consistent, so there are some wrong correspondences. 

In this paper, the RANSAC (random sample consistency) algorithm is used to eliminate error correspondences.

##### 3.4. Description of the Algorithm

The rough point cloud registration algorithm for feature extraction and matching mainly uses the FPFH description, Hausdorff distance, and RANSAC algorithm to perform pairwise registration of point clouds, aiming to provide their accurate registration of point clouds and good initial position. 

The specific algorithm description is shown as Algorithm  [1]![](https://i.imgur.com/rrS6toG.png)

- In lines 1-6, the feature points are extracted according to the method mentioned in Section [3.1]. 
- The reserved points are obtained in lines 2-4, and concave and convex points are judged in lines 5 and 6. 
- Finally, the feature points of the source point cloud are obtained. 
- Line 7 performs similar operations on the target point cloud to get the feature points set. 
- Lines 8-12, as mentioned in Section [3.2], perform a lookup based on corresponding points. 
- Line 13 uses RANSAC to eliminate the corresponding error points. 
- Line 14 solves the rigid body transformation matrix. 
- Line 15 transforms the source point cloud to complete the initial registration.

