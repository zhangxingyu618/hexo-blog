---
title: vue3 + G6 采坑笔记
---

# vue3 + G6 采坑笔记

### 1.axios 获取数据异步问题

![image-20210622164011097](https://i.loli.net/2021/11/11/ZMkrPVI7ztXBfub.png)

原本想 getData 方法在 onBeforeMount 生命周期运行，draw 绘制的方法在 onMounted生命周期中进行。但是在数据还没有获取得到的时候，onMounted就已经运行了，这才意识到不对，直接把draw写在 axios.get之后就可。

### 2.reactive的数据存取问题

```javascript
const data: any = reactive({ nodes: [], edges: [] });

 data.nodes = [...res.data.nodes];
 data.edges = [...res.data.edges];
```

如果res.data.nodes里面有包裹 [ ] ，则需要用到扩展运算符 ... 

#### 3.G6的数据更换之后的图形再次渲染问题

需要将G6生成的实例化对象设置为全局对象

```javascript
let graph:any = reactive(Object)

 graph = new G6.Graph({ 
 ...
 })
```

只要实例化对象不是同一个，后面再次渲染就会出现两个图形，导致不是更新数据，而是再次绘制一个新的图像。

### 4.添加节点的相关代码

```js
function add(this: any) {
      let newNode = reactive({
        id: num.value.toString(),
        label: (num.value+1).toString(),
      });
      let newEdges = reactive({
        source: (num.value-1).toString(), 
        target: num.value.toString(), 
        label: "测试"
      });
      data.nodes.push(newNode);
      data.edges.push(newEdges);
      console.log(data, "更新数据");
      num.value = num.value + 1;
	//再次渲染
      graph.render();
     
    }
```

