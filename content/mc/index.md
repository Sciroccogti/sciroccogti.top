---
layout: article
title: 暗夜基地MC服务器
publishdate:       2020-02-03T11:00:00+08:00
lastmod:    2020-02-03T11:00:00+08:00
---

![img](https://tietu.mclists.cn/banner/mc.sciroccogti.top_25565.jpg)

**简介**：*a fibric mc server of Dark Night Base*

**地址**：`mc.sciroccogti.top:25565`

**海外**: `sg.ob-studio.cn:25503`

**分类**：生存

**版本**：`1.14.4-fabric`

**预览**：[世界地图 by Overviewer](https://www.sciroccogti.top/map/)

## 进服指南

### 下载

#### HMCL

我们选用 **HMCL启动器**：[下载链接](https://hmcl.huangyuhui.net/download)

普通用户请选择 *Windows* 版本`.exe`

#### Java

我们使用的是 *Java* 版 MC，自然需要 *Java* 支持。强烈建议前往 
[Java(64位) for Windows官网](https://www.java.com/zh_CN/download/windows-64bit.jsp)下载安装。
如果下载速度较慢，可以从群文件中下载，但不保证最新。

注意：本服务器仅支持`64位`的 *Java*，因此切勿安装32位的。
如果您正在使用32位的浏览器，网页有可能会自动跳转至32位的下载页面。

### 注册

为了支持使用自定义皮肤，我们采用了外置登录的方式，接入了[LittleSkin皮肤站](https://littleskin.cn)，
请在此站注册，并添加外置登录认证服务器：`https://littleskin.cn/api/yggdrasil`

您可以在此站选择喜爱的皮肤、饰品，抑或是自己上传。

### 选择游戏版本

本服务器目前是 **1.14.4** 版本，请选择安装该版本。

本服务器目前没有加装 *mod* 的意向，因此无需安装 *forge* 或其它整合包。

只需一杯咖啡（或者更少）的时间，您的游戏就已安装完毕。

！注意：如果遇到 *加载版本列表失败，点击此处重试* 的提示，请尝试刷新数次。若仍然无法加载，请在启动器设置中将 *下载源* 改为 *官方*。

#### 推荐的插件

安装一些本地插件不仅可以带来更多可玩性，甚至也能优化游戏性能，大幅提升游戏体验。
以下列举一些推荐的插件，可以按需安装。

> 由于 *Fabric* 优质的高版本支持，我们推荐且仅列出基于 *Fabric* 的插件。
>
> 要安装 *Fabric* 插件，你需要在[选择游戏版本](https://www.sciroccogti.top/mc/#heading-3)
> 时选择附加 *Fabric* 版本。
> 下载好插件的`.jar`包后，在 *HMCL* 的 *游戏管理* -> *模组管理* 中添加对应的`.jar`文件即可。

* **fabric-api**：要使用以下的插件，必须安装该插件。版本最好在0.4.2及以上。
* **modmenu**：能够显示 *Fabric* 插件列表的插件，可以安装一下，虽然其实没什么用。
* **VoxelMap**：超好用的地图类插件，不仅能显示小地图、坐标、附近生物，还能建立导航点，强烈安利。
* **optifabric**：如果要同时使用 *Fabric* 和 *OptiFine* ，就必须安装这个插件。
* **OptiFine**：可以大幅优化FPS（甚至可以达到翻倍的效果），还能支持添加光影包。不依赖 *Fabric* ，如果要同时和 *Fabric* 使用，需要安装 *optfabric*。
* **CustomSkinLoader**：*HMCL* 默认自带的皮肤加载插件，记得别卸载就行。

### 开始游戏

选择 *多人游戏*，添加服务器，地址为`mc.sciroccogti.top`

进服后会提示是否下载资源包，这里建议下载。

> 每个客户端仅需下载一次资源包，除非资源包更新。

### 

### 游戏注意事项

服务器关闭了友伤。

## paper.yml

```yml
fix-zero-tick-instant-grow-farms: false # 允许强制催熟
```
