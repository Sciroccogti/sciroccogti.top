---
layout:     article
title:      让你的 Ubuntu 看起来像 Mac
date:       2020-04-02T18:30:00+08:00
summary:    " "
tags:       ["软件"]
show_author_profile: true
---

# 让你的 Ubuntu 看起来像 Mac

参考教程：[史上最良心的 Ubuntu desktop 美化优化指导(1)](https://zhuanlan.zhihu.com/p/63584709)

在 Ubuntu 18.04 测试通过

## 安装美化必要的工具

```Bash
sudo apt update
sudo apt install gnome-tweaks
sudo apt install chrome-gnome-shell
```

打开 `https://extensions.gnome.org/` ，根据提示安装 Firefox 浏览器的 gnome 扩展

### 安装主题

- [User Themes](https://extensions.gnome.org/extension/19/user-themes/)
- [Mcmojave 主题](https://github.com/vinceliuice/Mojave-gtk-theme)：
建议源码安装以获得最新更新
- [Firefox 主题](https://github.com/vinceliuice/Mojave-gtk-theme/blob/master/src/other/firefox)：
是上面那个主题配套的“Safari”主题
- [模糊效果 blyr 插件](https://extensions.gnome.org/extension/1251/blyr/)

### 安装图标

- [Cupertino iCons Collection](https://www.gnome-look.org/p/1102582/)：
解压到 `~/.icons` 目录

### 安装光标

- [OSX El Capitan](https://www.gnome-look.org/p/1084939/)：
也解压到 `~/.icons` 目录

### 更换 dock
- [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)

### 锁屏

- [High Ubunterra](https://www.gnome-look.org/p/1207015/)

其中的右键设为壁纸脚本似乎有问题，建议运行：

```Bash
mv your_picture ~/.cache/SetAsWallpaper/huwallpaper.jpg
gsettings set org.gnome.desktop.background picture-uri "file:///$HOME/.cache/SetAsWallpaper/huwallpaper.jpg"
pkexec convert -resize 1440 -quality 100 -brightness-contrast -10x-15 -blur 0x30 $HOME/.cache/SetAsWallpaper/* /usr/share/backgrounds/gdmlock.jpg
gsettings set org.gnome.desktop.screensaver picture-uri "file:///usr/share/backgrounds/gdmlock.jpg"
```

***

以上文件安装后均需在 *tweaks* 软件中设置，如图：
![](/img/tweaks.png)

### 启动动画

[Darwin Plymouth](https://www.gnome-look.org/p/1009320/)

由于这是一个老款主题，需要修改其中路径。

解压缩后，修改其中的文件 `darwin.plymouth`，将 `/lib` 替换为 `/usr/share`：
```
[Plymouth Theme]
Name=Darwin OS X Plymouth
Description=A Plymouth of OS X Yosemite
ModuleName=script

[script]
ImageDir=/usr/share/plymouth/themes/darwin
ScriptFile=/usr/share/plymouth/themes/darwin/darwin.script
```

复制到 `/usr/share/plymouth/themes/darwin`

运行：
```Bash
sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/darwin/darwin.plymouth 100
sudo update-alternatives --config default.plymouth
# 选择对应主题
sudo update-initramfs -u
```
