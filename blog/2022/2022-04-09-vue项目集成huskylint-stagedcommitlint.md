---
title: "vue项目集成husky,lint-staged,commitlint"
date: "2022-04-09"
categories: 
  - "front-end"
tags: 
  - "long-term"
---

### 需求场景

Git在多人合作时，应该尽量保持代码格式规范，以及commit信息清晰。这一点可以通过git的钩子实现。

### 解决方案

#### 步骤一：安装husky添加pre-commit，commit-msg钩子

文档地址：[https://typicode.github.io/husky/#/?id=automatic-recommended](https://typicode.github.io/husky/#/?id=automatic-recommended)

hooks不生效原因: [https://typicode.github.io/husky/#/?id=hooks-not-running](https://typicode.github.io/husky/#/?id=hooks-not-running)

```bash
//安装husky,会在根目录生成.husky目录,以及pre-commit钩子
npx husky-init
npm install
//添加commit-msg钩子,unix环境
npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
//添加commit-msg钩子,windows环境下  
//node_modules/.bin/husky  add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
```

#### 步骤二：安装commitlint并配置规则

文档地址：[https://commitlint.js.org/#/guides-local-setup?id=install-commitlint](https://commitlint.js.org/#/guides-local-setup?id=install-commitlint)

config-conventional默认配置:[https://github.com/conventional-changelog/commitlint/blob/master/@commitlint/config-conventional/index.js](https://github.com/conventional-changelog/commitlint/blob/master/@commitlint/config-conventional/index.js)

```bash
npm i @commitlint/cli @commitlint/config-conventional -D
```

新建`.commitlintrc.js`文件配填写以下配置

```json
module.exports = {
  /* type(scope?): subject  例子：feat(server): test */
  // 使用预设的配置 https://github.com/conventional-changelog/commitlint/blob/master/@commitlint/config-conventional/index.js
  extends: ["@commitlint/config-conventional"],
  rules: {
    "type-enum": [
      2,
      "always",
      ["feat", "fix", "docs", "style", "refactor", "chore", "revert"],
    ], // 改变预设中的提交类型
    "type-case": [2, "always", "lower-case"], // 提交类型必须使用小写
    "type-empty": [2, "never"], // type不能为空
    // 'header-max-length': [2, 'always', 5], // header内容的最大长度为5
    // 'subject-min-length': [2, 'always', 1], // subject内容的最小长度为1
    // 'body-max-length': [2, 'always', 10], // body内容的最大长度为10
    // 'footer-max-length': [2, 'always', 5], // footer内容的最大长度为5
  },
};
```

确保husky的commit-msg钩子内容如下

```bash
#!/bin/sh
. "$(dirname -- "$0")/_/husky.sh"

npx --no-install commitlint --edit $1
```

#### 步骤三：安装lint-staged并配置规则

文档地址：[https://github.com/okonet/lint-staged#readme](https://github.com/okonet/lint-staged#readme)

```bash
npm i lint-staged -D
```

在package.json中填写以下配置

```json
{
"lint-staged": {
    "src/**/*.{js,json,vue,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  }
}
```

确保husky的pre-commit钩子内容如下

```bash
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx --no-install lint-staged
```
