---
layout: post
title: 天翼网关3.0超级密码
date: 2026-07-18 12:11:00 +0800
categories: [Notes]
tags: [天翼网关]
---

### 如何获取天翼网关3.0超级密码

[Bilibili视频](https://www.bilibili.com/video/BV1E3411L7qr/)

[网盘链接](https://cloud.189.cn/t/aU3Efa7rqiAj)
访问码: `**peu6**`

进入光猫管理界面，插入U盘（可能需要格式化为FAT32才能使用）
点击存储管理，进入U盘界面，右键`嵌套框`进入审核元素（F12,要选择控制台的`内置存储嵌套框`）

```javascript
openfile("../../../userconfig/cfg", false)
```

复制`db_user_cfg.xml`到U盘
执行命令（Powershell）

```powershell
.\ztecfg.exe -d AESCBC -i .\db_user_cfg.xml -o jiemi.cfg
```

在`jiemi.cfg`里搜索`telecomadmin`，下面的pass就是密码
