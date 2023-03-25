## 将伪数组转为真正的数组

> Array.prototype.slice.call() <br/>
> Array.from()

## less 和 sass 区别

Less 是基于 JavaScript，是在客户端进行处理的；Sass 是基于 Ruby，是在服务器端进行处理的。

**定义变量：**Less 定义变量时使用前缀：@；Sass 定义变量时使用前缀：$。

## 单页面应用有什么 SEO 方案？

> 服务端渲染重构:[Nuxt](https://link.juejin.cn/?target=https%3A%2F%2Fzh.nuxtjs.org%2F), [Next](https://link.juejin.cn/?target=https%3A%2F%2Fnextjs.org%2F).

## 预渲染

原理: **启动一个无头浏览器, 加载应用程序的路由, 将结果保存到静态 HTML 文件中**

适合:

- **内容不会发生变化的页面**: 例如营销页面以及广告页面

不适合:

- **内容会变化的页面**: 像博客这种- -是不行的, 因为内容在编译后就确定了, 再修改内容, 也不会有变化

优点:

- **代码侵入少**: 安装一个 plugin, 指定路由即可

缺点:

- **覆盖范围少**: 几乎只适合静态页面

- **路由(页面)较多时构建时间长**

- **不科学上网 phantomjs 下不下来**: 当时踩的坑, 转头就捣鼓梯子去了

## 什么是 CDN

CDN 又叫内容分发网络，通过把资源部署到世界各地，用户在访问时按照就近原则从离用户最近的服务器获取资源，从而加速资源的获取速度。 CDN 其实是通过优化物理链路层传输过程中的网速有限、丢包等问题来提升网速的。

## 深度复制对象

总结一下——structuredClone()不会复制对象的原型链： 「死全捆能」

- 内置对象的副本具有与原始对象相同的原型。

- 自定义类的实例副本始终具有原型 Object.prototype（如普通对象）。

## 如果⼀段 js 执行时间非常长,怎么去分析?

## 如何判定一个元素是否处于事件冒泡阶段？

答：利用 e.currentTarget 和 e.target 判断是否为同一元素，如果是同一元素就是在冒泡，e.currentTarget 指的是被绑定了事件的元素，也就是事件源，e.target 则是点击到的事件源下面的某个元素,也就是触发事件元素

## 模块化开发的区别？

答：1.commonjs -->同步
2.amd&cmd -->异步
3.EsModule -->静态引入，不能使用变量，其他模块可以

## ES Module 和 CommonJS 的区别

CommonJS 输出的是值的拷贝，ES Module 输出的是值的引用

CommonJS 是运行时加载（module.exports），ES Module 是编译时输出接口

CommonJS 的 require（）是同步加载模块，ESModule 的 import 是异步加载模块，静态编译时加载，有独立的模块依赖解析

CommonJS 模块的顶层 this 指向当前模块，ES6 模块中，顶层 this 指向 undefined

ES Module：静态加载/编译时加载

CommonJS：运行加载

ESM 效率要比 CommonJS 模块的加载方式高，动态绑定关系

import：静态执行，会提升，不可修改/只读

export default：指定模块的输出，输出一个叫做 default 的方法/变量，系统允许修改名称

import（）：动态加载模块，当需要按需加载时使用

## 什么是同源策略

只有当协议，域名，端口都一致的时候，才被称为同源

## 解决跨域常见的 5 种方法

- JSONP （JSONP 只支持 GET 请求，不支持 POST 请求 ）

- 反向代理（写一个接口 ，由这个接口在后端去调用 ，并拿到返回值，然后再返回给 index.html，这就是一个代理的模式。相当于绕过了浏览器端，自然就不存在跨域问题。 ）

- CORS 方法 （设置响应头，在 header 中添加

  header('Access-Control-Allow-Origin:\*');//允许所有来源访问

  header('Access-Control-Allow-Method:POST,GET');//允许访问的方式）

- webpack 代理需要另外一个插件：webpack-dev-server。 只需要条件一个 proxy 属性

- nginx 代理一般使用在生产环境。是服务端解决跨域的一种方案。
