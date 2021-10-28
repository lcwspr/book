# 理解shell

## shell类型

* 系统启动什么样的shell, 取决于个人用户ID配置。 例如`/etc/passwd`文件中的相关内容

## 父子shell

* shell关系

## 进程列表

* `pwd;ls;cd /etc/pwd/cd;ls` 可以将一系列命令放在一起按顺序执行
* `(pwd;ls;cd /etc/pwd;cd;ls)`: 会创建子shell

## 子shell用法

1. 后台模式
   * sleep 
2. 将进程列表置入后台
   * `(sleep 2; echo $BASH_SUBSHELL; sleep 2)`
   * `(sleep 2; echo $BASH_SUBSHELL; sleep 2)&`
     * 可以在子shell中工作，又可以不阻塞IO   

3. 协程
   * 做两件事，在后台生成一个子shell, 并在子shell中执行命令
   * `coproc 子shell中执行指令`
   * `coproc sleep 10`

## bash内建命令

* 当执行外部命令时，会创建出来一个子进程(称之为衍生 forking).
* 内建命令： 不需要子进程来执行，和shell编译成一体。