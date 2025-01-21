---
title: React中useState
published: 2025-01-20
description: react中useState的问题
tags: [react]
category: Web
draft: false
---

## 渲染和提交
- 触发
  + 应用启动时候初次渲染
  + 运行时组件（或其祖先之一）状态发生了改变。`set`函数即能够改变状态
- 渲染
  渲染过程中会递归渲染。递归渲染`return`中的组件
  + 初次渲染时，从根组件开始递归渲染
  + 运行时渲染，从状态发生改变的组件递归渲染
  > 可以看作是生成一个虚拟DOM的过程
- 提交：将渲染的更改提交到DOM
  + 初次渲染：将创建的所有DOM节点放在屏幕
  + 运行时渲染：react计算用最少的操作更新DOM使之与最新的渲染输出匹配
  > 更新DOM的方式并不是JSX中的组件（一个return对应的function为组件）为单位。**React 仅在渲染之间存在差异时才会更改不同的DOM节点**
### 一个问题？
[text](https://react.docschina.org/learn/render-and-commit#step-3-react-commits-changes-to-the-dom)
input组件的分类
- 受控的
  value属性如果由state或者props控制，那么会更新
- 非受控的


## state是一个快照
- 设置 state 不会立刻更改现有渲染中的变量，但会请求一次新的渲染。在事件处理函数执行完成后，便开始执行新的渲染。
### 事件处理函数中的setState函数执行
**会等到所有代其他码执行完毕后再执行state更新**。这意味着两件事：
- 即使在setState之后的代码，用到的也不是新值，而是旧值。
  ```
  onClick={()=>{
    A;
    setState();
    B;
  }
  ```
  实际上执行的顺序也是A B setState
- 事件处理函数在执行过程中不会被中断，在事件处理函数执行过程中不会触发重新渲染。同时也有利于提高渲染速度。类似批处理。
### 使用更新函数
在`setState`中使用更新函数`setNumber(n => n + 1);`(n与set对应的状态名不一定要一致)。但是setNumber**状态的更新还是在其他代码执行完毕后再执行的**
```javascript
import { useState } from 'react';

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        alert("1 "+number)
        setNumber(n => n + 1);
        alert("2 "+number)
        setNumber(n => n + 1);
      }}>+3</button>
    </>
  )
}
```
上述代码输出1 0和2 0之后，{number}显示的number值为2。

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