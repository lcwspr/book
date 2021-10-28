# nginx安装

## nginx 简介

* nginx是一个高性能的http服务器端软件，不过他还有很多其他的功能和作用。
* nginx的几种安装方式
  1. 通过操作系统包管理器进行安装
     * 优点： 简单
     * 缺点： 无法自定义安装那些模块
  2. 通过官方网站下载源码进行编译安装
     * 优点： 能够自定义那些模块需要安装，那些模块不需要安装，定制化较高，如果要使用第三方模块，则必须使用编译安装的方式
     * 缺点： 没有包管理器安装方便，升级的时候也比较费事
  3. 通过docker进行安装
* nginx模块
  * nginx是高度模块化的，不同的模块拥有不同的功能，所以如果想要在使用nginx的时候能过够使用特定的功能，那么必须要安装对应的模块才行

* nginx的两个版本
  1. `nginx.org`: 开源版本
  2. `nginx.com`: 商业版本

## 源码编译安装说明

1. `./configure --help`
   * 可以看到很多选项信息
   * `--prefix`: 使用`--prefix`选项可以指定nginx编译安装的目录
   * 出了常见的选项之外，还可以看到很多类似`--with-XXX_module` 或 `--without-XXX_module`的选项
     * `--with-XXX_module`: 表示指明安装对应模块，(也就是不指明就不会安装)
     * `--without-XXX_module`: 表名指明不安装对应模块， (也就是不指明就会安装)
   * 我们可以决定一些可选模块的安装与否，但是无法绝对默认的标准模块是否安装
2. nginx编译
   * `# ./configure --prefix=/srv/nginx --with-file-aio --with-http_auth_request_module --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_addition_module --with-http_xslt_module=dynamic --with-http_geoip_module=dynamic --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_degradation_module --with-http_slice_module --with-http_stub_status_module --with-http_perl_module=dynamic --with-pcre --with-pcre-jit --with-stream=dynamic --with-stream_ssl_module`

## vim 高亮

* 通过以上方法安装nginx后，当使用vim编辑器编译配置文件，vim编辑器无法自动识别nginx语句
* nginx源码包提供了高亮文件
  * `cd nginx-1.14.1`
  * `cp -r contrib/vim/* /usr/share/vim/vimfiles/`

# nginx 静态文件服务器

## 目录简介

```
conf		// 存放nginx相关的配置文件
html		// 默认提供的Web服务的根目录
logs         // nginx目录的日志存放目录
modules		// 目录中存放了一些模块会用到的库。
sbin	    // 存放了nginx的二进制文件
```

## nginx默认配置文件

* `conf/nginx.conf`: 主配置文件

  * `sed -i '/^[[:space:]]*#/'d nginx.conf`

* 有用的配置

  ```nginx
  worker_processes 1;
  
  events {
      worker_connections 1024;
  }
  
  http {
      include mime.types;
      default_type application/octet-stream;
      
      sendfile on;
      keepalive_timeout 65;
      
      server {
          listen 80;
          server_name localhost;
          
          location / {
              root html;
              index index.html index.htm;
          }
          
          error_page 500 502 503 504 /50x.html;
          location = /50x.html {
              root html;
          }
      }
  }
  ```

* 从如上配置可以看出，上述示例可以分为几个逻辑部分

  * http部分
  * server 部分
  * location 部分

* 或者说，上述示例可以分为几个逻辑块

  * http块： http有关的公共配置
  * server块： 一台主机可能提供多个web服务
    * 每一个server就代表一个http服务，我们可以同时配置多个server，以便同时提供多个http服务，不同的server可以使用不同的配置，写入到某个server块中的配置只对对应的http服务生效，如果多个server存在共同的公用配置，则可以将共同的配置写在http块中，以便多个server共享这些配置
  * location块
    * 访问网络资源都通过url访问，location可以当作url的一部分
    * 我们可以通过location将url中的路径和服务器的某个目录建立管理关系

* 同样，nginx还有很多其他功能块配置，同时还有一个全局区域配置

  * 用于全局的功能配置

* 在配置文件中，有各种各样的配置项，比如刚才提到的`worker_processes`, `include`, `listen`等等。

  * 这些配置项目称之为配置指令，配置指令后面会跟随一个或者多个值，可以称之为配置参数

* 一个配置指令通常会跟随一个或者多个配置参数，要正确使用配置指令，需要理解这些指令对应的功能，

* 基本的配置语法

  1. 每个指令都是以分号结尾的，分号代表了指令的配置结束
  2. 为了方便查看，通常将每个指令单独放在一行
  3. 块的基本结构就是大括号`{}`, 每个块后面都有一对大括号
     * 块和配置指令是由对应关系的，就是每个特定块，有特定的配置指令
  4. nginx使用井号作为注释

* nginx默认会提供一个服务，其实就是nginx中的一个Server块，默认监听在80端口: `listen 80;`

  ```nginx
  location / {
      root html;		# 当前location 所对应的文档的根目录在哪里
      index index.html index.htm; # 表示没有指明任何资源，默认资源文件
  }
  ```

  * location 可以理解为url的一部分，那么当访问`http://baidu.com/`这个url, 这个location最后的`/`就是locaiton中的`locaiton /`

## 软件源安装

* 有固定的文件配置路径
* server配置不放在nginx.conf中， 只能在`/etc/nginx/conf.d/default.conf`中找到默认配置的server块
  * `include /etc/nginx/conf.d/*.conf`
  * 表示将指定的文件中的内容包含到当前位置

## 基础命令

* 源码编译安装，环境变量配置

  ```bash
  1、创建/etc/profile.d/nginx.sh文件，以便写入环境变量配置。
   
  2、在/etc/profile.d/nginx.sh文件中写入如下内容：
  nginx_home=/srv/nginx
  PATH=$nginx_home/sbin:$PATH
  export PATH
   
  3、使用如下命令重载刚才的配置
  # source /etc/profile
  ```

* nginx 命令
  1. `nginx -h`: 帮助
  2. `nginx -v`: 版本信息
  3. `nginx -V`: 编译信息
  4. `nginx -c`: 指定配置文件
  5. `nginx -t || -T`: 测试配置文件语法问题
  6. `nginx -s`: 向正在运行的nginx进程发送信号
     * `nginx -s quit`
     * `nginx -s reload`
     * `nginx -s reopen`
     * `nginx -s stop`

## 模块，配置指令，块

1. 默认server配置

   ```nginx
       server {
           listen       80;
           server_name  localhost;
    
           location / {
               root   html;
               index  index.html index.htm;
           }
    
           error_page   500 502 503 504  /50x.html;
           location = /50x.html {
               root   html;
           }
       }
   ```

   