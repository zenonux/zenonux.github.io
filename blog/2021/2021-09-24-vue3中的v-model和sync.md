---
title: "vue3中的v-model和sync"
date: "2021-09-24"
categories: 
  - "front-end"
tags: 
  - "vue"
---

### vue2中v-model

```markup
<div v-model="title"></div>
```

它实际上是下面写法的语法糖

```markup
<div :value="title" @input="title = $event"></div>
```

### vue2中sync

```markup
<div title.sync="title"></div>
```

它实际上是下面写法的语法糖

```markup
<div :value="title" @update:title="title = $event"></div>
```

可以发现其实v-model和sync都差不多，v-model中value属性和input事件是一对，sync中自定义属性title和update:title是一对。可以说sync是v-model的超集，v-model也可以算是sync表单情况的语法糖。

### vue3中v-model

在vue2中v-model和sync是类似的功能，所以作者做了优化，将两种写法合并到一起，为了降低心智吧。

```markup
<div v-model="title"></div>
```

他实际上是下面写法的语法糖

```markup
  <div :modelValue="title" @update:modelValue="title = $event"></div>
```

可以看到vue3中不再是value属性和input事件，而是 modelValue 属性和update: modelValue 事件

sync写法

```markup
<div v-model:title="title"></div>
```
