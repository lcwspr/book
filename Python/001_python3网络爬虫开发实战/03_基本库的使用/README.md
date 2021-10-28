# 基本请求库的使用

## 使用urllib(内置请求库)

1. 四个模块
   1. request: 最基本的http请求模块，可以用来模拟发送请求。
   2. error: 异常处理模块
   3. parse: 一个工具模块,提供了需要URL处理方法, 比如拆分,解析,合并
   4. rebotparser: 分析robots.txt

### 发送请求

1. `urlopen()`

   1. `urlopen.request`模块提供了最基本的构造HTTP请求的方法, 利用它可以模拟浏览器的一个请求发起过程

      * 处理授权验证
      * 重定向
      * 浏览器Cookies

   2. 基本使用

      ```python
      import urllib.request
      resp = urllib.request.urlopen('http://baidu.com')
      s = resp.read().decode('utf-8')
      ```

   3. urlopen返回HTTPResponse对象

      1. read()
      2. readinto()
      3. getheader(name)
      4. getheaders(): 返回所有响应头
      5. fileno()
      6. msg
      7. version
      8. status
      9. reason
      10. debuglevel
      11. closed

   4. 常用参数
      1. data参数
         * 发送post请求

          ```
          import urllib.parse
          import urllib.request

          data = bytes(urllib.parse.urlencode({'word': 'hello'}), encoding='utf-8')
          resp = urllib.request.urlopen('http://httpbin.org/post', data=data)
          ```

      2. timeout参数

         * timeout参数用于设置超时时间, 单位为秒, 如果设置了超时时间,那么超过了超时时间就会抛出异常

           ```python
           from urllib.request import urlopen
           resp = urlopen('http://httpbin/get', timeout=1)
           print(resp.read())
           ```

         * 超时错误捕捉

           ```python
           import socket
           import urllib.request
           import urllib.error
           
           try:
               resp = urllib.request.urlopen('http://httpbin.org/get', timeout=0.1)
           except urllib.error.URLError as e:
               print(e.reason, type(e.reason))
               if isinstance(e.reason, socket.timeout):
                   print('TIME OUT')
           ```

      3. 其他参数

         1. context参数: 必须是ssl.SSLContext类型
         2. cafile: ca证书文件
         3. capath: ca证书路径

2. Request

   1. urlopen能够发起最基本的请求,但是如果加入请求头等,就会比较费事

   2. 可以使用Request来构建请求

      ```python
      from urllib.request import urllib
      from urllib.request import Request
      request = Request('https://python.org')
      resp = urlopen(request)
      ```

   3. 函数原型: `class Request(url, data=None, headers={}, origin_req_host=None, unverifiable=False, method=None)`
   4. Request参数
      1. 第一个参数用于请求url,必传
      2. 如果要传入data, 必须穿bytes类型, 如果时字典, 可以使用urlencode编码
      3. header: 请求头, 可以通过Request实例的add_header方法添加

   5. 请求构建

      ```python
      from urllib import request, parse
      
      url = 'http://httpbin.org/post'
      headers = {
          'User-Agent': 'Mozilla/4.0 (Compatible; MSIE 5.5; Windows NT)',
          'Host': 'httpbin.org'
      }
      dict = {
          'name': 'Germey'
      }
      
      data = bytes(parse.urlencode(dict), encoding='utf-8')
      req = request.Request(url=url, data=data, headers=headers, method='POST')
      resp = request.urlopen(req)
      ```

3. 构建更为强大的请求

   1. 基本请求可以构建,但是更高级操作怎么处理: (Cookies处理, 代理设置)   --- Handler

   2. 所有Handler的父类, BaseHandler,, 提供了最基本的`default_open()`, `protocol_request()

   3. 各个子Handler继承这个父类

      1. HTTPDefaultErrorHandler: 用于处理HTTP响应错误
      2. HTTPRedirectHandler: 用于处理重定向
      3. HTTPCookieProcessor: 用于处理Cookies
      4. ProxyHandler: 用于设置代理, 默认代理为空
      5. HTTPPasswordMgr: 用于管理密码,维护了用户名和密码的表
      6. HTTPBasicAuthHandler: 用于管理认证.

   4. 另一个比较重要的类是OpenerDirector(urlopen就是一个Opener)

      1. 之前使用urlopen和Request是类库封装好的功能, 现在需要更底层的操作 Opener
         1. Opener可以使用open方法, 和urlopen一样
         2. 我们需要使用Handler构建Opener

   5. 构建请求

      1. 登录验证网页

         ```python
         from urllib.request import HTTPPasswordMgrWithDefaultRealm, HTTPBasicAuthHandler, build_opener
         from urllib.error import URLError
         
         username = 'username'
         password = 'password'
         url = 'http://localhost:5000/'
         
         p = HTTPPasswordMgrWithDefaltRealm()
         p.add_password(None, url, username, password)
         auth_handler = HTTPBasicAuthHandler(p)
         opener = build_opener(auth_handler)
         
         try:
             result = opener.open(url)
             html = result.read()
         
         ```

         