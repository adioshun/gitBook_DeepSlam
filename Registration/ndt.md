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






