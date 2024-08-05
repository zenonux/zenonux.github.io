---
title: "ts中enum的使用方式"
date: "2021-09-26"
categories:
  - "front-end"
tags:
  - "ts"
---

### 需求场景

枚举的作用类似于常量，多数情况下优先使用枚举而不是常量。

### 简单场景

```typescript
enum Platform {
  "andorid" = 1,
  "ios" = 2,
}
```

简单场景下，推荐使用 const，因为 enum 会成对象，const 只生成常量，占用的开销少，缺点是不能遍历 enum

```typescript
const enum Platform {
  "andorid" = 1,
  "ios" = 2,
}
```

### 复杂场景（结合 namespace）

在使用枚举时，往往会需要一个辅助函数去展示属性的值，这个时候可以配合 namespace

```typescript
enum Platform {
  "andorid" = 1,
  "ios" = 2,
}
namespace Platform {
  export function getText(value: number) {
    if (value === 1) {
      return "ANDORID_PLATFORM";
    }
    if (value === 2) {
      return "IOS_PLATFORM";
    }
  }
}
```

这样写的一个好处就是枚举合辅助方法能保持在同一命名空间下，维护方便。缺点就是如果需要遍历枚举的属性，就会多出命名空间中方法属性。

### 2023-03-16 更新

由于 ts 目前提供的 enum 功能简单，最终也是编译成对象。使用上只是语义上更清晰了而已，但是复杂场景需要方法支持的时候并不好用。所以我的实际项目上使用 buildEnum 辅助函数生成 enum 对象（普通 Object 对象），配合 ts 的推导，可以自动提示 enum 对象的所有属性和方法。

```typescript
export const ReportStatus = buildEnum(
  {
    ToHandle: 0,
    Handled: 1,
  },
  [
    {
      symbol: "ToHandle",
      label: "待处理",
    },
    {
      symbol: "Handled",
      label: "已处理",
    },
  ]
);

export function buildEnum<T extends Record<string, string | number>>(
  obj: T,
  labelArr: {
    symbol: string;
    label: string;
  }[]
) {
  return Object.assign(obj, {
    Options: labelArr.map((v) => {
      return {
        label: v.label,
        value: obj[v.symbol],
      };
    }),
    getLabel(value: string | number) {
      const macthed = labelArr.filter((v) => obj[v.symbol] == value)[0];
      return macthed?.label ?? "";
    },
  });
}
```
