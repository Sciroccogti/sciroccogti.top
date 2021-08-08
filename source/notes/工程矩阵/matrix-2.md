---
title: 第二章 - 内积空间和等距变换
date: 2021-08-08T16:00:00+08:00
categories: 工程矩阵
---

## 2-1 内积空间的概念

内积就是点乘

### 2-1-1 内积空间的定义

假设 V 是数域 F上的线性空间，在 V 上定义了一个二元函数 $\langle\alpha,\beta\rangle$，若
1. $\langle\alpha,\beta\rangle=\overline{\langle\beta,\alpha\rangle}$
2. $\forall\alpha,\beta,\gamma\in V,\langle\alpha+\beta,\gamma\rangle=\langle\alpha,\gamma\rangle+\langle\beta,\gamma\rangle$
3. $\forall\alpha,\beta\in V,k\in F, \langle k\alpha+\beta,\beta\rangle=k\langle\alpha,\beta\rangle$
4. $\forall\alpha\in V,\langle\alpha,\alpha\rangle\geq0$；且等号成立当且仅当 $\alpha=\theta$
则称 $\langle\alpha,\beta\rangle$ 是 $\alpha,\beta$ 的内积。
- 定义了内积的线性空间称为内积空间
- 当 $F=R$ 时，称 V 是欧基里德空间，简称欧氏空间
- 当 $F=C$ 时，称 V 是酉空间

欧基里德空间和酉空间统称为内积空间

**迹（trace）**：主对角线元素之和，也是特征值之和

**标准内积**：
1. 在空间 $V=R^n$ 上定义内积 $\langle\alpha,\beta\rangle=\beta^T\alpha$ ,则 $R^n$ 是欧氏空间
2. 在空间 $V=C^n$ 上定义内积 $\langle\alpha,\beta\rangle=\beta^H\alpha$，则 $C_3[x]$ 是酉空间

### 2-1-2 内积空间的性质

1. $\langle\alpha,\beta+\gamma\rangle=\langle\alpha,\beta\rangle+\langle\alpha,\gamma\rangle$
2. $\langle\alpha,k\beta\rangle=\bar{k}\langle\alpha,\beta\rangle$
3. $\langle\sum_{i=1}^sk_i\alpha_i,\sum_{j=1}^tl_j\beta_j\rangle=\sum_{i=1}^s\sum_{j=1}^tk_i\bar{l_j}\langle\alpha_i,\beta_j\rangle$
4. 对任意 $\alpha_in V,\langle\alpha,\theta\rangle=\langle\theta,\alpha\rangle=0$

#### 度量矩阵

设 $\varepsilon_1,\varepsilon_2,\dots,\varepsilon_n$ 是 V 的基，$\alpha,\beta\in V$ 的坐标是
$$X=(x_1,x_2,\dots,x_n)^T, Y=(y_1,y_2,\dots,y_n)^T$$
则 $\langle\alpha,\beta\rangle=\sum_{i=1}^n\sum_{j=1}^nx_i\bar{y_j}\langle\varepsilon_i,\varepsilon_j\rangle=X^TA\overline{Y}$
其中，$A=(\langle\varepsilon_i,\varepsilon_j\rangle)_{n\times n}$，称 A 是 V 在基$\varepsilon_1,\varepsilon_2,\dots,\varepsilon_n$ 下的度量矩阵
- 若 $F=R$，则度量矩阵是对称矩阵：$A=A^T$；
- 若 $F=C$，则度量矩阵是Hermite矩阵：$A=A^H$

度量矩阵须为正定阵

### 2-1-3 模与正交性

**定义**：
设 $\alpha\in V,\alpha$ 的模（长度）定义为 $\|\alpha\|=\sqrt{\langle\alpha,\alpha\rangle}$，若$\|\alpha\|=1$，则称 α 是单位向量。

**性质**：
1. $\forall\alpha\in V,\|\alpha\|\geq0$，且 $\|\alpha\|=0\Leftrightarrow\alpha=\theta$；
2. $\|k\alpha\|=|k|\|\alpha\|$
    故若 $\alpha\neq\theta$，则称 $\frac{1}{\|\alpha\|}\alpha$ 是单位向量

**柯西不等式**：
$\forall\alpha,\beta\in V,|\langle\alpha,\beta\rangle|\leq\|\alpha\|\|\beta\|$，当且仅当 $\alpha,\beta$ 线性相关时等号成立，即两者平行

> 可以从夹角公式 $cos\varphi=\frac{\langle\alpha,\beta\rangle}{\|\alpha\|\|\beta\|}$ 推出柯西不等式 $ac+bd\leq\sqrt{(a^2+b^2)(c^2+d^2)}$

- 线性相关：向量组不全两两正交。若只有两个向量，则两者平行
- 线性无关：向量组两两正交

**三角不等式**：
$\forall\alpha,\beta\in V,\|\alpha\|+\|\beta\|\geq\|\alpha+\beta\|$

**向量距离**：
$$d(\alpha,\beta)=\|\alpha-\beta\|$$

**三角不等式的距离形式**：
$\forall\alpha,\beta,\gamma\in V,d(\alpha,\gamma)\leq d(\alpha,\beta)+d(\beta,\gamma)$

**正交性**：若向量 $\alpha,\beta$ 的内积为零，则称 $\alpha,\beta$ 是正交的，记  $\alpha\perp\beta$ 

**勾股定理**：若 $\alpha\perp\beta$，则 $\|\alpha+\beta\|^2=\|\alpha\|^2+\|\beta\|^2$
- 由两两正交的非零向量组成的向量组称为正交向量组
- 由两两正交的单位向量组成的向量组称为标准正交向量组
- 由正交向量组组成的基称为是正交基
- 由标准正交向量组组成的基称为是标准正交基

#### 标准正交基下的内积

设 $\varepsilon_1,\varepsilon_2,\dots,\varepsilon_n$ 是 V 的标准正交基，$\alpha,\beta\in V$
在 $\varepsilon_1,\varepsilon_2,\dots,\varepsilon_n$ 下的坐标是 X,Y
则 $\langle\alpha,\beta\rangle Y^HX=\langle X,Y\rangle_{C^n}$

### 2-1-4 Schmidt 正交化方法

设 $\alpha_1,\alpha_2,\dots,\alpha_s\in V$ 是线性无关的，
1. 正交化：
$$\beta_1=\alpha_1$$
$$\beta_2=\alpha_2-\frac{\langle\alpha_2,\beta_1\rangle}{\langle\beta_1,\beta_1\rangle}\beta_1$$
$$\beta_3=\alpha_3-\frac{\langle\alpha_3,\beta_2\rangle}{\langle\beta_2,\beta_2\rangle}\beta_2-\frac{\langle\alpha_3,\beta_1\rangle}{\langle\beta_1,\beta_1\rangle}\beta_1$$
$$\dots$$
$$\beta_s=\alpha_s-\frac{\langle\alpha_s,\beta_{s-1}\rangle}{\langle\beta_{s-1},\beta_{s-1}\rangle}\beta_{s-1}-\dots-\frac{\langle\alpha_s,\beta_1\rangle}{\langle\beta_1,\beta_1\rangle}\beta_1$$
2. 单位化：$\gamma_i=\frac{1}{\|\beta_i\|}\beta_i,i=1,2,\dots,s$
则 $\gamma_1,\gamma_2,\dots,\gamma_s$ 是与 $\alpha_1,\alpha_2,\dots,\alpha_s$ 等价的标准正交向量组

> 推导：$\beta_2=\alpha_2-k\beta_1, \beta_2\perp\beta_1$

### 2-1-5 酉矩阵

**定义**：
若 n 阶复矩阵 A 满足 $A^HA=I$，则称为酉矩阵

A 是酉矩阵$\Leftrightarrow A^{-1}=A^H\Leftrightarrow A$的行/列向量组是 $C^n$ 的标准正交基

**定理**：
设 $\alpha_1,\alpha_2,\dots,\alpha_n$ 是 V 的标准正交基，
$$(\gamma_1,\gamma_2,\dots,\gamma_n)=(\alpha_1,\alpha_2,\dots,\alpha_n)U$$
则 $\gamma_1,\gamma_2,\dots,\gamma_n$ 是标准正交基 $\Leftrightarrow U$ 是酉矩阵.

#### Schmidt正交化方法的应用

$(AB)^H=B^HA^H$

1. 若 A,B 是同阶酉矩阵，则 $A^{-1},AB$ 都是酉矩阵
2. 假设 A 是上（下）三角矩阵，若 A 是酉矩阵，则 A 是对角阵，且其主对角元的模均等于1.

如果 $\alpha_1,\alpha_2,\dots,\alpha_n$ 是 V 的基，则有标准正交基 $\gamma_1,\gamma_2,\dots,\gamma_n$ 使
$(\gamma_1,\gamma_2,\dots,\gamma_n)=(\alpha_1,\alpha_2,\dots,\alpha_n)T$
其中，T是上三角矩阵，且其主对角元均大于零

### 2-1-6 基扩充

#### 基扩充定理

假设 W 是 V 的子空间，$\alpha_1,\alpha_2,\dots,\alpha_s$ 是 W 的标准正交基，则
存在 $\alpha_{s+1},\alpha_{s+2},\dots,\alpha_n$ 使
得 $\alpha_1,\alpha_2,\dots,\alpha_s,\alpha_{s+1},\alpha_{s+2},\dots,\alpha_n$ 是 V 的标准正交基。

## 2-2 正交补空间

**正交性**：
设 $W\leq V,\alpha\in V$，若 $\forall\beta\in W,\alpha\perp\beta$，称 $\alpha\perp W$
若 $W_1,W_2\leq V$，对$\forall\alpha_1\in W_1,\alpha_2\in W_2.\alpha_1\perp\alpha_2$，称 $W_1\perp W_2$

**定理**
设 $W=L(\alpha_1,\alpha_2,\dots,\alpha_s),\eta\in V$，则 $\eta\perp W\Leftrightarrow\forall j,\eta\perp\alpha_j$

### 2-2-1 正交补空间

**定义**：
设 $W\leq V$，记
$$W^\perp=\{a\in V|\alpha\perp W\}$$
易证这是 V 的子空间，称是 W 在 V 中的正交补空间

**定理**：
设 $W\leq V$，则$V=W\oplus W^\perp$
而且，若 $V=W+U$，且 $W\perp U$，则 $U=W^\perp$.

**推论**：
若 $W\leq V$，则 $(W^\perp)^\perp=W$

### 2-2-2 $R(A)^\perp$ 和 $K(A)^\perp$

**定理**：
$R(A)^\perp=K(A)^H,K(A)^\perp=R(A)^H$

### 2-2-3 正投影

已知 $W\leq V,\alpha\in V$，若 $\eta\in W$ 满足
$$d(\alpha,\eta)=\min_{\xi\in W}d(\alpha,\xi)$$
则称 $\eta$ 为 $\alpha$ 在 W 中的正投影

**定理**：
假设 $W\leq V,\alpha\in V$，则
1. 若 $\alpha$ 在 W 中的正投影存在，则正投影必定是唯一的；
2. $\eta\in W$ 是 $\alpha$ 在 W 中的正投影当且仅当 $\eta-\alpha\perp W$

**定理**：
如果 $W\leq V$ 是有限维的，则任意 $\alpha\in V$ 在 W 中的正投影必定存在

### 2-2-4 应用

**最小二乘解**：
设 $A\in C^{s\times n}$，线性方程组 $Ax=b$ 的最佳近似解 为 $A^HAx=A^Hb$ 的解

## 2-3 等距变换

**定义**：
设 V 是内积空间，$f\in Hom(V，V)$，若
$$\langle f(\alpha),f(\beta)\rangle=\langle\alpha,\beta\rangle,\forall\alpha\beta\in V$$
称 $f$ 是等距变换
若 $F=R$，称 $f$ 是正交变换
若 $F=C$，称 $f$ 是酉变换

**充要条件**：
设 V 是内积空间，$f\in Hom(V，V)$，下述条件等价：
1. $f$ 保持长度不变
2. $f$ 保持内积不变
3. $f$ 将标准正交基变为标准正交基
4. $f$ 在标准正交基下的矩阵是酉矩阵

### 镜像变换

假设 V 是一个欧氏空间，$\omega\in V$ 是一个单位向量，映射
$$f:V\rightarrow V，\alpha\rightarrow\alpha-2\langle\alpha,\omega\rangle\omega$$
则是 V 上的等距变换（正交变换）
