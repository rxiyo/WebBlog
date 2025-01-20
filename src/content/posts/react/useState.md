---
title: React中useState
published: 2025-01-20
description: react中useState的问题
tags: [react]
category: Web
draft: false
---

## state是一个快照
### 问题描述
`t`和`tq`均是两个state。tq会随着输入及时变化。在按钮的onClick函数如下。需要注意的是，**`setQ()`**会异步的更新值。因此打印输出的依然是旧值，而不是新的值。在一些换页操作中，可以通过简单的加减操作来实现同步。但是在以下情况中需要使用其他方法。
```javascript
 const fetchData = () => {
    setQ(tq);
    console.log(q);
    console.log("use fetchData");
    setLoading(true);
    axios
      .get(base_api + q)
      ......
  };
```
### 解决
```javascript
// 假设你有一个方法来更新q的值
const updateQ = (newQ) => {
setQ(newQ);
};

useEffect(() => {
if (q) { // 确保q不为空时才发起请求
    setLoading(true);
    axios
    ......
}
}, [q]); // 监听q的变化
```
> 感觉上甚至有点像将`setQ`和请求的函数放在了不同的作用域。因此请求时的用到的值是更新之后的q值。