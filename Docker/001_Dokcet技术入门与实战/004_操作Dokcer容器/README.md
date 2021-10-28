# 操作容器

## 概述

1. 容器是Docker的一个核心概念。容器时镜像的一个运行实例

## 创建容器

1. `docker create`命令用于新建一个容器。
   * `docker create -it ubuntu:latest`
   * 新建容器处于停止状态， 可以使用start命令启动它
   * 参数
     1. `-d` 是否在后台运行容器，默认false
     2. `-i`: 保持标准输入打开, 默认为false
     3. `-t`: 是否分配伪终端
     4. `-p`: net映射本地主机端口
     5. `-v`: 挂在主机上的文件卷到容器内
2. 启动容器
   * `docker start af`
3. 新建并启动容器
   * `docker run ubuntu /bin/echo 'Hello World!'`
   * 启动一个终端，允许用户进行交互
     * `docker run -it ubuntu:18.04 /bin/bash`
       * `-t`: 让docker分配一个伪终端(pseudo-tty): 并绑定到容器的标准输入上
       * `-i`: 让容器的标准输入保持打开
   * 后台守护运行，`-d`: 
4. 获取容器的输出信息
   * `docker logs`

## 停止容器

1. 可以使用`docker pause`命令来暂停一个运行中的容器
2. 终止容器
   1. `docker stop`命令
   2. `docker start`

## 进入容器

1. 使用`-d`参数，容器启动之后会进入后台，用户无法看到容器中的信息，可以使用attach或exec命令进入容器
2. attach： 不怎么使用
3. `docker exec`: 可以在运行中的容器内，直接执行命令
   1. `-d`: 后台执行
   2. `-i`: 标准输入接受用户命令

## 删除容器

1. `docker rm`: 删除处于终止或退出装填的容器