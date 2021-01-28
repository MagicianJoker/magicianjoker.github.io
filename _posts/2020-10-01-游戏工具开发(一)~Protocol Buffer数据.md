---
title: "游戏工具开发(一)"
subtitle: "Protocal Buffer数据"
layout: post
date:   2020-10-01
author: "MagicianJoker"
header-style: text
tags:
  - 工具
  - Unity
---

Protobuf(简称PB)是Google提供的一种与平台无关、语言无关、可扩展且轻便高效的协议数据交换格式工具库(类似Json),作为一种效率(转化效率，时间效率和空间效率)和兼容性都很优秀的二进制数据传输格式，可以用于诸如网络传输、配置文件、数据存储等诸多领域。其序列化后的数据是以紧凑的二进制流形式展现的，所以几乎不可直接查看。

- 优点:

- 缺点:二进制报文，没有格式化制的可读性，要想看懂只能反序列化了，不过这点基本上不是问题~

# Unity使用Protobuf流程

游戏开发中,我们会把数据存放在.proto文件中,然后用protoc编译器把proto文件编译成我们Unity中使用的.cs文件,编译过程就是把.proto里定义的数据对象抓换成数据类,当类有了之后，我们就可以创建并给参数赋值使用了。

1. C#使用的protobuf的DLL文件
2. proto编译器

# protobuf的.dll文件

protobuf的.dll文件是实现类的对象及数据转换所需要用到的,针对Unity使用来说,ProtoBuf的版本基本可分为两个版本

1. [谷歌官方版 ](https://github.com/protocolbuffers/protobuf/tree/master/csharp)   主库名:Google.ProtoBuf.dll

   [CSharpTree](https://github.com/protocolbuffers/protobuf/releases)

   ![image-20210122154020806](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122154020.png)

     ![image-20210122182311280](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122182311.png)

   VS打开.sln,然后生成

   ![image-20210122182440871](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122182440.png)

   

   可能产生的问题:![image-20210122182523918](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122182523.png)

   打开错误提示中的global.json文件,显示版本为3.0.100

   ![image-20210122182608607](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122182608.png)

   此时我们再查看个人电脑上的dotnet版本,cmd命令: dotnet --info

   ![image-20210122183331320](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122183331.png)

   然后修改我们的global.json,将version的值修改为我们的5.0.102,继续生成

   ![image-20210122183026608](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122183026.png)

   ![image-20210122183047822](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122183047.png)

   此时把生成的文件放入到Unity工程之中,就可以愉快的玩耍了

2. [.Net社区版](https://github.com/protobuf-net/protobuf-net)    主库名:protobuf-net.dll

![image-20210122154201688](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122154201.png)

Tips:(1)由于Protobuf谷歌官方版不支持.Net3.5及以下版本，所以在无法切换.Net版本的情况下如果要在Unity3D当中使用，则需要用到第三方开源的Protobuf-net库,也就是第二个版本

(2)切换Unity的运行版本为.Net4.x

# proto编译器

编译器是用来将.proto文件编译成相应语音脚本的工具

编译器可以直接从GitHub上[下载](https://github.com/protocolbuffers/protobuf/releases),选择对应的protobuf包 （如 protoc-3.14.0-win64.zip）， 在bin文件夹下有对应得 protoc.exe 编译器

![image-20210122141551485](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122141551.png)

![image-20210122154107235](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122154107.png)

## 实现protobuf数据的转换

![image-20210122142614946](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122142614.png)

1. 手撸一把.proto文件

![image-20210122164636228](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122164636.png)

2. 将proto文件放入文件夹proto_input文件夹下 (后面涉及到导出批处理)
3. 新建批处理文件gen_csharp.bat,将proto文件转换成我们目标需要的格式(.cs)

![image-20210122143341618](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122143341.png)

4.一键执行我们编写的.bat,导出相应的.cs文件

![image-20210122143628405](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/20210122143628.png)

Tips:具体的一些proto语法可以查看[官方文档](https://developers.google.com/protocol-buffers/docs/proto3)











