# Registration이란 

## 1. 정의 



## 2. [분류](https://simpleelastix.readthedocs.io/GroupwiseRegistration.html)


### 2.1 Rigid Registration

A rigid transform can register objects that are related by rotation and translation.

예)if you are registering images of a patient’s bones

### 2.2 Affine Registration
The affine transform allows for shearing and scaling in addition to the rotation and translation. 


### 2.3 Non-rigid Registration

Non-rigid registration methods are capable of aligning images where correspondence cannot be achieved without localized deformations and can therefore better accomodate anatomical, physiological and pathological variability between patients.


### 2.4 Groupwise Registration
Groupwise registration methods try to mitigate uncertainties associated with any one image by simultaneously registering all images in a population.


### 2.5 Point-based Registation

Point-based registration allows us to help the registration via pre-defined sets of corresponding points. 


