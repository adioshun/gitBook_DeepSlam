# Pose Estimation 

> [Vehicle Detection and Pose Estimation in Autonomous Convoys](https://brage.bibsys.no/xmlui/bitstream/handle/11250/2455922/Baardseth_Elisabeth.pdf?sequence=1&isAllowed=y): 2017, Master Thesis





![](https://i.imgur.com/yQUQgc2.png)

pose = position($$\rho$$,Distance), orientation($$\gamma $$), rotation($$ \omega$$)

## 1. Implementation of POSIT


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







## SoftPOSIT

SoftPOSIT is an algorithm for determining the pose of a 3D object from a single 2D image in the case that correspondences between model features and image features are unknown. 

http://users.umiacs.umd.edu/~daniel/Site_2/Code.html

---

# 구현물 

https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_calib3d/py_pose/py_pose.html


http://www.aforgenet.com/articles/posit/

https://github.com/shervn/TDCV17-3DPoseEstimation


[Real-time object recognition and 6DOF pose estimation based on Linemod algorithm with ROS and PCL pointcloud](http://ros-developer.com/2017/05/12/real-time-object-recognition-and-6dof-pose-estimation-based-on-linemod-algorithm-with-ros-and-pcl-pointcloud/)

[3D pose estimation ROS package using ArUco marker boards](https://github.com/gaya-/ar_sys)

http://wiki.ros.org/ar_sys

