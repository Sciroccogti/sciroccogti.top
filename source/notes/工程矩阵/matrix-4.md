---
title: 第四章 - Hermite 二次型
date: 2021-08-22T19:30:00+08:00
categories: 工程矩阵
layout: note
---

## 4-1 H 阵和正规阵

### 4-1-1 Hermite二次型与H阵

**定义**：
设 $A\in C^{n\times n}$，若有 $A^H=A$，则称矩阵为 Hermite 矩阵，简称为H阵，这时的 $f(x)$ 称为是 Hermite 二次型。

H 阵主对角线一定都是实数

### 4-1-2 H 阵的性质

**实对称矩阵的性质**：
1. 实对称矩阵的特征值都是实数
2. 实对称矩阵的属于不同特征值的特征向量相互正交
3. 对任意实对称矩阵 $A$，存在正交矩阵 $Q$，使得 $Q^TAQ$ 是对角阵

**H阵的性质**
1. H 阵的特征值均是实数
2. H 阵的属于不同特征值的特征向量相互正交
3. 若 A 是 H 阵，则必存在酉矩阵 U，使得 $U^HAU$ 是对角阵

可知 $A\sim \Lambda$

### 4-1-3 正规阵

**定义**：
设 $A\in C^{n\times n}$，若 $A^HA=AA^H$，则称 A 是正规阵

H阵，酉矩阵，反H阵均是正规阵

**定理**：
若 A 既是上三角的，又是正规的，则 A 必是对角阵


**定理**：
$A\in C^{n\times n}$ 是正规阵 $\Leftrightarrow A$ 酉相似于对角阵

**定理**：
$A\in C^{n\times n}$ 是正规阵 $\Leftrightarrow A$ 有 n 个两两正交的单位特征向量

幂等阵的特征值非 0 即 1

## 4-2 标准形

### 4-2-1 共轭合同关系

#### 可逆线性变换

若 A，B 都是 H 阵，且对 $\forall X\in C^{n},X^HAX=X^HBX$，则 $A=B$

设 $f(X)=X^HAX, g(Y)=Y^HBY, C$ 是可逆矩阵，
若在 $X=CY$ 下，$f(x)=g(Y)$，则 $B=C^HAC$

**定义**：
设 A，B 是 H 阵，若有可逆阵 C，使得 $B=C^HAC$，则称 A 与 B 是共轭合同的

共轭合同关系满足：反身性，对称性，传递性

### 4-2-2 Hermite二次型的标准形

#### 标准形

**定义**：
假设 Hermite 二次型 $f(X)$ 在可逆线性变换下 $X=CY$ 变成只含“平方”项的形式
$$\begin{aligned}g(Y)&=d_1y_1\overline{y_1}+d_2y_2\overline{y_2}+\dots+d_ny_n\overline{y_n}\\
&=d_1|y_1|^2+d_2|y_2|^2+\dots+d_n|y_n|^2\end{aligned}$$
则称 $g(Y)$ 是 $f(X)$ 的标准型

标准形的计算：
1. 配方法（初等变换法）
2. 酉变换法

### 4-2-3 酉变换下的标准形

假设 Hermite 二次型 $f(X)=X^HAX$，A 是相应的 Hermite 矩阵，酉矩阵 U 满足
$$U^H==\left(\begin{array}{cccc}a_1& & & \\ &a_2& & \\ & & \ddots & \\ & & & a_n\end{array}\right)$$
令 $X=UY$，则
$$f(X)=a_1|y_1|^2+a_2|y_p|^2+\dots+a_n|y_n|^2$$

## 4-3 惯性定理

### 4-3-1 Hermite二次型的惯性定理

#### 唯一性

**定理**：
若 $f(X)$ 在可逆线性变换 $X=CY$ 下变成标准形
$$g(Y)=d_1|y_1|^2+\dots+d_p|y_p|^2-d_{p+1}|y_{p+1}|^2\dots-d_r|y_r|^2$$
在可逆线性变换 $X=DZ$ 下变成标准形：
$$h(Y)=k_1|z_1|^2+\dots+k_q|z_q|^2-k_{q+1}|z_{q+1}|^2-\dots-k_r|z_r|^2$$
其中，$d_i, k_i$ 均大于零。则 $p=q$

**定义**：
Hermite 二次型标准形中的正项个数称为其正惯性指数，负项个数称为其负惯性指数

两者之和为秩

### 4-3-2 关于 H 阵的惯性定理规范形

#### 贯性定理的矩阵形式

若 H 阵 A 与
$$\Lambda_1=\left(\begin{array}{cccc}a_1& & & \\ &a_2& & \\ & & \ddots & \\ & & & a_n\end{array}\right), \Lambda_2=\left(\begin{array}{cccc}b_1& & & \\ &b_2& & \\ & & \ddots & \\ & & & b_n\end{array}\right)$$
共轭合同，则 $a_1,a_2,\dots,a_n$ 与 $b_1,b_2,\dots,b_n$ 中正、负项个数相同

**定义**：
与 H 阵 A 共轭合同的对角阵中的正项个数称为 A 的正惯性指数，负项个数称为 A 的负惯性指数

### 4-3-3 规范形

如果 $n\times n$ Hermite 矩阵 A 的正、负惯性指数分别是 $p,q$，
则 A 必定与矩阵 $\begin{pmatrix}I_p & O & O\\ O & -I_q & O\\ O & O & O\end{pmatrix}$
共轭合同。称此矩阵为A的规范形

**定理**：
$n\times n Hermite$矩阵 A，B 共合同$\Leftrightarrow A,B$ 有相同的正、负惯性指数 $\Leftrightarrow$ 相同的秩和正惯性指数

## 4-4 有定性

### 4-4-1 正定性

**定义**：
设 $A$ 是 $H$ 阵，$f(X)=X^HAX$，若对 $\forall X_0\neq\theta,f(X_0)>0$，
则称 $f$ 是正定的，$A$ 是正定的 $H$ 阵

如何建立判别方法：
1. 设 $D=\begin{pmatrix}d_1& & & \\ &d_2& & \\ & & \ddots & \\ & & & d_n\end{pmatrix}$
    则D是正定的 $\Leftrightarrow \forall d_i>0$
2. 若 H 阵 A,B 共轭合同，则 A 正定 $\Leftrightarrow B$ 正定
3. 若 H 阵 A 与 $D=\begin{pmatrix}d_1& & & \\ &d_2& & \\ & & \ddots & \\ & & & d_n\end{pmatrix}$
    共轭合同，则 A 正定 $\Leftrightarrow \forall d_i>0$

#### 正定的充要条件

**定理**：
设 A 是 $n\times n Hermite$ 阵，则下述条件等价：
1. A 是正定的
2. A 的特征值均大于零
3. A 与 I 共轭合同
4. 存在可逆阵 P 使得 $A=P^HP$
5. A 的各顺序主子式均大于零

正定阵隐含为 Hermite 阵

### 4-4-2 其它有定性

**定义**：
设 A 是 H 阵，$f(x)=X^HAX$
1. 若对 $\forall X_0\neq\theta,f(X_0)<0$，则称 $f$ 是负定的，$A$ 是负定的 H 阵
2. 若对 $\forall X_0\neq\theta,f(X_0)\geq 0$，则称 $f$ 是半正定的，$A$ 是半正定的 H 阵
3. 若对 $\forall X_0\neq\theta,f(X_0)\leq 0$，则称 $f$ 是半负定的，$A$ 是半负定的 H 阵

$f$ 负定 $\Leftrightarrow -f$ 正定

$A$ 负定 $\Leftrightarrow -A$ 正定 
$\Leftrightarrow -A$ 的偶数阶顺序主子式 > 0$\Leftrightarrow -A$ 的奇数阶顺序主子式 < 0

正定矩阵与半正定矩阵的和一定是正定矩阵

如何建立判别方法：
1. 设 $D=\begin{pmatrix}d_1& & & \\ &d_2& & \\ & & \ddots & \\ & & & d_n\end{pmatrix}$
    则D是半正定的 $\Leftrightarrow \forall d_i\geq0$
2. 若 H 阵 A,B 共轭合同，则 A 半正定 $\Leftrightarrow B$ 半正定
3. 若 H 阵 A 与 $D=\begin{pmatrix}d_1& & & \\ &d_2& & \\ & & \ddots & \\ & & & d_n\end{pmatrix}$
    共轭合同，则 A 半正定 $\Leftrightarrow \forall d_i\geq0$

#### 半正定的充要条件

**定理**：
设 A 是 $n\times n Hermite$阵，则下述条件等价：
1. A是半正定的
2. A的特征值均大于或等于零
3. A 与 $\begin{pmatrix}I_r & \\ & O\end{pmatrix}$ 共轭合同；
4. 存在矩阵 P 使得 $A=P^HP$
5. A的各主子式均大于或等于零

## 4-5 Rayleigh商

### 4-5-1 Rayleigh商

设 A 是 n 阶 H 阵，则 $\forall X\in C^n,X^HAX\inR$，于是，可以定义一复变量的实值函数
$$R(X)=\frac{X^HAX}{X^HX},\forall\theta\neq X\in C^n$$
称此函数为 A 的 Rayleigh 商

### 4-5-2 第一定理

假设 H 阵 $A\in C^{n\times n}$，A 的特征值 $\lambda_1\leq\lambda_2\leq\dots\leq\lambda_n$，则
$$\lambda_1=\min_{\theta\neq X\in C^n}R(X), \lambda_n=\max_{\theta\neq X\in C^n}R(X)$$

酉矩阵为正规阵
