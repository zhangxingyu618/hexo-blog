---
title: LogicFlow初上手
---

#  LogicFlow初上手

>因为之前用的G6-edit，转过来之后好用了太多，方便了太多，主要是G6-edit没有完整详细的文档，好像也没开源不能商用。

### logicflow 有非常好的流程图编辑功能

通过 `npm` 或 `yarn` 来安装 `LogicFlow`。

```sh
# npm
$ npm install @logicflow/core --save

# yarn
$ yarn add @logicflow/core
```

安装完成之后，使用 `import` 或 `require` 进行引用。

```js
import LogicFlow from '@logicflow/core';
import '@logicflow/core/dist/style/index.css';
```

### 用法非常简单

1.通过 `JSON` 的数据格式，来让 `LogicFlow` 渲染。该数据中需要有 `nodes`（节点） 和 `edges`（边） 字段，分别用数组表示：

```js
const data = {
  // 节点
  nodes: [
    {
      id: 50,
      type: 'rect',
      x: 100,
      y: 150,
      text: '你好',
    },
    {
      id: 21,
      type: 'circle',
      x: 300,
      y: 150,
    },
  ],
  // 边
  edges: [
    {
      type: 'polyline',
      sourceNodeId: 50,
      targetNodeId: 21,
    },
  ],
};
```

2.创建一个 `LogicFlow` 的实例，此时可以传入一些参数来控制画布，比如画布的大小。

```js
const lf = new LogicFlow({
  container: document.querySelector('#container'),
  stopScrollGraph: true,
  stopZoomGraph: true,
  width: 500,
  height: 500,
  grid: {
    type: 'dot',
    size: 20,
  },
});
```

3.通过刚才创建的实例，来渲染画布。

```js
lf.render(data);
```

到此，我们就创建好了一个最简单的示例。

![image-20210624165630709](https://i.loli.net/2021/11/11/3dUANH95Rl4P2iO.png)

>logicflow的节点你可以任意拖拽，两个节点之间的连线也可以自由连接，可编辑性非常强大。

### logicflow 的相关API非常强大，包括控制栏还有拖拽栏都可以利用API非常简单的实现

#### 控制面板

```ts
import LogicFlow from '@logicflow/core';
import { Control } from '@logicflow/extension';
import '@logicflow/extension/lib/style/index.css'

LogicFlow.use(Control);
```

![image-20210624165536045](https://i.loli.net/2021/11/11/srAMShNTxOFvQ3Z.png)

#### 拖拽面板

```ts
import LogicFlow from '@logicflow/core';
import { DndPanel } from '@logicflow/extension';
import '@logicflow/extension/lib/style/index.css'

LogicFlow.use(DndPanel);
```

![image-20210624165558372](https://i.loli.net/2021/11/11/JiTazKtM5FR2dDm.png)

等等功能都可以调用API快速在实现。包括节点的各种API真的是功能非常强大又非常贴心的框架，简单滴代码开发一个可拖拽的流程图编辑器。

还有他的自定义程度也非常高，如果API自带模板不能满足也可以高度自定义组件以及相关方法。