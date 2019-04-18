# 3차원 공간 강체 변환

주요 목표
1. 회전 행렬, 변형 행렬, 쿼터니언 및 오일러 각 : 3차원 공간에서 강체 변환의 설명을 이해합니다.
2. Eigen 라이브러리의 행렬을 마스터하고 Geometry 모듈을 사용합니다.

```
3차원 공간에서 강체가 어떻게 기술되는지를 설명
- 회전 & 이동으로 구성
    - 이동 변환은 선형 변환이므로 문제가 많지 않지만 
    - 회전 변환은 다루기 어렵습니다. 
- 이 장에서는 회전 행렬, 쿼터니언, 오일러 각의 의미와 그 계산 방법 및 변환 방법을 소개합니다. 
- 실습에서는 선형 대수학 라이브러리 Eigen을 소개합니다. 
```

[Lecture 2: Visual Navigation for Flying Robots (Dr. Jürgen Sturm)](https://www.youtube.com/watch?v=0wOp4k_lJvI&feature=youtu.be&list=PLTBdjV_4f-EKeki5ps2WHqJqyQvxls4ha): youtube, 1:42min

[What are quaternions, and how do you visualize them? A story of four dimensions.](https://www.youtube.com/watch?v=d4EgbgTm0Bg&feature=youtu.be): youtube, 3Blue1Brown, 31min

## 3.1 회전 행렬

- 포인트 : 3차원 공간상의 점, 3개의 숫자로 표현 
- 벡터 : 

> 좌표계 : 외손 시스템 or 오른손 시스템


### A. 점과 벡터, 좌표계 

#### 가. 벡터 연산 (벡터&벡터 or 벡터 & 숫자)

###### 숫자 곱하기, 더하기, 빼기

> 다른 문건 참고 

###### 내적 곱

![](https://i.imgur.com/kwXywjS.png)

- 내적은 벡터 간의 투영 관계를 설명 할 수 있습니다.


###### 외적 곱

![](https://i.imgur.com/8uFxzeJ.png)

- 외적을 사용하여 벡터의 회전을 나타낼 수 있습니다.


- 외적의 결과벡터는 
    - a, b 두 벡터에 수직
    - 크기는 $$ \mid a \mid \mid b \mid sin \< a,b \> $$이며 
    - 두 벡터에 의해 형성된 사변형의 방향 영역입니다. 
    - 외적의 경우 ⋀ 기호를 써서 a를 행렬로 만들수 있습니다. 이는 Skew-symmetric (반대칭행렬) 이고, 반대칭 기호로서 ⋀를 쓸 수 있습니다.
    - 따라서 외적 a x b는 행렬과 벡터 a ⋀ b의 곱셈으로 쓰여지며 선형 연산이 됩니다. 



### B. 좌표계 간의 유클리드 변환








### C. 변환 행렬 및 동차 좌표 (Transformation matrix and homogeneous coord.)



## 3.2 연습 : Eigen



## 3.3 회전 벡터와 오일러 각



### A. 회전 벡터



### B. 오일러 각



## 3.4 쿼터니언

### A. 쿼터니언 정의 

### B. 쿼터니언 연산 


### C. 회전을 나타내기 위해 쿼터니언을 사용 



#### D. 쿼터니에서 회전 행렬로 변환 



## 3.5 *유사, 아핀, 투영 변환


### A. Similarity transform


### B. Affine transform


### C. Projective transform


## 3.6 실습 : Eigen Geometry 모듈



## 3.7 시각적 표현












