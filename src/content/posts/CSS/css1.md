---
title: CSS的样式选择
published: 2025-01-11
description: 样式选择的方式
tags: [css]
category: Web
draft: false
---

- [错误处理](#错误处理)
- [选择方式](#选择方式)
- [属性选择器](#属性选择器)
- [伪类和伪元素](#伪类和伪元素)
- [关于类选择器](#关于类选择器)
- [关系选择器](#关系选择器)

## 错误处理
- 当浏览器遇到无法解析的选择器的时候，他会直接忽略整个选择器规则，然后解析下一个 CSS 选择器。
- 当选择器内发生语法错误时，会忽略错误的项目，其他的项目正常渲染
## 选择方式
1. 元素选择器 <br>
选择所有p和li 
```CSS
p,
li {
  color: green;
}
```
2. 类选择器
```
in html
<li class="special">项目二</li>
in css
.special {
  color: orange;
  font-weight: bold;
}
```
3. id选择器
```
#unique {
}
```
>  id在元素中用id标签指定
4. 元素选择器和类一起使用
```
li.special {
  color: orange;
  font-weight: bold;
}
```
5. 位置：元素的所有子元素 
<br> 可以三个及以上嵌套
```
li em {
  color: rebeccapurple;
}
```
6. 位置：出现某元素后且与之有相同层级 <br>设置的是最后一类元素的样式 
```
h1 + p {
  font-size: 200%;
}
```
> 直接出现在标题后面并且与标题具有相同层级的**段落**样式
7. 状态
```
a:link {//未访问过的
  color: pink;
}
a:visited {//访问过的
  color: green;
}
a:hover {//鼠标悬停
  text-decoration: none;
}
```
8. 标签属性选择器
    - 根据是否存在`a[title]`
    - 根据特定值是否存在`a[href="https://example.com"]`
9. 伪元素选择器
>  对p的第一行（没有这个<>元素）进行样式
```
p::first-line {
}
```
10.  运算符选择
> 选择\<article>元素的初代子元素
```
article > p {
}
```

## 属性选择器
1. 存否和值选择器
  - `li[class]`:任何带有class属性的li都会被选择
  - `li[class='a']`:匹配一个类别为a的元素
  - `li[class~='a']`:class="a"和class="a b c"会被选择。用空格分隔的会被选择
> [attr|=value]常用于语言分类，选择那些 attr 属性的值以 value 开头，并且后面紧跟一个连字符（-）的元素。（也可以完全等于value）
2. 子字符串匹配选择器
  - `li[class^="a"]`:以a开头
  - `li[class$="a"]`:以a结尾
  - `li[class*="a"]`:出现a
> 大小写不敏感：`li[class^="a" i]`

## 伪类和伪元素
1. 冒号开头的即为伪类
在artical元素中选择第一个p元素
```
article p:first-child {
  font-size: 120%;
  font-weight: bold;
}
```
其他常见
  - `:last-child`
  - `:only-child`:`div:only-child`没有兄弟的div元素
  - `:invalid`:用来选择任何未通过验证的 \<form>、\<fieldset>、\<input> 或其他表单元素。
  - `:hover`
  - `:focus`

2. 伪元素:双冒号开头的即为伪元素
选择artical中所有p元素的第一行。可以自适应屏幕宽度，不受到父元素的影响。
```
article p::first-line {
  font-size: 120%;
  font-weight: bold;
}
```
> 例`article p:first-child::first-line`对第一段的第一行进行选择

特殊的伪元素:
  - `::before`在开始渲染选定元素之前先渲染指定内容
  - `::after`
> 不会被屏幕阅读器读，起到视觉性提醒作用。content属性指定文本内容
```css
.box::before {
  content: "这应该显示在其他内容之前。";
}
```

## 关于类选择器
```html
<div class="a b c"> </div>
```
```css
.a{
}
.b{
}
.c{
}
```
> 一个元素可以有多个类

## 关系选择器
1. 后代选择器 <br>
`" "`能用于嵌套
2. 子代关系选择器 <br>
`>`不能用于嵌套
`A > B`选择A中直接子元素B
3. 邻接兄弟 <br>
`+`同级关系
`p + img`选中所有紧随\<p>元素之后的\<img>元素
4. 通用兄弟 <br>
`p ~ img`选中所有的\<p>元素后任何同级地方的\<img>元素
