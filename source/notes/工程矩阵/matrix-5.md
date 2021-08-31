---
title: 第五章 - 范数和矩阵函数
date: 2021-08-31T12:00:00+08:00
categories: 工程矩阵
layout: note
---

## 5-1 向量范数

### 5-1-1 定义

设 $V$ 是数域 $F$ 上线性空间，$\nu$ 是定义在 $V$ 上的实值函数。如果 $\nu$ 满足：
1. 对任意 $\theta\neq\alpha\in V, \nu(\alpha)>0$（恒正性）
2. 对任意 $\alpha\in V,k\in F, \nu(k\alpha)=|k|\nu(\alpha)$（齐性）
3. 对任意 $\alpha,\beta\in V, \nu(\alpha+\beta)\leq \nu(\alpha)+\nu(\beta)$（三角不等式）
则称 $\nu$ 是 $V$ 上的范数。
定义了范数的线性空间称为赋范线性空间

### 5-1-2 长度与范数

设 $V$ 是内积空间，则 $V$ 上内积下的长度 $\|\bullet\|$ 是 $V$ 上的一个范数

因此，从现在起，在不致于引起混淆的情况下，任意线性空间上的范数就记为 $\|\bullet\|$

### 5-1-3 $C^n$ 中的范数

对任意 $X=(x_1,x_2,\dots,x_n)\in C^n$
1. 向量 1-范数：$\|X\|_1=\sum^n_{i=1}|x_i|$
2. 向量 2-范数：$\|X\|_2=\sqrt{\sum^n_{i=1}|x_i|^2}$
3. 向量 $\infty-$范数：$\|X\|_\infty=\max_{1\leq i\leq n}|x_i|$

$C^n$ 中更多的范数对任意 $X=(x_1,x_2,\dots,x_n)\in C^n$，
1. $p\geq1$ 时，有向量 p-范数：$\|X\|_p=(\sum^n_{i=1}|x_i|^p)^{1/p}$
2. 如果 $\|\bullet\|$ 是已知的范数，A 是一可逆矩阵向量，则 $\|X\|_A=\|AX\|$也是 $C^n$ 上的一种范数

### 5-1-4 V上的范数

设 $V$ 是数域 $F$ 上 $n$ 维线性空间，$\alpha_1,\alpha_2,\dots,\alpha_n$ 是V的一组
基，$\|\bullet\|$ 是 $C^n$ 上已知的范数，据此可以定义 $V$ 上的范数：
若 $\eta\in V$ 在基 $\alpha_1,\alpha_2,\dots,\alpha_n $ 下的坐标是 $X$，规定
$$\|\eta\|=\|X\|$$

### 5-1-5 序列的收敛性

#### 向量序列的收敛性

设 $\|\bullet\|$ 是 V 上的范数，$\{\eta_k\}^\infty_{k=1}$ 是 V 中的一个向量序列，$\eta_0\in V$。如果
$$\lim_{k\rightarrow\infty}\|\eta_k-\eta_0\|=0$$
则称向量序列 $\{\eta_k\}^\infty_{k=1}$ 在范数 $\|\bullet\|$ 下收敛到 $\eta_0$，记为
$$\lim_{k\rightarrow\infty}\eta_k=\eta_0$$

#### 范数的可比较性

假设 $\|\bullet\|$ 和 $\|\bullet\|'$ 都是线性空间 $V$ 上的范数。若存在大于零的数 $k_i\leq k_2$，
使得对任意 $\eta\in V$，不等式 $k_1\|\eta\|'\leq\|\eta\|\leq k_2\|\eta\|'$ 成立，
则称 $V$ 上的范数 $\|\bullet\|$ 和 $\|\bullet\|$ 是可比较的

**定理**：
有限维线性空间 V 上任意两个范数都是可比较的

## 5-2 矩阵范数

### 5-2-1 矩阵 p 范数

矩阵p-范数：
设矩阵 $A=(a_{ij})_{m\times n}$，则有下列矩阵范数：
$$\|A\|_{m_1}=\sum_{i,j}|a_{ij}|$$
$$\|A\|_{m_2}=\left(\sum_{i,j}|a_{ij}|^2\right)^{1/2}=(\operatorname{tr}A^HA)^{1/2}=(\operatorname{tr}AA^H)^{1/2}$$
$$\|A\|_{m_\infty}=\max_{i,j}\{|a_{ij}|\}$$
$\|A\|_{m_2}$ 又记为 $\|A\|_F$，称为 Frobenius 范数，简称 F 范数

**性质**：
F 范数是酉不变的：若 U,V 是酉矩阵，则 $\|A\|_F=\|UAV\|_F$

### 5-2-2 相容性

**定义**：
设 $C^{s\times m},C^{m\times n},C^{s\times n}$ 中定义了范数 $\|\bullet\|_a$，$\|\bullet\|_b$，$\|\bullet\|_c$，
若对 $\forall A\in C^{s\times m}, B\in C^{m\times n}$
$$\|AB\|_c\leq\|A\|_a\|B\|_b$$
则称范数 $\|\bullet\|_a$，$\|\bullet\|_b$，$\|\bullet\|_c$ 是相容的

**定理**：
$\|\bullet\|_{m_1}$，$\|\bullet\|_{m_2}$ 是相容的，$\|\bullet\|_{m_\infty}$ 是不相容的

### 5-2-3 算子范数

设 $\|\bullet\|_{\nu_n}$，$\|\bullet\|_{\nu_m}$ 分别是 $C^n, C^m$ 上的范数，定义 $C^{m\times n}$ 上的实值函数 $\|\bullet\|$：
$$\|A\|=\max_{\theta\neq X\in C^n}\frac{\|AX\|_{\nu_m}}{\|X\|_{\nu_n}}$$
称是由 $\|\bullet\|$ 是由 $\|\bullet\|_{\nu_n}$，$\|\bullet\|_{\nu_m}$ 诱导的算子范数

**定理**：
算子范数一定是相容的矩阵范数

### 5-2-4三个重要的算子范数

$\|\bullet\|_1$，$\|\bullet\|_2$，$\|\bullet\|_\infty$ 诱导的 A 的算子范数分别被称为
A 的算子 1-范数，算子 2-范数，算子 $\infty-$范数，分别记为$\|A\|_1$，$\|A\|_2$，$\|A\|_\infty$

**定理**：
设 $A=(a_{ij})_{s\times n}$，则
$\|A\|_1=\max_{1\leq j\leq n}\left\{\sum_{i=1}^s|a_{ij}|\right\}$，列模和范数
$\|A\|_2=\sqrt{\rho(A^HA)}$，谱范数
$\|A\|_\infty=\max_{1\leq i\leq s}\left\{\sum_{j=1}^n|a_{ij}|\right\}$，行模和范数

## 5-3 收敛定理

### 5-3-1 矩阵序列的收敛性

**定义**：
设矩阵序列 $\{A_k\}_{1\leq k\leq+\infty}, A_k=\left(a_{ij}^{(k)}\right)_{n\times n}$，
如果 $A=(a_{ij})_{n\times n}$，且 $\forall i,j,\lim_{k\rightarrow\infty}A_{ij}^{(k)}=a_{ij}$，
则称 $\lim_{k\rightarrow\infty}A_k=A$

可以证明：若 $\|\bullet\|$ 是一矩阵范数，则
$$\lim_{k\rightarrow\infty}A_k=A\Leftrightarrow\lim_{k\rightarrow\infty}\|A_k-A\|=0$$

### 5-3-2 幂序列

对给定的方阵 A ，考虑方阵序列 $\{A^k\}$

**定理**：
若有相容矩阵范数 $\|\bullet\|$，使得 $\|A\|<1$，则 $\lim_{k\leftarrow\infty}A^k=O$

**定理**：
$\lim_{k\rightarrow\infty}A^k=O\Leftrightarrow\rho(A)<1$

### 5-3-3 谱半径

**定理**：
若 $\|\bullet\|$ 是相容矩阵范数，则 $\rho(A)\leq\|A\|$

**定理**：
对任意矩阵 $A\in C^{n\times n}$，若 $\varepsilon>0$，则一定存在 $C^{n\times n}$ 上相容矩阵
范数 $\|\bullet\|$，使得 $\|A\|<\rho(A)+\varepsilon$

### 5-3-4 矩阵幂级数

设 A 是方阵，对于幂级数
$$\sum_{i=0}^{+\infty}a_ix^i, f_n(x)=\sum^n_{i=0}a_ix^i$$
若矩阵序列 ${f_n(A)}$ 收敛于矩阵 M，则称矩阵幂级数 $\sum_{i=0}^{+\infty}a_iA^i$ 收敛于 M

**定理**：
若幂级数 $\sum_{i=0}^{+\infty}a_ix^i$ 的收敛半径为 $r$，则
- 当 $\rho(A)<r$ 时，矩阵幂级数 $\sum_{i=0}^{+\infty}a_iA^i$ 收敛
- 当 $\rho(A)>r$ 时，矩阵幂级数 $\sum_{i=0}^{+\infty}a_iA^i$ 发散

## 5-4 矩阵函数

### 5-4-1 定义

设函数 $f(x)$ 可以展开成幂级数
$$f(x)=\sum_{i=0}^{+\infty}a_ix^i, |x|<R$$
设 $A\in C^{n\times n}$，且 $p(A)<R$，定义
$$f(A)=\sum_{i=0}^{+\infty}a_iA^i=\lim_{n\rightarrow+\infty}\sum_{i=0}^na_iA^i$$

几个重要的函数
$$e^{x}=\sum_{i=0}^{+\infty} \frac{x^{i}}{i !}$$
$$\sin x=\sum_{i=0}^{+\infty}(-1)^{i} \frac{x^{2 i+1}}{(2 i+1) !}$$
$$\cos x=\sum_{i=0}^{+\infty}(-1)^{i} \frac{x^{2 i}}{(2 i) !}$$

> $e=\sum_{i=0}^{+\infty} \frac{1}{i !}$

### 5-4-2 Jordan 形矩阵

#### Jordan 形矩阵的函数

假设
$$f(x)=\sum_{k=0}^\infty a_kx^k=\lim_{n\rightarrow\infty}f_n(x)$$
其中 $f_n(x)=\sum_{k=0}^n a_kx^k$

$$J=\begin{pmatrix}J_1&&&\\&J_2&&\\&&\ddots&\\&&&J_s\end{pmatrix}$$
$$f_n(J)=\begin{pmatrix}f_n(J_1)&&&\\&f_n(J_2)&&\\&&\ddots&\\&&&f_n(J_s)\end{pmatrix}$$
令 $n\rightarrow\infty$，得
$$f(J)=\begin{pmatrix}f(J_1)&&&\\&f(J_2)&&\\&&\ddots&\\&&&f(J_s)\end{pmatrix}$$

#### Jordan 块的函数

设 $n\times n$ 若当块 $J_0=\begin{pmatrix}\lambda_0&1&&\\&\lambda_0&\ddots&\\&&\ddots&1\\&&&\lambda_0\end{pmatrix}$，则
$$f_{k}\left(J_{0}\right)=
\left(\begin{array}{cccccc}
f_{k}\left(\lambda_{0}\right) & \frac{f_{k}^{\prime}\left(\lambda_{0}\right)}{1 !} & \frac{f_{k}^{\prime \prime}\left(\lambda_{0}\right)}{2 !} & \cdots & \frac{f_{k}(n-2)\left(\lambda_{0}\right)}{(n-2) !} & \frac{f_{k}(n-1)}{(n-1) !} \\
0 & f_{k}\left(\lambda_{0}\right) & \frac{f_{k}^{\prime}\left(\lambda_{0}\right)}{1 !} & \ddots & \cdots & \frac{f_{k}(n-2)\left(\lambda_{0}\right)}{(n-2) !} \\
0 & 0 & f_{k}\left(\lambda_{0}\right) & \ddots & \ddots & \vdots \\
\vdots & \vdots & \vdots & \ddots & \ddots & \frac{f_{k}^{\prime \prime}\left(\lambda_{0}\right)}{2 !} \\
\vdots & \vdots & \vdots & \cdots & \cdots & \frac{f_{k}^{\prime}\left(\lambda_{0}\right)}{1 !} \\
0 & 0 & 0 & \cdots & \cdots & f_{k}\left(\lambda_{0}\right)
\end{array}\right)$$
$$f\left(J_{0}\right)=
\left(\begin{array}{cccccc}
f\left(\lambda_{0}\right) & \frac{f^{\prime}\left(\lambda_{0}\right)}{1 !} & \frac{f^{\prime \prime}\left(\lambda_{0}\right)}{2 !} & \cdots & \frac{f(n-2)\left(\lambda_{0}\right)}{(n-2) !} & \frac{f(n-1)}{(n-1) !} \\
0 & f\left(\lambda_{0}\right) & \frac{f^{\prime}\left(\lambda_{0}\right)}{1 !} & \ddots & \cdots & \frac{f(n-2)\left(\lambda_{0}\right)}{(n-2) !} \\
0 & 0 & f\left(\lambda_{0}\right) & \ddots & \ddots & \vdots \\
\vdots & \vdots & \vdots & \ddots & \ddots & \frac{f^{\prime \prime}\left(\lambda_{0}\right)}{2 !} \\
\vdots & \vdots & \vdots & \cdots & \cdots & \frac{f^{\prime}\left(\lambda_{0}\right)}{1 !} \\
0 & 0 & 0 & \cdots & \cdots & f\left(\lambda_{0}\right)
\end{array}\right)$$

#### 利用Jordan 标准形计算

**定理**
设矩阵 A 的 Jordan 标准形是
$$P^{-1}AP=J=\begin{pmatrix}J_1&&&\\&J_2&&\\&&\ddots&\\&&&J_s\end{pmatrix}$$
则
$$f(A)=Pf(J)P^{-1}$$

**定理**
己知 $n\times n$ 矩阵 A 的特征值为 $\lambda_1,\lambda_2\dots\lambda_n$，则 $f(A)$ 的特征
值为 $f(\lambda_1),f(\lambda_2)\dots f(\lambda_n)$

### 5-4-3 待定系数法

设矩阵 A 的 Jordan 标准形是
$$P^{-1}AP=J=\begin{pmatrix}J_1&&&\\&J_2&&\\&&\ddots&\\&&&J_s\end{pmatrix}$$
则 $f(A)=Pf(J)P^{-1}$
其中，$f(J)=\begin{pmatrix}f(J_1)&&&\\&f(J_2)&&\\&&\ddots&\\&&&f(J_s)\end{pmatrix}$

**定理**：
若 A 的最小多项式为 $m(\lambda)=\prod_{i=1}^s(\lambda-\lambda_i)^{t_i}$，则
$f(A)=g(A)\Leftrightarrow$ 对每个特征值 $\lambda_i$，

$$f\left(\lambda_{i}\right)=g\left(\lambda_{i}\right),\\
f^{\prime}\left(\lambda_{i}\right)=g^{\prime}\left(\lambda_{i}\right), \\
\cdots,\\
f^{\left(t_{i}-1\right)}\left(\lambda_{i}\right)=g^{\left(t_{i}-1\right)}\left(\lambda_{i}\right) $$

### 性质

**定理**：
设 $A,B\in C^{n\times n}, O$ 是 $n\times n$ 零矩阵，则
1. $e^O=I$
2. 若 $AB=BA$，则 $e^Ae^B=e^Be^A=e^{A+B}$
3. $(e^A)^{-1}=e^{-A}$

$(A^B)^H=A^{(B^H)}$
