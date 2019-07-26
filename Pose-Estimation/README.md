# Pose Estimation 

센서 퓨전 인식 및 자세 추정 




---


# Vehicle Detection and Pose Estimation for Autonomous Driving

> [Bc. Libor Novák](https://dspace.cvut.cz/bitstream/handle/10467/68586/F3-DP-2017-Novak-Libor-vehicle_detection_and_pose_estimation_for_autonomous_driving.pdf): 2017, Master Thesis, 75p

> [깃허브](https://github.com/libornovax/master_thesis_code): Python, Caffe framework


## Abstract

단안 카메라를 이용하여 차량의 2D/3D bbox생성 네트워크 제안 `The thesis presents a fully convolutional neural network for 2D and 3D bounding box detection of cars from monocular images intended for autonomous driving applications. `

기존 방식 대비 제안 방식은 End-to-End 방식이 차별점이다. `In contrast with previous deep neural network methods applied to 3D bounding box detection, the introduced network is end-to-end trainable and detects objects at multiple scales in a single pass.`

We introduce a novel 3D bounding box representation, which is independent of the image projection matrix (camera used to take the images).

Therefore, the detector may be trained on several different datasets at a time and also detect 3D bounding boxes on completely different datasets than it was trained on.

제안 네트워크 속도 : 10FPS `The presented multi-scale end-to-end network is capable of processing 0.5MPx KITTI images in 10fps, which makes it about an order of magnitude faster than the closest competitor that has superior detection results. Therefore, it is possible to be used in autonomous driving scenarios.`

![](https://i.imgur.com/9kWEgpo.png)