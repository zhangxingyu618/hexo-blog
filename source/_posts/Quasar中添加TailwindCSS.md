---
title: Quasar 中添加 tailwindcss
---

## Quasar 中添加 tailwindcss 

> 踩大坑了，搞了整整一天才研究明白

结果操作是非常简单，但是我把tailwindcss安装文档从vite到next到nuxt都研究了一遍。把tailwind文档研究后，发现是quasar的问题。单纯的引入并不能引入成功。

从quasar的文档从入门开始看仔细研究，一开始以为可以用quasar的启动文件boot，在启动文件引入tailwind的css文件，照样是没有任何作用，我都已经开始怀疑引入的这个**@tailwind**是不是有毛病，quasar识别不了？

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

接着试验用vite去引入tailwind，很容易 直接成功，然后我尝试用quasar引入elementui+，因为elemenui+需要使用app.use()调用，用quasar的boot启动文件是可以调用VUEapp的。但是，tailwind没有默认导出文件！只能import引入css。到底是quasar的问题还是tailwind的问题？

#### 结果来了

在通篇阅读quasar的文档后，在文档的最下角发现了 **应用扩展**

> 应用扩展是一种轻松注入具有各种依赖项、启动文件、模板和自定义逻辑的复杂（或简单）库的方法。 他们可以扩展webpack、`quasar.conf.js`，将外部UI组件紧密耦合到核心，甚至可以通过Quasar CLI注册新命令。 它们可以与`quasar dev`一起运行，并且可以完全访问当前的实时`ctx`（上下文）。

所有应用扩展必须在其名称前加上`quasar-app-extension-`。 该前缀之后的所有内容均被视为其简短别名。 在整个文档中，我们将其称为`ext-id`。

附查找应用扩展网址

[quasar-app-extension - npm search (npmjs.com)](https://www.npmjs.com/search?q=quasar-app-extension)

##### 安装应用扩展

```bash
$ quasar ext add <ext-id>
```

##### 查看已安装的应用拓展

```bash
$ quasar ext
$ quasar info
$ cat quasar.extensions.json
```

##### 更新应用扩展

```bash
$ quasar ext add <ext-id>
```

##### 删除应用扩展

```bash
$ quasar ext remove <ext-id>
```

#### 然而这个tailwind就用quasar的扩展，但文档怎么不说？？？

[quasar-app-extension-tailwindcss2 - npm (npmjs.com)](https://www.npmjs.com/package/quasar-app-extension-tailwindcss2)

```bash
$ quasar ext add tailwindcss2
```

安装完成后会在src目录下创建extensions文件夹

安装的时候会让选择一个前缀，因为quasar里面的类也有很多相似的，怕引起冲突，需要选择一个前缀以保证css样式的类名不会发生冲突

如扩展前缀为 **qa-**

后面的所有tailwind的样式类都需要在前面添加 **qa-**    例:

```html
<div class="qa-p-6 qa-max-w-sm qa-mx-auto qa-bg-white qa-rounded-xl qa-shadow-md qa-flex qa-items-center qa-space-x-4">
    <div class="qa-flex-shrink-0">
      <img class="qa-h-12 qa-w-12" src="/favicon.ico" alt="ChitChat Logo" />
    </div>
    <div>
      <div class="qa-text-xl qa-font-medium qa-text-black">ChitChat</div>
      <p class="qa-text-gray-500">You have a new message!</p>
    </div>
</div>
```

