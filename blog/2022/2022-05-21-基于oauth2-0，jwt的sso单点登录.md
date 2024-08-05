---
title: "基于Oauth2.0，JWT的SSO单点登录"
date: "2022-05-21"
categories: 
  - "back-end"
tags: 
  - "jwt"
  - "oauth"
  - "sso"
---

### 需求场景

当公司网站越来越多时，还是希望账号能打通，登录公司a网站后，打开b网站需要登录时可以不用输密码直接登录，主要是方便用户登录，简化流程，不用记那么多的密码。单点登录可以说是这一痛点的解决方案了。

### 常用解决方案

#### 方案一：基于cas认证的单点登录

如果公司使用java技术栈，接入开源的cas是很不错的。

[apereo/cas: Apereo CAS - Identity & Single Sign On for all earthlings and beyond. (github.com)](https://github.com/apereo/cas)

#### 方案二： 基于oauth2.0授权的单点登录

研究下来，发现oauth2.0授权和cas认证的核心流程思想基本一样。没啥太明显的区别。cas是个开源的框架，直接接入，开箱即用，省心。而oauth2.0只是个授权协议规范而已，具体怎么实现要自己去写，目前网上也没有什么比较好的类似于cas这种可以开箱即用，稳定维护的项目。所以与其接入一个不怎么靠谱的开源项目，不如搞懂流程，方便后续的踩坑。

1. 用户访问a网站需要登录，a网站后台跳转sso认证中心，
2. sso认证中心根据cookie判断用户未登录，弹出登录页面
3. 用户填完密码，sso校验后生成一次性鉴权码code，设置cookie，session 并携带code重定向至a网站前端页面
4. 前端页面获取url参数中的code，向a网站后台发送ajax请求
5. 后台接收到code请求sso认证中心
6. sso认证中心返回access\_token
7. 后台获取accessToken并保存，返回前端自己的鉴权accessToken
8. 前端获取a网站的accessToken，登录成功
9. 用户访问b网站要登录，b网站后台跳转sso认证中心
10. 由于访问a网站时，sso留下了cookie，现在sso根据cookie和session知道用户已经登录过，不再弹出登录框，直接返回code
11. 后续流程保持不变

#### 方案三：基于第三方收费的sso服务

### 相关开源项目

1. [apereo/cas: Apereo CAS - Identity & Single Sign On for all earthlings and beyond. (github.com)](https://github.com/apereo/cas)
2. [authelia/authelia: The Single Sign-On Multi-Factor portal for web apps (github.com)](https://github.com/authelia/authelia)
