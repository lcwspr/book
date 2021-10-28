# 使用Docker镜像

## 概述

1. 镜像是Docker三大核心概念中最重要的，
2. Docker运行容器前需要本地存在对应的镜像，如果镜像不存在，Docker会尝试先从默认镜像仓库下载(默认使用Docker Hub公共注册服务器中的仓库， 也可以配置使用自定义的镜像仓库)
3. 本章围绕镜像这一核心概念介绍具体操作
   1. 如何使用pull命令从Docker Hub仓库中下载镜像到本地
   2. 如何查看本地已有的镜像信息和管理镜像标签
   3. 如何在远端仓库使用search命令进行搜索和过滤
   4. 如何删除镜像标签和镜像文件
   5. 如何创建用户定制的镜像并且保存为外部文件
   6. 如果往Docker Hub仓库中推送自己的镜像

## 获取镜像

1. 下载镜像命令

   * `docker pull NAME[:TAG]`
     * NAME: 镜像仓库名称
     * TAG：镜像的标签(往往表示版本信息)

   * 例如获取ununtu 18.04系统基础镜像
     * `docker pull ununtu:18.04`
     * 注意： 如果不显示指定TAG, 默认会选择最新latest标签(生产环境不要用最新的)
   * 有时需要使用镜像代理服务来加速Docker镜像获取过程, 可以添加`--registry-mirror=proxy_URL`

2. 镜像文件构成

   * 镜像文件一般由若干层(layer)组成，29c289ac2398这样的串是层的唯一id(世纪完整的id包括256bit, 64个十六进制字符组成)， 下载时会输出镜像各层信息，不同镜像包含相通层，本地只会存储层的一份内容

3. 镜像下载的仓库地址

   1. 严格来说，镜像仓库地址名称签名还应该添加仓库地址(registry), 不过默认使用docker hub可以省略
      * 也就是`docker pull ubuntu:18.04`相当于`docker pull regisry.hub.docker.com/ubuntu:18.04`
   2. 如果从非官方仓库下载，需要在仓库名称前面指定完整的仓库地址。
      * `hub.c.163.com/public/ubuntu:18.04`

5. 代理服务

   * 启动docker服务时，`--registry-mirror-proxy_URL`

## 查看镜像信息

1. 使用images命令列出镜像
   1. `docker images`
   2. `docker image ls`
2. docker images列出信息
   1. 来自于那个仓库
   2. 镜像的标签信息
   3. 镜像的ID: 
      * 最为重要，如果两个镜像ID相同，那么说明他们指向同一个镜像，只是具有不同的标签名
      * 使用镜像ID,一般可以使用该ID前若干个字符组成的可区分串替代完整ID
   4. 创建时间
   5. 镜像大小
3. images子命令主要支持的选项
   1. `-a, --all=true|false`:  列出所有(包括临时文件)镜像文件，默认为否
   2. `--digests=true|false`: 列出镜像的数字摘要值，默认为否
   3. `-f, --filter=[]`: 过滤列出的镜像， 如dangling=true只显示没有被使用的镜像，也可指定带有特定标注的镜像
4. 使用tag命令添加镜像标签
   1. `docker tag ubuntu:latest mylinux:latest`
   2. 实际上他们指向了同一个镜像文件，只是别名不同而已
5. 使用inspect命令查看详细信息
   * `docker [image] inspect ubuntu:18.04`
   * 展示镜像的详细信息， 包括制作者，适应架构，各层的数字摘要
     * `docker [image] inspect -f {{".Architecture"}} ubuntu:18.04`
6. 使用history命令查看进行历史
   * `docker histroy ubuntu:18.04`
   * 可以使用`--no-trunc`来输出完整输出

## 搜寻镜像

1. 使用docker的search子命令可以搜索Docker Hub官方仓库的镜像
   1. `docker search [option] keyword`

## 删除和清理镜像

1. 使用标签删除镜像
   1. `docker rmi`或者是`docker image rm`
   2. `docker rmi IMAGE [IMAGE...]`: 其中IMAGE可以为标签或ID
      * 当镜像有多个标签是时，实际上只会删除标签
2. 使用镜像ID来删除镜像
   1. 说明
      1. 会先尝试删除所有指向该镜像的标签，然后删除镜像文件本身
      2. 如果镜像创建的容器存在时，镜像文件默认无法删除。
   2. 查看本机存在的所有容器
      * `docker ps -a`
   3. 默认如果存在该镜像创建的容器，那么镜像文件无法删除
      * `docker rmi -f ubuntu:18.04`
   4. 推荐先删除依赖镜像的容器
      * `docker rm 容器id`
3. 清理镜像
   1. `docker image prune -f`
   2. 参数
      1. `-a`: 删除所有无用镜像，不光是临时镜像
      2. `-filter filter`: 只清理符合给定过滤器的镜像
      3. `-f`: 强制删除镜像

## 创建镜像

1. 基于已有镜像创建的容器创建

   1. 命令
      * `docker [container] commit`
      * `docker [container] commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]`
   2. 命令参数
      1. `-a`: 作者信息
      2. `-c`: 提交的时候执行Dockerfile指令
         1. CMD
         2. ENTRYPOINT
         3. ENV
         4. EXPOSE
         5. LABEL
         6. ONBUILD
         7. USER
         8. VOLUME
         9. WORKDIR
      3. `-m`:  提交信息
      4. `-p`: 提交时暂停容器运行
   3. 实例演示
      1. 首先启动一个镜像，并在其中进行修改操作(容器id为a925)
         1. `docker run -it ubuntu:18.04 /bin/bash`
         2. `touch test`
         3. `exit`
      2. 该容器与原镜像已经发生了改变，可以提交为一个新的镜像
         * `docker [container] commit -m 'Add a new file' -a 'Docker New' a925xx test:0.1`
           * 顺利会返回镜像id
      3. 查看本地镜像列表
         * `docker images`

2. 基于本地模板导入

   1. 命令
      * `docker [container] import`
      * `docker [image] import [OPTIONS] file|URL-[REPOSITORY[:TAG]]`
   2. 镜像模板
      * `cat ubuntu.tar.gz | docker import - ubuntu:18.04`

3. 基于Dockerfile创建(利用给定的指令描述基于某个父镜像创建新镜像的过程)

   1. Dockerfile编写

      ```
      FROM debian:stretch-slim
      
      LABEL version="1.0" maintainer="docker user <docker_user@github>"
      
      RUN apt-get update && \
      	apt-get install -y python3 && \
      	apt-get clean && \
      	rm -rf /var/lib/apt/lists/*
      ```

   2. 创建镜像的过程
      
      * `docker [image] build -t python:3` 

##  存出和载入镜像

1. 存出镜像
   * `docker [image] save`:  支持使用`-o`参数
   * `docker save -o ubuntu_18.04.tar ubuntu:18.04`
     * 导出本地的ubuntu:18.04镜像为文件ubuntu_18.04.tar

2. 导入镜像
   * `docker load -i ubuntu_18.04.tar`
   * `docker load < ubuntu_18.04.tar`

## 上传镜像

1. push子命令，可以使用`docker [image] push`命令上传镜像到仓库，默认上传到Docker Hub, 需登录
   * `docker [image] push NAME[:TAG] | [REGISTRY_HOST[:REGISTRY_PORT]/]NAME[:TAG]`