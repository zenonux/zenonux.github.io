---
title: "z-index不生效？"
date: "2022-02-08"
categories:
  - "front-end"
tags:
  - "css"
---

### 需求场景

考虑以下场景，A 元素包含 B，C 元素，B 元素包含 B1 元素，C 元素包含 C1 元素。为什么 C1 元素的 z-index 明明很高，却始终在 B1 元素下面？

```markup
  <div id="A" style="position: relative;">
        <div id="B">
            <div id="B1" style="position: absolute;z-index:1000;">B1</div>
        </div>
        <div id="C" style="position: relative;z-index: 0;">
            <div id="C1" style="position: absolute;z-index:9000;">C1</div>
        </div>
    </div>
```

然后我把代码稍作改动，为什么 C1 又在 B1 上面了呢？

```markup
   <div id="A" style="position: relative;">
        <div id="B">
            <div id="B1" style="position: absolute;z-index:1000;">B1</div>
        </div>
        <div id="C" style="position: relative;z-index:auto;">
            <div id="C1" style="position: absolute;z-index:9000;">C1</div>
        </div>
   </div>
```

### 解决方案

z-index 的使用涉及到一个层叠上下文的概念。首先只有 position 元素的值为非 static 时，z-index 才会生效，才是有意义的。每一个值为非 static 的 position 元素都会创建一个层叠上下文环境。在我们的示例中就是 A 层叠环境里包含 B1 层叠环境和 C 层叠环境，C 层叠环境包含 C1 层叠环境。这里就可以发现 A 到 C1 有 2 层而 A 到 B1 只有 1 层，所以 C1 的 z-index 无论多大都不会盖住 B1。

那么问题来了，为什么第二种情况把 z-index=0 改成 auto 就变了呢？因为 auto 不会创建层叠上下文环境！！！是个特殊值

### 进阶思考

其实能创建层叠上下文的不止 z-index，还有 transform 等

详细参考:[https://zhuanlan.zhihu.com/p/340371083](https://zhuanlan.zhihu.com/p/340371083)
