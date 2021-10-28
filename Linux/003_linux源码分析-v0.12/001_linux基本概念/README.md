# 概念

## Linux诞生和发展

* Linux系统是Unix操作系统的克隆系统，诞生于1991年10月5日。如今是世界上使用最多的一种UNIX类操作系统
* Linux操作系统的诞生，发展，成长依赖于以下五个重要支柱
  1. UNIX操作系统
  2. MINIX操作系统
  3. GNU计划
  4. POSIX标准
  5. Internet网络
* 简史
  1. UNIX操作系统诞生
     * 由贝尔实验室Ken.Thompson和Dennis Ritchie在DEC PDP-7小型机器开发的一个分时操作系统
  2. MINIX操作系统
     * 由AST开发，大学教授。
  3. GNU计划
     * GNU计划和自由软件基金对是由史托曼创办的，是自由软件的完整操作系统。各种使用Linux作为核心的GNU操作系统正在被广泛的使用
  4. POSIX标准
     * Portable Operating System Interface For Computing System: 是由IEEE和ISO/IEC开发的一簇标准。用于保证编制的应用程序可以在源代码一级上在多种操作系统上一致和运行。
     * 该UNIX用户组原来视图将AT&T的System V和BSD操作系统调用接口之间的区别重新调用集成

## 0.12版本内核描述注释

1. 发布主要文件
   * `bootimage-0.12.Z`: 具有美国键盘代码的压缩启动映像文件
     * 引导启动Image文件，主要包括磁盘引导扇区代码，操作系统加载程序和内核执行代码
   * `rootimage-0.12.Z`: 以1200KB压缩的根文件系统映像文件
     * 就是用于向内核提供最基本支持的根文件系统，其中包括操作系统最起码的一些配置文件和命令执行程序
   * `linux-0.12.tar.Z`:  内核源代码文件，大小为120B 
   * `as86.tar.Z`：二进制执行文件，16为汇编程序和装入程序
     * 16位汇编器链接程序软件包
   * `INSTALL-0.11`: 更新过的安装信息文件