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
HOST: coolqb.top:8080  //主机名 虚拟主机 域名 DNS解析为IP地址
Connection: keep-live //表示是否需要持久连接
User-Agent: //请求发出着 兼容性以及定制化需求
Accept:text/plain, text/html //制定客户端能够接受的内容类型
Accept-Charset: iso-8859-5 //浏览器可以接受的字符编码集
Accept-Encoding: compress, gzip //浏览器可以值吃的web服务器返回内容压缩编码类型
Accept-Language: en, zh //浏览器可接受的语言
Accept-Ranges: bytes //可以请求网页实体的一个或者多个子范围字段
Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ== //HTTP授权的授权证书
Cache-Control: no-cache //制定请求和响应遵循的缓存机制
Cookie: $Version=1;Skin=new //请求会携带该域名下所有cookie值
Content-Length: 348 //请求的内容长度
Conent-Type: application //请求与实体对应的MIME信息
Date: Tue, 15 Nov 2010 08:12:31 GMT //请求发送的日期和时间
Expect: 100-continue //请求特定的服务器行为
From: user@email.com //发出请求的用户Email
If-Match: “737060cd8c284d8af7ad3082f209582d” //请求内容与实体匹配生效
If-Modified-Since: Sat, 29 Oct 2010 19:43:31 GMT //指定时间之后被修改则成功 未修改返回304
If-None-Match: “737060cd8c284d8af7ad3082f209582d” //内容未改变返回304 参数为服务器先前发送的Etag 与服务器回应的Etag比较是否改变
If-Range: “737060cd8c284d8af7ad3082f209582d” //未改变 发送丢失的部分 参数也为Etag
If-Unmodified-Since: Sat, 29 Oct 2010 19:43:31 GMT //指定时间内未修改成功
Max-Forwards: 10 //限制信息通过代理和网关的传送时间
Pragma: no-cache //包含实现特定的指令
Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ== //连接到代理的授权证书
Range: bytes=500-999 //请求范围内的部分实体
Referer: http://www.zcmhi.com/archives/71.html //先前网页的地址 当前请求网页紧随其后 即来路
TE: trailers,deflate;q=0.5 //客户端愿意接受的传输编码
Upgrade: HTTP/2.0, SHTTP/1.3, IRC/6.9, RTA/x11 //向服务端指定协议
Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1) //通知中间网关或代理服务器地址 通信协议
Warn: 199 Miscellaneous warning //消息实体的警告信息
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
Server: Apache/1.3.27 (Unix) (Red-Hat/Linux) //web服务器软件名称	
Age: 12 //从原始服务器到代理缓存形成的估算时间（以秒计，非负）
Accept-Ranges: bytes //表明服务器是否支持指定范围请求及哪种类型的分段请求
Allow: GET, HEAD //对某网络资源的有效的请求行为，不允许则返回405
Cache-Control: no-cache //告诉所有的缓存机制是否可以缓存及哪种类型
Content-Encoding: gzip //web服务器支持的返回内容压缩编码类型
Content-Language: en,zh //响应体的语言
Content-Length: 362 //响应体长度
Content-Location: /index.htm //请求资源可替代的备用的另一地址
Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ== //返回资源的MD5校验值
Content-Range: bytes 21010-47021/47022 //在整个返回体中本部分的字节位置	
Connect: close
Content-Type: text/html; charset=utf-8 //返回内容的MIME类型
Date: Tue, 15 Nov 2010 08:12:31 GMT //原始服务器消息发出的时间
ETag: “737060cd8c284d8af7ad3082f209582d” //请求变量的实体标签的当前值
Expires: Thu, 01 Dec 2010 16:00:00 GMT //响应过期的日期和时间
Last-Modified: Tue, 15 Nov 2010 12:45:26 GMT //请求资源的最后修改时间
Location: http://www.zcmhi.com/archives/94.html //用来重定向接收方到非请求URL的位置来完成请求或标识新的资源
Pragma: no-cache //包括实现特定的指令，它可应用到响应链上的任何接收方	
Proxy-Authenticate: Basic //它指出认证方案和可应用到代理的该URL上的参数
Refresh: 5; url=http://www.atool.org/httptest.php //	应用于重定向或一个新的资源被创造，在5秒之后重定向（由网景提出，被大部分浏览器支持）
Retry-After: 120 //如果实体暂时不可取，通知客户端在指定时间之后再次尝试
Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1 //设置Http Cookie	
Trailer: Max-Forwards //指出头域在分块传输编码的尾部存在	
Transfer-Encoding:chunked //文件传输编码	
Vary: * //告诉下游代理是使用缓存响应还是从原始服务器请求
Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1) //告知代理客户端响应是通过哪里发送的
Warning: 199 Miscellaneous warning //警告实体可能存在的问题
WWW-Authenticate: Basic //表明客户端请求实体应该使用的授权方案	
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

##### 5 服务器错误

* 500 Internal Server Error 服务器遇到了一个未曾预料的状况
* 501 Not Implemented 服务器不支持当前请求所需要的某个功能
* 502 Bad Gateway 作为网关 或者代理工作的服务器尝试执行请求时，从上游服务器接受到无效的响应
* 503 Service Unavailable 由于临时的服务器维护或者过载 服务器当前无法处理请求
* 504 Gateway Timeout 作为网关 或者代理工作的服务器尝试执行请求时，未能及时从上游服务器或者辅助服务器收到相应
* 505 HTTP Version Not Supported 服务器不支持 或者拒绝支持在请求中使用的HTTP版本
* 506 Variant Also Negotiates 服务器存在内部配置错误
* 600 Unparseable Response Headers 源站没有返回响应头部 只返回实体内容



