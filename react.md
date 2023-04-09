# React



## React性能优化

思路 

+ 减少render执⾏次数 
+ 减少渲染的节点 
+ 降低渲染计算量 
+ VDOM 
+ 使⽤⼯具分析性能 
+ 使⽤不可突变数据结构，数组使⽤concat，对象使⽤Object.assign() 
+ 组件尽可能拆分 
+ 列表类组件优化
+  bind函数优化 
+ 不滥⽤props 
+ reactDOMServer服务端渲染组件

### React.memo

缓存组件
记忆组件渲染结果，提⾼组件性能
只检查props是否变化
做浅⽐较
第⼆个参数可传⼊⾃定义⽐较函数
areEqual⽅法和shouldComponentUpdate返回值相反

### React.useMemo 

缓存⼤量计算 

useMemo 的第⼀个参数就是⼀个函数，这个函数返回的值会被缓存起来，同时这个值会作 为 useMemo 的返回值，第⼆个参数是⼀个数组依赖，如果数组⾥⾯的值有变化，那么就会 重新去执⾏第⼀个参数⾥⾯的函数，并将函数返回的值缓存起来并作为 useMemo 的返回 值。

### PureComponent 

避免重复渲染 

React.Component并未实现 shouldComponentUpdate()，⽽ React.PureComponent中以浅 层对⽐ Prop 和 State 的⽅式来实现了该函数。 

shouldComponentUpdate函数中做的是“浅层⽐较”。若是“深层⽐较”，那时某个特定组件 的⾏为，需要我们⾃⼰编写。 

⽗组件状态的每次更新，都会导致⼦组件的重新渲染，即使是传⼊相同props。但是这⾥的 重新渲染不是说会更新DOM,⽽是每次都会调⽤diif算法来判断是否需要更新DOM。这对于 ⼤型组件例如组件树来说是⾮常消耗性能的。 

shouldComponentUpdate⽣命周期来确保只有当组件props状态改变时才会重新渲染. 

PureComponent会进⾏浅⽐较来判断组件是否应该重新渲染，对于传⼊的基本类型props， 只要值相同，浅⽐较就会认为相同，对于传⼊的引⽤类型props，浅⽐较只会认为传⼊的 props是不是同⼀个引⽤，如果不是，哪怕这两个对象中的内容完全⼀样，也会被认为是不 同的props。 

PureComponent，因为进⾏浅⽐较也会花费时间，这种优化更适⽤于⼤型的展⽰组件上。 ⼤型组件也可以拆分成多个⼩组件，并使⽤memo来包裹⼩组件，也可以提升性能。

+ /确保数据类型是值类型 如果是引⽤类型，
+ 不应当有深层次的数据变化(解构)

避免使⽤内联对象 

使⽤内联对象时，react会在每次渲染时重新创建对此对象的引⽤，这会导致接收此对象的 组件将其视为不同的对象,因此，该组件对于prop的浅层⽐较始终返回false,导致组件⼀直重 新渲染。

避免使⽤匿名函数

组件懒加载 可以使⽤新的React.Lazy和React.Suspense轻松完成。

### React.lazy 

定义⼀个动态加载的组件，这可以直接缩减打包后 bundle 的体积，延迟加载在初次渲染时 不需要渲染的组件

### React.Suspense 

悬挂 终⽌ 暂停 

配合渲染 lazy 组件，在等待加载 lazy组件时展⽰ loading 元素，不⾄于直接空⽩，提升⽤ 户体验；

```react
<Suspense fallback={<PageLoading />}>{this.renderSettingDrawer()}
</Suspense>
const SettingDrawer = React.lazy(() =>
import('@/components/SettingDrawer'));
```

⽤ CSS , ⽽不是强制加/卸载组件 ,  渲染成本很⾼，尤其是在需要更改DOM时。此操作可能⾮常消耗性能并可能导致延迟

### React.Fragment 

聚合⼦元素列表，不在DOM中添加额外标签

```react
<React.Fragment>
 <h1>Hello there!</h1>
 <h1>Hello there again!</h1>
</React.Fragment>
```

### key

保证key具有唯⼀性 

DIff算法根据key判断元素时新创建还是被移动的元素，从⽽减少不必要渲染

虽然key是⼀个prop，但是接受key的组件并不能读取到key的值，因为key和ref是React保留 的两个特殊prop

### 合理使⽤Context 

⽆需为每层组件⼿动添加 Props，通过provider接⼜在组件树间进⾏数据传递

原则 

Context 中只定义被⼤多数组件所共⽤的属性 

+ 使⽤createContext创建⼀个上下⽂ 
+ 设置provider并通过value接⼜传递state数据 
+ 局部组件从value接⼜中传递的数据对象中获取读写接⼜ 

虚拟列表 合理设计组件 简化Props 简化State 减少组件嵌套



## React组件通信

⽗组件向⼦组件传递 

React的数据流是单向的，这是最常见的⽅式，props 

⼦组件向⽗组件传递 ⽗组件向⼦组件传⼀个函数，然后通过这个函数的回调拿到⼦组件传递的值 

兄弟组件之间的通信 

⽗组件作为中间层实现数据互通 

⽗组件向后代组件传递 最普通的事情，像全局数据⼀样。 使⽤context可共享数据，其他数据都能读取对应的数据。 

⾮关系组件传递 组件间关系类型复杂，可以将数据进⾏⼀个全局资源管理，从⽽实现通信，例如redux dva



## React生命周期

### react15

```js
constructor() // 构造函数
componentWillReceiveProps() // ⽗组件状态属性更新触发
shouldComponentUpdate() // 组件更新时调⽤，在此可拦截更新
componentWillMount() // 初始化渲染时调⽤（挂载前调⽤）
componentWillUpdate() // 组件更新时调⽤
componentDidUpdate() // 组件更新后调⽤
componentDidMount() // 初始化渲染时调⽤（挂载后调⽤）
render() // ⽣成组件虚拟Dom
componentWillUnmount() // 组件卸载时调⽤
```

#### React16

```js
constructor() // 构造函数
getDerivedStateFromProps() // 组件初始化和更新时调⽤
shouldComponentUpdate() // 组件更新时调⽤，在此可拦截更新
render() // ⽣成虚拟Dom
getSnapshotBeforeUpdate() // 组件更新时调⽤
componentDidMount() // 组件初始化时调⽤（挂载后调⽤）
componentDidUpdate(prevProps, prevState) // 组件更新后调⽤
componentWillUnmount() // 组件卸载时调⽤
```

#### constructor 

实例过程中⾃动调⽤，⽅法内部通过super关键字获取⽗组件的props 

通常初始化state或者this上挂载⽅法

#### static getDerivedStateFromProps(nextProps, prevState)

静态⽅法(纯函数) 

执⾏时机：组件创建和更新阶段，不论是props变化还是state变化，都会调⽤ 

在每次render⽅法前调⽤，第⼀个参数为即将更新的props，第⼆个参数为上⼀个状态的 state，⽐较props 和 state来加⼀些限制条件，防⽌⽆⽤的state更新 

该⽅法返回⼀个新对象作为新的state或者返回null表⽰state状态不需要更新

#### getSnapshotBeforeUpdate(prevProps, prevState) 

该周期函数在render后执⾏，执⾏之时DOM元素还没有被更新 该⽅法返回⼀个Snapshot值，作为componentDidUpdate第三个参数传⼊

⽬的在于获取组件更新前的信息，⽐如组件的滚动位置之类的，在组件更新后可以根据这些 信息恢复UI视觉上的状态

#### componentDidMount

 组件挂载到ADOM节点后执⾏，在render之后执⾏，执⾏⼀些数据获取，事件监听等操作 

#### shouldComponentDidMount 

告知组件本⾝基于当前的props和state是否需要重新渲染组件，默认情况返回true。 执⾏时机：到新的props或者state时都会调⽤，通过返回true或者false告知组件更新与否 ⼀般情况，不建议在该周期⽅法中进⾏深层⽐较，会影响效率 同时也不能调⽤setState，会导致⽆限循环 

#### componentDidUpdate 

执⾏时机：组件更新结束后触发 

在该⽅法中，可以根据前后的props和state的变化做相应的操作，如获取数据，修改DOM样 式等

#### componentWillUnmount 

组件卸载前，清理⼀些注册或监听事件，或者取消订阅的⽹络请求 ⼀旦⼀个组件实例被卸载，其不会被再次挂载，只可能被重新创建



## React Router

客户端路由 实现原理 

+ 基于hash 路由，监听hashchange 事件，location.hash=xxxx 改变路由 

+ 基于H5的 history，通过history，pushState 和 replaceState 修改URL，能应⽤ history.go() 等 API，允许通过 ⾃定义事件 触发实现

react-router实现原理： 

基于 history 库实现，可 保存 浏览器 历史记录 

维护列表，每次回收URL发⽣变化的回收，通过配置的路径，匹配对应的 Component 并 render

获取URL参数 

+ get ⽅法 this.props.location.search 获取 URL 得到字符串，解析参数，或者⾃⼰封装⽅法获取参数 
+ 动态路由传值 如 path='/admin/:id'，this.props.match.params.id 获取 URL中动态部分路由 id值，或者使 ⽤hooks的 API获取 
+ query 或 state传值 组件 的 to属性可以传递对象 {pathname:'/admin',query:'111',state:'111'}， this.props.location.state或 this.props.location.query 获取，⼀旦刷新页⾯ 数据丢失



## Hooks

Hooks好处 

+ 跨组件复⽤，轻量，改造成本⼩，不影响原来组件层级结构和嵌套地狱 
+ hook没⽣命周期，class有（hook可以使⽤钩⼦函数模仿⽣命周期） 
+ 状态与UI隔离，状态逻辑粒度更⼩，可以把业务逻辑抽离出来做⾃定义hook hook缺点 状态不同步，容易产⽣闭包，需要使⽤useRef去记录

hook缺点 : 状态不同步，容易产⽣闭包，需要使⽤useRef去记录

为啥useState使⽤数组

解构赋值！！

解决问题 

+ 组件间逻辑复⽤ 
+ 复杂组件理解 
+ 难以理解的class 

使⽤限制

+ 不再循环、条件和嵌套函数中调⽤(链表 实现Hook，可能导致 数组取值错位) 

+ 仅在函数组件中调⽤hook(因为没有 this) 

useLayoutEffect和useEffect

 共同点 都是处理副作⽤，包括 DOM改变，订阅设置，定时器操作 

不同点 useEffect异步调⽤，按顺序执⾏，屏幕像素改变后执⾏，可能会闪烁 useLayoutEffect在所有DOM变更后同步调⽤，处理 DOM操作，样式调整；改变屏幕像素 之前执⾏(会推迟页⾯显⽰的时间，先改变DOM后渲染)，不会闪烁，总是⽐ useEffect先执 ⾏！ 

useLayoutEffect 和 componentDidMount，componentDidUpdate 执⾏时机⼀样，在浏览 器将所有变化渲染到屏幕之前执⾏ 

建议使⽤ useEffect！建议使⽤ useEffect！建议使⽤ useEffect！ 避免阻塞视觉更新 页⾯有异常就再替换为 useLayoutEffect



### 有状态组件和⽆状态组件

有状态组件 特点 

+ 是类组件 
+ 有继承 
+ 有this 
+ 有⽣命周期 
+ 使⽤较多，易触发⽣命周期钩⼦函数 
+ 内部使⽤state，根据外部组件传⼊的props和⾃⾝state渲染

使⽤场景： 需要使⽤状态的 需要状态操作组成的

⽆状态组件 特点 

+ 不依赖⾃⾝state 
+ 可以是类组件或函数组件 
+ 可避免使⽤this 
+ 组件内部不维护state，props改变，组件re-render 

使⽤场景 组件不需要管理state

优点 简化代码 专注render 组件不需要实例化，⽆⽣命周期 视图和数据解耦



### 受控组件和非受控组件

受控组件 

表单状态变化，触发onChange事件，更新组件state 受控组件中，组件渲染出的状态和它的value或checked属性相对应，react通过这种⽅式消 除了组件的局部状态，使组件变得可控 

缺点 多个输⼊框需要获取到全部值时，需要每个都编写事件处理函数，代码变得臃肿 后来，出现了⾮受控组件 

⾮受控组件 

表单组件没有value props 可使⽤ref 从 DOM 中获取表单值，⽽不是编写事件处理函数 使⽤⾮受控组件可以减少代码量 合成事件 充当浏览器原⽣事件的跨浏览器包装器 的对象 将不同浏览器⾏为组合到⼀个 API中，确保事件显⽰⼀致的 属性

