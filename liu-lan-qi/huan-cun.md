> 原文链接：[https://github.com/ljianshu/Blog/issues/23](https://github.com/ljianshu/Blog/issues/23)

## 缓存位置

#### Service Worker

* 运行在浏览器背后的独立线程 
* 传输协议必须为**https** 因为涉及请求拦截 所以必须适应https协议来保障安全 
* 可以**自由控制**缓存哪些文件、如何匹配缓存、如何读取缓存 并且缓存是持续性的

实现缓存 先**注册**service worker 然后**监听**到install事件以后就可以缓存需要的文件 下次请求进行拦截 如果命中 直接读取 

没有命中 调用fetch函数获取数据 根据**缓存查找优先级**去查找数据 但是不管是从memory cache 还是从网络请求中获取的数据 都会显示是从service worker中获取的数据

#### Memory Cache

内存中的缓存 主要包含当前页面中已经抓去







