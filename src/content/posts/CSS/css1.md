---
title: CSS的样式选择
published: 2025-01-11
description: 样式选择的方式
tags: [css]
category: Web
draft: false
---
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
3. 元素选择器和类一起使用
```
li.special {
  color: orange;
  font-weight: bold;
}
```
4. 位置：元素的所有子元素 
<br> 可以三个及以上嵌套
```
li em {
  color: rebeccapurple;
}
```
5. 位置：出现某元素后且与之有相同层级 <br>设置的是最后一类元素的样式 
```
h1 + p {
  font-size: 200%;
}
```
> 直接出现在标题后面并且与标题具有相同层级的**段落**样式
6. 状态
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
