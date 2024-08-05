---
title: "vue部署到阿里云oss"
date: "2021-08-31"
categories: 
  - "front-end"
tags: 
  - "oss"
  - "vue"
---

### 环境条件

基于vue-cli创建的项目

### 需求场景

vue-cli构建的项目在build之后会生成dist目录，我们需要把dist目录里面的index.html上传至服务器，css，js，img等其他文件上传至oss。

### 步骤一：修改vue.config.js中的publicPath

```javascript
const ossUrlPrefix='test.oss-cn-shanghai.aliyuncs.com';
module.exports = {
  publicPath:process.env.NODE_ENV == "development" ? '/' : ossUrlPrefix,
 }
```

### 步骤二：新建.deploy.config.js,修改package.json

```javascript
module.exports = {
  distPath: './dist',
  jsonPath: './deploy.version.json',
  maxVersionCountOfMode: 5,
  oss: {
    accessKeyId: '',
    accessKeySecret: '',
    region: 'oss-cn-shanghai',
    bucket: 'test',
    prefix: (mode, version) => {
      return mode + '@' + version
    },
  },
  stag: {
    host: '',
    username: '',
    password: '',
    serverPath: '',
  },
  prod: {
    host: '',
    username: '',
    password: '',
    serverPath: '',
  },
}
```

```json
{
  "scripts": {
    "deploy:stag": "oss-deploy upload stag",
    "clear:stag": "oss-deploy clear stag",
    "deploy:prod": "oss-deploy upload prod",
    "clear:prod": "oss-deploy clear prod"
  }
}
```

### 步骤三：build & deploy

```bash
npm run build:prod
npm run deploy:prod
```

### 详细文档

[https://www.npmjs.com/package/@urcloud/oss-deploy](https://www.npmjs.com/package/@urcloud/oss-deploy)
