https://blog.csdn.net/fourier_legend/article/details/88933443

- 목적 :  Build a low drift odometer -> 3D Point Cloud Map (Loop Closure는 고려 안함)


![](https://i.imgur.com/ENEOPGp.png)

Mainly through the following steps

- Point Cloud Registration - Receives laser data, completes point cloud registration and feature point cloud (edge ​​and face) extraction.
- Lidar Odometry - Issues an odometer at 10hz by matching a feature point cloud. The accuracy of the odometer at this time is not high.
- Lidar Mapping - Receives odometer information and current point cloud data, performs fine matching based on the rough matching odometer pose, registers the point cloud to the map according to the estimated pose, and publishes the updated pose according to 1hz.
- Transform Integration - Receives pose information published by lidar odometry and lidar mapping, and publishes odometer information at 10hz.




## Analysis of Algorithms
How to select the feature point and the planar point 
The author first defines a formula for measuring the smoothness of the point. The degree of smoothness of the point is measured by measuring the difference in distance between the two points. The point with the largest c value will be the edge point and the point with the smallest cz value will be the plane point. Divide 360 ​​degrees into four regions, each of which produces a maximum of two edge points and four plane points. These edge points and plane points are shown below. 
These extracted points are used as feature points to complete the matching of the front and rear frames to estimate their pose.

After constructing the loss function feature points, convert to the map coordinate system according to the tf relationship, find the nearest edge point and plane point in the map, and construct a transformation matrix by using the two nearest edge points and plane points as corresponding points, (t_x , t_y, t_z, theta), find the Jacobian for the conversion, and use the Gauss-Newton method to narrow the loss function until convergence.

## Algorithm pseudo code

![](https://img-blog.csdnimg.cn/2019040218251192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ZvdXJpZXJfTGVnZW5k,size_16,color_FFFFFF,t_70)


