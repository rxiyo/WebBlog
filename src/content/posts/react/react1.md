---
title: React杂记
published: 2025-01-17
description: react的一些杂项
tags: [react]
category: Web
draft: false
---

## 组件之间的通信
组件A中使用`import`导入了B，则A为父组件，B为子组件
### 父传子
父传子主要通过props实现
- 父的准备：<br>
  使用`<ChildPart/>`插入子模块时，为其设置props。
    ```javascript
    return(
        <ChildPart prop1={可是是函数名作为回调函数} props2={变量名、常量名等}>
    )
    ```
- 子的准备：<br>
  `function()`中设置好参数
    ```javascript
    function ChildPart({prop1, prop2}){
    }
    ```
>  子模块中也可以设置默认参数

### 子传父
主要通过回调函数实现
- 父的准备 <br>
  利用父传子的方法将回调函数(是在父组件中生命的)设为props传递给子组件
    ```javascript
    export default function FatherPart(){
        const [infoFromChild, setInfo] = useState("");
        //设置回调函数callback
        const callback = (msg) => {
            setInfo(msg)    
        }
        return (<div> <ChildPart func={callback}></div>)
    }
    ```
- 子的准备
  调用通过props传递的回调函数以实现子传父
    ```javascript
    function ChildPart({func}){
        return (<button onClick={func(100)}> click me</button>)
    }
    ```
>   也可以把父组件中`infoFromChild`和`setInfo`都传入子组件,总而能够在子组件中根据旧值来更新新值

### 关于`children`
父组件中使用子组件有两种方式。
- `<ChildCompoent/>`
- `<ChildCompoent>中间的内容</ChildCompoent>`
在方式2中，子组件首尾标签之间的内容是通过`children`prop在子组件中渲染的。
```javascript
function AlertButton({ message, children }) {
  return (
    <button onClick={() => alert(message)}>
      {children}
    </button>
  );
}
export default function Toolbar() {
  return (
    <div>
      <AlertButton message="正在播放！">
        播放电影
      </AlertButton>
    </div>
  );
}
```

