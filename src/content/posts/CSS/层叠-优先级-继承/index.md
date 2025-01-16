---
title: 层叠、优先级与继承与一些数值设置
published: 2025-01-16
description: CSS中层叠、优先级与继承与一些数值设置
tags: [css]
category: Web
draft: false
---



# 层叠-优先级-继承关系
## 层叠
当多个规则来自同一个源，且具有相同的元素选择器，有相同的优先级，则**顺序在最后的生效。**

## 优先级
1. 浏览器计算优先级的方法
    - style内的样式优先级最高
    - ID>类>元素(/<p>还有一些伪元素)
2.  强制应用
`!important`
```
.better {
  background-color: gray;
  border: none !important;
}
```
> !important也能被覆盖，前提是两个（1）优先级相同且位置更后（2）优先级更高


## 继承
一些设置在父元素上的 CSS 属性是可以被子元素继承的，有些则不能
1. 常见的不能被继承的属性：
width,margin,padding,border
2. 控制继承
- inherit:子元素属性与父元素属性一样
- initial:将应用于选定元素的属性值设置为该属性的初始值
- revert:
- revert-layer:
- unset:如果属性是自然继承那么就是 inherit，否则和 initial一样
3. 撤销属性all
值可以是`inherit initial unset revert`

****
# 数值设置

## em与rem
- em
  是父元素字体大小的多少
- rem
  是根元素字体大小的多少

## 百分比
**如果将元素的字体大小设置为百分比，那么它将是元素父元素字体大小的百分比**

## 指定颜色的放肆
- 颜色关键字  `antiquewhite`
- 十六进制RGB `rgb(2 121 139` ；加入不透明度数` rgb(197 93 161 / 0.7)`


## 函数
`calc(20% + 100px)`

## min- max-
- min- 
  避免溢出的同时并处理变化容量的内容
- max-
  在图像处理中，没有足够空间以原有宽度展示图像时，让图像缩小，同时确保它们不会比这一宽度大。

## 视口
相对于浏览器窗口而言
- vh
- vw
> 视口是相对于浏览器窗口
> %是相对于父元素
