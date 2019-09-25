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



