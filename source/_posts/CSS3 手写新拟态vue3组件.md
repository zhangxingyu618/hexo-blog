---
title: CSS3手写新拟态vue3组件
---
# CS3手写新拟态vue3组件

![image-20210714163247179](https://i.loli.net/2021/11/11/4HA9cp58T1NyFPl.png)

#### 

#### 按钮的拟态组件效果

```vue
<template>
  <button>
    <slot></slot>
  </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  setup() {
    //不能为空
  },
});
</script>


<style scoped>
button {
  border: none;
  padding: 20px 40px;
  cursor: pointer;
  font-weight: 500;
  letter-spacing: 2px;
  color: #5a84a2;
  font-size: 18px;
  border-radius: 60px;
  background-color: #ecf0f3;
  box-shadow: -2px -2px 8px rgba(255, 255, 255, 1),
    -2px -2px 12px rgba(255, 255, 255, 0.5),
    inset 2px 2px 4px rgba(255, 255, 255, 0.1), 2px 2px 8px rgba(0, 0, 0, 0.15);
}

button:hover {
  box-shadow: inset -2px -2px 8px rgba(255, 255, 255, 1),
    inset -2px -2px 12px rgba(255, 255, 255, 0.5),
    inset 2px 2px 4px rgba(255, 255, 255, 0.1),
    inset 2px 2px 8px rgba(0, 0, 0, 0.15);
}
</style>

```



#### 下拉框拟态组件

```vue
<template>
  <div class="dropdown">
    <button class="dropbtn">
      <slot name="title"></slot>
    </button>
    <div class="dropdown-content">
      <slot name="item"></slot>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  setup() {
    // 不能为空
  },
});
</script>

  <style scoped>
.dropbtn {
  box-shadow: -5px -5px 12px rgba(255, 255, 255, 1),
    -5px -5px 16px rgba(255, 255, 255, 0.5),
    inset 5px 5px 8px rgba(255, 255, 255, 0.1), 5px 5px 12px rgba(0, 0, 0, 0.15);
  background: #ecf0f3;
  color: #5a84a2;
  border-radius: 10px;
  padding: 20px 30px;
  font-size: 16px;
  border: none;
  cursor: pointer;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  border-radius: 10px;
  cursor: pointer;
  color: #5a84a2;
  min-width: 130px;
  box-shadow: -5px -5px 12px rgba(255, 255, 255, 1),
    -5px -5px 16px rgba(255, 255, 255, 0.5),
    inset 5px 5px 8px rgba(255, 255, 255, 0.1), 5px 5px 12px rgba(0, 0, 0, 0.15);
}

.dropdown-content div {
  border-radius: 10px;
  color: #5a84a2;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content div:hover {
  box-shadow: inset -5px -5px 12px rgba(255, 255, 255, 1),
    inset -5px -5px 16px rgba(255, 255, 255, 0.5),
    inset 5px 5px 8px rgba(255, 255, 255, 0.1),
    inset 5px 5px 12px rgba(0, 0, 0, 0.15);
}

.dropdown:hover .dropdown-content {
  display: block;
}

.dropdown:hover .dropbtn {
  box-shadow: inset -5px -5px 12px rgba(255, 255, 255, 1),
    inset -5px -5px 16px rgba(255, 255, 255, 0.5),
    inset 5px 5px 8px rgba(255, 255, 255, 0.1),
    inset 5px 5px 12px rgba(0, 0, 0, 0.15);
}
</style>
  
```

在父组件中可以这样引用

```vue
<!-- 按钮组件 -->
<Neu_button> 按钮 </Neu_button>
<!-- 下拉框组件 -->
    <Neu_dropdown style="padding-left:50px">
      <template v-slot:title> 下拉框 </template>
      <template v-slot:item>
        <!-- 需要加样式 -->
        <div>111</div>
        <div>111</div>
        <div>222</div>
        <div>111</div>
        <div>111</div>
      </template>
    </Neu_dropdown>

```

#### 拟态头像框

```vue
<div class="inner-shadow-ring item"> </div>
    <div class="inner-shadow-ring-2 item"> </div>

<style>
.item {
  position: relative;
  width: 200px;
  height: 200px;
  margin-left: 80px;
  margin-top: 80px;
  background: #ecf0f3;
}
.inner-shadow-ring {
  border-radius: 100%;
  box-shadow: 9px 9px 15px #d1d9e6, -9px -9px 15px #fff;
}

.inner-shadow-ring:before {
  content: "";
  position: absolute;
  left: 10%;
  top: 10%;
  width: 80%;
  height: 80%;
  border-radius: 100%;
  background: #ecf0f3;
  background-image:url(../../public/head.jpg);
  background-position: 50% 50%;
  background-size:100% 100%;
  box-shadow: inset 9px 9px 15px #d1d9e6, inset -9px -9px 15px #fff;
}
.inner-shadow-ring-2 {
  border-radius: 100%;
  box-shadow: inset 9px 9px 15px #d1d9e6, inset -9px -9px 15px #fff;
}

.inner-shadow-ring-2:before {
  content: "";
  position: absolute;
  left: 10%;
  top: 10%;
  width: 80%;
  height: 80%;
  border-radius: 100%;
  background: #ecf0f3;
  background-image:url(../../public/head.jpg);
  background-position: 50% 50%;
  background-size:100% 100%;
  box-shadow: 9px 9px 15px #d1d9e6, -9px -9px 15px rgb(247, 247, 247);
  /* box-shadow: inset 3px 3px 15px #d1d9e6, inset -3px -3px 15px #fff; */
}
</style>
```

