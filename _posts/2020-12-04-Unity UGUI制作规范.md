---
title: "Unity UGUI制作规范"
subtitle: "「记录」积累"
layout: post
author: "MagicianJoker"
header-style: text
tags:
  - Unity
---

# UGUI 制作规范

## Canvas基本结构

1.开发时的选定标准，根据开发立项确定的开发适配设置，Game视图设置

![image-20201204192838980](https://raw.githubusercontent.com/MagicianJoker/magicianjoker.github.io/main/imageBed/202012/04/192839-258651.png)

2.Canvas的RenderMode一般选取ScreeSpace模式的Camera,此处可填可不填，代码做统一处理

CanvasScaler 设计后面的适配工作，UIScaleMode选择Scale with Screen Size

Reference Resolution 就是默认的填写开发的标准

Match项在Width和Height之间寻求平衡，一般竖屏是偏Width横屏片偏Height（待验证）

![image-20201209153057351](https://raw.githubusercontent.com/MagicianJoker/magicianjoker.github.io/main/imageBed/202012/09/153113-308639.png)



---

## Canvas问题

- Canvas下UI元素改变(位置,颜色,大小)再或者增减,会导致整个Canvas下所有元素的Rebuild,尽可能频繁变化的UI元素从复杂的Canvas分离出来，使动态UI元素的变化引起的网格更新或重建涉及范围变小,减轻Canvas更新和重建带来的性能消耗.

  1.Canvas作为根节点,之后用Panel作为某一个界面的父节点,打开界面时放入Canvas下

  2.空UIRoot作为所有UI的根节点,每一个功能界面都以独立的Canvas作为容器

  

  讨论点:(1) 整个游戏只有一个Canvas,会带来无谓的性能消耗

  (2) Canvas多了会有额外的性能消耗,DrawCall问题

  

  归论:每个功能肯定要有一个独立的Canvas,对于界面复杂的功能,酌情拆分出子Canvas(原则是以动静分离为主),UGUI中Canvas少DrawCall不一定会少,不必特在意此处,界面臃肿的时候重建的消耗是远高于多出来的几个DrawCall的

  Tips:Profile里Canvas.BuildBatch查看Canvas重建的消耗

  ---

  

  ​		