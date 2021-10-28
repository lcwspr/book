# 爬虫基础

## HTTP基本原理

### URI和URL

1. URI： Uniform Resource Identifier, 就是统一资源标志符。
2. URL: Uniform Resource Locator, 统一资源定位符
3. URN: 统一资源名称

### 超文本

1. hypertext: 不只是文本， 包含一系列标签， 央视。

### http和https

1. http: 超文本传输协议， 用于从网络传输超文本数据到本地浏览器的传送协议， 能过够保证高效而且准确的传送超文本.
2. https: Hyper text Transfer Protocal over Secure Socket Layer: 即http下加入SSL层

### Http请求过程

* 我们在浏览器输入一个URL, 回车后便可以在浏览器中观察到页面内容，这个过程是浏览器向网站发送了一个网络请求， 网站服务器就受到这个请求后进行处理和解析。然后返回对应的响应数据。

#### chrome浏览器请求网址过程

1. Name
2. Status
3. Type
4. Initiator
5. Size
6. Time
7. Waterfall

#### 请求

1. 常见请求方法
   * get
   * post
   * put
   * delete

2. 请求头
   1. Accept
   2. Accept-Language
   3. Host
   4. Cookie
   5. Referer
   6. User-Agent
   7. Content-Type
      1. application/x-www-form-urlencoded
      2. appliaction/json
      3. multipart/form-data
      4. text/xml

#### 常用状态码

1. 301： 永久移动
2. 302： 临时移动
3. 400： 错误请求
4. 401： 未认证，没有进行身份认证
5. 403： 未授权， 已经认证，但是没有权限

### 响应

#### 响应头

1. Date
2. Last-Modified
3. Content-Encoding
4. Server
5. Content-Type
6. Set-Cookie
7. Expires

#### 响应体

1. 最重要的数据，响应体数据

## 网页基础

### HTML & CSS & JS

### 选择器

```text
.class				# 类名
#id					# id
element				# 元素
element, element	 # 选择两个元素节点
element element	     # 选择后代元素
element>element		# 选择直接子元素
element+element		# 选择兄弟元素
[attribute]			# 属性选择器
[attribute=value]	# 属性值为xxx
[attribute~=value]	# 属性带有xxx的
:hover
:active
:link
:vistied
:hover
:focus
:first-letter
:first-line
:first-child
:before
:after
:lang(language)
[attribute^="value"]
[attribute$="value"]
[attribute*="value"]
:root
:empty
:not(selector)
```

## 爬虫原理

### 基本原理讲述

1. 获取网页
2. 提取信息
3. 保存数据
4. 自动化程序

### 会话和Cookies

1. Session和Cookies的相关知识。

### 无状态HTTP

1. Http无状态指的是HTTP 协议对于事务处理是没有记忆能力的，也就是服务器不知道客户端是什么状态当我们向服务器发送请求后，服务器解析请求，然后返回对应的响应，服务器负责完成这个过程。