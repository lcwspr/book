# 使用Linux环境变量

## 什么是环境变量

* bash shell用环境变量的特性来存储有关shell会话和工作环境的信息(环境变量)。用于在内存中存储数据，以便后序shell脚本能够方便的访问
  * 全局变量
  * 局部变量
* 全局环境变量对于shell会话和所有生成的子shell都是可见的。局部变量则只对创建他们的shell可见。

## 定义变量

1. 定义局部变量
   * `my_var="This is lcwspr"`
2. 定义全局变量
   * `export my_var="Good Job!!"`

## 删除环境变量

* `unset` : 删除环境变量

## 默认shell环境变量

1. `CDPATH`
2. `HOME`
3. `PS1` `PS2`

## PATH环境变量

## 定位系统环境变量

1. 登陆时作为默认登录shell
   * `/etc/profile`
   * `$HOME/.bash_profile`
   * `$HOME/.bash_login`
   * `$HOME/.profile`
   * `$HOME/.bashrc`
2. 作为非登录shell的交互式shell
   1. 不是通过登录启动的， 交互式shell
   2. 配置读取
      * 不会访问`/etc/profile`
      * 只会检查HOME下的`.bashrc`
3. 作为运行脚本的非交互shell
   * 系统执行shell脚本时用的就是这种shell. 

## 数组变量

* 环境变量可以作为数组使用，数组是能够存储多个值的变量。 可以单独引用，也可以作为整个数组来引用
* 要显示整个数组变量，可以使用星号作为通配符放在索引值的位置
  * `echo ${mytest[*]}`： 也可以改变某个索引值的变量
* 