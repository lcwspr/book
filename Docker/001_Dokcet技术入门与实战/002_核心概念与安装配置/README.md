# 核心概念与安装配置

## 三大核心概念

1. 镜像(Image)
2. 容器(Container)
3. 仓库(Repository)

## 核心概念

1. Docker镜像
   * Docker镜像类似于虚拟机镜像，可以理解为一个只读的模板
     * 一个镜像可以包含一个基本的操作系统环境，里面仅仅安装了Apache应用程序
   * 镜像是创建Docker容器的基础(镜像自身是只读的，容器从镜像启动的时候，会在镜像的最上层创建一个可写层)
2. Docker容器
   * Docker容器类似于一个轻量级的沙箱， Docker利用容器来运行和隔离应用
   * 容器是从镜像创建的运行实例。它可以启动，开始，停止，删除，而这些容器都是彼此相互隔离，相互看不见的。
   * 可以把容器看作一个简易版的Linux系统环境(包括root用户权限，进程空间，用户空间和网络空间)以及运行在其中的应用程序打包而成的盒子。
3. Docker仓库
   1. Docker仓库类似于代码仓库，是Docker集中存放镜像文件的场所
   2. 有时候会将Docker仓库和仓库注册服务器(Registry)混为一谈，并不严格区分。
      1. 但是仓库注册服务器是存放仓库的地方，往往存放着多个仓库(每个仓库存放某一类镜像，往往包含多个镜像文件)， 通过不同的标签tag来进行区分。
      2. 根据所存储的镜像公开与否，Docker仓库分为公开仓库和私有仓库库。

## 安装Docker引擎

1. 目前Docker支持的服务有
   1. Docker引擎： 包括支持在桌面系统或者云平台安装Docker, 以及为企业提供简单安全弹性的容器集群编排和管理
   2. DockerHub: 官方提供的云托管服务，可以提供共有或者私有的镜像仓库
   3. DockerCloud: 官方提供的容器云服务，可以完成容器的部署于管理，可以完整的支持容器化项目，还有CI, CD功能
2. Docker引擎目前分为两个版本
   1. 社区版本(Community Edition, CE): 社区版本包括大部分核心功能
   2. 企业版本(Enterprise Edition, EE): 企业版本通过付费形式， 提供认证支持，镜像管理，容器托管，安全扫描等功能

## 配置Docker服务

1. 为了避免每次使用Docker命令时都需要切换到特权模式，可以将当前用户加入安装中自动创建的docker用户组
   * `sudo usermod -aG docker USER_NAME`
2. Docker服务启动实际上是调用了dockerd命令， 支持多种启动参数，因此，用户可以直接通过dockerd命令启动Docker服务
   * `dockerd -D -H tcp://127.0.0.1:2376`
   * 选项可以写入`/etc/docker/daemon.json`, 由dockerd服务启动时读取
3. Docker系统启动管理
   1. `/etc/systemd/system/docker.service.d/docker.conf`
   2. 更改systemd配置文件后需要使用`systemctl daemon-reload`重新读取配置文件
   3. 重启docker服务`systemctl start docker.service`
4. 如果服务启动不正常，可以查看相关日志
   1. 例如redhat系列，日志文件为`/var/log/messages`
   2. unbutu或CentOS可以使用`journalctl -u docker.service`
5. 每次重启docker服务之后，可以使用`docker info`来确保服务正常运行