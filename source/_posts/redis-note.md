---
title: Redis 速成笔记
date: 2019-09-15 23:07:19
tags:
 - redis
 - Redis
categories: tech
photos: https://pic4.zhimg.com/v2-28fd545558f10779dc90d15d80f117b8_720w.jpg
---
# Redis下载和安装

## Redis简介

> Redis 是完全开源免费的，使用ANSI C语言编写，支持网络，遵守BSD协议，是一个高性能的key-value数据库。

## 下载安装

- [Windows (非官方)](https://github.com/microsoftarchive/redis/releases)

- [Unix](https://redis.io/download)

安装

- Linux

  > make	//简单编译
  >
  > make MALLOC=libc	//编译添加malloc加速引擎
  >
  > 二进制可执行文件在./src目录下

## 启动




## 常用命令

### 5种常见数据类型

- String （字符串）
- Hash （哈希）
- List （列表）
- Set （集合）
- zset （sorted set ：有序集合）

#### String 字符串

```sh
set {key} {value}    // 设置 key=value
get {key}    // 获取key对应的值
append {key} {value}    // 追加值到一个键
incr {key}    // 增加key的值加一次
rename {key} {newkeyname}    // 重命名key的值
```

#### Hash 哈希

```sh
hset {key} {field} {value}   // 设置 {key}的{field}属性的值为{value}
hget {key} {field}    // 获取{key}的{field}属性的值
hgetall person    // 获取{key}的所有属性的值
```

#### List 列表

```sh
lpush list1 aa1     // 从右边加
lpush list1 aa1
rpush list1 word	// 从左边加

lrange {key} {start_index} {stop_index}
lrange list1 0 2    // 将list1中的值取出，取出范围0~2
```

#### Set 集合

```sh
sadd {key} {member}    // 添加member到key的集合中
smembers {key}     // 查看名为key的集合成员
sismember {key} {member1} // 确定member1是否在key中存在
```

#### zset(Sorted Set) 有序集合

```sh
zadd {key} {score} {member}
```

例：

```sh
zadd vicker 0 redis
zadd vicker 0 mongodb
zadd vicker 0 
```
