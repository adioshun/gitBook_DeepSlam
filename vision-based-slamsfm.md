

# SfM

SfM 완전이해
- toy-sfm 코드를 통해 framework 을 완전이해하였다. 이 역시 앞으로 큰 자산이 될 듯. sfm에 best view select part 가 using sequential image 로 바뀌면 visual odometry 이고 여기에 loop closing module 이 붙으면 vSLAM이 된다!라는 간단한 핵심 파악. (물론 vSLAM의 경우 실제 모듈은 병렬적으로 즉 PTAM 적으로 구성되어야 함)

Structure from motion (SfM) is the process of estimating the 3-D structure of a scene from a set of 2-D images. This example shows you how to estimate the poses of a calibrated camera from two images, reconstruct the 3-D structure of the scene up to an unknown scale factor, and then recover the actual scale factor by detecting an object of a known size.

두장의 이미지를 이용하여 3D 정보를 출려 ㄱ하는것??

The Structure From Motion PipeLIne [Youtube)](https://www.youtube.com/watch?v=i7ierVkXYa8)
- 여러 사진(예:671)을 찍은다. 
- 각 사진에서 특징점을 추출 한다. 
- 사진들간의 특징점 연결선을 추출 한다. 

- [A Survey of Structure from Motion](https://arxiv.org/abs/1701.08493)ㅣ 2017

---

- [Augmented Reality And Vision-based SLAM 증강 현실과 비전 기반 슬램](http://metacups.blog.me/100088432677)

---


