---
title: "js数组转对象reduce"
date: "2022-03-10"
categories: 
  - "front-end"
tags: 
  - "js"
---

### 需求场景

最近在写一个小程序端类似于github calendar的功能。参考了一些源码发现都是svg形式或者react的，并且第一格都代表周日，不符合中国周一是第一天的习惯。小程序没法直接用，没办法只能自己造轮子了。写的过程中有一个需要将数组转为对象，然后新的对象再和另一个数组合并的功能。其中数组转对象，我就使用了最简单的for循环。然而后面却发现使用reduce方式也可以实现数组转对象，这是什么操作，花里胡哨啊。

### Reduce实现的优点

for循环实际是命令式编程，reduce是函数式编程。函数式编程的一个优点就是看起来比较清晰，性能当然没那么好。不过这年头还是代码清晰易维护重要啊，性能等出现了再去优化也不迟。

```typescript
const dataTmp = data.reduce((target, v) => {
    let day = getDayOfYear(new Date(v.date))
    target[day] = v;
    return target;
}, {});
```

```typescript
const dataTmp={};
for(let i=0;i<data.length;i++){
    let day = getDayOfYear(new Date(data[i].date))
    dataTmp[day]=data[i]
}
```

贴一下自己实现的github calendar，后续抽空继续优化。[https://github.com/zenonux/calendar-graph](https://github.com/zenonux/calendar-graph)
