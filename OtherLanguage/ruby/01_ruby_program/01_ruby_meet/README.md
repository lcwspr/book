# ruby

## ruby概览

### ruby是一门面向对象的语言

* ruby通过调用构造函数来创建对象, 标准构造函数称为new
  * `song = Song.new("Ruby Tuesday")`
* 调用方法创建对象，`.`号之前的称之为接收者

### ruby的一些基础支持

* 语法问题

  * `puts "hello"`
  * `puts("Hello")`

* 字符串

  * `"my name is #{name}"`
  * `$greeting = "Hello"`
  * `@name = "pro"`
  * `puts("#$greeting, #$name")`

* ruby方法的返回值是最后一个被求值的表达式

  ```ruby
  def pr(name)
      "Good night, ${name}"
  end
  ```

* 名称惯例
  * 局部变量，方法参数和方法名都必须以小写字符或者下划线开头
  * 全局变量都有`$`字符
  * 实例变量都以`@`符号开头
  * 类变量都以`@@`开始
  * 类名称，模块名称，常量，第一个字母大写
* 一般，多个单词的实例变量使用下划线，多个单词类变量采用驼峰

### 数组和散列表

* `nil`是一个对象，用来表示没有东西

* `%w`可以让我们快速创建一组单词的数组

* 默认如果索引一个散列表没有包含的键，就会返回`nil`, 创建散列表可以指定默认值

  * `user_hash = Hash.new(0)`

* gets 从标准输入读取，文件结尾返回`nil`

  ```ruby
  while line = gets()
      puts line.downcase
  end
  ```

* 正则： 类似js