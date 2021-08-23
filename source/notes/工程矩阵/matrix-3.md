---
title: 第三章 - 矩阵的相似标准形
date: 2021-08-15T12:30:00+08:00
categories: 工程矩阵
layout: note
---

## 3-1 特征值与特征向量

### 3-1-1 定义和计算

#### 矩阵的特征值与特征向量

**定义**：
假设 A 是 n 阶方阵，$\lambda_0$ 是数，若存在 n 维列向量 $\eta$，使得
$\eta\neq\theta$，且 $A\eta=\lambda_0\eta$
则称 $\lambda_0$ 是 A 的特征值，$\eta$ 是 A 的属于特征值 $\lambda_0$ 的特征向量。

**定理**：
假设 A 是 n 阶方阵，则 A 相似于对角阵的充分必要条件是 A
有 n 个线性无关的特征向量特征向量。

#### 线性变换的特征值与特征向量

**定义**：
设 $f$ 是线性空间上的线性变换，假设 $\lambda_0\in F$，
若存在$\eta\in V$使得 $\theta\neq\eta\in V$，且 $f(\eta)=\lambda_0\eta$
则称 $\lambda_0$ 是线性变换 $f$ 的特征值，$\eta$ 是相应于 $\lambda_0$ 的特征向量。

**线性变换的可对角化问题**：
设 V 是 n 维线性空间，$f$ 是线性空间 V 上的线性变换，
则存在 V 的基使得 $f$ 的矩阵是对角阵当且仅当 $f$有个线性无关的特征向量。

#### 线性变换的特征值、特征向量的计算

设 $f$ 在 V 的基 $\alpha_1,\alpha_2,\dots,\alpha_n$ 下的矩阵是 A
若 $\lambda_0\in F,\eta\in V$ 在基 $\alpha_1,\alpha_2,\dots,\alpha_n$ 下的坐标是 $x_0$，
则 $f(\eta)$在基 $\alpha_1,\alpha_2,\dots,\alpha_n$ 下的坐标是 $Ax_0$，故
$$f(\eta)=\lambda_0\eta\Leftrightarrow Ax_0=\lambda_0x_0$$
即：$\eta$ 是 $f$ 的属于特征值 $\lambda_0$ 的特征向量当且仅当 $x_0$ 是 A 的属于特征值 $\lambda_0$ 的特征向量。

**行列式**：
取行列式某一行/列，对该列的每个元素求其代数余子式，并与该元素相乘，最后将所有乘积相加

**代数余子式**：
把元素 $a_{ij}$ 所在的第 $i$ 行和第 $j$ 列划去，得到余子式 $M_{ij}$，$M_{ij}\times(-1)^{i+j}=A_{ij}$，$A_{ij}$ 即为代数余子式

$\begin{array}{c|c}A & O \\ \hline O & A\end{array}$ 的行列式 $=A$ 的行列式的平方

**定理**：
若 $A,B\in C^{n\times n}$ 是相似的，则 $|\lambda I-A|=|\lambda I-B|$

注意：
1. 定理的逆命题不成立
2. 可定义线性变换的特征多项式

$|AB|=|A||B|$

$|P^{-1}||P|=1$

### 3-1-2 特征多项式

#### 特征多项式的计算

**定义**：
假设矩阵 $A=(a_{ij})_{n\times n}$，$1\leq i_1<i2<\dots<i_k\leq n$，则 A 的第 $i_1,i_2,\dots,i_k$ 行，
第 $i_1,i_2,\dots,i_k$ 列交叉处的元素构成的 k 阶子式称为 A 的 k 阶主子式

#### Cauchy-Binet公式

**定理**：
设 $A=(a_{ij})_{n\times n}$，则
$$|\lambda I-A|=\lambda^n+b_1\lambda^{n-1}+b_2\lambda^{n-2}+\dots+(-1)^kb_k\lambda^{n-k}+\dots+(-1)^{n-1}b_{n-1}\lambda+(-1)^nb_n$$
其中，$b_j$ 为 A 的所有 j 阶主子式之和，特别地
$$b_1=-\sum_{i=1}^na_{ii}, b_n=(-1)^n|A|$$

#### 矩阵的迹

**定义**：
设 $A=(a_{ij})_{n\times n}$，称 $\sum_{i=1}^na_{ii}$ 为 A 的迹，记为 $tr(A)$

1. 若$A=(a_{ij})_{n\times n}$ 的特征值为 $\lambda_1,\lambda_2,\dots,\lambda_n$，则
$$tr(A)=\sum_{i=1}^n\lambda_i,|A|=\Pi_{i=1}^n\lambda_i$$
2. 若 $A,B$ 相似，则 $tr(A)=tr(B),|A|=|B|

$r(A)\leq m\Rightarrow A$ 的结束大于 m 的子行列式应全为零，主子式应全为零

$AB$ 不一定等于 $BA$，但$tr(AB)$ 不一定等于 $tr(BA)$

#### 化零多项式

**引理**：
设 $f(x)$ 是多项式，若 $f(A)=0$，则 A 的特征值均是 $f(x)=0$ 的根，称 $f(x)$ 为 A 的化零多项式

### 3-1-3 Hamilton-Cayley 定理

**Schur 引理**：
对 $\forall A\in C^{n\times n}$，存在酉矩阵 U 使得 $U^HAU$ 是上三角矩阵。

**定理**：
设 $A\in F^{n\times n},C(\lambda)=|\lambda I-A|$，则 $C(A)=O$。

**定理**：
设 $f\in Hom(V,V),C(\lambda)$是 $f$ 的特征多项式，则 $C(f)=O$。

### 3-1-4 最小多项式

#### 矩阵的最小多项式

根据 Hamilton-Cayley 定理，一定存在最小多项式

**定义**：
矩阵 A 的次数最低的、最高次项系数为一的化零多项式称为 A 的最小多项式

**性质**：
1. 若 $m(x),\phi(x)$ 分别是矩阵 A 的最小多项式、化零多项式，则 $m(x)|\phi(x)$
2. 任意矩阵的最小多项式是唯一的，
3. 如果矩阵 $A,B$ 相似，则 $A,B$ 有相同的最小多项式

#### 线性变换的最小多项式

**定义**：
设线性变换 $f\in V$ 在 V 的一组基下的矩阵为 $A,A$ 的最小多项式称为 $f$ 的最小多项式

**等价定义**：
线性变换 $f$ 的次数最低的、最高次项系数为一的化零多项式称为 $f$ 的最小多项式

设 $C(\lambda)=(\lambda-\lambda_1)^{C_1}\dots(\lambda-\lambda_s)^{C_s}$，$m(\lambda)=(\lambda-\lambda_1)^{t_1}\dots(\lambda-\lambda_s)^{t_s}$，有 $1\leq t_j\leq C_j$

**定理**：
设 $m(x),C(x)$ 分别是矩阵 A 的最小多项式和特征多项式，
则 $m(x)|C(x)$，并且，对 $\lambda_0\in C,m(\lambda_0)=0\Leftrightarrow C(\lambda_0)=0$

## 3-2 可对角化问题

1. $n\times n$ 矩阵 A 相似于对角阵 $\Leftrightarrow A$ 有 n 个线性无关的特征向量
2. 矩阵的属于不同特征值的特征向量线性无关
3. 若 $\lambda_1,\lambda_2,\dots,\lambda_s$ 是矩阵 A 的互不相同的特征值，
    $\eta_{1i},\eta_{2i},\dots,\eta_{t_ii}$ 是 A 相应于特征值 $\lambda_i$ 的线性无关的特征向量，则
    $$\eta_{11},\eta_{21},\dots,\eta_{t_1i},\eta_{12},\eta_{22},\dots,\eta_{t_22},\dots,\eta_{1s},\eta_{2s},\dots,\eta_{t_ss}$$
    线性无关

#### 线性变换的可对角化问题

**定理**：
假设 V 是 n 维线性空间，$f\in Hom(V,V)$。则
1. $f$ 可对角化当且仅当 $f$ 有 n 个线性无关的特征向量
2. $f$ 的属于不同特征值的特征向量线性无关
3. 若 $\lambda_1,\lambda_2,\dots,\lambda_s$ 是矩阵 A 的互不相同的特征值，
    $\eta_{1i},\eta_{2i},\dots,\eta_{t_ii}$ 是 $f$ 相应于特征值 $\lambda$ 的线性无关的特征向量，则
    $$\eta_{11},\eta_{21},\dots,\eta_{t_1i},\eta_{12},\eta_{22},\dots,\eta_{t_22},\dots,\eta_{1s},\eta_{2s},\dots,\eta_{t_ss}$$
    线性无关

### 3-2-1 特征子空间

**定义**：
设 $f\in Hom(V,V)$，$\lambda_0$ 是 $f$ 的特征值，称
$$V\lambda_0=\{\eta\in V|f(\eta)=\lambda_0\eta\}$$
为 $f$ 的相应于特征值 $\lambda_0$ 的特征子空间

相应于特征值 $\lambda_0$，$f$ 刚好有 $dimV_{\lambda_0}$个线性无关的特征向量

**定理**：
设 $\lambda_1,\lambda_2,\dots,\lambda_s$ 为 $f$ 的相异特征值，则 $V_{\lambda_1}+V_{\lambda_2}+\dots+V_{\lambda_s}$ 是直和。

**定理**：
假设 $dimV=n,f\in Hom(V,V)$ 的特征多项式为
$$C(\lambda)=(\lambda-\lambda_1)^{C_1}(\lambda-\lambda_2)^{C_2}\dots(\lambda-\lambda_s)^{C_s}$$
则存在 V 的基使得 $f$ 的矩阵是对角阵的充分必要条件是
$$dimV_{\lambda_1}+dimV_{\lambda_2}+\dots+dimV_{\lambda_s}=n$$

### 3-2-2 几何重数

**定理**：
设 $f\in Hom(V,V)$ 的特征多项式是 $C(\lambda)=\Pi_{i=1}^s(\lambda-\lambda_i)^{c_i}$，则 $dimV_{\lambda_i}\leq{c_i}$。
其中 $dimV_{\lambda_i}$ 称为几何重数，${c_i}$ 称为代数重数

**定理**：
设 $f\in Hom(V,V)$ 的特征多项式是 $C(\lambda)=\Pi_{i=1}^s(\lambda-\lambda_i)^{c_i}$，则下述条件是等价的：
1. $f$是可对角化的
2. $\forall i, dimV_{\lambda_i}=c_i$
3. $V=V_{\lambda_1}\oplus V_{\lambda_2}\oplus\dots\oplus V_{\lambda_s}$

### 3-2-3 最小多项式与可对角化

**引理**：
若 n 阶矩阵 $M_i$ 满足 $M_1M_2\dots M_s=O$，则 $\sum_{i=1}^sr(M_i)\leq(s-1)n$

**定理**：
$n\times n$ 矩阵 A 相似于对角阵当且仅当 A 的最小多项式无重根

对角阵的行列式等于其主对角线元素之积

## 3-3 若当标准形

### 3-3-1 Jordan 形矩阵

**定义**：
1. 形如 $\left(\begin{array}{cccc}a& 1& & \\ & a&\ddots& \\& &\ddots & 1\\ & & & a\end{array}\right)$ 的矩阵称为 Jordan 块
2. 形如 $J=\left(\begin{array}{cccc}J_1& & & \\ & J_2& & \\& &\ddots & \\ & & & J_s\end{array}\right)$（其中 $J_i$ 均为 Jordan 块）的矩阵称为 Jordan 形矩阵

### 3-3-2 Jordan 标准形

对角阵是一种若当形矩阵

**定义**：
若 $J$ 是若当形矩阵，且矩阵 $A$ 与 $J$ 相似，则称 $J$ 是 $A$ 的若当标准形

### 3-3-3 唯一性

若 $J=\left(\begin{array}{cccc}J_1& & & \\ & J_2& & \\& &\ddots & \\ & & & J_s\end{array}\right)$ 是矩阵 $A$ 的 Jordan 标准形，$K=\left(\begin{array}{cccc}J_{i_1}& & & \\ & J_{i_2}& & \\& &\ddots & \\ & & & J_{i_s}\end{array}\right)$
其中，$J_{i_1},J_{i_2},\dots,J_{i_s}$ 是 $J_1,J_2,\dots,J_s$ 的一个排列，则 K 也是 A 的 Jordan 标准形。

下面的定理表明：在承认存在性的前提下，除了相差 Jordan 块的次序外，每个矩阵的 Jordan 标准形是唯一的

**定理**：
（假设矩阵的Jordan标准形是存在的）设 $\lambda_0$ 是 n 阶方阵 A 的特征值，
则对任意一正整数 k，A 的 Jordan 标准形中主对角元为 $\lambda_0$ 且阶数为 k 的 Jordan 块的块数等于
$$r(B^{k-1})-2(B^k)+r(B^{k+1})$$
其中，$B=A-\lambda_0I$

$r(N^k)=\begin{cases}n-k,&k\leq n\\0,&k\geq n\end{cases}$，并约定 $N^0=I$

$J$ 中阶数为 $k$ 的 Jordan 阵块数：$r(J-\lambda_0I)^{k-1}-2r(J-\lambda_0I)k+r(J-\lambda_0I)^{k+1}$

可逆矩阵的 k 次方后的秩不变

仅有 Jordan 阵顺序不同的 Jordan 标准形算作同一个

$r(A-I)=r(J-I)$

#### Jordan标准形与最小多项式

**定理**：
若 $M=\begin{array}{cc}A & O \\ \hline O & B\end{array}$
则矩阵 $M,A,B$ 的最小多项式间有关系：$m_M(\lambda)=[m_A(\lambda),m_B(\lambda)]$

**定理**：
假设矩阵 A 的最小多项式是 $m(\lambda)=\Pi_{i=1}^s(\lambda-\lambda_i)^{r_i}$，
则 $r_i$ 即是 A 的 Jordan 标准形中以 $\lambda_i$ 为主对角元的 Jordan 块的最高阶数。
特别地，A 相似于对角阵 $\Leftrightarrow A$ 的最小多项式无重根

相似矩阵有相同的迹，相同的秩

## 3-4 特征值的分布

### 3-4-1 谱半径和盖尔圆

**定义**：
设 $A=(a_{ij})_{n\times n}$，称 A 的特征值的集合为 A 的谱，
称 A 的特征值的模的最大值为 A 的谱半径，记为 $\rho(A)$。记
$$R=|a_{i1}|+\dots+|a_{ii-1}|+|a_{ii+1}|+\dots+|a_{in}|$$
$$C=\{z||z-a_{ii}|\leq R_i\}$$
称之为 A 的第 i 个盖尔圆；
称 $G=\cup_{i=1}^nC_i$ 为 A 的盖尔圆系

### 3-4-2 第一圆盘定理

**定理**：
矩阵 A 的特征值必定在 A 的盖尔圆系中

注意：并不是每个盖尔圆上都有特征值，但是在盖尔圆之外没有特征值.

#### 3-4-3 第二圆盘定理

**定义**：
设 $A\in C^{n\times n}$，在 A 的 n 个盖尔圆中，有 k 个圆构成一连通区域，
但与其余 $n=k$ 个圆不相交，则称这个连通区域为 $k$ 区

**定理**：
A 的盖尔圆的 $k$ 区中有且仅有 A 的 k 个特征值

$A\sim A^T$

**推论**：
如果 A 的 n 个盖尔圆互不相交，则 A 有 n 个互不相等的特征值

#### 3-4-4 谱半径的估计

设 $A=(a_{ij})_{n\times n}$
$$\rho_1=\max_{1\leq i\leq n}\left\{\sum_{j=1}^n|a_{ij}|\right\},\rho_2=\max_{1\leq j\leq n}\left\{\sum_{i=1}^n|a_{ij}|\right\}$$
则 $\rho(A)\leq \rho_1,\rho_2$


