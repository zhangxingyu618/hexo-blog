---
title: vue3 + G6 采坑笔记 2
---

# vue3 + G6 采坑笔记 2（.d.ts 类型声明文件）

今天了解了一下g6-editor流程图编辑框架导包的时候

```js
import G6Editor from "@antv/g6-editor";
```

出现这样的错误

```
无法找到模块“@antv/g6-editor”的声明文件。“c:/Users/Lenovo/Desktop/vue/myvue3/node_modules/@antv/g6-editor/build/g6Editor.js”隐式拥有 "any" 类型。
  尝试使用 `npm i --save-dev @types/antv__g6-editor` (如果存在)，或者添加一个包含 `declare module '@antv/g6-editor';` 的新声明(.d.ts)文件ts(7016)
```

> 尝试使用 `npm i --save-dev @types/antv__g6-editor` 也不行

后面发现 是因为在使用 Typescript 的过程中， 第三方类库并没有ts的.d.ts 类型的声明文件，所以无法在目前的项目中正常使用。如果要顺利使用这些库， 可能需要我们添加声明文件。

## 解决方法

在src目录下新建一个types目录,然后在types 目录下新建一个 index.d.ts文件然后在文件中添加代码 declare module "第三方类库名"。

```js
declare module '@antv/g6-editor';
```

就可以运行了。

