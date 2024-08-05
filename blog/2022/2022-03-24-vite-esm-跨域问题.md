---
title: "vite esm 跨域问题"
date: "2022-03-24"
categories: 
  - "front-end"
tags: 
  - "vite"
---

### 需求场景

因为vue3以及vite的发布，目前一些新的项目已经切换到vue3以及vite打包工具上。由于之前的项目会把打包后的静态资源上传到阿里云oss，然而使用vite打包上传后却出现了问题。竟然提示cors跨域问题，简直是不可思议！！因为这个demo项目中并没有涉及到ajax交互，而且之前也使用vite完成过一些项目，怎么就突然有问题了，是哪里的使用姿势不对？只听过ajax的跨域问题，还没听过js加载的跨域问题，嗯，现在你听说了。

### 问题原因

因为vite使用了esm模块化加载，也正是因为esm可以让js打包体积更小的优点，算是vite的一个亮点。不过esm加载其他域名下的js就是有跨域的问题的。所有跨域的 ESM 资源加载都需要在资源响应头上添加 `Access-Control-Allow-Origin` 的响应头。
