---
title: "element ui省市区地区选择器"
date: "2021-10-05"
categories: 
  - "front-end"
tags: 
  - "ts"
---

### 需求场景

element ui一直没有开箱即用省市区地区选择器，可能是考虑国际化的原因。想要实现，可以基于cascader组件。那么问题来了，哪里有稳定持续维护的省市区数据源？看到不少文章使用的是\`element-china-area-data\`npm 包，看了下数据源已经很久没更新了，此外这个包的省市区还加上了市辖区三个字，感觉没啥意义。

### 解决方案

由于移动端经常使用vant组件库，里面的Area组件刚好提供了数据源npm包[https://www.npmjs.com/package/@vant/area-data](https://www.npmjs.com/package/@vant/area-data),为了保持移动端和桌面端省市区数据的一致性，于是发布了一个基于此数据源生成的符合element ui cascader组件格式的npm包[https://www.npmjs.com/package/@urcloud/area-data](https://www.npmjs.com/package/@urcloud/area-data)。

### 实现功能

- 将vant area的数据格式转为Element UI的数据格式
- 省市区地区选择器支持全部选项
- 支持Element UI和Element Plus

### 数据格式

```javascript
[
 {
    label:'北京市',
    value:'110000',
    children:[
      {
        label:'北京市',
        value:'110100',
        children:[
          {
            lable:'东城区',
            value:'110101'
          },
          ...
        ]
      },
      ...
    ]
  },
  ...
]
```

### 使用方式

```markup
<template>
    <div class="demo-title demo-1">vant数据源：</div>
   <el-cascader
      v-model="value1"
      :options="options1"
    ></el-cascader>
     <div class="demo-title demo-2">vant数据源：加全部</div>
   <el-cascader
      v-model="value2"
      :options="options2"
    ></el-cascader>
</template>
<script>
import {defineComponent} from 'vue';
import  {getAreaTree} from '@urcloud/china-area-data';
export default defineComponent({
    setup(){
      return {
        value1:'',
        options1:getAreaTree(),
        value2:'',
        options2:getAreaTree(true),
      }
    }
})
</script>
```
