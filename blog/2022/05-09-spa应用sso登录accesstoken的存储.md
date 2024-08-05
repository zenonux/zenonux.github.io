---
title: "SPA应用Oauth2.0登录accessToken的获取"
date: "2022-05-09"
categories: 
  - "front-end"
tags: 
  - "sso"
---

### 需求场景

之前在做微信公众号开发时，一直是前端需要登录时，跳转后台提供的登录页面，后台会重定向至微信的用户授权页面，用户点击登录之后微信会回调到后台的登录结果页并且携带code，后台结果页拿到code，调用微信的接口获取accessToken，然后将accessToken通过重定向url参数的方式返回到SPA。这样虽然前端部分简化了登录流程，但是也带来一个安全隐患。accessToken是通过url参数重定向到前端的，如果用户直接分享这个带accessToken的页面，就会出现accessToken泄露的问题，未登录的用户打开会变成已经登录的状态。之前为了解决这个隐患，都是前端在获取accessToken的同时，在url中删除accessToken参数并刷新页面。虽然能解决问题，但是不是很优雅，总觉得这样不好，更希望accessToken是通过cookie httpOnly方式获取，这样在url上就不会体现，安全上要好很多。也不需要做url参数隐藏的处理。

### 常规方案

更通用的方案是前端去重定向至微信用户授权页面，用户授权后再重定向至前端页面并且携带code，前端再通过ajax请求后台获取到accessToken。这样的话，accessToken就不会暴露在url上面。不过依旧有一个问题，就是code也是通过url参数传递到前端的，那还是绕不过一个问题，用户直接将带code的页面分享出去。搜了半天也没看到有人有类似的疑问。我的考虑是获取code的页面往往是一个专门用来处理登录问题的路径如/login?code=这个页面只会短暂停留，ajax获取到accessToken后就会跳走，用户不会或者来不及分享这个页面。此外最重要的这个code是只能使用一次的，登录了就不能使用了。accessToken不一定都会这么做。

### 2022-5-9更新

常规方案和我之前使用的方案其实核心就一点不同，前端是直接获取accessToken还是先获取code，再通过code获取accessToken。这就要回到oauth2.0设计的初衷了，他为什么需要一个中间的code，而不直接返回accessToken呢？我之前的做法其实就相当于丢弃了oauth2.0的code，直接获取accessToken。后来才发现原来我所考虑的弊端就是oauth2.0设计code的原因啊，就是比直接获取accessToken安全了一丢丢。之前看Oauth2.0的介绍时也只是知道流程，确实没考虑过人家为什么要多此一举，设计一个中间code。至于为什么没有人和我有一样的安全疑问，估计一种是和我一样知道怎么用不知道为什么这么设计的，我也不关心你们为啥这么设计，反正我按你的规范来了，一种是真的理解了oauth2.0规范也就没啥疑问了。

### 相关参考

[https://jcbaey.com/oauth2-oidc-best-practices-in-spa/](https://jcbaey.com/oauth2-oidc-best-practices-in-spa/)
