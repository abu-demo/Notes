## HTTPS

HTTPS是在HTTP上建立SSL加密层，并对传输数据进行加密

1. 对数据进行加密 并建立一个信息安全通道 来保证传输过程中的数据安全、
2. 对网站服务器进行真实身份认证

## 存在背景

##### HTTP缺点

* HTTP使用明文 内容可能被窃听
* 无法证明报文的完整性
* 不验证通信方的身份

##### HTTPS

* 数据隐私性：内容经过对称加密，每个连接生成一个唯一的加密密匙
* 数据完整性：内容传输经过完整性校验
* 身份认证： 第三方无法伪造服务器（客户端）身份

## 如何解决？

HTTPS协议是HTTP通信接口部分用SSL和TLS协议代替了而已

通常HTTP直接和TCP通信 使用SSL 则演变成**HTTP**先和**SSL**通信 再和**TCP**通信

 ![](/assets/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f31322f32322f313637643438626337376565363966383f773d35363126683d32393726663d706e6726733d313430313839.png)

#### 1 解决内容可能被窃听的问题

##### 对称加密  

加密和解密通用一个密匙 在怎么安全把密匙转交给对方是一个问题

**非对称加密**

一把叫做私有密匙 一把叫做公开密匙（可以发布）用公匙加密信息 用私匙解密



##### 


