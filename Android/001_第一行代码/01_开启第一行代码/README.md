# 第一行代码

## 了解全貌，Android

* 安卓最初由Andy Rubin等人创办，2005年，Google收购了这家成立了22个月的公司。
* 之后，因为安卓的开放源代码策略，使得安卓移动急剧流行

## 安卓系统架构

1. Linux内核层
   * Android系统是基于Linux内核的简介。这一层为安卓设备的各种硬件提供了底层的驱动，比如显示驱动，音频驱动，照相机驱动，蓝牙驱动，WiFi驱动
2. 系统运行库层
   * 通过一些C/C++库位安卓提供了主要的特性，比如Sqlite库提供了数据库的支持。Webkit库提供了浏览器内核的支持
   * 还包括一些Android运行时，提供一些核心库，允许开发者使用Java语言编写Android环境。
3. 应用框架层
   * 主要提供了构建应用程序可能用到的API，安卓自带的核心应用就是应用这些完成的
4. 应用层
   * 所有安装在手机上的应用都属于这一层。

## 安卓应用开发特色

1. 四大组件
   * Android系统四大组件分别是Activity, Service, BroadcastReceiver, ContentProvider
2. 丰富的系统控件
3. SQLite数据库: 轻量级，运算速度极快的关系型数据库
4. 强大的多媒体

## 环境搭建

### 需要准备的工具

1. JDK
2. Android SDK
3. Android Studio

### 搭建开发环境

* 安装Java
* 安卓android studio

### 项目创建

1. start a new Andorid Studio project
2. select Empty Activity
3. 填入项目包名
4. save location: 表示项目存放位置
5. Language: 选择kotlin

### 启动模拟器

* 点击选择虚拟机， 安装新的虚拟机

### 运行helloWorld

* 点击运行按钮，程序会在模拟器上跑起来。

## 分析第一个Andorid程序

### 主目录结构

1. 打开project模式， 显示真实的项目路径
2. 分析主目录结构
   1. `.gradle`和`.idea`: android studio自动生成的文件
   2. `app`: 项目中代码，资源等内容都是直接放在这个目录下的，我们的开发工作也基本在这个目录进行
   3. `build`: 包含了一些编译自动生成的文件
   4. gradle: 这个目录包含gradle wrapper的配置文件，使用gradle wrapper方式不需要将gradle下载好，而是会自动根据本地缓存情况来决定是否联网下载gradle. Android Studio默认就是启动gradle wrapper方式的。
   5. `.gitignore`: 用来将指定的目录或文件排除在版本控制之外。
   6. `build.gradle`:项目全局的gradle构建脚本，通常这个文件的内容不需要修改(稍后分析)
   7. `gradle.properties`: 全局的gradle配置文件，在这里的配置的属性将会影响到项目中所有的gradle编译脚本
   8. `gradlew和gradlew.bat`: 是用来在命令行执行gradle命令的。
   9. HelloWorld.iml:  iml文件是所有idea项目都会生成的一个文件，用于标识是一个idea项目
   10. local.properties: 用于指定本机的SDK路径，通常不需要修改

### app目录结构分析

1. `build`: 和外层一样，包含了编译时自动生成的一些文件，内容目录会更加负责
2. `libs`: 假如用到了第三方jar包，就需要把这些jar包放在libs目录下
3. `androidTest`: 用于编写AndroidTest测试用例，可以对项目进行自动化测试
4. `java`: Java目录是放置我们所有Java代码的地方(Kotlin代码也放在这)
5. res: 项目中所有用到的图片，布局，字符串都放在这。
6. `AndroidManifest.xml`: 整个Android项目的配置文件，在程序中定义的四大组件都需要在这个文件注册。另外还可以在这个文件给应用程序添加权限声明。
7. `test`: 用于编写Unit Test测试用例 
8. `.gitignore`: 用于将app模块内指定的目录或者文件排除在版本控制之外。
9. `app.iml`: idea, 自动生成，不需要关心
10. `build.gradle`: app模块的构建脚本，会指定很多项目构建相关的配置
11. `proguard-rules.pro`: 混淆规则，用于打包混淆加密

### 项目中资源文件详解

1. res目录下的资源
   1.  `drawable`: 开头的目录都是用来放图片的
   2. `mipmap`: 开头的目录都是用来
   3. `values`: 开头的都是用来放字符串，样式，颜色等配置的
   4. layout开头的目录都是用来放置布局文件的。

2. 如何使用资源

   1. res/values/strings.xml

      ```xml
      <resources>
      	<string name="app_name">Hello World!!</string>
      </resources>
      ```

   2. 两种引用方式

      1. 在代码中通过`R.string.app_name`可以获得该字符串的引用
      2. 在XML中通过`@string/app_name`可以获得字符串引用

### 详解build.gradle文件

* Android Studio采用Gradle来构建项目。非常新建的构建工具，采用Groovy的领域特定语言

* 我们首先看一下最外层的build.gradle

  ```groovy
  // Top-level build file where you can add configuration options common to all sub-projects/modules.
  buildscript {
      ext.kotlin_version = "1.3.72"
      repositories {
          google()
          jcenter()
      }
      dependencies {
          classpath "com.android.tools.build:gradle:4.0.0"
          classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
  
          // NOTE: Do not place your application dependencies here; they belong
          // in the individual module build.gradle files
      }
  }
  
  allprojects {
      repositories {
          google()
          jcenter()
      }
  }
  
  task clean(type: Delete) {
      delete rootProject.buildDir
  }
  ```

  * repositories闭包，声明了google()和jcenter两行配置，分别对应了一个代码仓库
  * dependencies中使用classpath声明了两个依赖： 一个Gradle插件， 一个Kotlin插件
    * Gradle并不只是用来构建Android项目的，Java，C++都可以使用

* 内层模块级别的构建配置

  ```groovy
  apply plugin: 'com.android.application'
  apply plugin: 'kotlin-android'
  apply plugin: 'kotlin-android-extensions'
  
  android {
      compileSdkVersion 29
      buildToolsVersion "29.0.3"
  
      defaultConfig {
          applicationId "top.lcwspr.helloworld"
          minSdkVersion 21
          targetSdkVersion 29
          versionCode 1
          versionName "1.0"
  
          testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
      }
  
      buildTypes {
          release {
              minifyEnabled false
              proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
          }
      }
  }
  
  dependencies {
      implementation fileTree(dir: "libs", include: ["*.jar"])
      implementation "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
      implementation 'androidx.core:core-ktx:1.1.0'
      implementation 'androidx.appcompat:appcompat:1.1.0'
      implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
      testImplementation 'junit:junit:4.12'
      androidTestImplementation 'androidx.test.ext:junit:1.1.1'
      androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
  
  }
  ```

  * 第一行： 应用了一个插件， 一般有两种值
    * `com.android.application`: 表示是一个应用程序模块
    * `com.android.library`: 表示这是一个库模块
  * 第二三行，声明了kotlin插件
    * kotlin-android: 想使用kotlin构建安卓项目，必须引入
    * kotlin-android-extensions： 引入了其他kotlin拓展功能
  * 一个大的安卓闭包
    * sdk版本
    * 构建工具版本
    * defaultconfig闭包
      * applicationIn是每一个应用的唯一标识
      * minSdkVersion: 最低兼容安卓版本
      * targetSdkVersion: 目标版本，已经调试过
      * versionCode versionName: 版本号，名
      * testInstrumentationRunner: 用于在项目中启动单元测试
    * buildTypes闭包: 用于指定生成安装文件的相关配置
      * debug： 可省略
      * release
        * minifyEnabled: 是否启动代码混淆
        * proguardFiles: 用于混淆的规则文件
  * dependencies闭包
    * 可以指定项目所依赖的所有依赖关系。
    * 三种依赖关系
      * 本地依赖： 对本地目录或jar包添加依赖
        * `implementation fileTree`: 就是一个本地依赖(标识libs目录下的所有jar包添加到构建路径)
      * 库依赖: 可以对项目中的库模块添加依赖
        * `implementation projcet`： `implementation project(':helper')`
      * 远程依赖： 对jcenter远程库中的项目添加依赖
        * `implementation androidx.appcompat:appcompat:1.1.0`: 就是一个标准的远程依赖库格式

## 日志工具的使用

1. Android中日志工具类是Log(android.util.log)
   1. `Log.v()`, `Log.d()`, `Log.i()`, `Log.w()`, `Log.e()`