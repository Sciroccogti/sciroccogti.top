---
title: 第一章 - 线性空间和线性变换
date: 2021-07-31T14:00:00+08:00
categories: 工程矩阵
---

## 1-1 线性空间

### 1-1-1 线性空间的定义

线性空间是由下述三个要素确定的代数系统：
1. 一个数域 $F$，一个非空集合 $V$ （$V$ 中的元素也称为向量）；
2. 两个运算：加法：$V+V\rightarrow V$；数乘：$F\times V\rightarrow V$；
3. 上述运算满足如下八个公理：**其实只需加法、乘法封闭**
   - 加法交换律：$\forall\alpha,\beta\in V$，有 $\alpha+\beta=\beta+\alpha$；
   - 加法结合律：$\forall\alpha,\beta,\gamma\in V$，有 $(\alpha+\beta)+\gamma=a+(\beta+\gamma)$；
   - 零元存在性：存在 $\theta\in V$，使得$\forall\alpha\in V$，有$\alpha+\theta=\alpha$；
   - 负元存在性：$\forall\alpha\in V$，存在 $\beta\in V$，使得 $\alpha+\beta=\theta$；
   - 幺等律：$\forall\alpha\in V$，$1\alpha=\alpha$；
   - 数乘结合律：$\forall k,l\in F,\forall\alpha\in V$，都有 $(kl)\alpha=k(l\alpha)$；
   - 分配律：$\forall k,l\in F,\alpha\in V$,有$(k+l)\alpha=k\alpha+l\alpha$；
   - 分配律：$\forall k\in F,\forall\alpha,\beta\in V$,都有$k(\alpha+\beta)=k\alpha+k\beta$。

### 1-1-2 线性空间的例子

1. 数域 $F$ 上所有 $n$ 维向量全体，按向量的加法和数乘，构成一个线性空间，记为 $F^n$
2. 数域 $F$ 上所有 $m\times n$ 矩阵全体，按矩阵的加法和数乘，构成一个线性空间.记为 $F^{m\times n}$
3. 数域 $F$ 上所有一元多项式全体，按多项式的加法和数乘，构成一个线性空间.记为 $F[x]$
4. 数域 $F$ 上所有次数小于n的一元多项式全体，按多项式的加法和数乘，构成一个线性空间，记为 $Fn[x]$

### 1-1-3 线性空间的性质

设$V$是数域$F$上的线性空间，$\alpha,\beta,\gamma\in V,k\in K$，则：
1. V中的零向量是唯一的.通常记为$\theta$：
2. V中任一向量$\alpha$的负向量是唯一的.通常记为$-\alpha$，
3. 加法消去律：若$\alpha+\gamma=\beta+\gamma$，则$\alpha=\beta$；
4. 向量方程的解：$\alpha+x=\beta$有唯一解，记为$x=\beta-\alpha$；
5. $(-k)\alpha=-k\alpha$，特别地，$(-1)\alpha=-\alpha$；
6. $k\alpha=\theta$，当且仅当$k=0$或$\alpha=\theta$。

## 1-2 基和维数

### 1-2-1 线性相关性

设$\alpha_1,\alpha_2,\dots,\alpha_s\in V$，若存在不全为零的数$k_1,k_2,\dots,k_s$ 使得$k_1\alpha_1+k_2\alpha_2+\dots+k_s\alpha_s=\theta$，则称向量组$\alpha_1,\alpha_2,\dots,\alpha_s$线性相关。否则，称$\alpha_1,\alpha_2,\dots,\alpha_s$线性无关

- **相关**：能表示
- **无关**：不能表示

#### 重要性质

1. 若s≥2，则$\alpha_1,\alpha_2,\dots,\alpha_s$线性相关当且仅当存在向量 $\alpha_j$，使得$\alpha_j$可由其余向量线性表示
2. 若$\alpha_1,\alpha_2,\dots,\alpha_s$线性无关，但$\beta,\alpha_1,\alpha_2,\dots,\alpha_s$线性相关，则$\beta$可由$\alpha_1,\alpha_2,\dots,\alpha_s$线性表示，而且，线性表示的方法是唯一的.
3. 若$t>s,\beta_1,\beta_2,\dots,\beta_t$可由$\alpha_1,\alpha_2,\dots,\alpha_s$线性表示，则$\beta_1,\beta_2,\dots,\beta_t$线性相关


若$\beta_1,\beta_2,\dots,\beta_t$可由$\alpha_1,\alpha_2,\dots,\alpha_s$线性表示，且$\beta_1,\beta_2,\dots,\beta_t$线性无关，则t≤s

若$\beta_1,\beta_2,\dots,\beta_t$与$\alpha_1,\alpha_2,\dots,\alpha_s$等价，且都线性无关，则$t=s$

==**等价**：两向量组可相互线性表示==

线性空间中的向量仅代表元素，因此向量也可以是矩阵

### 1-2-2 基、维数和坐标

#### 基

**定义**：
若$\alpha_1,\alpha_2,\dots,\alpha_n\in V$ 满足条件：
1. $\alpha_1,\alpha_2,\dots,\alpha_n$ 线性无关
2. 任意的 $\eta\in V$ 均可由 $\alpha_1,\alpha_2,\dots,\alpha_n$线性表示
则称$\alpha_1,\alpha_2,\dots,\alpha_n$ 是 V 的一组基

#### 维数

1. 若 $V$ 的某一组基中含$n$个向量，则$V$的任一组基中都含$n$个向量，称$n$是$V$的维数，记为$dimV$
2. 若$dim V=n$，则$V$中任意$n+1$个向量线性相关
3. 线性空间的基不一定存在，
   - 如：只含一个零向量的空间称为零空间，规定零子空间的维数为$0$.
   - 再如：$V=F[x]$规定 $dimF[x]=\infty$

**定理**：若 $dim V=n$，则 V 中任意 $n$ 个线性无关的向量均构成 $V$ 的基

#### 坐标

**定义**：
设 $\alpha_1,\alpha_2,\dots,\alpha_n$ 是V的一组基，$\beta\in V$，且 $\beta=x_1\alpha_1+x_2\alpha_2+\dots+x_n\alpha_n$，则称 $x_1,x_2,\dots,x_n$ 是β在基$\alpha_1,\alpha_2,\dots,\alpha_n$下的坐标，或$\begin{pmatrix}x_1\\x_2\\\vdots\\x_n \end{pmatrix}$是β在基$\alpha_1,\alpha_2,\dots,\alpha_n$下的坐标（列向量）

性质：
1. 线性空间的基是有序的
2. 基相当于几何空间中的坐标系

**定理**：
假设，$\eta,\eta_i\in V$ 在基$\alpha_1,\alpha_2,\dots,\alpha_n$下的坐标分别是$X$及$X_i,i=1,2,\dots,s$，则
1. $\eta=\theta\Leftrightarrow X=\theta$；
2. $\eta=k_1\eta_1+k_2\eta_2+\dots+k_s\eta_s\Leftrightarrow X=k_1X_1+k_2X_2+\dots+k_sX_s$
3. $\eta_1,\eta_2,\dots,\eta_s$线性相关$\Leftrightarrow X_1,X_2,\dots,X_s$线性相关.

$X_1X_2X_3$ 的秩：
1. 若 $=3$：线性无关
2. 若 $<3$：线性相关
即其阶梯矩阵非零行的数量

### 1-2-3 基变换和坐标变换

#### 形式记号

设$\alpha_1,\alpha_2,\dots,\alpha_s\in V$,定义形式行向量$\alpha_1,\alpha_2,\dots,\alpha_s$。
比如，若 $X=\begin{pmatrix}x_1\\x_2\\\vdots\\x_n \end{pmatrix}$ 是β在基$\alpha_1,\alpha_2,\dots,\alpha_n$下的坐标，
则$\beta$可形式地记成$\beta=(\alpha_1,\alpha_2,\dots,\alpha_n)\begin{pmatrix}x_1\\x_2\\\vdots\\x_n \end{pmatrix}=(\alpha_1,\alpha_2,\dots,\alpha_n)X$。
若$\beta_1,\beta_2,\dots,\beta_t$可由$\alpha_1,\alpha_2,\dots,\alpha_s$线性表示，
于是，我们可以找到一个s×t矩阵A使得$(\beta_1,\beta_2,\dots,\beta_t)=(\alpha_1,\alpha_2,\dots,\alpha_s)A$

**性质**：
若 $(\beta_1,\beta_2,\dots,\beta_t)=(\alpha_1,\alpha_2,\dots,\alpha_s)A$，
$(\gamma_1,\gamma_2,\dots,\gamma_p)=(\beta_1,\beta_2,\dots,\beta_t)B$
则$(\gamma_1,\gamma_2,\dots,\gamma_p)=(\alpha_1,\alpha_2,\dots,\alpha_s)(AB)$

#### 过渡矩阵

**定义**：
设 $\alpha_1,\alpha_2,\dots,\alpha_n$及$\beta_1,\beta_2,\dots,\beta_n$都是V的基，且
$(\beta_1,\beta_2,\dots,\beta_n)=(\alpha_1,\alpha_2,\dots,\alpha_n)A$
则称A是从基$\alpha_1,\alpha_2,\dots,\alpha_n$到基$\beta_1,\beta_2,\dots,\beta_n$的过渡矩阵

==过渡矩阵是右乘的！且顺序是反的！==
例如：若$X=x(\alpha_1,\alpha_2,\dots,\alpha_n)$，$XA=x(\beta_1,\beta_2,\dots,\beta_n)$
则知$A$为从基$\alpha_1,\alpha_2,\dots,\alpha_n$到基$\beta_1,\beta_2,\dots,\beta_n$的过渡矩阵
但$X$在$\beta$下应为$xA^{-1}$

**性质**：
1. 过渡矩阵一定是可逆的
2. 若从基$\alpha_1,\alpha_2,\dots,\alpha_n$到基$\beta_1,\beta_2,\dots,\beta_n$的过渡矩阵是A，则从基$\beta_1,\beta_2,\dots,\beta_n$到基$\alpha_1,\alpha_2,\dots,\alpha_n$的过渡矩阵是$A^{-1}$.
3. 若从基$\alpha_1,\alpha_2,\dots,\alpha_n$到基$\beta_1,\beta_2,\dots,\beta_n$的过渡矩阵是A，从基$\beta_1,\beta_2,\dots,\beta_n$到基$\gamma_1,\gamma_2,\dots,\gamma_n$的过渡矩阵是B，则从基$\alpha_1,\alpha_2,\dots,\alpha_n$到基$\gamma_1,\gamma_2,\dots,\gamma_n$的过渡矩阵是$AB$.

#### 坐标变换公式

设 $\eta\in V$在基$\alpha_1,\alpha_2,\dots,\alpha_n$下的坐标是X，在基$\beta_1,\beta_2,\dots,\beta_n$下的坐标是Y，而从基$\alpha_1,\alpha_2,\dots,\alpha_n$到基$\beta_1,\beta_2,\dots,\beta_n$的过渡矩阵是$P$，则==$X=PY$，或$Y=P^{-1}X$==

## 1-3 子空间

### 1-3-1 子空间的定义

设 V 是数域 F 上的线性空间， W 是 V 的非空子集。若 W 关于 V 的运算也构成 F 上的线性空间，则称 W 是 V 的子空间.记 $W\leq V$

> W的运算与V中的运算应当相同

### 1-3-2 充分必要条件

设$W\subseteq V$，则 $W$ 是 $V$ 的子空间$\Leftrightarrow W$ 关于线性运算封闭

### 1-3-3 重要子空间

1. 设 $A\in F^{s\times n},V=\{\eta\in F^n|A\eta=\theta\}$，称 V 是齐次线性方程组 $Ax=\theta$ 的解空间.（基础解系是 V 的一组基，维数是 $n-r$。）
2. 设 $V$ 是 $F$ 上的线性空间，$\alpha_1,\alpha_2,\dots,\alpha_s\in V$，集合
   $$W=\left\{\sum^s_{i=1}k_i\alpha_i|\forall k_i\in F\right\}$$
   称 W 是由 $\alpha_1,\alpha_2,\dots,\alpha_s$ 生成的子空间
   称 $\alpha_1,\alpha_2,\dots,\alpha_s$ 是W的生成元。记 $W=L(\alpha_1,\alpha_2,\dots,\alpha_s)$

**性质**：
1. 若 $W=L(\alpha_1,\alpha_2,\dots,\alpha_s)$ ，则 $\forall k_j\in W$
2. $L(\alpha_1,\alpha_2,\dots,\alpha_s)=L(\beta_1,\beta_2,\dots,\beta_t)\Leftrightarrow\alpha_1,\alpha_2,\dots,\alpha_s$与 $\beta_1,\beta_2,\dots,\beta_t$ 等价
3. $\alpha_1,\alpha_2,\dots,\alpha_s$ 的极大无关组是 $L(\alpha_1,\alpha_2,\dots,\alpha_s)$ 的基，故$dimL(\alpha_1,\alpha_2,\dots,\alpha_s)=r(\alpha_1,\alpha_2,\dots,\alpha_s)$

### 1-3-4 基扩充定理

有限维线性空间 V 中任意线性无关向量组均可扩充成 V 的基

## 1-4 子空间的交与和

并集并不是子空间

### 1-4-1 交与和的定义

**定义**
$V_1\cap V_2=\{\eta\in V|\eta\in V_1,\eta\in V_2$
$V_1+V_2=\{\eta\in V | \exist \eta\in V_1,\eta\in V_2 s.t.\eta=\eta_1+\eta_2\}$ 分别称为子空间的交与和

**定理**
$V_1\cap V_2,V_1+V_2$都是 V 的子空间.

### 1-4-2 维数定理

**定理**：
若 $V_1=L(\alpha_1,\alpha_2,\dots,\alpha_s),V_2=L(\beta_1,\beta_2,\dots,\beta_t)$
则 $V_1+V_2=L(\alpha_1,\alpha_2,\dots,\alpha_s,\beta_1,\beta_2,\dots,\beta_t)$

**维数定理**：
假设$V_1,V_2\leq V$，有$dim(V_1+V_2)=dim V_1+dim V_2-dim(V_1\cap V_2)$

### 1-4-3 直和

**定义**
设 $V_1,V_2\leq V$，若$\forall\eta\in V_1+V_2, \exist$唯一的 $\eta_1\in V_1, \eta_2\in V_2$，使得 $\eta=\eta_1+\eta_2$，
则称 $V_1+V_2$ 是直和，记为$V_1\oplus V_2$

==**定理**：==
设 $V_1,V_2\leq V$，则下述条件是等价的：
1. $V_1+V_2$ 直和
2. $\theta$ 的表示方式是唯一的
3. $V_1\cap V_2=\{\theta\}$
4. $dim(Vi+V2)=dimV_1+dim V_2$；
5. 将$V_1,V_2$的基合在一起就是$V_1+V_2$的基

**多个子空间的直和**：
设 $V_1,V_2,\dots,V_s\leq V$，若 $\forall\eta\in V_1+V_2+\dots+V_s$，
$\exist$唯一的$\eta_i\in V_i,i=1,2,\dots,s$，使得$\eta=\sum^s_{i=1}\eta_i$，
则称 $V_1+V_2+\dots+V_s$ 是直和，记为 $V_1\oplus V_2\oplus\dots\oplus V_s$.

**定理**：
设$V_1,V_2,\dots,V_s\leq V$，则下述条件是等价的：
1. $V_1+V_2+\dots+V_s$ 直和
2. $\theta$ 的表示方式是唯一的
3. $V_j\cap\sum_{i\neq j}V_i=\{\theta\}$
4. $dim\sum^s_{i=1}V_i=\sum_{i=1}^sdimV_i$；
5. 将$V_1,V_2,\dots,V_s$的基合在一起就是$V_1+V_2+\dots+V_s$的基

## 1-5 线性映射

### 1-5-1 映射的概念

**定义**：
设 S 和 T 是两个集合，$f$ 是一个法则，使得对 $S$ 中每个元素 $x$，
在 T 中必存在唯一的元素 y 与之对应，则称 $f$ 是 S 到 T 的映射，
记为
$$f:S\rightarrow T,f(x)=y$$
如果$f(x)=y$，则称 y 为 x 的象，x 为 y 的原象
S在映射 $f$ 下的全体象记为 $f(S)$，称为 $f$ 的值域
集合S到自身的映射 $f:S\rightarrow S$ 称为S上的变换
集合S到自身的映射 $f:S\rightarrow S$，$x\rightarrow x$称为S上的恒等变换

**定义**：
设映射 $f:S\rightarrow T$，若 $f(S)=T$.则称 $f$ 是满射
若由 $f(a)=f(b)$ 必能推得 $a=b$，则称 $f$ 是单射
若 $f$ 既是满射又是单射，则称 $f$ 是双射

**定理**：
$f:S\rightarrow S$ 是双射 $\Leftrightarrow f$是可逆映射
（即，存在映射$g:T\rightarrow S$，使得$gf=I_S$，fg=I_T）

**线性映射**
设 V,U 是数域 F 上的线性空间，若映射$f:V\rightarrow U$满足条件：
1. $\forall\in V,k\in F,f(kx)=kf(x)$ 齐性
2. $\forall x,y\in V,f(x+y)=f(x)+f(y)$ 可加性
则称 $f$ 是从 V 到 U 的**线性映射**，
从 V 到 U 的线性映射全体记为 $Hom(V,U)$
V 到 V 自身的线性映射称为 V 上的**线性变换**

假设$f:V\rightarrow U$是线性映射.则：
1. $f(\theta)=\theta$；
2. 若 $\alpha_1,\alpha_2,\dots,\alpha_s\in V, k_1,k_2,\dots,k_s\in F$
   则 $f(\sum_{i=1}^sk_i\alpha_i)=\sum_{i=1}^sk_if(\alpha_i)$
3. 若 $\alpha_1,\alpha_2,\dots,\alpha_s\in V$ 线性相关，则 $f(\alpha_1),f(\alpha_2),\dots,f(\alpha_s)\in U$ 线性相关
4. 若 $V=L(\alpha_1,\alpha_2,\dots,\alpha_s)$，则 $f$ 的值域
$$R(f)=L(f(\alpha_1),f(\alpha_2),\dots,f(\alpha_s))$$
5. $K(f)=\{x\in V|f(x)=\theta\}$是 V 的子空间，称为 $f$ 的核空间，也记作 $f^{-1}(\theta)$

#### 线性变换的运算

假设 $f,f'\in Hom(V,U),g\in Hom(U,W),k\in F$，定义 $kf,f+f',gf$ 如下：
1. $kf:V\rightarrow U,(kf)(x)=kf(x)$
2. $f+f':V\rightarrow U,(f+f')(x)=f(x)+f'(x)$
3. $gf:V\rightarrow W,(gf)(x)=g(f(x))$ 容易记错！不满足交换律
容易验证，以上运算的结果仍然都是线性映射

$f$ 是线性变换

**性质**：
设 $f,g,h\in Hom(V,V)$。则：
1. $(fg)h=f(gh)$
2. $f(g+h)=fg+fh$
3. $(f+g)h=fh+gh$

### 1-5-2 基下的矩阵

设$f\in Hom(V,U)$，选定基偶：
$$V:\alpha_1,\alpha_2,\dots,\alpha_n,U:\beta_1,\beta_2,\dots,\beta_s$$
若
$$(f(\alpha_1),f(\alpha_2),\dots,f(\alpha_s))=(\beta_1,\beta_2,\dots,\beta_s)A$$
则称 A 是 $f$ 在选定基偶下的矩阵
特别如果 $U=V$，且$\alpha_i=\beta_i$，
$$(f(\alpha_1),f(\alpha_2),\dots,f(\alpha_s))=(\alpha_1,\alpha_2,\dots,\alpha_s)A$$
则称 A 是线性变换 $f$在所选基下的矩阵.

**定理**：
若$f\in Hom(V,U)$在基偶
$$V:\alpha_1,\alpha_2,\dots,\alpha_n;U:\beta_1,\beta_2,\dots,\beta_s$$
下的矩阵是 $A, \eta\in V$ 在 $\alpha_1,\alpha_2,\dots,\alpha_n$的坐标是 $X$，
则 $f(n)$ 在基 $\beta_1,\beta_2,\dots,\beta_s$ 下的坐标是 $AX$.

**定理**：
设 $f\in Hom(V,U)$在选定基偶：$V$ 的一组基 $\alpha_1,\alpha_2,\dots,\alpha_n$ 到
基 $\beta_1,\beta_2,\dots,\beta_s$ 的过渡矩阵是 $P$，$U$ 的一组基$\xi_1,\xi_2,\dots,\xi_s$到
基 $\eta_1,\eta_2,\dots,\ets_s$ 的过渡矩阵是$Q$，
若$f$在基偶 $\{a_i\}_1^n$ 与 $\{\xi_i\}_1^s$ 下矩阵为A，在基偶 $\{\beta_i\}_1^n$ 与 $\{\eta_i\}_1^s$ 下矩阵为 $B$，
则 $B=Q^{-1}AP$
特别是，若 $f\in Hom(V,V)$ 在基 $\alpha_1,\alpha_2,\dots,\alpha_n$ 下的矩阵是 $A$,
则 $f$ 在新的基$\alpha'_1,\alpha'_2,\dots,\alpha'_n)=(\alpha_1,\alpha_2,\dots,\alpha_n)P$ 下的矩阵
是 $B=P^{-1}AP$

> 可知 A 与 B 相似，也就是说同一线性变换在不同的基偶下是相似的

**定理**：
假设 $f,g\in Hom(V,V)$ 在 V 的基 $\alpha_1,\alpha_2,\dots,\alpha_s$ 下的矩阵分别
是A，B，设 $k\in F$，则在基 $\alpha_1,\alpha_2,\dots,\alpha_s$ 下，
1. $kf$ 的矩阵是 $kA$
2. $f+g$ 的矩阵是 $A+B$；
3. $fg$ 的矩阵是 $AB$；
4. $f$ 可逆 $\Leftrightarrow$ 矩阵 $A$ 可逆，并且，$f^{-1}$ 的矩阵是 $A^{-1}$

### 1-5-3 值域和核

假设 $f\in Hom(V,U)$，则
- $f$ 是满射$\Leftrightarrow R(f)=U$。若 $dim U<\infty$，则 $R(f)=U\Leftrightarrow dimR(f)=dim U$
- $f$ 是单射$\Leftrightarrow K(f)=\{\theta\}\Leftrightarrow dim K(f)=0$

#### 值域的计算

若 $f\in Hom(V,U)$ 在基偶 $V: \alpha_1,\alpha_2,\dots,\alpha_n$，$U: \beta_1,\beta_2,\dots,\beta_s$ 下的矩阵是 A，即
$$(f(\alpha_1),f(\alpha_2),\dots,f(\alpha_n))=(\beta_1,\beta_2,\dots,\beta_s)A$$
由于
$$R(f)=L(f(\alpha_1),f(\alpha_2),\dots,f(\alpha_n))$$
$f(\alpha_1),f(\alpha_2),\dots,f(\alpha_s)$ 的极大无关组是 $R(f)$的基
特别地，$dim R(f)=r(A)$

### 1-5-4 核子空间的计算

若 $f\in Hom(V,U)$ 在基偶 $V: \alpha_1,\alpha_2,\dots,\alpha_n$，$U: \beta_1,\beta_2,\dots,\beta_s$ 下的矩阵是 A，$y\in V$ 在 $\alpha_1,\alpha_2,\dots,\alpha_s$ 的坐标是 X，则 $f(\eta)$ 在基$\beta_1,\beta_2,\dots,\beta_s$下的坐标是 $AX$。因此，
$$\eta\in K(f)\Leftrightarrow AX=\theta$$
从而，若 $X_1,X_2,\dots,X_{n-r}$ 是 $AX=\theta$ 的基础解系，$\eta_j$ 是以 $X_j$ 为坐标的 $V$ 中的向量，则 $\eta_1,\eta_2,\dots,\eta_{n-r}$ 是 $K(f)$ 的基
$$dimK(f)=n-r(A)$$

**维数定理**：
假设 $dim V<\infty,f\in Hom(V,U)$，则
$$dim R(f)+dim K(f)=dimV$$

**推论**：
设 $dim V<\infty,f\in Hom(V,V)$ ，则 $f$ 可逆 $\Leftrightarrow f$ 是单射 $\Leftrightarrow f$ 是满射
> 对无限维空间，推论不成立

### 1-5-5 不变子空间

设 $f\in Hom(V,V),W\leq V$，若 $\forall\eta\in W$，有 $f(\eta)\in W$，则称 W 是 $f$ 的不变子空间
