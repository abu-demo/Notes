## HTTP协议

超文本传输协议 基于 TCP/IP协议

#### 特点

* 简单快速
* 灵活
* 无连接
* 无状态

## HTTP报文

#### 请求报文

* ##### 请求行 request line

```js
POST /chapter7/user.html HTTP/1.1
//请求方法  GET HEAD POST PUT DELETE
//URI 
//协议和协议版本
```

> ##### GET 和 POST的区别
>
> GET  回退无害  浏览器主动缓存  参数保存在浏览器历史记录里 URL长度有限制所以参数有限制
>
> POST 回退会再次提交请求 不会主动缓存 参数不会保留 没有限制 请求两次

* ##### 请求头 header

```js
HOST: coolqb.top  //主机名 虚拟主机 域名 DNS解析为IP地址
Connection: keep-live //长连接
User-Agent: //请求发出着 兼容性以及定制化需求
```

* ##### 空行 表示请求头已经结束
* ##### 请求体

```js
name=tom&password=1234&realName=tomson //参数
```

#### 响应报文

* ##### 响应行

```js
HTTP/1.1 200 OK
//协议 状态码 说明短语
```

* ##### 响应头

```js
Server: Apache
Last-Modified: Fri, 31 Aug 2007 02:02:20 GMT
ETag: "45bael-16a-46d776ac"
Accept-Ranges: bytes
Content-Length: 362
Connect: close
Conetnt-Type: text/html
```

* ##### 空行
* ##### 响应体

```js
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>hackr.jp</title>
</head>
<body>
<img src="hackr.gif" alt="hackr.jp" width="240" height="84" />
</body>
</html>
```

#### 请求方法

* GET 请求指定的页面信息，并返回实体主体。
* HEAD 类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头
* POST 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。
* PUT 从客户端向服务器传送的数据取代指定的文档的内容。
* DELETE 请求服务器删除指定的页面。

#### 状态码

##### 1 消息 已被接受 需要继续处理 

* 100 Continue 客户端应当继续发送请求 

##### 2 成功 已成功被服务器接收、理解、并接受

* 200 OK 表示正常状态
* 201 Created 请求已经被实现 而且有一个新的资源已经依据请求的需要而建立
* 202 Accepted 服务器已经接受 但尚未处理 可能会也可能不会被执行
* 204 NoContent 服务器成功处理了请求 但不需要返回任何实体内容 

##### 3 重定向 客户端需要采取进一步操作才能完成请求

* 300 Multiple Choices 有一系列可供选择的回馈信息 自行选择一个首选的地址进行重定向
* 301 Moved Permanently 被请求资源已永久移动到新位置
* 302 Move Temporarily 请求的资源临时从不同的URI响应请求
* 303 See Other 对应当前请求的响应可以在另一个URL上找到
* 304 Not Modified 文档未过期 禁止包含消息体
* 305 Use Proxy 被请求的资源必须通过指定的代理才能被访问
* 307 Temporary Redirect 请求的资源临时从不同的URI响应请求

##### 4 请求错误 客户端错误

* 400 Bad Request 语义有误 无法被服务器理解 或者 请求参数有误
* 401 Unauthorized 需要用户验证 
* 402 Payment Required 位了将来可能的需求预留的
* 403 Forbidden 服务器理解请求 但是拒绝执行
* 404 Not Found 请求失败 服务器上未找到
* 405 Method Not Allowed 请求行中指定的请求方法不能被用于请求相应的资源
* 406 Not Acceptable 请求的资源特性无法满足请求头中的条件 因而无法生成响应体
* 407 Proxy Authentication Required 与401类似 只不过客户端必须在代理服务器上进行身份验证
* 408 Request Timrout 请求超时
* 409 Conflict 被请求资源的当前状态之间存在冲突 
* 410 Gone 资源已经不可用







