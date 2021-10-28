# 如何学习vscode

## 学会搜索

* 做一个优秀的Google程序员，一个优秀的Stack Overflow程序员

## Visual Studio Code简介

### Visual Studio Code概述

1. 跨平台

2. IntelliSense
3. 代码调试
4. 内置Git支持

### 用户体验

1. Terminal
2. 调试器
3. 版本控制

### 生态

* vscode不仅是一个编辑器，还有这强大的生态，VSCode把许多重要组件抽离出来，使其成为大家都可以复用的产品
* 开源组件
  * Language Server Protocol(LSP)
  * Debug Adapter Protocol (DAP)
  * Monaco Editor

## 核心组件

1. Electron
2. Monaco Editor
3. TypeScript
4. Language Server Protocol
   * 提供了诸如自动补全，定义跳转，代码格式化等与编程语言相关的功能
   * Language Server Protocol(LSP)是编辑器/IDE与语言服务器之间的一种协议， 通过JSON-RPC传输消息，可以让不同编辑器/IDE方便嵌入各种编程语言，
   * 三个问题
     1. 语言服务器通常是由原生的编程语言实现的，但vscode是基于node.js运行环境的
     2. 语言功能经常是资源消耗密集型的，为了验证一个文件，语言服务器要去解析大量文件，生成抽象语法树
     3. 最后，集成不同的语言工具和不同的编辑器需要大量工作。从语言工具的角度来看，他们需要适应代码编辑器的不同API。
5. Debug Adapter Protocol
   * 抽象了开发工具与调试工具之间的通信。
6. Xterm.js
   * 集成终端， 是基于一个被广泛使用的Xterm.js进行开发的。

