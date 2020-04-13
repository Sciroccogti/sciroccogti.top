---
title: 计算机视觉
date: 2020-04-09T23:30:00+08:00
weight: 5
---

# 计算机视觉

3周实验，1周报告

## 图像处理基础

### 图像定义

- 图像：二维函数 $f(x,y)$
- 数字图像：由像素构成
  - 用二维矩阵描述
  - 像素值为整数
  - 原点为左上角

### 空间滤波

图像 * 模板

![](1.png)

### 空间滤波的应用

边缘检测
- 图像梯度 ${\Delta}f=[\frac{{\partial}f}{{\partial}x},\frac{{\partial}f}{{\partial}y}]$
- 通过梯度计算边缘点

### Hough 变换

Hough 变换原理：
- 利用图像空间和 Hough 参数空间的点－线对偶性
- 把图像空间中的检测问题转换到参数空间
- 通过检测参数空间中的极值点来估计该曲线的参数

#### 直线

参数空间：y=mx+b，m和b为变量，x和y为参数

由此每个点(x, y)对应一条参数空间m,b上的直线

直线拟合：
多个点则得到多条参数空间中的直线，获得一或多个交点。
相交最多的参数交点即为拟合得到的直线。

还可以用极坐标：$\rho=x\cos\theta+y\sin\theta$

||方程式|参数空间|
|---|---|---|
|斜截式|$y=mx+b$|m, b|
|极坐标|$xcos\theta+tsin\theta=\rho$|θ, ρ|

### 圆

若圆的半径未知，参数空间是圆锥

||方程式|参数空间|
|---|---|---|
|半径已知|$(x-a)^2+(y-b)^2=r^2$|a, b|
|半径未知|$(x-a)^2+(y-b)^2=r^2$|a, b, r|

## 相机与成像模型

### 小孔成像

![](2.png)

透视投影方程：（相似三角形）

$$P,O,P'三点共线\Rightarrow\overrightarrow{OP'}=\lambda\overrightarrow{OP}\Rightarrow
\begin{cases}x'={\lambda}x\\y'={\lambda}y\\f'={\lambda}z\end{cases}$$

$$P'在平面W上{\Rightarrow}z'=f'$$

$$\Rrightarrow\begin{cases}x'=f'\frac{x}{z}\\y'=f'\frac{y}{z}\end{cases}$$

### 成像特点

1. 近大远小
2. 不保持平行性：平面上的平行线在像平面上可能相交（铁轨）

聚焦条件：$\frac{1}{f}=\frac{1}{z}+\frac{1}{z'}$

变焦：改变焦距（移动镜头组中镜片的相对位置）

对焦：让像成在底片上，通常移动镜头来实现

薄透镜：透镜厚度在计算中可忽略不计

## 相机标定

相机标定：求解 3D 到 2D 的映射的参数

### 相机的几何模型

#### 齐次坐标

用 n+1 维向量表示 n 维向量：
- 原坐标 $[x_1,x_2,\dots,x_n]$
- 齐次坐标 $[hx_1,hx_2,\dots,hx_n,h]$

平面：
- $ax+by+cz-d=0$
- $\begin{pmatrix}a\\b\\c\\-d\end{pmatrix}\cdot
\begin{pmatrix}x\\y\\z\\1\end{pmatrix}=0$

球面：
- $x^2+y^2+z^2=R^2$
- $\begin{pmatrix}x,y,z,1\end{pmatrix}
\begin{pmatrix}1&0&0&0\\0&1&0&0\\0&0&1&0\\0&0&0&-R^2\end{pmatrix}
\begin{pmatrix}x\\y\\z\\1\end{pmatrix}=0$

#### 坐标系变换

![](3.png)

世界坐标系，相机坐标系，

![](4.png)

