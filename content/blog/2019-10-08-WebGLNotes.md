---
layout:     article
title:      WebGL笔记
date:       2019-10-08 8:00
updated:    2019-10-23 9:00
abstract:   学得一塌糊涂
tags:       ["学习", "编程"]
#cascade:
#   banner:
show_author_profile: true
---
计算机图形学笔记系列
<!--more-->
# WebGL

1.	现在不再支持立即绘制
2.	支持GPU

用回调函数构造显示函数

## 基本结构

-	描述页面（HTML）
-	定义着色器（HTML）
-	计算或指定数据（JS）
-	发送数据至GPU（JS）
-	绘制（JS）

### HTML

```html
<!DOCTYPE html>
<html>
<head>
<script id=“webgl”>
</script>
</head>
<body>
<canvas id=“glcanvas” width=“512”>
FUCK IE
</canvas>
</body>
</html>
```

### WebGL 照相机

正交视图：x、y、z三轴在[-1, 1]间的立方体内默认投影到z=0的投影屏幕上。

### 视窗

```Javascript
glViewport(x, y, w, h);//
```

## 着色器

应用程序定义vPosition

1.	顶点着色器
2.	片元着色器

## 数据类型

基础：int，float，bool

数组：vec3

矩阵：mat3

结构体：

### 修饰符

`const`：

`attribute`：由应用程序传入，可以逐顶点

`uniform`：着色器中无法修改

### 命名规范

传入到顶点着色器的：v开头

Varying变量：f开头