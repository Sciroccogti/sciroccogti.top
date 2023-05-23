---
title:      在 ThinkPad X13 Yoga 上配置 Manjaro
date:       2023-04-16T00:45:00+08:00
tags:       ["软件"]
image:      https://wallpaperaccess.com/full/1995669.png
show_author_profile: true
---

## 安装

安装 Manjaro 就遇到了挺大的麻烦

### fcitx5

```sh
sudo pacman -S fcitx5-im fcitx5-pinyin-zhwiki fcitx5-chinese-addons
```

在 `/etc/profile` 中添加：
```sh
export XMODIFIERS=@im=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
```

> 在其它的配置文件中修改的环境变量似乎并不生效

AUR 中可以安装 `fcitx5-pinyin-moegirl`

### Wayland

#### zotero

参考 [Revisiting Wayland for ArchLinux](https://rgoswami.me/posts/revisiting-wayland-2021-archlinux/#reference-management)：

新建 `$HOME/.zotero/zotero/$PROFILE/user.js`：
```js
user_pref('layout.css.devPixelsPerPx', '2');
```

### KDE

KDE 的配置文件位于 `~/.config/plasma-org.kde.plasma.desktop-appletsrc`

推荐安装 [Plasma Customization Saver](https://store.kde.org/p/1298955/) 来备份和管理配置文件

配置文件语法如下：
```yaml
[Containments][25]
plugin=org.kde.panel # 容器 25 为面板

[Containments][25][Applets][26]
immutability=1
plugin=org.kde.plasma.kickoff # 容器 25 的挂件 应用程序启动器

[Containments][25][Applets][30]
immutability=1
plugin=org.kde.plasma.systemtray # 系统托盘

[Containments][25][Applets][30][Configuration]
PreloadWeight=55
SystrayContainmentId=31 # 系统托盘为容器 31

[Containments][25][General]
AppletOrder=26;50;51;56;48;30;42 # 容器 25 中挂件的排序
```

如果不幸写错了配置，可以如下重启：
```sh
kquitapp5 plasmashell
kstart plasmashell
```
