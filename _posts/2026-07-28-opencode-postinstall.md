---
layout: post
title: 修复 cd $(npm root -g)/opencode-ai && node postinstall.mjs 报错
date: 2026-07-28 10:10:00 +0800
categories: [Notes]
tags: [opencode, npm, error]
---

修复 `cd $(npm root -g)/opencode-ai && node postinstall.mjs` 报错

### 1. `npm rebuild failed`

postinstall 脚本内部会执行 `npm rebuild opencode-ai --ignore-scripts`，失败原因通常是权限问题。

```bash
npm rebuild opencode-ai --ignore-scripts -g
```

### 2. `EACCES: permission denied`

全局 node_modules 被 root 占用，或 `~/.cache` 目录权限不对。

```bash
sudo chown -R $(whoami) ~/.cache
# 或者重定向 XDG_CACHE_HOME
export XDG_CACHE_HOME=$HOME/.cache
```

### 3. 找不到 `opencode` 命令

postinstall 没成功创建 bin 链接，需要手动安装平台包。

```bash
npm install -g opencode-darwin-arm64   # M1/M2 Mac
npm install -g opencode-darwin-x64     # Intel Mac
npm install -g opencode-linux-x64      # Linux

ln -sf "$(npm root -g)/opencode-darwin-arm64/bin/opencode" /usr/local/bin/opencode
```

### 4. 跳过 postinstall 重新安装

```bash
npm install -g opencode-ai --ignore-scripts
cd $(npm root -g)/opencode-ai && node postinstall.mjs
```

一句话总结：`postinstall.mjs` 本质是帮你在全局装二进制文件，大部分报错都源于权限不足或平台包未安装，手动安装对应平台包即可绕过。
