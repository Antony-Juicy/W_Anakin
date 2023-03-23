# useEffect 和 useLayoutEffect 的原理与区别

在 React hook 中，useEffect 用来取代 componentDidMount 和 componentDidUpdate。主要作用是当页面渲染后，进行一些副作用操作（比如访问 DOM，请求数据）。

useEffect 和 useLayoutEffect 的执行时机不一样，前者被异步调度，当页面渲染完成后再去执行，不会阻塞页面渲染。

useLayoutEffect 是在 commit 阶段新的 DOM 准备完成，但还未渲染到屏幕之前，同步执行。

- 模拟 componentDidMount - useEffect 依赖 [ ]
- 模拟 compenentDidUpdate - useEffect 无依赖 ，或者 依赖 [a,b,c]
- 模拟 componentWillUnMount - useEffect 中返回一个函数

# useCallback 与 useMemo 区别

seCallback 与 useMemo 有些许不同，缓存的是**函数本身以及它的引用地址**，而不是返回值。

**useMemo**返回缓存的**变量**，**useCallback**返回缓存的**函数**

用法：React.memo(component, Func)，第一个参数是自定义组件，第二个参数是一个函数，用来判断组件需不需要重新渲染。如果省略第二个参数，默认会对该组件的 props 进行浅比较
