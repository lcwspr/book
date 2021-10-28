# 更多结构化命令

## for 命令

1. 命令格式

   ```bash
   for i in xxx; do 
   	echo $
   done
   ```

2. 用通配符读取目录

   ```bash
   for file in /home/rich/test/*
   do
   	if [-d "$file"]
   	then
   		echo "$file is a directory"
   	fi
   done
   ```

## C风格for命令

* `for ((a = 1; a < 10; a++ ))`

## while命令

1. 基本

   ```bash
   while test com
   do
   	other commands
   done
   ```

   