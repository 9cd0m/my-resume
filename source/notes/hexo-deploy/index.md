---
title: 用 GitHub Actions 部署 Hexo 踩过的 5 个坑
layout: page
date: 2026-01-20 21:00:00
---

这个站点从"本地能跑"到"线上能看"，中间折腾了五个回合。记下来，免得下次再踩。

### 坑 1：主题目录没被提交

`git clone` 下来的主题自带 `.git`，外层项目 `git add .` 时它被当成 submodule，仓库里只有一个指针。
结果：本地正常，线上构建出来没有主题。

**修法**：克隆后删掉 `themes/<主题>/.git`，让主题变成普通文件。

### 坑 2：Pages 的 Source 选成了分支

用官方的 artifact 部署流（`upload-pages-artifact` + `deploy-pages`）时，Pages 的 Source 必须是 **GitHub Actions**。
选成 "Deploy from a branch" 会在 `configure-pages` 这一步报 `Get Pages site failed`。

### 坑 3：`npm ci` 找不到锁文件

`package-lock.json` 被写进了 `.gitignore`，CI 里 `npm ci` 直接失败。
锁文件必须提交——它是 CI 能复现你本地环境的唯一依据。

### 坑 4：Windows 不区分大小写，Linux 区分

本地引用 `Style.css` 能跑，Ubuntu runner 上 404。
所有文件引用的大小写必须和磁盘上完全一致。

### 坑 5：主题改了没生效

`hexo generate` 有缓存，改 `.pug` 之后不 `hexo clean` 会看到旧页面。
改主题模板后固定流程：`hexo clean` → `hexo server`。
