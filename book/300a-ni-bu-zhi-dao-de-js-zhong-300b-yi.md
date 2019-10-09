## 1

#### 类型 七种

string    boolean    number    null（假值）    undefined    object（function）    symbol

typeof    string    boolean    uumber    "object"    undefined    object（function）    symbol

typeof返回字符串

未声明是undeclared

声明未赋值是undefined

## 2

#### 数组

可以存放任何类型 不需要预设大小  delete可以删除单元值 但并不影响数组长度

类数组 转化为数组 slice\(\)  Array.from\(\)

字符串 获取字符 chatAt（）

字符串不可变是不会改变原始值 而是创建返回新数组  而数组成员则是在其原始值上操作

借用数组

Array.prototype.join.call\(a, "-"\);

Array.prototype.map.call\(a, function\(\){

return v.toUpperCase\(\) + ".";

\)}.join\(""\);

字符串反转 var c= a.split\(""\).reserve\(\).join\(""\);

#### 数字

prototype.tofixed\(\) 指定小数点后显示位数 四舍五入

prototype.toPrecision\(\) 有效数位显示位数

注意：“.”是有效数字运算符 所以 42.tofixed\(\)不成立 要42..tofixed\(\)才可得42

Number.EPSILON误差范围 机器精度

整数检测 Number.isInteger\(..\)方法

特殊

null 空 undefined 未定义 NaN 非自反 isNaN 检查

无穷数 -Infinity

特殊等式 Object.is\(..\)判断两值是否绝对相等 == ===效率更高

值和引用 简单值 6个基本类型

复合值 对象 函数 引用赋值

## 3

#### 原生函数

String\(\) Number\(\) Boolean\(\) Array\(\) Object\(\) Function\(\) RegExp\(\) Date\(\) Error\(\) Symbol\(\)  所有typeof返回值均为object

new创建的是基本封装对象

内部属性class 无法直接访问 可以通过 Object.prototype.toString.call\(\[1,2,3\]\); \|\| "\[object.Array\]"

封装对象包装 js自动为其封装

拆封 1）valueOf\(\) 函数 2）使用到的地方会隐形拆封

原生函数作为构造函数

* Array Object Function 不建议

* RegExp\(\) 动态创建正则可使用 （常用）

* Date\(\) 只能new 参数为事件 默认为当前unix时间戳 Date.now\(\)

* Error\(\)

* Symbol\(\) 符号 唯一性 不加new

原生原型 function是空函数 RegExp\(\)是空正则 Array是空数组可修改

## 4

#### 强制类型转换

显示 隐式（强制）

ToString JSON.stringify\(\);  字符串化

toJSON\(\)要JSON安全 不安全的JSON undefined function symbol 包含循环引用的对象（会自动忽略）

ToNumber true- 1 false- 0 undefined- NaN  null- 0  对以0开头的十六进制数按照十进制处理！

ToBoolean

假值 undefined null false +0 -0 NaN "" 强制转换结果为false

假值对象 自己创建的外来值

真值 假值列表以外的值

**显示类型转换**

字符串和数字之间的转换 通过String\(\) Number\(\)两个内建函数来实现 还可以通过toString\(\) +号 ～字位操作“非”

parseInt\(\) 第一个参数接收字符串 第二个参数接收进制数

剩下的 一些特例和一些奇怪的字符识别的特例 就不写了 记不住的

**隐式转换**

字符串和数字 “+” 如果有一方是字符串则进行拼接操作 如果是数字则进行相加操作

\|\| &&操作数选择器择一返回 “短路”操作

宽松相等 == （允许强制类型转换） 严格相等 === （不允许强制类型转换）

NaN != NaN 唯一的自反 +0 = -0 对象指向同一个值视为相等

数字==字符串 字符串ToNumber\(\)转换成数字

其他类型和布尔类型 总是布尔转换成数字 true - 1 false - 0

null == undefined 结果为true 视为同一个东西

对象和非对象 总是ToPrimitive\(\) 调用valueOf\(\) 再调用toString\(\)

避免出错 true flase \[\] "" 0 尽量不用==

## 5

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

## 6

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

## 7

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

