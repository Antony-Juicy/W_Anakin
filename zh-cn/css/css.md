## box-sizing:border-box 和 box-sizing；content-box 的区别

border-box：边框和内边距的值是包含在 width 内的。（怪异盒模型）
区别：
content-box：padding 和 border 不被包含在定义的 width 和 height 之内。

盒子的实际宽度=设置的 width+padding+border

border-box：padding 和 border 被包含在定义的 width 和 height 之内。
盒子的实际宽度=设置的 width（padding 和 border 不会影响实际宽度）

## 清除浮动的方式

1.额外标签法（隔墙法）--》在浮动元素末尾添加一个空标签

2.父级添加 overflow 属性

3.父级添加 after 伪元素

4.父级添加双伪元素（万能清除法）

## http 状态码

- 200 - 请求成功
- 301 - 资源（网页等）被永久转移到其它 URL
- 404 - 请求的资源（网页等）不存在
- 500 - 内部服务器错误

| 1\*\* | 信息，服务器收到请求，需要请求者继续执行操作   |
| ----- | ---------------------------------------------- |
| 2\*\* | 成功，操作被成功接收并处理                     |
| 3\*\* | 重定向，需要进一步的操作以完成请求             |
| 4\*\* | 客户端错误，请求包含语法错误或无法完成请求     |
| 5\*\* | 服务器错误，服务器在处理请求的过程中发生了错误 |

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

## 请说一下你常用的字符串方法（至少七个）

- trim(): 去首尾空格
- split(sep，limit)：将字符串分割为字符数组，limit 为从头开始执行分割的最大数量
- indexOf(str):返回 str 在父串中第一次出现的位置，若没有则返回-1

- lastIndexOf(str):返回 str 在父串中最后一次出现的位置，若没有则返回-1

- substr(start，length)：从字符索引 start 的位置开始，返回长度为 length 的子串

- substring(from,to)：返回字符索引在 from 和 to（不含）之间的子串

- slice(start,end)：返回字符索引在 start 和 end（不含）之间的子串

- toLowerCase()：将字符串转换为小写

- toUpperCase()：将字符串转换为大写

- replace(str1,str2):str1 也可以为正则表达式，用 str2 替换 str1

- concat(str1,str2,...):连接多个字符串，返回连接后的字符串的副本

- match(regex):搜索字符串，并返回正则表达式的所有匹配

- charAt(index):返回指定索引处的字符串

- charCodeAt(index):返回指定索引处的字符的 Unicode 的值

- fromCharCode():将 Unicode 值转换成实际的字符串

- search(regex):基于正则表达式搜索字符串，并返回第一个匹配的位置

- valueOf()：返回原始字符串值

## 字符串截取方法 substr、 substring、 slice 三者的区别

- substr(n,m)：截取的是字符串中索引为 n 开始的，并且截取 m 位

- substring(n,m)：从索引为 n 的位置开始截取，截取到索引为 m 的位置但是不包含索引为 m 这一项

- slice(n,m)：和 substring 一样，但是他可以支持负数索引

## 判断 Array 类型的几种方式 0

1、[ ] instanceof Array

2、[ ].constructor === Array

3、Object.prototype.toString.call([]) === '[object Array]'

4、Array.isArray([])

## Map 相对于 WeakMap ：

Map 的键可以是任意类型， WeakMap 只接受对象作为键（null 除外），不接受其他类型的值作为键 Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键；

WeakMap 的键是弱引用，键所指向的对象可以被垃圾回收，此时键是无效的

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

1.冒泡：当下级节点触发某个事件的时候，该事件会逐级向上触发上级节点的同类事件（自顶向上）

2.捕获：即是从上级节点传递到下级节点（自底向上）

第三个参数决定，默认是 fasle，冒泡阶段

**缺点:**

如果把所有事件都用事件代理，可能会出现事件误判
**阻止事件冒泡**

ev.stopPropagation();

**如何阻止默认事件**

return false 或者 ev.prevent Default();

**事件委托原理**

事件委托就是基于 js 的事件流产生的，事件委托是理由冒泡，将事件加在父元素或者祖先元素上，触发该事件

通过对上面事件委托代码的观察，我们可以很容易得出事件委托的好处：

① 减少页面绑定事件数量，由于页面事件绑定数量越多，页面执行性能越差，所以事件委托可以提高页面的性能

② 事件委托可以灵活的处理子节点动态变化的场景，无论子节点增加还是减少，事件都无需重新绑定

## 什么是 JS 变量提升 与 块级作用域

变量提升：就是会把变量定义提升到当前作用域的最上面

块级作用域：JS 中作用域有：全局作用域、函数作用域。没有块作用域的概念。ES6 中新增了块级作用域。

块作用域由 { } 包括，if 语句和 for 语句里面的{ }也属于块作用域。在外边不能调用块作用域里边定义的变量

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

## 介绍 Flex 布局，Flex 是什么属性的缩写。

- flex 属性是 flex-grow、flex-shrink 和 flex-basis 的简写

## css div 垂直水平居中，并完成 div 高度永远是宽度的一半（宽度可以不指定）

- width 设置百分比
- padding 撑高
- 如果只是要相对于 body 而言的话，还可以使用 vw 和 vh
- 伪元素设置 margin-top: 100%撑高

双重嵌套，外层 relative，内层 absolute

## 实现两栏布局的方式：

- 左 float，然后右 margin-left（右边自适应）
- 右 float，margin-right

**flex 实现两栏布局**
position + margin
左边元素固定宽度，右边的元素设置 flex: 1

- 利用绝对定位，父级元素设为相对定位。左边元素 absolute 定位，宽度固定。右边元素的 margin-left 的值设为左边元素的宽度值，绝对定位后相当于脱离文档流，right 对齐点变为左上角，设置 margin 即可

- 利用绝对定位，父级元素设为相对定位。左边元素宽度固定，右边元素 absolute 定位， left 为宽度大小，其余方向定位为 0

## 三列布局的方式

- position + margin-left + margin-right

## 请你讲一讲 CSS 的权重和优先级

- 从 0 开始，一个行内样式+1000，一个 id 选择器+100，一个属性选择器、class 或者伪类+10，一个元素选择器，或者伪元素+1，通配符+0

**优先级**

- 权重相同，写在后面的覆盖前面的
  使用 !important 达到最大优先级，都使用 !important 时，权重大的优先级高

## CSS 动画有哪些？

animation、transition、transform、translate 这几个属性要搞清楚：

- animation：用于设置动画属性，他是一个简写的属性，包含 6 个属性

- transition：用于设置元素的样式过度，和 animation 有着类似的效果，但细节上有很大的不同

- transform：用于元素进行旋转、缩放、移动或倾斜，和设置样式的动画并没有什么关系

- translate：translate 只是 transform 的一个属性值，即移动，除此之外还有 scale 等

## rgba()和 opacity 这两个的透明效果有什么区别

- opacity 是属性，rgba()是函数，计算之后是个属性值；
- opacity 作用于元素和元素的内容，内容会继承元素的透明度，取值 0-1；
- rgba() 一般作为背景色 background-color 或者颜色 color 的属性值，透明度由其中的 alpha 值生效，取值 0-1；
