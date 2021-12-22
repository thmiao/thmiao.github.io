---
title: "关于protocol buffer命名冲突与解决"
date: 2021-11-26T10:55:54+08:00
draft: false
tags : [
    "protobuf",
    "Golang"
]
---

&emsp;&emsp;使用google.golang.org/protobuf或者github.com/golang/protobuf的时候经常能看到file "xx.proto" is already registered的Warning，甚至在一些版本下直接报Error。

&emsp;&emsp;这是因为所有链接到Go二进制文件的协议缓冲区声明都被插入到全局注册表中。每个protobuf声明(例如，enum, enum值，或者消息)都有一个绝对名称，它是包名和.proto源文件中声明的相对名称的连接(例如，my.proto.package.MyMessage.NestedMessage)。protobuf语言假设所有声明都是唯一的。如果链接到Go二进制文件中的两个protobuf声明具有相同的名称，那么这将导致名称空间冲突，注册中心不可能根据名称正确解析该声明。根据所使用的Go protobufs版本的不同，这可能会在初始时产生恐慌，也可能会悄无声息地消除冲突，并在稍后的运行时导致潜在的bug。

![](../../images/protobuf.png)

&emsp;&emsp;如果你使用的版本是报Error而带来了困扰，并且暂时不想通过更改命名的方式来解决，官方文档中提供了两种解决方案。一个是在编译时将命名冲突报错的策略调整为Warning，另一个是通过环境变量在执行时调整为Warning。

![](../../images/protobuf_git.png)

&emsp;&emsp;当然也可以使用较旧的版本，比如google.golang.org/protobuf v1.26.0之前的版本或者是github.com/golang/protobuf v1.5.0之前的版本。