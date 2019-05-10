# Registration이란 

## 1. 정의 

- point set registration(=point matching) 

- the process of finding a spatial transformation that aligns two point sets. 

- 목적 : merging multiple data sets into a globally consistent model, and mapping a new measurement to a known data set to identify features or to estimate its pose. 

- 확용 분야 
    - optical character recognition,
    - augmented reality
    - aligning data from magnetic resonance imaging with computer aided tomography scans.

### 1.1 [Overview of problem](https://en.wikipedia.org/wiki/Point_set_registration)



--- 
## 2. [분류](https://simpleelastix.readthedocs.io/GroupwiseRegistration.html)

### 2.1 정합은 점군 데이터의 개수에 따라,

- 데이터가 둘이면 이중 정합(pairwise registration),
- 셋 이상이면 다중 정합(multiview registration)으로 구분할 수 있다.

### 2.2 물체의 Rigid 여부에 따라 

#### A. Rigid Registration


- Given two point sets, rigid registration yields a **rigid transformation** which maps one point set to the other. 

- A rigid transformation is defined as a transformation that does not change the distance between any two points. 

- Typically such a transformation consists of translation and rotation.[2] In rare cases, the point set may also be mirrored.

- A rigid transform can register objects that are related by rotation and translation.


예)if you are registering images of a patient’s bones

#### B. Non-rigid Registration

- Given two point sets, non-rigid registration yields a **non-rigid transformation** which maps one point set to the other.

- Non-rigid transformations include **affine transformations** such as scaling and shear mapping. 

- However, in the context of point set registration, non-rigid registration typically involves nonlinear transformation.

- Non-rigid registration methods are capable of aligning images where correspondence cannot be achieved without localized deformations and can therefore better accomodate anatomical, physiological and pathological variability between patients.


#### C. 기타

> 2D용(??)

- Affine Registration : The affine transform allows for shearing and scaling in addition to the rotation and translation. 

- Groupwise Registration : Groupwise registration methods try to mitigate uncertainties associated with any one image by simultaneously registering all images in a population.

- Point-based Registation : Point-based registration allows us to help the registration via pre-defined sets of corresponding points. 


---

## 3. 알고리즘 

> [WIKIPedia](https://en.wikipedia.org/wiki/Point_set_registration)

### 3.1 Iterative closest point

```
Besl, Paul; McKay, Neil (1992). "A Method for Registration of 3-D Shapes". IEEE Transactions on Pattern Analysis and Machine Intelligence. 14 (2): 239–256. doi:10.1109/34.121791.
```

- The algorithm performs **rigid registration** in an iterative fashion 

- and then finding the least squares rigid transformation

### 3.2 Robust point matching



### 3.3 Thin plate spline robust point matching

The thin plate spline robust point matching (TPS-RPM) algorithm by Chui and Rangarajan augments the RPM method to perform **non-rigid registration** by parametrizing the transformation as a thin plate spline.

### 3.4 The kernel correlation (KC) 

- KC approach of point set registration was introduced by Tsin and Kanade.[7] 

- Compared with ICP, the KC algorithm is more robust against noisy data. 

- Unlike ICP, where, for every model point, only the closest scene point is considered, here every scene point affects every model point.

### 3.5 Coherent point drift

- Coherent point drift (CPD) was introduced by Myronenko and Song.

- The algorithm takes a probabilistic approach to aligning point sets, similar to the GMM KC method. 

- Unlike earlier approaches to non-rigid registration which assume a thin plate spline transformation model, CPD is agnostic with regard to the transformation model used. 


### 3.6 Sorting the Correspondence Space (SCS)

- This algorithm was introduced in 2013 by H. Assalih to accommodate **sonar image** registration.

- These kinds of images tend to have high amounts of **noise**, so it is expected to have lots of outliers in the point sets to match. 

- SCS delivers high robustness against outliers and can surpass ICP and CPD performance in the presence of outliers. 

- SCS doesn’t use iterative optimization in high dimensional space and is neither probabilistic nor spectral. 

- SCS can match rigid and non-rigid transformations, and performs best when the target transformation is between **three and six degrees of freedom**.