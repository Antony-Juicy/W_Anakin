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

## margin 和 padding 分别适合什么场景使用？

    何时使用 margin：
            需要在border外侧添加空白

            空白处不需要背景色

            上下相连的两个盒子之间的空白，需要相互抵消时。

    何时使用padding：

            需要在border内侧添加空白

            空白处需要背景颜色

            上下相连的两个盒子的空白，希望为两者之和。

## **游览器的重绘与回流**

答：1.当 render tree 中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如 background-color。则就叫称为重绘。

2.当 render tree 中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建。这就称为回流(reflow)。每个页面至少需要一次回流，就是在页面第一次加载的时候，这时候是一定会发生回流的，因为要构建 render tree。在回流的时候，浏览器会使渲染树中受到影响的部分失效，并重新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过程成为重绘。

## 移动端最佳适配解决方案

viewport 来替代此方案。 「v pro 投」

安装 postcss-px-to-viewport 这个包 px 单位转换为 vw、vh

目录新建一个名为 postcss.config.js 的文件

```
module.exports = {
plugins: {
'postcss-px-to-viewport': {
unitToConvert: "px", // 要转化的单位
 viewportWidth: 375, // UI 设计稿的宽度
 unitPrecision: 6, // 转换后的精度，即小数点位数
 propList: ["*"], // 指定转换的 css 属性的单位，\*代表全部 css 属性的单位都进行转换
 viewportUnit: "vw", // 指定需要转换成的视窗单位，默认 vw
 fontViewportUnit: "vw", // 指定字体需要转换成的视窗单位，默认 vw selectorBlackList: ["wrap"], // 指定不转换为视窗单位的类名，
 minPixelValue: 1, // 默认值 1，小于或等于 1px 则不进行转换
 mediaQuery: true, // 是否在媒体查询的 css 代码中也进行转换，默认 false
 replace: true, // 是否转换后直接更换属性值
 exclude: [/node_modules/], // 设置忽略文件，用正则做目录名匹配
 }
}
}
```

## Js 的事件委托是什么，原理是什么

1.冒泡：当下级节点触发某个事件的时候，该事件会逐级向上触发上级节点的同类事件

2.捕获：即是从上级节点传递到下级节点

**事件委托原理**

事件委托就是基于 js 的事件流产生的，事件委托是理由冒泡，将事件加在父元素或者祖先元素上，触发该事件

通过对上面事件委托代码的观察，我们可以很容易得出事件委托的好处：

① .减少页面绑定事件数量，由于页面事件绑定数量越多，页面执行性能越差，所以事件委托可以提高页面的性能

② .事件委托可以灵活的处理子节点动态变化的场景，无论子节点增加还是减少，事件都无需重新绑定

## 改变函数内部的 this 指针的指向

使用 call()或者 apply()，可以改变 this 的指向；

call 和 apply 的区别：

call 和 apply 的区别在于参数，他们两个的第一个参数都是一样的，表示调用该函数的对象；

apply 的第二个参数是数组，是[arg1,arg2,arg3]这种形式，而 call 是 arg1,arg2,arg3 这样的形式。

bind 函数返回新的函数，这个函数内的 this 指针指向 obj 对象。

## js 实现继承的方法有哪些

**原型链继承**

将构造函数的原型设置为另一个构造函数的实例对象，这样就可以继承另一个原型对象的所有属性和方法，可以继续往上，最终形成原型链

第一个问题是 ： 原型引用类型属性的实例之间不再具有自己的独特性了

第二个问题： 在创建子类型的实例时，没有办法在不影响所有对象实例的情况下给超类型的构造函数中传递参数

**借用构造函数继承**

为了解决原型中包含引用类型值的问题，开始使用借用构造函数，也叫伪造对象或经典继承

**组合继承**

也叫伪经典继承，将原型链和借用构造函数的技术组合到一块。使用原型链实现对原型属性和方法的继承，而通过构造函数来实现对实例属性的继承

**原型式继承**

不自定义类型的情况下，临时创建一个构造函数，借助已有的对象作为临时构造函数的原型，然后在此基础实例化对象，并返回

**寄生式继承**

其实就是在原型式继承得到对象的基础上，在内部再以某种方式来增强对象，然后返回

**寄生式组合式继承**

组合继承是 JS 中最常用的继承模式，但其实它也有不足，组合继承无论什么情况下都会调用两次超类型的构造函数，并且创建的每个实例中都要屏蔽超类型对象的所有实例属性。

寄生组合式继承就解决了上述问题，被认为是最理想的继承范式。

ES6 **class 继承**

通过 class extends

## Ajax 原理

做异步请求的，在页面不刷新的情况下向服务器发送 HTTP 请求

实现流程:

1. 创建 XMLHttpRequest 对象
2. 创建一个新的 http 请求，并指定请求方法，URL 是否为异步
3. 设置 响应 Http 请求状态变化的函数
4. 发送 Http 请求
5. 对异步返回的数据进行处理

## script 标签中 defer 和 async 的区别

**defer**

属性告诉浏览器不要等待脚本，浏览器会继续处理 HTML，构建 DOM。该脚本“在后台”加载，然后在 DOM 完全构建完成后再运行。
另外，defer 脚本总是在 DOM 准备好时执行（但在 DOMContentLoaded 事件之前）

> 页面内容立即显示。<br/>
> DOMContentLoaded 事件处理程序等待 defer 脚本执行完之后执行

**async**

> 页面内容立即显示：async 不阻塞<br/>
> DOMContentLoaded 可能发生在 async 之前或之后<br/>
> small.js 先加载完就会在 long.js 之前执行，但如果 long.js 在之前有缓存，那么 long.js 先执行。

## css 怎么开启硬件加速(GPU 加速)

浏览器在处理下面的 css 的时候，会使用 GPU 渲染

-transform (当 3D 变换的样式出现时会使用 GPU 加速)

- opacity

- filter

- will-change

采用 transform: translateZ(0)

采用 transform: translate3d(0, 0, 0)

使用 CSS 的 will-change 属性。will-change 可以设置为 opacity、transform、 top、
