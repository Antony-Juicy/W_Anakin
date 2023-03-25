## 水平垂直居中的方式有哪些

- position +margin:auto：父容器相对定位，子容器绝对定位，上下左右设置为 0，marginQ 置为 auto

- position + transform：父容器相对定位，子容器绝对定位，top,left 设置为 50%，transform:translate(-50% -50%)
- filex 布局：为父容器设置 @display : filex; @ justify-content:center: ③ align-items:center

- grid 网格布局：为父容器设置 @display: grid; @ justify-items: center; ③ align-content: center;

## HTML 语义化标签有哪些?语义化有什么优点

常用语义化标签有

- header：定义文档或节的页眉

- footer：定义文档或节的页脚

- article：定义文档内的文章

- section：定义文档中的节

- aside ：定义页面内容之外的内容

- main：定义文档的主内容

  > [!TIP]
  > 有利于开发和维护,有利于 SE0，搜索、语义化更具可读性,代码更好维护

## css 长度单位 px、em.rem、vh

- px：绝对长度，表示固定的像素，一旦设置了，就无法适应页面大小去改变

- em：相对长度，相对于父元素的宇体大小，2em 表示当前父元素字体大小的 2 倍

- rem：相对长度，和 em 一样，2rem 表示当前字体的 2 倍，只不过是相对于浏览器基准 （html)字

- vhw：相对长度，相对于页面视口来计算，100vh，相当于视口高度的 100%

## 让页面里的字体变清晰，变细用 CSS 怎么做？

- webkit-font-smoothing 在 window 系统下没有起作用，但是在 10S 设备上起作用
- webkit-font-smoothing：antialiased 是最佳的，灰度平滑

**Css 中实现文字强制不换行、超出自动换行：**

word-break:break-all; ---英文 <br/>white-space:pre-wrap; ---中文
<br/>

> [!TIP]
> word-wrap: break-word;word-break: break-word
