---
title: "解决MongoDB Compass报Current topology does not support sessions"
date: 2021-12-07T17:50:07+08:00
draft: false
tags : [
    "node.js",
    "MongoDB"
]
---

​		用MongoDB Compass的时候下意识点了更新从1.8.4更新到了1.9.5，然后就没法访问文档了，报`Current topology does not support sessions`的错误。各种地方寻找解决方案没有找到解决，但猜测是Server使用的MongoDB版本是3.4.24低于支持transactions的4.0版本导致的兼容问题。因为没法对使用的MongoDB进行升级，暂时采取了对MongoDB Compass版本进行回退，回退后可正常使用。

