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

* 空行
* 响应体

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



