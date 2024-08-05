---
title: "ts实现valueOf"
date: "2022-08-06"
categories: 
  - "front-end"
---

### 需求场景

ts自带的操作符有keyof，typeof，可是没有valueOf

### 解决方案

```typescript
type ValueOf<T> = T[keyof T];
```
