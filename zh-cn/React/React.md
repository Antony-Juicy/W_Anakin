## 常见的数据结构栈（Stack）：

栈（Stack）：栈是一种特殊的线性表，它只能在一个表的一个固定端进行数据结点的插入和删除操作。<br/>
队列（Queue）：队列和栈类似，也是一种特殊的线性表。和栈不同的是，队列只允许在表的一端进行插入操作，而在另一端进行删除操作。<br/>
数组（Array）：数组是一种聚合数据类型，它是将具有相同类型的若干变量有序地组织在一起的集合。<br/>
链表（Linked List）：链表是一种数据元素按照链式存储结构进行存储的数据结构，这种存储结构具有在物理上存在非连续的特点。<br/>
树（Tree）：树是典型的非线性结构，它是包括，2 个结点的有穷集合 K。<br/>
图（Graph）：图是另一种非线性数据结构。在图结构中，数据结点一般称为顶点，而边是顶点的有序偶对。<br/>
堆（Heap）：堆是一种特殊的树形数据结构，一般讨论的堆都是二叉堆。<br/>
散列表（Hash table）：散列表源自于散列函数(Hash function)，其思想是如果在结构中存在关键字和 T 相等的记录，那么必定在 F(T)的存储位置可以找到该记录，这样就可以不用进行比较操作而直接取得所查记录。

## React 的设计思想

> [!TIP]
> 组件化、数据驱动视图、虚拟 DOM

## react 生命周期

componentWillMount 挂载前

compomentDidMount 挂载后

componentWillUpdate 数据更新前

componentDidUpdate 数据更新后

componentWillUnmount 组件将要销毁时

## JSX 与 JS 的区别？

JS 可以被打包工具直接编译，不需要额外转换，jsx 需要通过 babel 编译，它是 React.createElement 的语法糖，使用 jsx 等价于 React.createElement

1.  jsx 是 js 的语法扩展，允许在 html 中写 JS； JS 是原生写法，需要通过 script 标签引入

**为什么在文件中没有使用 react，也要在文件顶部 import React from “react”**

只要使用了 jsx，就需要引用 react，因为 jsx 本质就是 React.createElement

**React 组件为什么不能返回多个元素**

1.  React 组件最后会编译为 render 函数，函数的返回值只能是 1 个，如果不用单独的根节点包裹，就会并列返回多个值，这在 js 中是不允许的
2.  react 的虚拟 DOM 是一个树状结构，树的根节点只能是 1 个，如果有多个根节点，无法确认是在哪棵树上进行更新

## state 和 props 区别是啥？

state 是组件自己管理数据，控制自己的状态，可变；

props 是外部传入的数据参数，不可变；

没有 state 的叫做无状态组件，有 state 的叫做有状态组件；

多用 props，少用 state，也就是多写无状态组件。

## 简述 React 的生命周期

**constructor** 可以进行 state 和 props 的初始化

**componentDidMount** 第一次渲染后调用，可以访问 DOM，进行异步请求和定时器、消息订阅

**shouldComponentUpdate** 返回一个布尔值，默认返回 true，可以通过这个生命周期钩子进行性能优化，确认不需要更新组件时调用

**componentDidUpdate** 在组件完成更新后调用

**componentWillUnmount** 组件从 DOM 中被移除的时候调用

## Redux 工作流

store 存储数据

state: 数据的状态，触发 view 的改变

action:参数（改变 state 唯一的方式）

reducer(必须是一个纯函数用于 state 修改逻辑):利用 state，action 来返回一个新的

- 常用方法
  - store.getState() 获取仓库最新状态
  - store.dispatch(action) 修改数据唯一方式
  - store.subscribe(fn) 监听数据修改
    redux 的工作原理
    state 保持在单一的 store 里面，改变 state 唯一 的方式是触发 actions，然后 action 来编写 reducers 来修改 state

## React 事件机制

**什么是合成事件**

**React 基于浏览器的事件机制实现了一套自身的事件机制，它符合 W3C 规范，包括事件触发、事件冒泡、事件捕获、事件合成和事件派发等**

**React 事件机制**总结如下：

事件绑定 事件触发

- **React 所有的事件绑定在 container 上**(react17 以后),而不是绑定在 DOM 元素上（作用：减少内存开销，所有的事件处理都在 container 上，其他节点没有绑定事件） container 「肯提呢」
- React 自身实现了一套冒泡机制，不能通过 return false 阻止冒泡
- React 通过**SytheticEvent**实现了**事件合成** 「谁提呢晒问」

合成事件是 React 模拟原生 DOM 事件所有能力的一个事件对象，即浏览器原生事件的跨浏览器包装器

根据 W3C 规范来定义合成事件，兼容所有浏览器，拥有与浏览器原生事件相同的接口，

## 受控组件和非受控组件区别是啥？

- 受控组件是 React 控制中的组件，并且是表单数据真实的唯一来源。

- 非受控组件是由 DOM 处理表单数据的地方，而不是在 React 组件中。

## 前端通用路由解决方案

- hash 模式

> 改变 URL 以#分割的路径字符串，让页面感知路由变化的一种模式,通过*hashchange*事件触发

- history 模式

> 通过浏览器的 history api 实现,通过*popState*事件触发

## React 组件更新逻辑

- 在使用 Hook 前先要了解，React 组件在什么情况下会刷新

  1. state 或 props 有更新时，当前组件会刷新
  2. 父组件有更新时，当前组件会刷新

- 但，从上面的情况看，其中有两个问题：
  1. 调用`setState()`，就会触发组件的重新渲染（无论前后的 state 是否一样，除非继承自`PureComponent`）
  2. 父组件更新，子组件也会自动的更新（无论子组件是否有必要更新）

Hook 除了能让函数组件使用一些类组特性外，还自带一些性能优化，使函数组件发挥出强大的优势

## react 组件通信方式有哪些

**父组件向子组件通信**

- **props 传递** 利用 React 单向数据流的思想，通过 props 传递

**子组件向父组件通信**

- **回调函数** 父组件向子组件传递一个函数，通过函数回调，拿到子组件传过来的值

**兄弟组件通信**

- 实际上就是通过父组件中转数据的，子组件 a 传递给父组件，父组件再传递给子组件 b

**Redux 工作原理**

Redux 是一个状态管理库，使用场景：

- 跨层级组件数据共享与通信
- 一些需要持久化的全局数据，比如用户登录信息

Store 一个全局状态管理对象

Reducer 一个纯函数，根据旧 state 和 props 更新新 state

Action 改变状态的唯一方式是 dispatch action

**谈谈你对高阶组件 HOC 的看法？**

1.简称 HOC ，是一个函数

2.入参：原来的 react 组件

3.返回值：新的 react 组件

4.是一个纯函数，不应该有任何的副作用。

答：**不是一个组件，而是一个用来包装组件的函数(高阶函数/纯函数)，并且必须返回一个新的函数**

纯函数

1. 不修改传入的参数
2. 固定输入有固定输出

定义高阶组件（1.把组件作为参数传入 2.返回一个新的组件）

- **普通方式、装饰器，多个高阶组件的组合**

- **作用：**1. 属性代理 操作 props 、操作组件实例 2.继承、属性劫持

## React18 有哪些更新？

react18，将所有事件都进行批处理，即多次 setState 会被合并为 1 次执行，提高了性能，在数据层，将多个状态更新合并成一次处理（在视图层，将多次渲染合并成一次渲染）

- concurrent Mode :渲染模型的变化 「肯可伦特」
- Automatic Batching :自动批量更新 state 变化，减少渲染次数
- Transition : 指定渲染优先级
- Suspense ：更加方便组织并行请求和 loading 状态的代码

1. 引入了新的 root API，支持 new concurrent renderer(并发模式的渲染)

2. setState 自动批处理 <!--react18，将所有事件都进行批处理，即多次setState会被合并为1次执行，提高了性能，在数据层，将多个状态更新合并成一次处理（在视图层，将多次渲染合并成一次渲染）-->

3. react 组件返回值更新 在 react17 中，返回空组件只能返回 null，显式返回 undefined 会报错 在 react18 中，支持 null 和 undefined 返回

## react fiber

1.为了使 react 渲染的过程中可以被中断，可以将控制权交还给浏览器，可以让位给高优先级的任务，浏览器空闲后在恢复渲染。

2.对于计算量比较大的 js 计算或者 dom 计算，就不会显得特别卡顿，而是是一帧一帧的有规律的执行任务

> [!TIP]
> generator 有类似的功能，为什么不直接使用，要使用 generator ，需要将涉及到所有的代码都包装成 generator\*的形式，非常麻烦，工作量很大

**什么是 fiber，fiber 解决了什么问题**

在 React16 以前，React 更新是通过**树的深度优先遍历**完成的，遍历是不能中断的，当树的层级深就会产生栈的层级过深，页面渲染速度变慢的问题，为了解决这个问题引入了 fiber，React fiber 就是虚拟 DOM，它是一个链表结构，返回了 return、children、siblings，分别代表父 fiber，子 fiber 和兄弟 fiber，随时可中断

**Fiber 是纤程，比线程更精细，表示对渲染线程实现更精细的控制**

**如何判断当前是否有高优任务呢**

1.当前 ji 环境其实是没有办法判断是否有高优任务，只能约定一个合理的执行时间，当超过这个执行时间，如果任务仍然没有执行完，中断当前任务，将控制权交给浏览器

2 .requestIdleCallback 回调函数 （浏览器 API） 浏览器在有空时候执行我们的回调，这个回调有一个参数，表示浏览器有多少时间供我们执行任务。

**react 预定 5 个优先级的登记**

- Immediate 最高优先级，这个优先级的任务应该马上被执行不能中断。 「迷笛」
- UserBlocking 这些任务一般是用户交互的结果，需要及时得到反馈。 「忧思布拉 king」
- Normal 不需用户立即就感受到的变化，比如网络请求。 「弄膜」
- low 这些任务可以延后，但最终也需要执行
- Idle 可以被无限期延后

## Express 和 koa 有什么关系，有什么区别？

Express.js 是一个灵活而简约的 Node.js 应用框架。这个插件并不是围绕着特定的组件构建的，因此它并不限制你使用什么技术。这就给了开发者尝试的自由。他们还可以获得闪电般的配置和纯 JavaScript 体验，这些特性使 Express.js 成为快速原型设计和敏捷开发市场的有力竞争者。

**Express.js 可以被用于：**

- 单页应用
- 多页应用
- 混合应用

**Express.js 主要特性：**

- 更快的服务端开发
- 赋能开发者更快地构建 RESTful API
- Express 支持 MVC 架构，但需要开发者做一些额外工作
- 开箱支持 NoSQL 数据库

**什么时候使用 Express.js：**

Express.js 是快速创建 Web 应用程序和服务的理想选择，因为它有现成的 API 生成工具。它是基于 JavaScript 的全栈方案 MEAN 的一部分。这意味着你可以使用 Express.js 来制作任何基于浏览器的企业级应用。

Koa.js 是一个开源的 Node web 框架，由 Express.js 原班人马创建。通过 Koa，他们的目标是为 Web 应用和 API 创建一个更小、更有价值、更强大的平台。它提供了多种高效的方法，以让构建服务的过程更快速。

**Koa.js 可以被用于：**

- 前台系统
- 后台系统
- 混合系统

**Koa.js 主要特性：**

- 代表现代和未来
- 与所有 Node.js 框架相比，体积更小。
- 有一个内置的错误捕捉器，防止网站崩溃。
- 使用 context 对象，该对象同时拥有请求和响应对象。

**什么时候使用 Koa.js：**

Koa.js 最适合用于创建服务器、路由、处理响应和处理错误。
