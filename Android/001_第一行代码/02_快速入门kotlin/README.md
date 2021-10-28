# 快速入门kotlin编程

## 安卓，java和kotlin

* 安卓系统诞生的前9年里，Google只提供了Java这一种语言来开发安卓应用，虽然在1.5版本引入NDK，支持使用C++/C进行本地开发，但是丝毫没有影响过java的地位
* 从2017年开始，Google在2017年I/O大会宣布: Kotlin成为安卓一级语言，和Java平起平坐，2019年，Kotlin成为安卓的第一开发语言。

## Kotlin语言简介

1. Kotlin语言是由JetBrains公司开发与设计的，早在2011年，JetBrains公司就公布了kotlin的第一个版本。并在2012年开源，但早期并没有获得关注
2. 2016年，Kotlin发布了1.0版本，表明Kotlin已经足够成熟稳定。并且JetBrain也在自家Idea上加入了对Kotlin的支持。自此Android终于有了第二种选择
3. 编程语言大致分为编译型语言和解释性语言。
   1. 编译型语言: 将我们编写的代码一次编译为二进制代码
   2. 解释性语言： 在程序运行时一句一句解释代码的执行
4. Java准确来讲属于解释形语言
   * 先编译为高效的Java虚拟机能解释的字节码，由Java虚拟机解释执行
   * 既然Java虚拟机并不关心，你的原始代码是由什么写成的，只关心生成的字节码。
5. Kotlin的优势
   1. 语法简介
   2. 语法更加高级
   3. Kotlin与Java兼容，kotlin可以直接调用Java编写的代码

## 运行kotlin程序

* 直接新建kotlin文件，新建main函数，可以直接运行

## 变量和函数

1. 在kotlin中定义变量的方式和Java区别很大，在Java中如果想要定义一个变量需要在变量前面声明变量的类型， 而Kotlin使用`val`和`var`两个关键字声明变量。
2. kotlin的编译器拥有出色的类型推导机制
3. 在kotlin中每一条语句的结尾不需要加上分号
4. Kotlin的类型推倒机制不是总可以正常工作，所以可以显示声明类型
   * `val a: Int = 10`

## 函数

* 函数和方法其实并没有区别，只是叫法不同

* 函数是用来运行代码的载体，可以在函数里编写很多行代码。运行这个函数会执行所有语句。

  ```kotlin
  fun methodName(param1: Int, param2: Int): Int {
      return 0
  }
  ```

* 语法糖

  * `fun largerNumber(num1: Int, num2: Int): Int = max(num1, num2)`
  * `fun largerNumber(num1: Int, num2: Int) = max(num1, num2)`

## 程序的控制逻辑

### 控制语句

1. if语句实现

   ```kotlin
   var value = 0 
   if (num1 > num2){
       value = num1
   } else{
       value = num2
   }
   ```

2. if语句有返回值

   * 返回最后执行语句的返回值

   * 返回最后一行代码作为返回值

     ```kotlin
     fun largerNumber(num1: Int, num2: Int) = if (num1 > num2) {
         num1
     } else {
         num2
     }
     ```

     

### 条件语句

1. when条件语句

   ```kotlin
   when(name) {
       "Tom" -> 86
       "Jim" -> 33
       else -> 0
   }
   ```

2. 可以进行类型匹配: is相当于instanceof

   ```kotlin
   fun checkNumber(num: Number){
       when(num){
           is Int -> println("is Int")
           is Double -> println("is Double")
           else println("not support")
       }
   }
   ```

### 循环语句

1. while循环： 和Java一样

2. for循环

   1. for-i循环被舍弃

   2. for-in循环

      ```kotlin
      for (i in 1..10) {
          println(i)
      }
      ```

      ```kotlin
      for (i in 1 until 10) {
      	println(i)
      }
      for (i in 0 until 10 step 2) {
          
      }
      for (i in 10 downTo 1) {
          println(i)
      }
      ```

## 面向对象编程

### 类与对象

1. 新建一个类

   ```kotlin
   class Person{
   
       var name = ""
       var age = 10
   
       fun eat() {
           println("\${} is eating. He is ${age} old..")
       }
   }
   ```

### 继承与构造函数

1. 继承，能够继承拥有父类的内容

   ```kotlin
   class Student : Person() {
       var sno = ""
       var grade = 0
   }
   ```

   * kotlin中任何一个非抽象类默认都是不可以被继承的，相当于java给类声明了final
   * 括号设计主构造函数和次构造函数等方面的知识

2. 任何一个语言都会有构造函数的概念，但是kotlin将构造函数分成了

   1. 主构造函数： 将会是你最常用的构造函数，每个类默认都带有一个不带参数的主构造函数(可以显示指明参数)

      ```kotlin
      class Student(val sno: String, val grade: Int): Person() {
          
      }
      val student = Student("a123", 5)
      ```

      * 这样就创建了一个Student对象，同时指定该学生的学号为a123

      * 因为主构造函数没有函数体，如果想要在主构造函数中编写逻辑，可以使用init结构体

        ```kotlin
        class Student(val sno: String, val grade: Int) : Person() {
            init {
                println("sno is " + sno)
                println("grade is " + grade)
            }
        }
        ```

      * 字类的主构造函数 调用父类中的哪个构造函数，在继承的时候通过括号来指定

        ```kotlin
        class Student(val sno: String, val grade: Int, name: String, age: Int):Perons(name, age){
            
        }
        ```

        

   2. 次构造函数

      ```kotlin
      class Student(var sno: String, var grade: Int) : Person() {
          constructor(sno:String, grade:Int, old: Int): this(sno, grade){
      
          }
      }
      ```

      * 注意： 既有主构造函数又有次构造函数，次构造函数必须调用主构造函数

      * 当类中只有次构造函数，没有主构造函数时。(当没有定义主构造函数，并定义了次构造函数，就没有主构造函数)

        ```
        class Student: Person {
        	constructor(name: String, age: Int): super(name, age){
        		
        	}
        }
        ```

## 接口

### 接口

1. 作用

   * 接口用于实现多态编程，我们都知道，Java是单继承结构的语言，任何一个类最多只能继承一个父类，但是却可以实现任意多个接口

   * 我们可以在接口中定义一系列行为，然后由具体的类去实现

     ```kotlin
     interface Study{
         fun readBooks()
         fun doHomework()
     }
     ```

   * 可以让Student类去实现Study接口，

     ```kotlin
     class Student(name: String, age: Int): Person(name, age), Study {
         override fun readBooks() {
             println(name + " is reading")
         }
         override fun doHomework() {
             println(name + " is doing homework")
         }
     }
     ```

## 函数的可见修饰符

1. 基本说明
   * private作用一样，都表示只在当前类内部可见，public表示对所有类可见(kotlin默认)
   * protected表示只对当前类和字类可见
   * internal: 只对模块内可见

## 数据类和单例类

1. 数据类
   1. MVC，MVP，MVVM中的M就是model， 就是数据类
   2. 数据类通常要重写equals(), hashCode()， toString()这几个方法

2. kotlin数据类生成

   1. `data class CellPhone(val brand:String, val price:Double)`

3. 单例类

   1. 单例类创建

      ```kotlin
      object Singleton {
          fun singletonTest() {
              println("Good job!!")
          }
      }
      ```

## Lambda编程

## 集合的创建与遍历

1. 创建集合

   1. 手动创建ArrayList

      ```kotlin
      val list = new ArrayList<String>()
      list.add("apple")
      list.add("Orange")
      list.add("Grape")
      ```

   2. kotlin方式

      ```kotlin
      val list = listOf("apple", "Banana", "orange", "pear") // 默认创建不可变集合
      ```

   3. 遍历集合

      ```kotlin
      val list = listOf("apple", "banana", "orange", "pear")
      for (fruit in list) {
          println(fruit)
      }
      ```

   4. 可变集合创建

      ```kotlin
      val list = mutableListOf("Apple", "Banana", "Orange", "Pear", "grape")
      list.add("Watermelons")
      ```

2. Set

   1. setOf()
   2. mutableSetOf()

3. Map

   1. 推荐使用方括号索引方式
   2. 简化添加数据: `val map = mapOf("apple" to 1, "banana" to 2, "Orange" to 3)`

### 函数式编程api

1. 寻找最长的一个

   ```kotlin
   val list = listOf("Apple", "Banana", "Orange", "Pear", "Grape")
   val maxLengthFruit = list.maxBy { it.length }
   ```

2. lambda语法
   
   * `{参数名1: 类型, 参数名2: 类型 -> 函数体}`