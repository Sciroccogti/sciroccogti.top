---
title: 第〇章 - 复习与引申
date: 2021-07-20T22:30:00+08:00
categories: 工程矩阵
---

# 第0章 复习与引申

## 0-1 矩阵的代数运算

#### 相似

**矩阵相似** ：可以通过初等行/列变换转换
  * 约当型： 与原矩阵相似的简单矩阵
  * 范数：用于刻划矩阵大小，$\parallel M-N\parallel$→$M$与$N$的差
  * 广义逆矩阵： 对方程 $AX=b$：
    1. 若 $A$ 可逆，则 $X=A^{-1}b$
    2. 若 $A$ 不可逆，则 $X=Gb$，其中$G$为广义逆矩阵

矩阵乘法中的 **非零零因子** ： $A\neq0$，$B\neq0$，但 $AB=0$，则 $A$ 为左零因子，$B$ 为右零因子

常见的类对角矩阵：
${N}_{n\times n}=\left(\begin{array}{ccccc}0& 1& & & \\ & 0& 1& & \\ & & 0& \ddots & \\ & & & \ddots & 1\\ & & & & 0\end{array}\right),$ ${N}^{2}=\left(\begin{array}{ccccc}0& 0& 1& & \\ & 0& 0& \ddots & \\ & & 0& \ddots & 1\\ & & & \ddots & 0\\ & & & & 0\end{array}\right),$ $\dots,$ ${N}^{n-1}=\left(\begin{array}{cccc}\ddots & & 0& 1\\ & \ddots & 0& 0\\ & & \ddots & \\ & & & \ddots \end{array}\right),$ ${N}^{n}=0$

#### 可交换

**可交换** ：$A B=B A$

**数量矩阵**： $kI$，其中 $k$ 为实数，$I$ 为单位阵
- 若A与任意同阶矩阵可交换，则A为数量矩阵

矩阵的乘法交换律不成立，乘法消去律也不成立，但乘法分配律成立

==**当矩阵AB=BA时，二项式定理成立**==

### 分块矩阵

**分块矩阵** ：将A、B两矩阵分块：
$A={\left({A}_{ij}\right)}_{p\times q},B={\left({B}_{ij}\right)}_{q\times r}$

在A的列的分法与B的行的分法相一致时，矩阵 $C=AB$ 也可以写成分块矩阵：
$C=\left(\begin{array}{cccc}{c}_{11}& {c}_{12}& \dots & {c}_{1r}\\ {c}_{21}& {c}_{22}& \dots & {c}_{2r}\\ \dots & \dots & \dots & \dots \\ {c}_{p1}& {c}_{p2}& \dots & {c}_{pr}\end{array}\right),$ ${C}_{ij}={A}_{i1}{B}_{1j}+{A}_{i2}{B}_{2j}+\dots +{A}_{iq}{B}_{qj}$

#### 秩

**秩** ：矩阵内最多呈线性无关的列向量数

若 $AB=0$ ，则 $r(A)+r(B)\leq n$

若 $\beta_1,\dots,\beta_t$ 可由 $\alpha_1,\dots,\alpha_n$ 线性表示，则 $r\{\beta_1,\dots,\beta_t\}\leq r\{\alpha_1,\dots,\alpha_n\}$

## 0-2 线性方程组

设方程组 $Ax=b, A=(a_{ij})_{s\times n}, b=(b_1b_2\dots b_s)^T$，则有
1. 有解 $\Leftrightarrow r(A)=r(A,b)$
2. 若 $r(A)=r(A,b)=r$，则有唯一解 $\Leftrightarrow r=n$
3. 若 $r(A)=r(A,b)=r<n$，则通解中有 $n-r$ 个自由未知量

### 基础解系

**基础解系**：若 $\{\eta_1,\dots,\eta_t\}$ 满足：
1. 是 $Ax=0$ 的解
2. 线性无关
3. $Ax=0$的任一解都可被其线性表示
则其为 $Ax=0$ 的基础解系

对于齐次线性方程组 $Ax=b, A=(a_{ij})_{s\times n}$，有
1. 有非零解 $\Leftrightarrow r(A)<n$（系数矩阵的秩小于未知量个数）
2. 若 $r(A)<n$，则其基础解系中含 $n-r$ 个解向量
3. 若 $r(A)<n$，则其任意 $n-r$ 个线性无关的解向量是其基础解系

### 阶梯形矩阵

满足下述条件的矩阵称为阶梯形矩阵：
1. 元素全为零的行均在矩阵的下方
2. 非零首元所在列的下标随着行标的增大而严格增大

满足下述条件的阶梯形矩阵称为简化阶梯形矩阵：
1. 各个非零行的非零首元均为 1
2. 除了非零首元外，非零首元所在的列其余元素都为零

### Gauss 消元法

1. 用初等行变换将增广矩阵化为阶梯形矩阵
2. 确定自由未知量：
   1. 找每行的非零首元
   2. 找对应未知量
3. 通过回代法用自由未知量表示2.2中的未知量（此步可借助简化阶梯形矩阵）

**共轭转置** $A^H$：$A=(a_{ij}), A^H=(\overline{a_{ji}})$，即先复数上的共轭，再转置

==**矩阵的秩** 等于==：
- 其非零子式的最高阶数
- 或等于其行/列向量的的秩
- 或以 $A$ 为基础解系的齐次线性方程组的解的秩

线性⽅程组恒有解 $\Leftrightarrow$ 系数矩阵的秩 = 增广矩阵的秩

> $\overline{\eta}^{T}\overline{A}^{T}=(\overline{A}\cdot\overline{\eta}) ^{T}=(\overline{A\eta}) ^{T}=\left( A\eta \right) ^{H}$

> 若阶梯矩阵有全零行，则有无穷多个解

## 0-3 向量

### 极大线性无关组

设向量组 $\alpha_1,\alpha_2,\dots,\alpha_s$ 的部分组 $\alpha_{i_1},\alpha_{i_2},\dots,\alpha_{i_r}$ 满足
1. $\alpha_{i_1},\alpha_{i_2},\dots,\alpha_{i_r}$ 线性无关（可用列方程表示）
2. $\alpha_1,\alpha_2,\dots,\alpha_s$ 中每个向量均可由 $\alpha_{i_1},\alpha_{i_2},\dots,\alpha_{i_r}$ 线性表示，则称 $\alpha_{i_1},\alpha_{i_2},\dots,\alpha_{i_r}$ 是 $\alpha_1,\alpha_2,\dots,\alpha_s$ 的一个极大无关组

1. **若一向量组的极大无关组中含 $r$ 个向量，则称这个向量组的秩为 $r$**
2. **若向量组的秩为 $r$，则该向量组中任意 $r$ 个线性无关的向量均为其极大无关组**

判断是否线性相关：
$x_1a_{i_1}+\dots+x_ra_{i_r}=\vec{0}$
- 若有非零解，则线性相关
- 若仅有全零解，则线性无关

### 矩阵的秩

**有关秩的不等式**：
1. $r(A+B)\leq r(A)+r(B)$
2. $r(AB)\leq r(A),r(B)$
3. 若 $A_{s\times x}B_{n\times t}=0$，则 $r(A)+r(B)\leq n$
4. $r(A_{s\times x}B_{n\times t})\geq r(A)+r(B)-n$
5. 对于 $M=\begin{pmatrix}A & C \\0 & B\end{pmatrix}$，$r(M)\geq r(A)+r(B)$

> 3 是 4 的特殊情况

**初等阵**：可以由单位阵经一次初等变换得到的矩阵

**幂等矩阵**：$A^2=A$

**可逆矩阵**：又称满秩矩阵，能通过初等变换得到单位阵（理由：$Ax=b, x=A^{-1}b$，可知方程有唯一解，即系数矩阵相似于单位阵）
- 可知可逆矩阵的行、列向量线性无关（初等变换后满秩）

**不可逆矩阵**：若 $A$ 为不可逆矩阵，则必有 $X\neq0$，使得 $AX=0$
- 可知不可逆矩阵的行、列向量线性相关（初等变换后有全零行）

线性无关=可逆，线性相关=不可逆

**满秩分解**：对于$s\times n$ 的矩阵 $A$,取$s\times r$ 的矩阵 $B$ 和 $r\times n$ 的矩阵 $C$，使得 $A=BC$，其中 $r=r(A)$
- 可取 $B$ 为 $A$ 的极大线性无关组，$C$ 则为各列用极大线性无关组表示时的对应系数

