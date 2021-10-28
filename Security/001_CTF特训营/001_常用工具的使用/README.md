# 常用工具的使用

## Burp suite

1. proxy模块
2. Repeater重放模块
   * 可以测试HTTP数据包中的Cookies和user-agent等浏览器不可以直接修改的字段是否存在注入，可以使用Rejpeater模块
     * 右键发送，或者可以使用`ctrl + r`
   * 例如检查IP
     * X-forwarded-for
     * x-real-ip

2. intruder暴力破解模块
   * 攻击类型
     1. Sniper类型
        * 只需要设置一个payload set, 在几个变量中逐一替换payload, 每次只会替换一个位置
        * 每次只会更换一个值，其他值都会是默认值
     2. Battering ram
        * 需要设置一个payload set, 两个变量位置替换相同的payloaed
     3. pitchfork
        *  需要设置多个payload set, 和每个变量的位置一一对应
     4. cluster bomb
        * 需要设置变量个数个数据集，之后对应每次请求，会对于变量进行排列组合
   * payload标签页
     * payload set
       * 可以设置每个位置使用的数据集
       * 常用payload set
         * Runtime file: 从文件读取
         * Number: 用于设置数字开始结束
         * Dates: 设置日期
3. Decoder
   * 编解码工具
4. Comparer
   * 比较模块

## Sqlmap

* 常用参数
  1. `-h`
  2. `-u`: 指定url
  3. `-data=DATA`: 指定Data文件
  4. `--dbs`: 查询数据库
  5. `--tables`: 查询表
  6. `--columns`: 查询字段
  7. `--dump`: 转存数据
  8. `-D`: 指定数据库名
  9. `-T`: 指定表名
  10. `-C`: 指定字段名
  11. `--users`: 查询数据库用户
  12. `--privileges`: 查询用户权限
  13. `--user-agent`: 自定义
  14. `--random-agent`: 随机选择
  15. `--tamper=TAMPER`

## 浏览器插件

## namp

1. 主机发现参数
   * `-sP`: 使用ping 扫描
   * `-PN`: 不使用ping
2. 扫描参数
   * `sS`: tcp syn扫描
   * `sV`: 版本号 服务
   * `-A`: OS版本
3. 扫描速度
   * `-T0`: 最慢