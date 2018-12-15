---
title: "Google Perftools"
date: 2018-11-07T10:31:02+08:00
draft: true
---

`gperftools` 可以用来对CPU上的性能和 heap 做分析，下面记录一些实际的用法。



# 使用方法

# 分析内存

## 内存泄漏

添加 HEAPCHECK=normal

## 内存持续增长

链接 `-ltcmalloc`

使用 `pprof` 画图

https://github.com/google/pprof



## 案例分析：stl container 的持续增长

# 性能分析