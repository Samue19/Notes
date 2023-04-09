# vue

声明式框架

MVVM模式，

虚拟DOM

区分编译时和运行时

组件化



### 双向绑定

双向绑定等于 响应式+事件监听

`Object.defineProperty(obj, prop, descriptor)`：会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。

```js
Object.defineProperty(obj, prop, {
    configurable: true,		// 可修改
    enumerable: true,		// 可枚举
    value: undefined,
    writable: true,			// 可写
    get() {
        return value;
    },
    set(newVal) {
        value = newVal;
    },
})
```

`new Proxy(target, handler)`：创建一个对象的代理，从而实现基本操作的拦截和自定义（如属性查找、赋值、枚举、函数调用等）。

`Reflect`:  是一个内置的对象，它提供拦截 JavaScript 操作的方法。这些方法与 [proxy handler (en-US)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy) 的方法相同。`Reflect` 不是一个函数对象，因此它是不可构造的。

```js
new Proxy(obj, {
    get: function (target, propKey, receiver) {
      return Reflect.get(target, propKey, receiver);
    },
    set: function (target, propKey, value, receiver) {
      return Reflect.set(target, propKey, value, receiver);
    },
  });
```



### Vue生命周期

+ beforeCreate：data 和 methods 未初始化
+ created：data，methods 初始化完成，DOM未挂载渲染
+ beforeMount：数据的 双向绑定还是显⽰{{}}
+ mounted：vue实例完成初始化，挂载渲染到页面
+ beforeUpdate：数据已更新，DOM未更新
+ update：避免在这个阶段改变状态，避免无限循环
+ beforeDestory：vue实例可用
+ destoryed：vue实例销毁，事件监听器被移除



```js
// mapping vue2 to vue3
beforeCreate -> use setup()
created -> use setup()
beforeMount -> onBeforeMount
mounted -> onMounted
beforeUpdate -> onBeforeUpdate
updated -> onUpdated
beforeDestory -> onBeforeUnmount
destroyed -> onUnmounted
activated -> onActivated
deactivated -> onDeactivated
errorCaptured -> onErrorCaptured
// added
onRenderTracked
onRenderTriggered
```



### 组件通信





父子通信,ref

数据懒加载

loading加载,



### computed，watch

computed：有缓存，不⽀持异步监听

watch： ⽆缓存，⽀持异步监听



### vue2 和 vue3 的区别

性能提升，Composition API，更好的ts支持

ref, computed, reactive, toRefs



### Vue-Router

https://juejin.cn/post/6890853087880970248

前端路由：不同路由对应不同页面
vue-router：将url和页面映射
hash，history模式
$router的push，replace对应history的replaceState，pushSate

调用 history.pushState() 或者 history.replaceState() 不会触发 popstate 事件。popstate 事件只会在浏览器某些行为下触发，比如点击后退按钮（或者在 JavaScript 中调用 history.back() 方法）。即，在同一文档的两个历史记录条目之间导航会触发该事件。

#### 源码

1. 首先会对重复安装进行过滤

2. 全局混入beforeCreate和destroyed 生命钩子，为每个Vue实例设置 _routerRoot属性，并为跟实例设置_router属性

3. 调用Vue中定义的defineReactive对_route进行劫持，其实是执行的依赖收集的过程，执行_route的get就会对当前的组件进行依赖收集，如果对_route进行重新赋值触发setter就会使收集的组件重新渲染，这里也是路由重新渲染的核心所在

4. 为Vue原型对象定义router和route属性，并对两个属性进行了劫持，使我们可以直接通过Vue对象实例访问到
5. 全局注册了Routerview和RouterLink两个组件，所以我们才可以在任何地方使用这两个组件，这两个组件的内容我们稍后分析

```js
  Vue.mixin({
    beforeCreate () {
      if (isDef(this.$options.router)) { // 设置根路由-根组件实例
        this._routerRoot = this
        this._router = this.$options.router
        this._router.init(this)
        // 定义响应式的 _route 对象
        Vue.util.defineReactive(this, '_route', this._router.history.current)
      } else { // 非根组件设置
        this._routerRoot = (this.$parent && this.$parent._routerRoot) || this
      }
      registerInstance(this, this)
    },
    destroyed () {
      registerInstance(this)
    }
  })
 Object.defineProperty(Vue.prototype, '$router', {
    get () { return this._routerRoot._router }
  })

  Object.defineProperty(Vue.prototype, '$route', {
    get () { return this._routerRoot._route }
  })
```

#### RouterView 和 RouterLink

RouterView

是无状态(没有 data ) 和无实例 (没有 this 上下文)的函数式组件。用一个简单的render函数返回虚拟节点使他们更容易渲染。

渲染的组件还可以内嵌，根据嵌套路径，渲染嵌套组件。

 类似一个占位插槽，并不会渲染本身DOM模板，而是根据自身所在嵌套层级以及的render函数的第二个参数作为参数，匹配当前路由(route===route === route===router.history.current)的嵌套层级matched，然后再用已匹配的matched的components中找到和RouterView name相同的组件。并渲染对应匹配到的组件，否则渲染空组件

RouterLink

相比，是一个普通的非抽象组件，通过router的resolve方法解析自身的to属性参数，并调用$router.push或者replace方法进行路由跳转。



#### 导航守卫执行顺序

1.导航被触发。
2.在失活的组件里调用离开守卫。
3.调用全局的 beforeEach 守卫。
4.在重用的组件里调用 beforeRouteUpdate 守卫 (2.2+)。
5.在路由配置里调用 beforeEnter。
6.解析异步路由组件。
7.在被激活的组件里调用 beforeRouteEnter。
8.调用全局的 beforeResolve 守卫 (2.5+)。
9.导航被确认。
10.调用全局的 afterEach 钩子。
11.触发 DOM 更新。
12.用创建好的实例调用 beforeRouteEnter 守卫中传给 next 的回调函数。

#### 优缺点

优点

+ 良好的交互体验,用户不需要刷新页面,页面显示流畅；
+ 良好的前后端工作分离模式,减轻服务器压力
+ 完全的前端组件化，便于修改和调整

缺点

+ 首次加载大量资源，加载时间相对比较长；
+ 不利于 SEO





### 构建篇

+ 使用的一些 npm 包名为什么要用 `@` 开头？
+ 除了介绍的 `browserslist` 这样的配置项可以写在单独的文件中外，还有哪些常用的配置项可以这样操作？又是如何配置的？
+ Vue CLI 3 还集成了哪些包，可以通过 `vue add` 命令安装？
+ `vue.config.js` 中还有哪些额外的配置？
+ `webpack-merge` 的合并原理是怎样的？
+ 使用 `chainWebpack` 获取到 webpack 中的某一插件后，如何修改其配置？
+ webpack 通过 DefinePlugin 内置插件将 process.env 注入到客户端代码中时，`process.env.NODE_ENV` 为什么要进行 JSON.stringify 处理？
+ `process.env` 中如何获取 package.json 中 name 的值？
+ 如何在 package.json 中的 scripts 字段中定义一些自定义脚本来切换不同的环境？























