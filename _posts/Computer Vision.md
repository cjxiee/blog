---
layout: post
title: "CIS580 computer vision"
categories: study
author: "Shijie Xie"
---

## Homography
Homogenous Coordinates are a system of coordinates used in the projective space. 

The projective space can be imagined as a plane located at Z = 1 in the 3D space.
Lines that cut through the origin of the 3D space and intersect the Z = 1 plane form points in the projective space.


A line is a plane of rays through origin.
(a,b,c) is a normal vector to the plane.

### Point-Line Duality
![image](https://user-images.githubusercontent.com/89954165/190836833-5127a651-9ebe-4fe6-bfa5-05aefa402eb6.png)


### Horizon
The horizon gives us the orientation of the ground plane with respect to the carmera. This is a line composed by all paralle line in one plane of R3

### Recover intrinsics from 3 vanishing points

We consider the simple case where the intrinsic matrix of a camera takes the
following form:
K =[f 0 u0
0 f v0
0 0 1]

Recover the image center from the projections of three orthogonal
vanishing points?

![541663430288_ pic_hd](https://user-images.githubusercontent.com/89954165/190876629-6a0b30b3-cf2c-4644-ab61-ffdbed09b1d7.jpg)

Theorem: The image center (u0, v0) is the orthocenter of the triangle formed
by the projections of three orthogonal vanishing points.

Proof: See figure 2. Let C = (u0, v0, 1) denote the homogeneous coordinates of the image center: it is defined as the intersection of image plane V1V2V3 with the optical axis, which is the line through O and perpendicular
to V1V2V3.

OC ⊥ V1V2V3 ⇒OCV1 ⊥ V1V2V3
OV1 ⊥ OV2 ⇒OCV1 ⊥ any line contained in V1V2V3

In particular OCV1 ⊥ V2V3. Moreover, OV1 ⊥ OV2, therefore OCV1 ⊥ OV2V3.
When two planes are perpendicular, their intersections with a third plane
are also perpendicular. Therefore, the intersection of OCV1 with V1V2V3 is
perpendicular to intersection of OV2V3 with V1V2V3.

In other words V1C ⊥ V2V3. A similar reasoning leads to V2C ⊥ V3V1 and
V3C ⊥ V1V2, therefore C is the orthocenter of V1V2V3.

![551663449333_ pic_hd](https://user-images.githubusercontent.com/89954165/190876695-0a897e94-3e9e-407f-b075-e42f8b2b45cb.jpg)

This elegant result would enable one to calibrate a camera using only the
vanishing points in an image. In practice we don’t use this method because it
is reliable only when there is a strong perspective in the image, i.e. when vanishing points have low coordinates. When it is not the case, the intersection
of parallel lines projected in the image have large coordinates (thousands of
pixels), and the relative error is too big to guarantee precise calibration.


## Retrieve camera pose
### PNP


### P3P
  P3P方法是众多解决PnP问题中的一种方案，是通过已知的3对精准匹配的2D-3D点求解图像间相对的位姿变换的一种方法，所用到的信息较少。我们首先需要知道的是P3P并不是直接根据2D-3D点求出相机位姿矩阵，而是先求出对应的2D点在当前相机坐标系下的3D坐标，然后根据世界坐标系下的3D坐标和当前相机坐标系下的3D坐标通过ICP信息求解相机位姿的。

  这段话来自：https://blog.csdn.net/ABC1225741797/article/details/108066505
