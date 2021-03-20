---
title: 强制http跳转至https
date: 2019-09-19 15:59:45
tags:
 - web
categories: tech
photos: https://tech.youzan.com/content/images/2018/03/http_to_https-1.jpg
---
一直想强制使用https协议，毕竟http不是那么的安全了。技术的跟进是必须的！
那么如何配置呢，在一番搜索之后终于找到了方法。

---

- 具体方法如下：

1. 确保你的服务器上运行的是nginx（本人用的是nginx平台，Apache平台如有需要请留言，有时间再更新），并且已经安装了证书且使用https访问正常。

2. 在nginx服务器配置里加入如下内容
```json
rewrite ^(.*)$ https://$host$1 permanent;
```

加在 listen 80 的下面，

3.保存，重启nginx服务，OK！


