# 构建基本脚本

## 使用多个命令

* `date ; who`

## 解释器注释

* `#!/bin/bash`

## 命令之替换

1. 返引号字符
2. $()

## 输入输出重定向

## 管道

## 执行数学运算

1. `expr 1+5`

2. `$[]`

## 浮点解决方案

1. bc 基本使用

## 结构化命令

1. if-then语句

   ```bash
   if command
   then
   	commands
   fi
   ```

2. if-then-else语句

   ```bash
   if command
   then
   	commands
   else
   	commands
   fi
   ```

3. test命令

   ```bash
   test
   if [ condition ]
   then
   	commands
   fi
   ```

4. 数值比较

   ```bash
   n1 -eq n2
   n1 -ge n2
   # eq, ge, gt, le, lt, ne
   ```

5. 字符串比较
   * `!=`
   * `=`
   * `<`
   * `>`
   * `-n str`: 字符串长度是否为0
   * `-z str1`: 

## 文件比较

* 允许测试Linux文件系统上面的文件和目录
  * `-d`: 检查是否是一个目录
  * `-e`: file是否存在
  * `-f`: 是否存在并是文件
  * `-r`: 是否存在可读