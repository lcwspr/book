# 基础内容

## 基本设置

1. 用户全局设置 用于所有vscode实例
   * 基本设置打卡方式
     * 文件中点击设置
     * `ctrl + shift + p`: open setting
     * `ctrl + ,`
   * json文件配置
     * `ctrl + shift + p`: 配置， `open setting json`
   * json文件位置
     * `%appdata%\code\user\settings.json`
     * `~/.config/Code/User/settings.json`
2. 工作区设置，用于项目，(可以提交到git)
   * 位于项目内的`.vscode`

## 语言设定

* `ctrl + shift + p`: `configure language specific setting`

## 命令面板

1. 基本快捷键
   1. `ctrl + p`: 文件跳转
   2. `ctrl shift + tab`: 打开文件跳转
   3. `ctrl + shift + p`: 命令面板
   4. `ctrl + shift + o`: 文件中的符号
   5. `ctrl + G`: 某一行
2. 并排
   1. 按住alt，单击
   2. `ctrl + \`,  一个文件分成两个
3. 缩略图
4. 面包屑导航
5. 文件过滤器
   * 可以过滤文件，显示
6. 禅模式
   * `ctrl + k, z`

## 编辑模式

1. 多光标
   * `alt + click`
   * `ctrl + alt + down`
   * `ctrl + d`: 选择相同单词
2. 列选择
   * `shift + alt`
3. 搜索
   * `ctrl + shift +ｆ`：　跨文件搜索

## 终端集成

## 命令行

* `code --help`

## 代码导航

1. 多个打开文件导航
   * `ctrl + tab`

## 代码片段

* `file` - `preferences` - `user snippets`
* 代码片段定义
  1. 键值对名： 代码片段的名字
  2. prefix: 触发关键字
  3. `body`: 填充内容
     * `${1:xxx}`: xxx为默认显示内容
     * `$0`: 最后光标位置
  4. `description`: 描述