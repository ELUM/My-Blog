---
title: 学习 Nodejs
published: 2024-07-09
image: ""
tags: [Nodejs]
category: "前端"
draft: false
---

前端开发中经常要用到 nodejs，或者说它是必备的环境了。所以重新系统的学习它，以便于使用。

## nodejs 底层原理

主要由 V8,Libuv 和第三方库组成

1. Libuv: 跨平台的异步 IO 库
2. 第三库: 异步 DNS 解析,HTTP 解析器(cares),HTTP2 解析器(old:http_parser,new:llhttp),解压压缩库(zlib),加密解密库(openssl)
3. V8: 实现 JS 解析,执行和支持自定义扩展,得益于 V8 支持自定义扩展,才有了 Node.js

你也可以理解成 js 应用层 桥 C/C++ 底层 C/C++
