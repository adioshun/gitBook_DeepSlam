# My Awesome Book

|논문명 | |
| --- | --- |
| 저자\(소속\) | \(\) |
| 학회/년도 | IROS 2015, [논문]() |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 | |
| 관련연구||
| 참고 | |
| 코드 | |



### A majority of SLAM systems share several common components:

- **feature detector** that finds point of interest within the image (features),
- **feature descriptor** that matches tracks features from one image to the next,
- **optimization** backend that uses said correspondences to build a geometry of the scene (map) and find the position of the robot,
- **loop closure detection algorithm** that recognizes previously visited areas and adds constraints to the map.
    - loop closure has the most potential to be solved with DL techniques.
    
> 출처 : [How can Deep Learning help Robotics and SLAM](https://nicolovaligi.com/deep-learning-robotics-slam.html)




## Software 

### Visual SLAM

- ORB-SLAM is arguably the most advanced open-source package for visual SLAM. 
    - ORB uses another common technique, a **bag of words (BoW)** representation

### LiDAR SLAM 