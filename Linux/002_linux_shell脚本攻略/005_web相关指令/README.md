# web相关

## Web页面下载

1. `wget URL`: 可以用于下载Web页面

   * `wget http://baidu.com -O hello.txt`: 指定保存文件

   * 可以使用`-o`: 指定日志文件位置 
   * `wget -t 5 URL`: 可以指定在放弃下载前尝试次数，0不断重试

2. 其他参数

   1. 下载限速
      * `wget --limit-rate 20k http://baidu.com`
   2. 可以使用`-Q`指定最大配额
      * `wget -Q http://baidu.com`
   3. 断点续传
      * `wget -c URL`
   4. 复制全站
      * `wget --mirror --convert-links http://baidu.com`
   5. http认证或者ftp页面
      * `wget -user username --password pass URL`

## CURL指令

1. 常用指令
   1. `-A`: 指定用户user-agent, 也可以通过`-H`直接指定user-agent
   2. `-b`: 用于向服务器发送cookie
      * `curl -b 'foo=bar;foo2=bar2' https://baidu.com`
      * `curl -b cookies.txt https://www.google.com`: 读取文件内容
   3. `-c`: 将服务器设置的cookie写入一个文件
      * `curl -c cookies.txt https://baidu.com`
   4. `-d`: 参数用于发送POST请求的数据体
      * `curl -d 'login=em' -d 'password=123' -X POST http://baidu.com`
      * 使用`-d`， HTTP请求会自动加上标头: `Content-Type: application/x-www-form-urlencoded`, 并会自动把请求转换为POST
      * `-d`: 参数可以读取本地文本文件的数据
   5. `--data-urlencode`: 发送POST请求体，区别在于会自动将发送的数据进行URL编码
   6. `-e`: 参数用来设置HTTP标头Referer, 表示请求来源
      * `curl -e 'http://baidu.com'`
   7. `-F`: 参数用来向服务器上传二进制文件
      * `curl -F 'file=@photo.png' https://google.com/profile`
      * 上面命令会给HTTP请求加上`Content-Type: multipart/form-data`, 然后将文件photo.png, 作为file字段上传

