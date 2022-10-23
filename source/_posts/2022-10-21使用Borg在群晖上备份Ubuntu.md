---
title:      使用Borg在群晖上备份Ubuntu
date:       2022-10-21T12:00:00+08:00
tags:       ["折腾"]
# cover:      https://simplecore.intel.com/newsroom/wp-content/uploads/sites/11/2020/12/oneapi-2x1-1.jpg
show_author_profile: true
---

群晖自带的 Active Backup for Business 暂不支持 Linux Kernel > 5.10，因此只能找第三方软件备份。

> 如果不幸已经安装了 ABfB 并且安装失败，可以看下载的压缩包里的 README 里的卸载方案。

[vorta](https://vorta.borgbase.com/) 是 [Borg](https://borgbackup.readthedocs.io/en/stable/) 的客户端可视化管理软件，
而 Borg 在群晖上有 SynoCommunity 提供的套件（其实也就是自动帮你用 pip 装 Borg 罢了），
因此选择了这个方案。

## 安装

客户端安装：
```bash
sudo apt install vorta
```

然后需要设置 ssh 密钥登录，可以看这篇 [群晖 Nas 使用 SSH Key 实现免密登录](https://dryyun.com/2019/01/08/synology-nas-login-with-ssh-key/)。
其中重启 sshd 环节只要在网页控制台重开 ssh 就行了，不用 `synoservicectl`。

另外，`authorized_keys` 里要写：
```
command="/usr/local/bin/borg serve --restrict-to-path /path/to/repo", ssh-ed25519 AAAA[...]
```
这样 vorta 登录进群晖的时候就可以自动调用 `borg serve`

> 群晖的 home 目录位于 `/volume1/home` 而非 `/home`

