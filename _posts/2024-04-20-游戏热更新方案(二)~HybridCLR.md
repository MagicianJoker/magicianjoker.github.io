---
title: "游戏热更新方案(二)"
subtitle: "HybirdCLR"
layout: post
date:   2024-04-20
author: "MagicianJoker"
header-style: text
tags:
  - 热更新
  - Unity
---

HybridCLR扩充了il2cpp运行时代码，使它由纯[AOT](https://en.wikipedia.org/wiki/Ahead-of-time_compilation) runtime变成AOT+Interpreter 混合runtime，进而原生支持动态加载assembly，从底层彻底支持了热更新。使用HybridCLR技术的游戏不仅能在Android平台，也能在IOS、Consoles、WebGL等所有il2cpp支持的平台上高效运行。



HybridCLR从mono的 [mixed mode execution](https://www.mono-project.com/news/2017/11/13/mono-interpreter/) 技术中得到启发，为unity的il2cpp之类的AOT runtime额外提供了interpreter模块，将它们由纯AOT运行时改造为"AOT + Interpreter"混合运行方式。

![icon](https://magicianhoker.oss-cn-beijing.aliyuncs.com/ImgBed/202507112122778.png)

更具体地说，HybridCLR做了以下几点工作：

- 实现了一个高效的元数据(dll)解析库
- 改造了元数据管理模块，实现了元数据的动态注册
- 实现了一个IL指令集到自定义的寄存器指令集的compiler
- 实现了一个高效的寄存器解释器
- 额外提供大量的instinct函数，提升解释器性能
