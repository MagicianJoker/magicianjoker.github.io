---
title: "游戏热更新方案(二)"
subtitle: "Xlua+InjectFix"
layout: post
date:   2021-03-01
author: "MagicianJoker"
header-style: text
tags:
  - 热更新
  - Unity
---

 xlua是AddLoader



## Xlua原理

### 业务场景

- C#对Lua方法的调用
- Lua对C#方法的调用
- Lua持有一个C#对象
- C#持有一个Lua对象

转换为最终的需求:

1. 传递一个C#对象给Lua
2. 传递一个Lua对象给C#

### C#对象传递到Lua



