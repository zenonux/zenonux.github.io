---
title: "sequlize设置timezone"
date: "2022-03-19"
categories: 
  - "back-end"
tags: 
  - "sequlize"
---

### 需求场景

使用sequlize读写mysql/mariadb数据时，默认会给每个表添加createdAt,updatedAt字段。由于一般情况下，项目timezone会使用东八区“+8:00”。如果在数据库中存储“+0:00”时区，就会经常遇到时间转换的问题。网上的答案大多数都是添加timezone字段即可。实际情况是添加timezone字段只会在存入数据库时使用“+8:00”区，而从数据库读取还是“+0:00”时区,还是需要进行时间转换的，如果一个个转就崩溃了，肯定不可取。

### 解决方案

后来终于在sequlize的issue中找到了解决方案，这个issue居然从2013年就存在了。。。至今未关闭。。。看到一些issue提到关于时区转换这块，文档还不够详细，确实啊，很容易坑人。核心代码如下

```typescript
 useFactory: (configService: ConfigService) => ({
        dialect: 'mariadb',
        //for writing to database
        timezone: '+08:00',
        dialectOptions: {
          // for reading from database
          dateStrings: true,
          typeCast: true,
        },
        ...
      })
```

相关issue：[https://github.com/sequelize/sequelize/issues/854](https://github.com/sequelize/sequelize/issues/854)
