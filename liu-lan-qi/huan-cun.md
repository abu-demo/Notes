> 原文链接：[https://github.com/ljianshu/Blog/issues/25](https://github.com/ljianshu/Blog/issues/25)

## Cookie

cookie 的本职工作 并非本地存储 而是“维持状态” 因为HTTP是无状态的 不对请求和响应之间的通信状态进行保存

cookie为了辨别用户身份 在第一次请求服务端生成 然后 存储在客户端 上加密过的数据 以键值对的形式存在

#### 原理

第一次访问网站 浏览器发出请求 服务端响应后 在响应头添加一个set-cookie选项 将cookie放入响应请求中 在浏览器第二次发请求的时候 会通过cookie请求头部 将cookie信息发送给服务器 服务器会辨别用户身份 另外 cookie的过期时间、域、路径、有效期、适用站点都可以根据需要来指定

#### 生成方式：

* **生成方式一**：http response header 中的set-cookie

domain被设置为设置cookie页面的主机名 我们也可以手动设置domain的值

```js
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2018 07:28:00 GMT;//可以指定一个特定的过期时间（Expires）或有效期（Max-Age）
```

当cookie的过期时间被设定时 。设定的日期和时间只与客户端有关 而不是服务端 如果不设定 默认为关闭窗口的时候

* **生成方式二**：js中可以通过document.cookie可以读写cookie 以键值对的形式展示

```js
document.cookie="userName = hello;domain = .coolqb.top" //domain 为域名限制
```

#### 缺陷

* **不够大** cookie的大小限制（一个name）在**4KB**左右 超过4K会被裁切 浏览器对cookie的个数也是有限制的
* **过多的cookie**会造成巨大的性能浪费 同一个域名下的所有请求都会携带cookie发送！！
* HTTP请求中的cookie是明文传输的 有**安全性**的问题

#### 安全

| 属性 | 作用 |
| :--- | :--- |
| value | 保存用户登录状态 应加密保存 |
| http-only | 不能通过js访问cookie 减少XSS攻击 |
| secure | 只能在协议为HTTPS的请求中携带 |
| same-site | 不能在跨域请求中携带cookie 减少CSRF攻击 |

## Web Storage

只能存储字符串

#### 1 LocalStorage

**特点**

* 保存期很长 
* 大小为5M
* 仅在客户端使用 
* 借口封装较好
* 要相同的协议、主机名、端口下
* 操作是同步的

**存取数据**

以键值对形式存在 以文本格式保存

```js
localStorage.setItem("key","value"); //存入数据 两个参数 一个是键名 一个是保存的数据
```

```js
var localValue = localStorage.getItem("key"); //读物数据
```

#### 2 sessionStorage

**特点**

* 会话级别的浏览器存储
* 大小为5M左右
* 仅在客户端使用
* 接口封装较好
* 要在相同的协议、主机名、端口、窗口下

基于以上特点 sessionStorage 可以有效对表单信息进行维护 比如刷新 信息不会丢失

**使用场景**

存储生命周期和它同步的会话级别的信息 

## IndexedDB

用于客户端存储大量结构化数据（包括文件和blobs） 运行在浏览器上的非关系型数据库 没有存储上线（不小于250M）不仅可以存储字符串 还可以存储二进制数据

**特点**

* **键值对存储** 对象仓库（object store）存放数据** 所有类型**的数据可以直接存入 包括js对象 主键不能重复
* **异步** 操作不会死锁浏览器 
* **支持事务** 数据操作失败可以回滚到之前状态 不回出现只处理了一半的情况
* **同源限制** 每一个数据库对应创建它的域名 不能跨域
* **存储空间大 **
* **支持二进制存储** 

##### 常见操作





