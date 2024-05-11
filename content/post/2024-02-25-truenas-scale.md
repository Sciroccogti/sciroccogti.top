---
title:      并不怎么好用的 TrueNAS Scale
date:       2024-02-25T21:00:00+08:00
tags:       ["折腾"]
# image:      https://n.sinaimg.cn/sinakd20201223ac/0/w2048h1152/20201223/612c-kftfpiv4382024.jpg
show_author_profile: true
draft:  true
---

## 前言

2022年的时候给实验室搭了一台NAS，当时选了 TrueNAS SCALE 的原因是免费且基于 Debian，而且能使用 Docker，感觉会很方便维护。

当时还是第一个版本 Angelfish，虽然是初版，但是社区资料也挺多了，确实方便使用（虽然实验室除了我根本没人用，也就搭的网页可能看的人多一些）

时隔两年，到了要写毕业论文的时候（或者可能有点来不及了坦白讲），就想搭一个 overleaf 或者运行 texlive 的服务器。
折腾了一整天终于在 Docker 里的 Portainer 里用 stack 搭好了，于是想顺便更新一下系统。

Boom！TrueNAS SCALE 23.10（Cobia）完全取消了对 Docker 的支持！
