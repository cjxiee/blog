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
We can estimate the camera pose from an AprilTag based on homog- raphy estimation iff we have 4 coplaner points. 

### P3P
  P3P方法是众多解决PnP问题中的一种方案，是通过已知的3对精准匹配的2D-3D点求解图像间相对的位姿变换的一种方法，所用到的信息较少。我们首先需要知道的是P3P并不是直接根据2D-3D点求出相机位姿矩阵，而是先求出对应的2D点在当前相机坐标系下的3D坐标，然后根据世界坐标系下的3D坐标和当前相机坐标系下的3D坐标通过ICP信息求解相机位姿的。

  这段话来自：https://blog.csdn.net/ABC1225741797/article/details/108066505
  
  The detial calculation is shown in the following link.
  Ref: https://haralick-org.torahcode.us/journals/three_point_perspective.pdf
  
  #### Procrustes is used to calibrated the Rotation matrix
  Since the R is not a orthnology and its det may not equal to, so Procrustes should be performed to minimize the error bewteen R with SO3.
  Y = RX + T
  Y describes the 3D points in camera frame, X describes the same 3D points in world frame. At lesat 3 correspondences are required
  R is the rotation of camera frame w.r.t the world frame, and T is the translation form camera frame w.r.t the world frame. These two information tell us where the camera is in the world frame, so called **camera pose**.
  
  ![191664565089_ pic](https://user-images.githubusercontent.com/89954165/193340646-9aa95a39-63aa-40c3-937b-87bd9de9d69a.jpg)

#### Projective Transformation, Affine transfomration, and Perspective Transformation

<img width="654" alt="image" src="https://user-images.githubusercontent.com/89954165/199633659-c172c19d-d8b7-4c7e-8c5d-2ea99162f905.png">


### Midterm review

#### PnP vs. SfM
  
    PnP: We know the 2D -> 3D coordniate pairs, calibrated coordinates and world coordinates. 
    Structure from Motion: only two calibrated coordinates of the same 3D point. 4 unknowns: R, T \lambda and \niu
    
<img width="793" alt="image" src="https://user-images.githubusercontent.com/89954165/197595309-f8bbe79c-912a-4e19-a133-6dd943268ef6.png">

    
#### Epipolar Constraint
    Remove the depth from constraint
    
<img width="837" alt="image" src="https://user-images.githubusercontent.com/89954165/197596814-5185fb82-8fda-4efa-ab45-596fcdf88299.png">
https://web.eecs.umich.edu/~justincj/teaching/eecs442/WI2021/assignments/hw6.pdf

#### Essential Matrix E
The essential matrix encodes epipolar geometry. Given a point in one image, multiplying by the essential matrix will tell us the epipolar line in the second view, Ep = l_{q}

##### Essential Matrix vs Homography
Homography maps a point ot a point (projective transformation).
Essential matrix maps a point to a line (perspective transformation).
#### Understanding of Epipolar Constraint
<img width="855" alt="image" src="https://user-images.githubusercontent.com/89954165/199632364-829e29de-afc3-4bad-94b9-d8b71179b459.png">


    Solve E with 8 point correspondences

<img width="830" alt="image" src="https://user-images.githubusercontent.com/89954165/197598129-584fa305-287a-46f1-8b75-130da188b91a.png">

<img width="833" alt="image" src="https://user-images.githubusercontent.com/89954165/197602513-0aeb0aa5-3fd8-45c0-8fbd-571904687f33.png">

<img width="839" alt="image" src="https://user-images.githubusercontent.com/89954165/197602714-418d924d-4d7c-4354-ba2e-7369ddc480ff.png">



    𝐸 is a singular matrix (Because 𝐸 = #𝑇𝑅, and det #𝑇 = 0)
     So smallest singular value is indeed zero!
     So, 𝜎1(𝐸) = 𝜎2(𝐸) = ||𝑇|| and 𝜎3 𝐸 = 0
    Side note: the ‘third singular vector’ of 𝐸 (null vector because 𝜎!= 0) is nothing but 
    the translation vector 𝑇 because:
    𝐸𝐸"𝑇 = -𝑇-𝑇"𝑇 = 𝑇× −𝑇×𝑇 = 0!
    So we already know 𝑻 in terms of 𝑬! (the 3rd left singular vector of 𝑬)
    
    
<img width="800" alt="image" src="https://user-images.githubusercontent.com/89954165/197608922-be3216a8-62e9-4493-a595-3b90d1607f48.png">



### Optical flow
    The motion of each pixel in between two frames is called optical flow
    Note: we are not showing correspondences for every pixel
    
    Optical Flow Over Patches: Let’s match small local regions (“patches”) between the two images.
    (Assumption: All pixels within a patch move in the same way
![image](https://user-images.githubusercontent.com/89954165/201974761-b61d4199-07ed-4dd0-884f-58a2956f6695.png)
![image](https://user-images.githubusercontent.com/89954165/201974821-1b5c8c1d-98f7-48c3-a83f-a3e75d7b01f1.png)
![image](https://user-images.githubusercontent.com/89954165/201976230-f4ecdfb3-315e-45e5-ad69-2a5e62f9d391.png)
#### Assumptions:
![image](https://user-images.githubusercontent.com/89954165/201980697-31e6a0fd-cd86-4ec2-9bca-94ab7ed781a2.png)
#### Issue:
![image](https://user-images.githubusercontent.com/89954165/201982441-f180865b-f234-4697-a868-c27e8fcceaec.png)
![image](https://user-images.githubusercontent.com/89954165/201983195-e6ba62e3-c4ce-4f41-8fec-1f693a28ee7d.png)
![image](https://user-images.githubusercontent.com/89954165/201983473-aea2c2ca-d51b-4b28-a1ab-8d5e220f0a43.png)
![image](https://user-images.githubusercontent.com/89954165/201984388-7d8e184b-a5d8-4e9c-9728-07ba3c6eebf1.png)
![image](https://user-images.githubusercontent.com/89954165/202001909-9f27aa64-ba1c-4d47-9a8f-9f674f2406ce.png)
![image](https://user-images.githubusercontent.com/89954165/202002337-157abedb-6976-436b-b514-2e6e56e476cb.png)





### RANSAC
<img width="1057" alt="image" src="https://user-images.githubusercontent.com/89954165/203155416-1dec15cd-5936-48b6-9500-eade71d0c3ac.png">

<img width="1180" alt="image" src="https://user-images.githubusercontent.com/89954165/203155373-a5cf1213-6dd9-46c5-8e4d-65c5f8ae7709.png">




#### 3D Recon
##### Unprojection
<img width="812" alt="image" src="https://user-images.githubusercontent.com/89954165/204117410-1a05a106-6ab7-4f4f-bc31-df33b0ac2668.png">
##### GRU融合结果
<img width="802" alt="image" src="https://user-images.githubusercontent.com/89954165/204117416-7788712c-9ddf-4772-9b01-c697de07a1b5.png">
##### Coarse to fine
<img width="816" alt="image" src="https://user-images.githubusercontent.com/89954165/204117423-a0713442-4c80-4958-9fd7-33c24cfe4e16.png">



   
    
