---
title: 单节点和分布式登录会话问题
date: 2019-09-15 23:08:21
tags:
 - tomcat
 - web
 - distributed
categories: Java
photos: https://insready.com/sites/default/files/SSO%20diagram.png
---
## 服务端登录验证问题简解

1. 单服务器 Tomcat

   - session保存浏览器和服务器的会话信息
   - 用户登录后，生成一个session，会分配一个SESSIONID
   - 客户端会把session保存到cookie中，每次发送请求是会携带sessionI让服务端去校验

2. 分布式session共享

   - Tomcat支持session共享，但会有广播风暴

   - 使用redis存储token

     服务端通过UUID，生成64或128位token，存入redis，然后返回给客户端

     客户端之后的每次请求都会携带token