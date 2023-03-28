## 性能监控指标

**根据相对应的指标**

- 比如⻚页⾯面性能检测利用工具，结合相对的指标逐个优化。

- 只请求当前需要的资源，异步加载, 懒加载, polyfill 的优化，

  > [!TIP]
  > 「利用 polyfill 插件 cdn 按需引入，减小包的大小」

- 缩减资源体积

  1.打包压缩 2.gzip 开启 3.图⽚片格式优化, 压缩, 根据屏幕分辨率展示不不同分辨率的图⽚片 4.尽量量控制 cookie 大⼩

- 时序优化

  js 中 promise.all 、ssr 、 prefetch、prerender、preload <!--「嵌入link 标签 <link rel="dns-prefetch" href="xxxxxx" />」-->

- 合理理利利⽤用缓存

  cdn、http 缓存、localStorage, sessionStorage

  ## 导致内存泄漏的方法，怎么监控内存泄漏

  - 全局变量

  - 被遗忘的定时器 <!--未被清理理的定时器器和回调函数-->

  - 脱离 Dom 的引用 <!--我们对 Dom 的操作, 会把 Dom 的引⽤用保存在⼀一个数组或者 Map 中-->

  - 闭包 <!--一个内部函数，有权访问包含其的外部函数中的变量。-->

    ## 监控内存泄漏

  - window.performance.memory

  - 开发阶段

    - 浏览器的 Performance
    - 移动端可使用 PerformanceDog

  #### 内存的⽣生命周期

  内存分配:当我们申明变量量、函数、对象的时候，系统会⾃自动为他们分配内存

  内存使用:即读写内存，也就是使⽤用变量量、函数等

  内存回收:使⽤用完毕，由垃圾回收机制⾃自动回收不不再使⽤用的内存

  #### Js 中的垃圾回收机制

  > [!TIP]
  > 垃圾回收算法主要依赖于引⽤用的概念。

  > 在内存管理理的环境中，一个对象如果有访问另一个对象的权限(隐式或者显式)，叫做一个对象引用另一个对象。

  - 例如，一个 Javascript 对象具有对它原型的引⽤用(隐式引⽤用)和对它属性的引⽤用(显式引用)。 <!--在这里，“对象”的概念不仅特指 JavaScript 对象，还包括函数作用域(或者全局词法作用域)。-->

  > 1 、引⽤用计数垃圾回收 2 、标记清除算法