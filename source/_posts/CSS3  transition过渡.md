---
title: CSS3 transition过渡
categories:  #设置分类
- css
---

# CSS3  transition过渡

html结构

```html
<div class="box1">  
  <div class="div1"></div>
  <div class="div2"></div>
  <div class="div3"></div>
</div>
```

先给元素设置transition过渡，指定样式和时间，这里设置all全部样式都采用0.3s的过渡

```css
.box1>div{
  /* 给元素所有变化都添加过渡动画, 也可以指定唯一的过渡样式属性*/
  transition: all .3s;
}
```

**宽度过渡**

```css
.div1:hover{width: 150px;}
```

**背景色过渡**

```css
.div2:hover{background: #999;}
```

**按贝塞尔曲线设置的过渡**

```css
/贝塞尔曲线过渡/
.div3{transition-timing-function: cubic-bezier(.39,.62,.74,1.39)}
.div3:hover{transform: translate3d(-25px, -25px, 0)}
```

### [#](https://xugaoyi.com/pages/02d7f59d98d87409/#贝塞尔曲线-cubic-bezier-x1-y1-x2-y2)贝塞尔曲线 cubic-bezier(x1,y1,x2,y2)

通过调整贝塞尔曲线可以设置出多种动画效果，比如反弹效果等 X轴的范围是0~1，Y轴的取值没有规定，但是也不宜过大。 如：直线linear，即cubic-bezier(0,0,1,1)

贝塞尔曲线在线工具：https://cubic-bezier.com/#.17,.67,.83,.67

参考：https://www.w3school.com.cn/css3/index.asp