> 原文链接：[https://github.com/ljianshu/Blog/issues/45](https://github.com/ljianshu/Blog/issues/45)

#### 1 AJAX

不需要重新刷新页面 通过异步请求加载后台数据 并呈现 提高用户体验 减少网络数据的传输量

#### 2 原理

核心是依赖浏览器提供的XMLHttpRequest对象 使浏览器可以发出HTTP请求与接受HTTP响应

#### 3 应用

```js
//创建ajax核心对象XMLHttpRequest（考虑兼容性）
var xhr = null;
if(window.XMLHttpREequest){  // 兼容 IE7+ Firefox Chrome Opera Safari
xhr = new XMLHttpRequest();
} else{ //兼容 IE6,IE5
xhr = new ActiveXObject("Microsoft.XMLHTTP");
}

//向服务器发送请求
xhr.open(method, url, async);
send(string); //post请求时才使用字符串参数 否则不用带参数

//实例 post注意请求头的格式内容
xhr.open("POST","text.html",true);
xhr.setReuqestHeader("Content-type","application/x-www-form-urlencoded");
xhr.send("fname=Henry&lname=Ford");

//responseText 同步处理
xhr.open("GET","info.txt",false);  
xhr.send();  
document.getElementById("myDiv").innerHTML=xhr.responseText;

//response 异步处理
 xhr.onreadystatechange=function()  { 
 if (xhr.readyState==4 &&xhr.status==200)  { 
 document.getElementById("myDiv").innerHTML=xhr.responseText;  }} 
```

##### readState

标识当前XMLHttpRequest对象处于什么状态 5个状态值 0-4 

* 0：未初始化 -- 尚未调用.open\(\)方法；
* 1：启动 -- 已经调用.open\(\)方法，但尚未调用.send\(\)方法；
* 2：发送 -- 已经调用.send\(\)方法，但尚未接收到响应；
* 3：接收 -- 已经接收到部分响应数据；
* 4：完成 -- 已经接收到全部响应数据，而且已经可以在客户端使用了；

##### state http状态码





