---
title: "svg icon集成方案"
date: "2023-03-15"
categories: 
  - "front-end"
tags: 
  - "feature"
---

### 背景

在svg还不流行时，图标的通用方案是png sprite图片。随着浏览器对svg的支持程度，目前都在接入svg图标。

### 开源解决方案

- iconify

优点：支持按需加载，方便使用各类开源图标库。内部后台管理系最佳选择。

缺点：图标部署在iconify网站上，离线方式使用没有按需加载的优势。

[iconify/iconify: Universal icon framework. One syntax for FontAwesome, Material Design Icons, DashIcons, Feather Icons, EmojiOne, Noto Emoji and many other open source icon sets (100+ icon sets, 100,000+ icons). SVG framework, React, Vue and Svelte components! (github.com)](https://github.com/iconify/iconify)

- unplugin-icons

优点：支持按需加载，大量开源前端ui库都采用此方式。前台应用最佳选择。

缺点：不支持动态图标。有动态图标需求的谨慎考虑。

[antfu/unplugin-icons: 🤹 Access thousands of icons as components on-demand universally. (github.com)](https://github.com/antfu/unplugin-icons)

- vite-plugin-svg-icons

不推荐，基于vite2，已经不再维护，目前仍有一些后台管理系统基于此方案。

[vbenjs/vite-plugin-svg-icons: Vite Plugin for fast creating SVG sprites. (github.com)](https://github.com/vbenjs/vite-plugin-svg-icons)

### 相关参考

[CSS Sprites: What They Are, Why They're Cool, and How To Use Them | CSS-Tricks - CSS-Tricks](https://css-tricks.com/css-sprites/)
