---
title: React中useRef与useEffect
published: 2025-01-23
description: react中ref
tags: [react]
category: Web
draft: false
---

## ref
- 可以记住信息，但同时不会触发新的渲染
- 渲染过程中不能读取或写入ref.current
- 与state不同，ref是一个同步更新的量
- ref本身是一个普通的JavaScript对象

### ref操作DOM元素
错误示例：
```
function VideoPlayer({ src, isPlaying }) {
  const ref = useRef(null);

  if (isPlaying) {
    ref.current.play();  // 渲染期间不能调用 `play()`。 
  } else {
    ref.current.pause(); // 同样，调用 `pause()` 也不行。
  }

  return <video ref={ref} src={src} loop playsInline />;
}
```
上述代码相当于在渲染期间调用play()和pause()。但逻辑上存在问题。在第一次渲染时，<video/>还并未被渲染，if判断语句会造成null错误。


## useEffect
- Effect 允许你在渲染完成，提交结束后执行一些代码，以便将组件与 React 外部的某个系统相同步。
- **Effect常用于由渲染本身，而不是按钮点击等事件引起的副作用**。默认执行的时间在提交DOM，页面更新之后。因此下述代码会产生死循环：
    ```javascript
    const [count, setCount] = useState(0);
    useEffect(() => {
    setCount(count + 1);
    });
    ```




> 