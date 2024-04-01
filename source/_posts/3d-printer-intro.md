---
title: 极简 3D 打印机使用说明
date: 2024-03-03 15:27:05
tags: 
    - Skyw
    - 3D Printer
    - 指南
keywords: 
    - 天空工厂
    - 3D 打印
    - 指南
    - 教程
categories: 技术
---

## 序

> 中指镇楼

![mf](/imgs/3d-printer-intro/a324a813094087f4f04496bd8e75fae5.jpg)

此文简要记录 [天空工场](https://www.skyw.me/) 3D 打印机使用方法。适用于极光尔沃 Z-603S （写文章的时候在一教 304 机房）和极光尔沃 A8（在 X-Lab）。

## 正文

### 0x00 准备模型

准备你要打印的 3D 模型，一般为 `.stl` 格式。当然其他一些常见的格式也是可以的。

比如下面这玩意儿：

![stl model](/imgs/3d-printer-intro/image.png)

### 0x01 模型切片

由于这些打印机是 FDM（[Fused filament fabrication - Wikipedia](https://en.wikipedia.org/wiki/Fused_filament_fabrication)）打印机，你需要把你的模型***切片***（Slice）。

1. 首先安装 [UltiMaker Cura - UltiMaker](https://ultimaker.com/software/ultimaker-cura/)。

2. 打开 `UltiMaker Cura` 后，添加打印机 `Z-603S`（A8 也是这个）:

    ![add printer 1](/imgs/3d-printer-intro/image-2.png)
    ![add printer 2](/imgs/3d-printer-intro/image-3.png)

3. 再导入你的模型：

    ![add model](/imgs/3d-printer-intro/image-1.png)

4. 调整位置和角度。

5. 调整打印参数，一般默认即可：

    > 如果不太明白的话，最好问问群友。比如有些情况下是不用加支撑（Support）的。

    ![change parameter](/imgs/3d-printer-intro/image-4.png)

6. 点右下角 Slice，保存 `.gcode` 文件。

### 0x02 打印

1. 问群友拿一台可以用，然后访问对应的 OctoPrint 前端。

2. 检查一下那一台上一个使用者擦屁股没（如果前端的摄像头看不到请自己到现场看一下）。（如果没有，你可以~~背地里骂一下他然后~~帮他擦屁股）

3. 按下图上传 gcode 文件，选中它，然后可以开始打印。

    ![OctoPrint](/imgs/3d-printer-intro/image-5.png)

4. 打印过程经常容易出现各种问题，如 [FDM 3D 打印常见的 7 个问题解决方法](http://www.artillery3d.cn/en/industry-news/20221014-68569)。如果失败了，请分析原因，或询问群友。弄坏了也没关系，可以试着修一修。

5. 拿走你打印的物品。清理干净热床。清理干净热床。清理干净热床。

## 结束了，就这么简单...吧？

不懂的可以先问问 Google 或者群友。第一次使用 3D 打印机可以先打印一点简单的东西试一试。

强烈推荐先读一读下面打印机的文档，尤其是它坏了的时候你会需要文档的（x

{% pdf /res/603S.pdf %}

{% pdf /res/A8.pdf %}
