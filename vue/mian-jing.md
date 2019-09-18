#### 1 MVVM

**Model** 数据模型 **View** UI组件

**ViewModel** 监听模型数据的改变和控制视图行为、处理用户交互 双向数据绑定

#### 2 生命周期

**beforeCreate**

**created**  完成数据观测 属性和方法的运算 初始化事件 el未挂载

**beforeMount **render函数 编译模版 data生成html

**mounted** el被vm.$el替代 ajax交互

**beforeUpdate updated beforeDestroy destoryed**

#### 3 双向数据绑定原理 Object.defineProperty\(\)

**数据劫持** 结合 **发布者-订阅者模式 **

#### 4 组件间传值

1. **父子组件** **props** **$emit**
2. **兄弟组件** **eventBus vueX**

**eventBus **引入新的vue实例 分别调用事件触发和监听来实现通信和参数传递

[借鉴](https://segmentfault.com/a/1190000013636153?utm_source=tag-newest)   [https://segmentfault.com/a/1190000013636153?utm\_source=tag-newest](https://segmentfault.com/a/1190000013636153?utm_source=tag-newest)

#### 5 路由 hash history

**hash**

**\#** **\#后面的字符** **window.location.hash**读取

请求只有\#之前的内容 所以路由即使没有全覆盖也不会返回404

**history  **

**H5 pushState\(\)** **replaceState\(\) **修改浏览器历史记录栈 以及popState事件的监听到状态变更

前端和后端url要保持一致  实现路由全覆盖

#### 6 vue路由的钩子函数

**beforeEach**

**to** 目标路由 **from** 当前路由 **next**

**afterEach**

#### 7 vueX

**store**  只读状态 一个应用一个store

**mutations**  改变状态 动态修改store中的状态或数据

**getter  **过滤数据

**action**  将mutations里面的方法变为异步

**modules  **可以让每一个模块有自己的state等

#### 8 vue-cli新增自定义指令

#### 9 自定义过滤器

#### 10 keep-alive

**include** 缓存 **exclude** 不缓存 优先级高

