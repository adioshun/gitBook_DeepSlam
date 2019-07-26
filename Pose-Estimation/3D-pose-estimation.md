# [3D Pose Estimation](http://www.aforgenet.com/articles/posit/)

> by Andrew Kirillov

The article describes application of POSIT algorithm for object's 3D pose estimation.




## Introduction
자세추정은 많은 응용분야를 가진다. `3D pose estimation of an object from its image plays important role in many different applications, like calibration, cartography, object recognition/tracking and, of course, augmented reality. `

많은 연구가 진행 되었다. `There are number of research papers published about 3D pose estimation describing different algorithms. `

가장 유면한건 POSIT알고리즘 이다. `The most popular of them seems to be POSIT algorithm, which is quite easy to follow and is implemented in number of software libraries. `


## POSIT algorithm

약어 설명 : POSIT stands for POS with ITerations, where POS stands for Pose from Orthography and Scaling. 

제안 논문 : The algorithm is described in "Model-Based Object Pose in 25 Lines of Code" paper by Daniel F. DeMenthon and Larry S. Davis. 

OpenCV에도 구현물 있음 `Implementation of this algorithm can be found in OpenCV library, for example. `

목적 : So what does POSIT do? It estimates 3D pose of an object, 
- which includes rotation over X/Y/Z axes and 
- shift along X/Y/Z axes.


요구 사항 `What does POSIT require to be able to do 3D pose estimation? `

1. First it requires image coordinates of some object's points (minimum 4 points). 
    - Very important to note is that these points must not be coplanar(동일평면) - i.e. they must not be all on the same plane. 
2. Then we need to know model coordinates of these points. 
    - This assumes that the model of the object we are estimating pose for is known, 
    - so we know coordinates of the corresponding points in the model. 
3. And finally the algorithm requires effective focal length of the camera used to picture the object. 

