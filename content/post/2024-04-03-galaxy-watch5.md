---
image:      https://images.samsung.com.cn/cn/galaxy-watch5/feature/galaxy-watch5-design.jpg
show_author_profile: true
date:       2024-04-18T14:00:00+08:00
tags:       ["折腾"]
title:      三星Galaxy Watch 5 与国行手机的艰难使用
draft:      false
---

我是闲鱼买的二手 Galaxy Watch 5 40mm 蓝牙版，500块左右，续航刚好一天多一点。
其实就算是44mm LTE也就这续航了，所以LTE的意义也不是很大。

能测血压、心电图、身体成分，佩戴也相当无感，而且就500块，要啥自行车。

## 1 初次安装手机软件

1. 如有，卸载已安装的所有三星手表相关APP
2. 从 [三星中国官网](https://apps.samsung.cn/gear) 下载 *三星智能穿戴App*
3. 按照App和手表的提示正常操作即可

只需要手动给 *三星健康* 和 *Watch 5 Manager* 自启动权限即可，其它权限如有需要，应用会自己申请的。

> 无需启用谷歌套件（毕竟是国行）

## 2 更新手表系统

安装更新时，直接用手表连接WiFi进行下载和安装，用手机进行安装有概率失败。

## 3 血压和心电图

https://github.com/ITDev93/SHM-MOD

## 4 解决 *三星健康* 卡在授权页的bug并支持微信步数

首先根据酷安PanamWebber的教程来设置 *三星健康*：[关于三星健康步数插件无法同步至微信运动的解决方法](https://www.coolapk.com/feed/44392293)

>  1. 首先，在你手机的`download`文件夹下面建立一个名为`SamsungHealth`的文件夹，然后在里面再建立一个名为`FeatureManagerOn`的文件夹(图一)
>  2. 进入三星健康设置→关于三星健康，连续点击版本号直到出现`Set`开头的选项(图二)
>  3. 将图三的选项改为`Dev`，图四划线的选项改为`On`
>  4. 改完之后返回，之后系统会提示你去设置里面强行停止三星健康，照做就是了，然后再到[查看链接](https://ecommerce.samsungassistant.cn/index.html#/jd/activity/524/0)里面去激活插件，权限记得全给，然后按着他的提示来就可以了

### 4-1 微信步数同步插件

酷安搜索 我的手表没电了 用户来安装修改版的步数同步插件

## 5 *三星智能穿戴* 提示更新但是无法安装

一般来说就是需要更新 *Watch 5 Manager* 了。对于 HyperOS 来说似乎不管是关闭 *安全守护* 还是 *系统优化* 都无法正常安装。这里暂且给一个个人提取的版本：

|版本号|下载链接|
|---|---|
|`24032551`|[watch5manager24032551.apk](/post/2024-04-03-galaxy-watch5/watch5manager24032551.apk)|

## 6 其它有用的App

### 6-1 WearOS 工具箱

用来通过无线调试给手表安装Apk，还自带一个应用商店，比较方便：[WearOS 工具箱](https://wearosbox.com/)

而工具箱的官网提供的文档也相当实用：[三星手表玩表技巧](https://help.wearosbox.com/faq/device/samsung.html)

### 6-2 米屋

第三方手表版米家「米屋」：[MiWu](https://github.com/sky130/MiWu)
