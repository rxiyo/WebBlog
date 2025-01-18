---
title: 溢出、图像、媒体和表单元素
published: 2025-01-18
description: css中溢出控制
tags: [css]
category: Web
draft: false
---
**css不会主动隐藏溢出的东西**

##  overflow属性
- 使用:
  ```
  .box{
    oveflow:一些可选值
  }
  ```
- 一些可选值
  + `hidden`
  + `scroll`:两个方向上都会有滚动条
  + `overflow-y:scroll`仅y轴方向上有滚动条
  + `auto`:浏览器依据内容决定是否有滚动条


## 图像
1. 使用`max-width:100%`
   为`<img>`标签添加样式
2. `object-fit`
```
img {
    width:100%;
    height:100%;
    object-fit:cover;//会按原有比例缩放图像，会充满盒子但是可能图像会被裁切
    objet-fit:contain;//会按原有比例缩放图像，会充满盒子且图像不会被裁切，但是会有空白
    object-fit:fill;//可能不按照比例进行缩放，会不裁切的充满整个盒子
}
```
>   flex 或者 grid 布局中，默认情况下元素会被拉伸到充满整块区域。但是图像不会被拉伸，而会对齐到网格区域或者弹性容器的起始处。可以对高度和宽度设置为100%进行拉伸