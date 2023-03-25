## 什么是 react hooks？React hooks 有什么优势？

useState、useEffect、useMemo、useCallback

Hook 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性。

1. 利于业务逻辑的封装和拆分，可以非常自由的组合各种自定义 hooks（自己封装的用到了 react hooks 的公共逻辑）
2. 可以在无需修改组件结构的情况下，复用状态逻辑
3. 定时器 监听等等都被聚合到同一块代码下

## class 「类组件的」 的缺点：

1. 组件间的状态逻辑很难复用
   > [!TIP]
   > 组件间如果有 state 的逻辑是相似，class 模式下基本都是高级组件来解决，但是我们需要在组件外部在包一层元素，会导致层级非常沉余
2. 复杂业务的有状态组件会越来越复杂
3. 监听和定时器的操作，被分割在多个区域
4. 类组件需要声明 constructor，函数组件不需要
5. 类组件需要手动绑定 this，函数组件不需要

   > [!TIP]
   > render 里 bind 每次都会返回一个新的函数，造成每次都重新渲染
   > 每次都是新的引用，箭头函数是在定义的时候确定了 this 指向，而不是使用的时候

6. 类组件有生命周期钩子，函数组件没有
7. 类组件可以定义并维护自己的 state，属于有状态组件，函数组件是无状态组件
8. 类组件需要继承 class，函数组件不需要
   **SetState 是同步还是异步呢？**
   > [!TIP]
   > setState 是一个异步方法，但是在 setTimeout/setInterval 等定时器里逃脱了 React 对它的掌控，变成了同步方法

## Hook 使用注意事项

1. 只能在函数内部的最外层调用 hook ，不要在循环，条件或嵌套函数中调用 。

2. 只能在 React 的函数组件中调用 Hook，不要在其他的 js 函数里调用
   > [!TIP]
   > Hook 底层是用链表来设计的，数据来源是根据下标来获取，多个时候会错位

## useEffect 和 useLayoutEffect 的原理与区别

在 React hook 中，useEffect 用来取代 componentDidMount 和 componentDidUpdate。主要作用是当页面渲染后，进行一些副作用操作（比如访问 DOM，请求数据）。

useEffect 和 useLayoutEffect 的执行时机不一样，前者被异步调度，当页面渲染完成后再去执行，不会阻塞页面渲染。

useLayoutEffect 是在 commit 阶段新的 DOM 准备完成，但还未渲染到屏幕之前，同步执行。

- 模拟 componentDidMount - useEffect 依赖 [ ]
- 模拟 compenentDidUpdate - useEffect 无依赖 ，或者 依赖 [a,b,c]
- 模拟 componentWillUnMount - useEffect 中返回一个函数

## useCallback 与 useMemo 区别

seCallback 与 useMemo 有些许不同，缓存的是**函数本身以及它的引用地址**，而不是返回值。

**useMemo**返回缓存的**变量**，**useCallback**返回缓存的**函数**

用法：React.memo(component, Func)，第一个参数是自定义组件，第二个参数是一个函数，用来判断组件需不需要重新渲染。如果省略第二个参数，默认会对该组件的 props 进行浅比较

## 常用 Hook API

### 1. useState

State Hook 能让函数组件也能使用 class 组件一样的状态特性，同时发挥函数组件轻便高效的特性，格式：`useState(defaultValue)`，返回最新**value**与**修改 value**方法组成的数组

### 2. useEffect

Effect Hook 可以让我们在函数组件中执行一些副作用操作，如 ajax 请求，定时器等。默认情况下，effect 将在每轮**渲染结束后执行**，React 保证了每次运行 effect 时，DOM 都已经更新完毕

- 默认 effect

  > 等效于 componentDidMount + componentDidUpdate 的效果 PS：ajax 请求以前在 class 组件中可能需要在`componentDidMount`和`componentDidUpdate`两个生命周期函数中编写相同的代码，有了`useEffect`，只需要写一次就行

- 指定依赖

  > 等效于 componentDidUpdate 的效果，只有在依赖发生改变时才执行 effect 中的代码

* 指定空依赖

  > 依赖为空数组，等效于 componentDidMount 的效果

* useEffect 返回一个函数

  > 实现 componentWillUnmount 的效果

### 3. useMemo

> 一般用于编写函数组件中无需重复执行的代码，以达到**优化性能**的目的，返回值为回调函数的结果

- 执行过程
  1. 回调函数初始化组件时会被执行
  2. 依赖改变时被执行
- 返回值：依赖改变返回新的值，否则返回缓存值

### 4. useCallback

> 与 useMemo 类似，但 useCallback **返回传入的函数**，不需要显性返回，一般用于定义事件处理函数

- 不指定依赖

  > 不论初始化或者组件更新都返回新的函数

* 指定依赖

  > 依赖更新时返回新的函数，否则返回缓存函数

* 空依赖

  > 初始化返回函数后并缓存，组件更新时永远返回缓存函数

## 额外的 Hook

1. useContext

> `useContext(MyContext)` 相当于 class 组件中的 `static contextType = MyContext` 或者 `<MyContext.Consumer>`，当组件上层最近的 `<MyContext.Provider>` 更新时，该 Hook 会触发重渲染

2. useReducer

> 简单版 redux，可以在不引入 redux 的情况下使用 redux 特性

> PS: 如果 Reducer Hook 的返回值与当前 state 相同，React 将跳过子组件的渲染及副作用的执行

3. useRef
   `useRef` 返回一个可变的 ref 对象，其 `.current` 属性被初始化为传入的参数，返回的 ref 对象在组件的整个生命周期内保持不变。

4. useLayoutEffect
5. useImperativeHandle
6. useDebugValue
