总结了几个 `Vue` 常见的问题：


### vue2.0组件的通信方式有哪些？

- ⽗⼦组件通信：`props` 和 `event`、`v-model`、 `.sync`、 `ref`、 `$parent` 和 `$children`

- ⾮⽗⼦组件通信：`$attr` 和 `$listeners`、 `provide` 和 `inject`、`eventbus`、通过根实例`$root`访问、`vuex`、`dispatch` 和 `brodcast`


### v-model是如何实现双向绑定的？

- 2.0 v-model 是⽤来在表单控件或者组件上创建双向绑定的，他的本质是 v-bind 和 v-on 的语法糖，在⼀个组件上使⽤ v-model ，默认会为组件绑定名为 `value` 的 prop 和名为 `input` 的事件。

### Vue 的⽗组件和⼦组件⽣命周期钩⼦执⾏顺序是什么？

- ⽗组件挂载完成⼀定是等⼦组件都挂载完成后，才算是⽗组件挂载完，所以⽗组件的mounted在⼦组件mouted之后

    ⽗ `beforeCreate` -> ⽗ `created` -> ⽗ `beforeMount` -> ⼦ `beforeCreate` -> ⼦ `created` -> ⼦ `beforeMount`-> ⼦ `mounted` -> ⽗ `mounted`

### v-show 和 v-if 有哪些区别？

- v-if 会在切换过程中对条件块的事件监听器和⼦组件进⾏销毁和重建，如果初始条件是false，则什么都不做，直到条件第⼀次为true时才开始渲染模块。

- v-show 只是基于css进⾏切换，不管初始条件是什么，都会渲染。

- 所以， v-if 切换的开销更⼤，⽽ v-show 初始化渲染开销更⼤，在需要频繁切换，或者切换的部分dom很复杂时，使⽤ v-show 更合适。渲染后很少切换的则使⽤ v-if 更合适。

### computed 和 watch 有什么区别？

- computed 计算属性，是依赖其他属性的计算值，并且有缓存，只有当依赖的值变化时才会更新。
- watch 是在监听的属性发⽣变化时，在回调中执⾏⼀些逻辑。
- 所以， computed 适合在模板渲染中，某个值是依赖了其他的响应式对象甚⾄是计算属性计算⽽来，⽽ watch 适合监听某个值的变化去完成⼀段复杂的业务逻辑。

### Object.defineProperty有哪些缺点？

- 1. Object.defineProperty 只能劫持对象的属性，⽽ Proxy 是直接代理对象
    由于 Object.defineProperty 只能对属性进⾏劫持，需要遍历对象的每个属性。⽽ Proxy 可
    以直接代理对象。

- 2. Object.defineProperty 对新增属性需要⼿动进⾏ Observe ， 由于
    Object.defineProperty 劫持的是对象的属性，所以新增属性时，需要重新遍历对象，对其新
    增属性再使⽤ Object.defineProperty 进⾏劫持。 也正是因为这个原因，使⽤ Vue 给 data
    中的数组或对象新增属性时，需要使⽤ vm.$set 才能保证新增的属性也是响应式的。

- 3. Proxy ⽀持13种拦截操作，这是 defineProperty 所不具有的。

- 4. 新标准性能红利,Proxy 作为新标准，⻓远来看，JS引擎会继续优化 Proxy ，但 getter 和 setter 基本不会再
    有针对性优化。

- 5. Proxy 兼容性差 ⽬前并没有⼀个完整⽀持 Proxy 所有拦截⽅法的Polyfill⽅案

### v-for 中 key 的作⽤是什么？

- key 是给每个 vnode 指定的唯⼀ id ，在同级的 vnode diff 过程中，可以根据 key 快速的对⽐，来判断是否为相同节点，并且利⽤ key 的唯⼀性可以⽣成 map 来更快的获取相应的节点。另外指定 key 后，就不再采⽤“就地复⽤”策略了，可以保证渲染的准确性。

### 为什么 v-for 和 v-if 不建议⽤在⼀起

- 当 v-for 和 v-if 处于同⼀个节点时， v-for 的优先级⽐ v-if 更⾼，这意味着 v-if 将分别重复运⾏于每个 v-for 循环中。如果要遍历的数组很⼤，⽽真正要展示的数据很少时，这将造成很⼤的性能浪费。这种场景建议使⽤ computed ，先对数据进⾏过滤。

### Vue的性能优化方面

- 编码阶段
    尽量减少data中的数据，data中的数据都会增加getter和setter，会收集对应的watcher
    v-if和v-for不能连⽤
    如果需要使⽤v-for给每项元素绑定事件时使⽤事件代理
    SPA ⻚⾯采⽤keep-alive缓存组件
    在更多的情况下，使⽤v-if替代v-show
    key保证唯⼀
    使⽤路由懒加载、异步组件
    防抖、节流
    第三⽅模块按需导⼊
    ⻓列表滚动到可视区域动态加载
    图⽚懒加载

- SEO优化
    预渲染
    服务端渲染SSR

- 打包优化
    压缩代码
    Tree Shaking/Scope Hoisting
    使⽤cdn加载第三⽅模块
    多线程打包happypack
    splitChunks抽离公共⽂件
    sourceMap优化
    
- ⽤户体验
    ⻣架屏
    PWA
    
- 还可以使⽤缓存(客户端缓存、服务端缓存)优化、服务端开启gzip压缩等。