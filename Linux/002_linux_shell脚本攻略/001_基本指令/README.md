# 基本指令

## 初始

1. shell脚本通常以shebang起始
   * `#!/bin/bash`
2. 两种执行方式
   1. 将脚本名作为命令行参数: `bash my.sh`
   2. 将脚本执行权限: `./my.sh`
3. 当启动交互式shell
   1. 会执行一组命令来初始化提示文本，颜色等设置。这组命令来自用户主目录中的脚本文件`~/.bashrc`， 登录shell则是`~/.bash_profile`
   2. 历史命令记录文件: `~/.bash_history`
4. 注释
   1. `# 这是注释内容`

## 输出内容

1. echo 
   1. `echo "welcome to bash"`:  echo输出一个字符串
      * 如不需要解析某个字符，可以使用反斜线转义
   2. `echo 'Welcome to bash'`: 也可以使用单引号
      * 单引号不会解析命令或变量，但是双引号会解析命令或者变量。
2. printf函数
   * printf命令接受引用文本或者由空格分隔的参数，我们可以使用格式化字符串来指定字符串的宽度，左右对齐方式，并且Printf不会自动添加换行符
   * `printf "%-5s %-10s %-4s \n" No Name Mark`
3. 补充
   1. 使用echo 和 printf命令时，要确保，选项出现在命令中的所有字符串之前，否则bash会将其视为另一个字符串。
   2. echo
      1. 可以使用`-n`禁用结尾换行

## 使用变量与环境变量

* 所有编程语言都使用变量来存放数据，以备随后使用或者修改，脚本语言一般来说不要求在创建变量之前声明其类型。
* 并且shell定义了一些变量，用于保存用到的配置信息，比如可用的打印机，搜索路径。

### 预备知识

1. 查看其他进程环境变量
   * `cat /proc/$PID/environ`
2. 设置变量
   * `varName=value`
3. 加上$访问内容
   * `echo $var`
4. 也可以写成
   * `echo ${var}`

### 补充shell特性

1. 获得字符串长度

   * `length=${#var}`

2. 识别当前所使用shell

   * `echo $SHELL`

3. if判断脚本

   ```bash
   if [$UID -ne 0]; then
   	echo "$USER is now root"
   else
   	echo "Hello Root"
   fi
   ```

4. 变量判断
   * `${parameter:+expression}`： 如果parameter有值且不为空，则使用expressiong的值

### 使用shell进行数学运算

* bash使用`let`, `(())`, `[]`执行基本的算术运算，工具expr和bc可以用来执行高级操作

* 几种运算方式

  1. let可以直接执行基本算术命令，但是用let， 不需要添加$

     1. 例如

        ```bash
        let result=no1+no2
        echo $result
        ```

     2. 自加操作
        * `let no1++`
     3. 自减操作
        * `let no2++`
     4. 简写形式
        1. `let no+=6`
        2. `let no-=6`

  2. 其他方法

     1. 操作符`[]`的使用方法和let命令一样
        * `result=$[no1+no2]`
        * `[]`之中，也可以使用$前缀
     2. 也可以使用`(())`操作符
     3. bc是一个用来数学运算的高级工具，包含大量选项，可以执行浮点运算
        1. `echo "4 * 0.56" | bc`
        2. 设定小数精度
           * `echo "scale=2;22/7" | bc`
        3. 进制转换，能够进制转换
           * `echo "obase=2;$no"|bc`

## 玩转文件描述符和重定向

* 文件描述符是与输入和输出流相关联的整数，最广为人知的就是`stdin`, `stdout`, `stderr`.
* 脚本可以使用大于号将输出重定向到文件中。

* tree命令
  * 即可以将数据重定向到文件，还可以提供一份重定向数据的副本作为管道中后续命令的stdin
  * 使用`-`, 可以将两个输出都重定向到屏幕

### 补充内容

1. 将文件重定向到命令

   ```bash
   cat file | cmd
   cmd1 | cmd2
   ```

2. 重定向脚本内部的文本块

   ```bash
   #!/bin/bash
   cat<<EOF>log.txt
   This is a generated fild. Do not edit.
   ```

## 数组和关联数组

1. 数组允许脚本利用索引将数据集合保存为独立的条目，Bash支持普通数组和关联数组，前者使用整数作为数组索引，后者使用字符串作为数组索引。

2. 基础知识
   1. 可以在单行中使用数值列表来定义一个数组
      * `array_var=(test1 test2 test3 test4)`
   2. 或者在定义时，定义成一组"索引-值"
      * `array_var[0]="test1"`
      * `array_var[1]="test2"`
   3. 打印特定索引的数组元素内容
      * `echo ${array_var[0]}`
      * `echo ${array_var[$index]}`
   4. 以列表形式打印数组中所有值
      * `echo ${array_var[*]}`
      * `echo ${array_var[@]}`
   5. 打印数组长度
      * `echo ${#array_var[*]}`
3. 定义关联数组
   1. `declare -A ass_array`
   2. 定义方式
      1. 使用行内索引值
         * `ass_array=([index1]=val1 [index2]=val2 )`
      2. 使用独立的索引-值进行赋值
         * `ass_array[index1]=val1`
   3. 列出数组的索引
      * `echo ${!fruits_value[*]}`

## 获取终端信息

* 处理终端的相关信息，比如行数，列数，光标位置，掩盖密码
* 终端相关命令参数
  1. 获取终端的行数和列数
     1. `tput cols`
     2. `tput lines`
  2. 打印当前的终端名
     1. `tput longname`
  3. 将光标移动到坐标(100, 100)处
     * `tput cup 100 100`
  4. 设置终端背景色
     * `tpu setb n`
  5. 设置终端前景色
     * `tput setf n`
  6. 设置文本样式粗体
     * `tput bold`
  7. 设置下划线的起止
     * `tput smul`
     * `tput rmul`
  8. 输入密码时，脚本不应该显示输入内容
     * `stty -echo`
     * `stty echo`

## 获取日期并设置

* 延时可以用来在程序执行过程中等待一段时间(比如1秒)。或者每隔几秒(或者几个月)监督某项任务。与时间和日期打交道需要理解如何描述并处理这两者
* 日期能够以多种格式呈现，在系统内部，时间呗存储成一个整数(时间戳)
* 相关命令
  * 读取日期
    * `date`

## 调试脚本

1. 我们可以利用bash内建的调试工具或者按照易于调试的方式编写
   * `bash -x script.sh`

## 函数和参数

* 函数的定义包括function命令，函数名，开闭括号

  ```bash
  function fname()
  {
  	statements;
  }
  ```

* 直接使用函数名调用
  * `fname()`
* 函数参数可以按位置访问， `$1` ， `$2`
* 常用参数
  1. `$@`: 将参数拓展成: `$1 $2 $3`

### 其他内容

1. 导出函数
   * 函数也能像环境变量一样使用export导出，如此一来，函数的作用域就可以拓展到子进程中。
2. 读取命令返回值
   * `$?`
3. 将一个命令的输出发送给另一个命令
   1. `|`: 相关内容
   2. `$()`: 会启动子shell执行命令
4. 利用子shell生成一个独立的进程
   * `$(cd /bin; ls)`













































































