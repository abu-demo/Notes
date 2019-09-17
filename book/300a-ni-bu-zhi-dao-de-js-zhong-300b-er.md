## 1

#### 事件循环

每一轮微一个**Tick**

主任务**栈** 函数调用形成**栈针**一次压栈 待处理事件形成**队列** 期间的对象分配在**堆**内存中

队列 微任务 nextTick callback promise process.nextTick 宏任务 settimeout setInterval IO sprit代码块

#### 回调

* 不够直观难以追踪

* 受控制反转影响 控制权交给第三方 来调用continuation 会导致一系列得麻烦

#### **Promise**

决议P控制 一旦决议 不可逆转

判断是都是promise 具有then\(\)方法的对象和函数 鸭子类型

Promise信任问题

* 调用过早

* 调用过晚 根据Promise决议来控制接下来的调用 所以 早晚都没有影响

* 回调未调用 成功或者失败都会有一个回调 如果未决议设置定时器 保证其不会永久挂住 至少有一个输出信号

* 调用次数过多或者过少 Promise只决议一次 如果注册了多次 那就和注册次数相同

* 未能传参 如果没有任何显式决议 那这个值就是undefined

* 吞掉错误 或 异常 导致return的Promise被拒绝 所以下面的Promise无法继续执行

链式流

return 创建一个Promise 如果返沪i一个Promise 将展开作为下一个.then\(\)的决议 如果不是 则会对其相应resolve\(\)

错误处理

异步执行的函数里面的错误没有捕捉

解决： - 定义定时器 Err时触发 限时内未处理 则警告 缺点 限制时长随意 而且有的时候允许异常存在

* 利用浏览器垃圾回收机制 判断 - defer\(\)

Promise 模式

Promise.all\[\] 门 控制数组中所有决议完成 才会运作后面的 传空值会立即完成

Promise.race\[\] 决议结果为数组中响应最快的 传空永不决议

建议finally 执行Promise超时了也要执行的事情 还要返回一个Promise 继续执行链接

变体 none\[\] 全部拒绝  any\[\] 忽略拒绝 只要有一个完成就可以 first\[\]第一个 last\[\] 最后一个

并发迭代 对所有Promise执行某个任务

Promise API

new Promise\(\) 构造器 必须和new一起使用 必须有回调函数

Promise.resolve\(\) Promise.reject\(\) then\(\) catch\(\) Promise.all\[\] Promise.race\[\]

**Promise局限性**

* 顺序错误处理 - 单一值 - 单决议 - 惯性 - 无法取消的Promise 

#### **生成器**

yield 暂停 打破函数完整性运行

迭代器 有next\(\)方法 iterable可以在其之上进行迭代的对象

iterable必须支持一个函数 \[Symbol.iterable\]:function\(\){ return this};

用it.next\(\) 迭代器控制 第一次的next\(\)启动生成器 无参

**异步迭代生成器**

把异步的代码堪称看似同步 通过生成器 yield的配合 可以在每一个异步结果查看其值 并捕捉Error

**Promise + 生成器**

yield 处一个Promise 然后通过Promise控制生成器的迭代器 继续进行下一个判断 辅助函数 Generator Runner

生成器中的Promise并发 可以利用Promise.all\[\]等 实现并发操作

**生成器委托**

消息委托 双向消息传递

异步委托 yield \*function\(\)

递归委托 可以使用yield委托实现异步的生成器递归 即一个yield委托到它自身的生成器

生成器并发 协调控制转移 彼此通信  “通信顺序进程CSP”

#### 程序性能

webworker 任务并行

Worker 之间以及它们和主程序之间，不会共享任何作用域或资源

var w1 = new Worker\( "[http://some.url.1/mycoolworker.js](http://some.url.1/mycoolworker.js)" \);

互相传送消息  一对一的关系 worker可以有子worker 叫subworker

```js
addEventListener( "message", function(evt){
// evt.data
} );
postMessage( "a really cool reply" );
```

中止worker  w1.terminate\(\);

worker环境

* worker内部无法访问主程序的任何资源 完全独立的线程

* 可以执行网络操作（Ajax、 WebSockets）以及设定定时器

* 可以访问几个重要的全局变量和功能的本地复本，包括 navigator、 location、 JSON 和 applicationCache

* 通过 importScripts\(..\) 向 Worker 同步加载额外的 JavaScript 脚本

数据传递

* 早期通过把数据序列化到一个字符串中进行传递 出了序列化导致的速度损失 还有被复制造成的双倍内存损失

* 现在 如果传递一个对象 可以使用“结构化克隆算法”  甚至可以处理对象有循环引用的情况 还是要双倍内存

* 对于大数据集 可以使用Transferable对象 对象所有权转移 数据没有移动

#### 共享worker

SharedWorker 所有页面共享的中心worker 唯一标识符 端口 port

端口初始化 w1.port.start\(\);

带端口传递信息

w1.port.addEventListener\( "message", handleMessages \);

w1.port.postMessage\( "something cool" \);

connect 为特定连接提供端口对象 函数内部

#### SIMD

单指令多数据 数据并行 利用低级指令级并行的底层运算

#### asm.js

JavaScript语言中可以高度优化的一个子集

