---
title: "清除input type=\"number\"默认箭头"
date: "2021-09-23"
categories: 
  - "front-end"
tags: 
  - "css"
---

### 需求场景

在移动端，部分手机的input当type为number时会出现上下箭头。

### 解决方案

```bash
input[type='number'] {
  -moz-appearance: textfield;
}
input[type='number']::-webkit-inner-spin-button,
input[type='number']::-webkit-outer-spin-button {
  -webkit-appearance: none;
}
```
